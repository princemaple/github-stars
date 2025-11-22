---
project: telemetry_ui
stars: 242
description: Telemetry based metrics UI. Take your telemetry metrics and display them in a web page.
url: https://github.com/mirego/telemetry_ui
---

  
  
Telemetry-based metrics UI. Take your `telemetry` metrics and display them in a web page.  
  

Features
--------

`TelemetryUI`’s primary goal is to display your application metrics without external infrastructure dependencies. Plug, Phoenix, Phoenix LiveView, Absinthe, Ecto, Erlang VM, Tesla, Finch, Redix, Oban, Broadway and others expose all sorts of data that can be useful. You can also emit your own events from your application.

Your data should not have to be uploaded somewhere else to have insighful metrics.

It comes with a Postgres backend, powered by Ecto, to quickly (and efficiently) store and query your application events.

### Advantages over other tools

-   Persisted metrics inside your own database
-   Live dashboard
-   Many built-in charts and visualizations using VegaLite

### Advanced features

-   100% custom UI hook to show your own components
-   100% custom data fetching to show live data
-   Shareable metrics page (secured, cacheable, without external requests)
-   Slack digest with rendered images
-   Multiple metrics dashboard living in the same app
-   Hot-reloading configuration without restarting your application
-   Dynamic configuration via functions for runtime flexibility
-   Hidden pages and custom styling per page

Checkout the Guides for more informations.

Usage
-----

### Installation

TelemetryUI is published on Hex. Add it to your list of dependencies in `mix.exs`:

\# mix.exs
def deps do
  \[
    {:telemetry\_ui, "~> 5.0"}
  \]
end

Configure TelemetryUI for test. This disables all TelemetryUI processes during testing.

\# config/test.exs
config :telemetry\_ui, disabled: true

Then run mix deps.get to install Telemetry and its dependencies.

After the packages are installed you must create a database migration to add the `telemetry_ui_events` table to your database:

mix ecto.gen.migration add\_telemetry\_ui\_events\_table

Open the generated migration in your editor and call the up and down functions on `TelemetryUI.Adapter.EctoPostgres.Migrations`:

defmodule MyApp.Repo.Migrations.AddTelemetryUIEventsTable do
  use Ecto.Migration

  @disable\_migration\_lock true
  @disable\_ddl\_transaction true

  def up do
    TelemetryUI.Backend.EctoPostgres.Migrations.up()
  end

  \# We specify \`version: 1\` in \`down\`, ensuring that we'll roll all the way back down if
  \# necessary, regardless of which version we've migrated \`up\` to.
  def down do
    TelemetryUI.Backend.EctoPostgres.Migrations.down(version: 1)
  end
end

This will run all of TelemetryUI's versioned migrations for your database. Migrations between versions are idempotent and rarely change after a release. As new versions are released you may need to run additional migrations.

Now, run the migration to create the table:

mix ecto.migrate

TelemetryUI instances are isolated supervision trees and must be included in your application's supervisor to run. Use the application configuration you've just set and include TelemetryUI in the list of supervised children:

\# lib/my\_app/application.ex
def start(\_type, \_args) do
  children \= \[
    MyApp.Repo,
    {TelemetryUI, telemetry\_config()}
  \]

  Supervisor.start\_link(children, strategy: :one\_for\_one, name: MyApp.Supervisor)
end

defp telemetry\_config do
  import TelemetryUI.Metrics

  \[
    metrics: \[
      last\_value("my\_app.users.total\_count", description: "Number of users", ui\_options: \[unit: " users"\]),
      counter("phoenix.router\_dispatch.stop.duration", description: "Number of requests", unit: {:native, :millisecond}, ui\_options: \[unit: " requests"\]),
      value\_over\_time("vm.memory.total", unit: {:byte, :megabyte}),
      distribution("phoenix.router\_dispatch.stop.duration", description: "Requests duration", unit: {:native, :millisecond}, reporter\_options: \[buckets: \[0, 100, 500, 2000\]\]),
    \],
    backend: %TelemetryUI.Backend.EctoPostgres{
      repo: MyApp.Repo,
      pruner\_threshold: \[months: \-1\],
      pruner\_interval\_ms: 84\_000,
      max\_buffer\_size: 10\_000,
      flush\_interval\_ms: 10\_000
    }
  \]
end

Since the config is read once at startup, you need to restart the server if you add new metrics to track. Alternatively, you can use the hot-reload feature (see guides/hot-reload.md).

To see the rendered metrics, you need to add a route to your router.

\# lib/my\_app\_web/router.ex
scope "/" do
  get("/metrics", TelemetryUI.Web, \[\], \[assigns: %{telemetry\_ui\_allowed: true}\])
end

### Image generation

Optionally, you can add 2 dependencies to generate png images from the charts. When you use the share feature, every chart will have an associated image (hidden) that will render a nice preview when sharing on Slack/other platforms.

\# mix.exs
def deps do
  \[
    #...
    {:vix, "~> 0.26"},
    {:vega\_lite\_convert, "~> 0.6"},
  \]
end

#### Security

Since it may contain sensitive data, `TelemetryUI` requires a special assign to render the page.

`:telemetry_ui_allowed` must be set to `true` in the `conn` struct before it enters the `TelemetryUI.Web` module.

By using a special assign to control access, you can integrate `TelemetryUI.Web` page with your existing authorization. We can imagine an admin protected section that also gives you access to the `TelemetryUI.Web` page:

pipeline :admin\_protected do
  plug(MyAppWeb.EnsureCurrentUser)
  plug(MyAppWeb.EnsureRole, :admin)
  plug(:enable\_telemetry\_ui)
end

def enable\_telemetry\_ui(conn, \_), do: assign(conn, :telemetry\_ui\_allowed, true)

That's it! You can declare as many metrics as you want and they will render in HTML on your page!

Configuration
-------------

### Dynamic Configuration

Instead of passing configuration directly, you can pass a function that returns the configuration. This enables dynamic configuration that can be reloaded at runtime:

\# Using anonymous function
{TelemetryUI, config: fn \-> telemetry\_config() end}

\# Using module and function tuple
{TelemetryUI, config: {MyApp.Telemetry, :config}}

This is particularly useful with the hot-reload feature (see guides/hot-reload.md).

### Named Instances

When running multiple TelemetryUI instances (e.g., for different dashboards with different permissions), you must give each instance a unique name:

\# lib/my\_app/application.ex
children \= \[
  {TelemetryUI, telemetry\_config() ++ \[name: :admin\]},
  {TelemetryUI, user\_config() ++ \[name: :user\_dashboard\]}
\]

Then reference the name in your router:

get("/admin/metrics", TelemetryUI.Web, \[\], \[assigns: %{telemetry\_ui\_allowed: true, telemetry\_ui\_name: :admin}\])
get("/user/metrics", TelemetryUI.Web, \[\], \[assigns: %{telemetry\_ui\_allowed: true, telemetry\_ui\_name: :user\_dashboard}\])

See guides/multi-metrics-endpoints.md for a complete example.

### Disabling TelemetryUI

You can disable all TelemetryUI processes (useful for testing):

\# config/test.exs
config :telemetry\_ui, disabled: true

For all configuration options, see guides/configuration-reference.md.

License
-------

`TelemetryUI` is © 2024 Mirego and may be freely distributed under the New BSD license. See the `LICENSE.md` file.

About Mirego
------------

Mirego is a team of passionate people who believe that work is a place where you can innovate and have fun. We’re a team of talented people who imagine and build beautiful Web and mobile applications. We come together to share ideas and change the world.

We also love open-source software and we try to give back to the community as much as we can.
