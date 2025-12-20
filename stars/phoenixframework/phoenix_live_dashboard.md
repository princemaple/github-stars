---
project: phoenix_live_dashboard
stars: 2136
description: Realtime dashboard with metrics, request logging, plus storage, OS and VM insights
url: https://github.com/phoenixframework/phoenix_live_dashboard
---

Phoenix LiveDashboard
=====================

Online Documentation.

LiveDashboard provides real-time performance monitoring and debugging tools for Phoenix developers. It provides the following modules:

-   Home - See general information about the system
    
-   OS Data - See general information about OS, such as CPU, Memory and Disk usage
    
-   Metrics - See how your application performs under different conditions by visualizing `:telemetry` events with real-time charts
    
-   Request logging - See everything that was logged for certain requests
    
-   Applications - See, filter, and search applications in the current node and view their processes in a supervision tree
    
-   Processes - See, filter, and search processes in the current node
    
-   Ports - See, filter, and search ports (responsible for I/O) in the current node
    
-   Sockets - See, filter, and search sockets (responsible for tcp/udp) in the current node
    
-   ETS - See, filter, and search ETS tables (in-memory storage) in the current node
    
-   Ecto Stats - Shows index, table, and general usage about the underlying Ecto Repo storage
    

The dashboard also works across nodes. If your nodes are connected via Distributed Erlang, then you can access information from node B while accessing the dashboard on node A.

Installation
------------

The LiveDashboard is built on top of LiveView. Both LiveView and LiveDashboard ship by default as part of Phoenix. But if you skipped them, you can LiveDashboard in three steps:

1.  Add the `phoenix_live_dashboard` dependency
2.  Configure LiveView
3.  Add dashboard access

### 1\. Add the `phoenix_live_dashboard` dependency

Add the following to your `mix.exs` and run `mix deps.get`:

def deps do
  \[
    {:phoenix\_live\_dashboard, "~> 0.7"}
  \]
end

### 2\. Configure LiveView

First, update your endpoint's configuration to include a signing salt:

\# config/config.exs
config :my\_app, MyAppWeb.Endpoint,
  live\_view: \[signing\_salt: "SECRET\_SALT"\]

Then add the `Phoenix.LiveView.Socket` declaration to your endpoint:

socket "/live", Phoenix.LiveView.Socket

And you are good to go!

### 3\. Add dashboard access for development-only usage

Once installed, update your router's configuration to forward requests to a LiveDashboard with a unique `name` of your choosing:

\# lib/my\_app\_web/router.ex
use MyAppWeb, :router
import Phoenix.LiveDashboard.Router

...

if Mix.env() \== :dev do
  scope "/" do
    pipe\_through :browser
    live\_dashboard "/dashboard"
  end
end

This is all. Run `mix phx.server` and access the "/dashboard" to configure the necessary modules.

### Extra: Add dashboard access on all environments (including production)

If you want to use the LiveDashboard in production, you should put authentication in front of it. For example, if you use `mix phx.gen.auth` to generate an Admin resource, you could use the following code:

\# lib/my\_app\_web/router.ex
use MyAppWeb, :router
import Phoenix.LiveDashboard.Router

...

pipeline :admins\_only do
  plug :fetch\_current\_admin
  plug :require\_authenticated\_admin
end

scope "/" do
  pipe\_through \[:browser, :admins\_only\]
  live\_dashboard "/dashboard"
end

If you'd rather have some quick and dirty HTTP Authentication, the following code can be used as a starting point:

\# lib/my\_app\_web/router.ex
use MyAppWeb, :router
import Phoenix.LiveDashboard.Router

...

pipeline :admins\_only do
  plug :admin\_basic\_auth
end

scope "/" do
  pipe\_through \[:browser, :admins\_only\]
  live\_dashboard "/dashboard"
end

defp admin\_basic\_auth(conn, \_opts) do
  username \= System.fetch\_env!("AUTH\_USERNAME")
  password \= System.fetch\_env!("AUTH\_PASSWORD")
  Plug.BasicAuth.basic\_auth(conn, username: username, password: password)
end

If you are running your application behind a proxy or a webserver, you also have to make sure they are configured for allowing WebSocket upgrades. For example, here is an article on how to configure Nginx with Phoenix and WebSockets.

Contributing
------------

For those planning to contribute to this project, you can run a dev version of the dashboard with the following commands:

```
$ mix setup
$ mix dev
```

Additionally, you may pass some options to enable Ecto testing. For example, to enable the PostgreSQL repo:

```
$ mix dev --postgres
```

...and to enable the MySQL repo:

```
$ mix dev --mysql
```

...and to enable the SQLite repo:

```
$ mix dev --sqlite
```

Alternatively, run `iex -S mix dev [flags]` if you also want a shell.

Before submitting a pull request, discard any changes that were made to the `dist` directory.

For example, to rollback using git restore:

```
$ git restore dist
```

License
-------

MIT License. Copyright (c) 2019 Michael Crumm, Chris McCord, José Valim.
