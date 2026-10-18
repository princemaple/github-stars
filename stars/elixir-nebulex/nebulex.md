---
project: nebulex
stars: 1404
description: In-memory and distributed caching toolkit for Elixir.
url: https://github.com/elixir-nebulex/nebulex
---

> **In-memory and distributed caching toolkit for Elixir**

* * *

🚀 About
--------

Nebulex adds caching to Elixir applications. Like Ecto, it is an abstraction: you use different caching backends through the same API, with little impact on your code.

You write against the Nebulex API instead of talking to Redis, Memcached, or an Elixir cache like Cachex directly. Nebulex also comes with declarative decorator-based caching, cache usage patterns, and distributed cache topologies.

* * *

Note

This README refers to the main branch of Nebulex, not the latest released version on Hex. Please refer to the getting started guide and the official documentation for the latest stable release.

* * *

📖 Usage
--------

To use Nebulex, add both `:nebulex` and your chosen cache adapter as dependencies in your `mix.exs` file.

> _**For more information about available adapters, check out the Nebulex adapters guide.**_

For example, to use the Generational Local Cache (`Nebulex.Adapters.Local` adapter), add the following to your `mix.exs`:

def deps do
  \[
    {:nebulex, "~> 3.0"},
    {:nebulex\_local, "~> 3.0"}, \# Generational local cache adapter
    {:decorator, "~> 1.4"},     \# Required for caching decorators
    {:telemetry, "~> 1.3"}      \# Required for telemetry events
  \]
end

All dependencies are optional, including the adapters, so you only load what you need:

-   For declarative decorator-based caching, add `:decorator` (recommended).
    
-   For Telemetry events, add `:telemetry` (recommended). See the Info API guide for cache stats and metrics.
    

Then run `mix deps.get`. To use another cache adapter, pick its dependency from the adapters guide.

Finally, in your cache definition, you'll need to specify the `adapter:` corresponding to the chosen dependency. For the local cache, it would be:

defmodule MyApp.Cache do
  use Nebulex.Cache,
    otp\_app: :my\_app,
    adapter: Nebulex.Adapters.Local
end

Don't forget to add `MyApp.Cache` to your application's supervision tree:

def start(\_type, \_args) do
  children \= \[
    MyApp.Cache
  \]

  \# ... rest of your supervision tree

You're now ready to use the cache:

iex\> MyApp.Cache.put("foo", "bar")
:ok
iex\> MyApp.Cache.fetch("foo")
{:ok, "bar"}

For more details, see the getting started guide and the online documentation.

* * *

⚡ Quick Start Example with Caching Decorators
---------------------------------------------

This example uses Nebulex with Ecto and declarative caching:

\# In config/config.exs
config :my\_app, MyApp.Cache,
  \# Create new generation every 12 hours
  gc\_interval: :timer.hours(12),
  \# Max 1M entries
  max\_size: 1\_000\_000,
  \# Max 2GB of memory
  allocated\_memory: 2\_000\_000\_000,
  \# Run size and memory checks every 10 seconds
  gc\_memory\_check\_interval: :timer.seconds(10)

\# Cache definition
defmodule MyApp.Cache do
  use Nebulex.Cache,
    otp\_app: :my\_app,
    adapter: Nebulex.Adapters.Local
end

\# Ecto schema
defmodule MyApp.Accounts.User do
  use Ecto.Schema

  schema "users" do
    field :username, :string
    field :password, :string
    field :role, :string
  end

  def changeset(user, attrs) do
    user
    |> cast(attrs, \[:username, :password, :role\])
    |> validate\_required(\[:username, :password, :role\])
  end
end

\# Accounts context with caching
defmodule MyApp.Accounts do
  use Nebulex.Caching, cache: MyApp.Cache

  alias MyApp.Accounts.User
  alias MyApp.Repo

  \# Cache entries expire after 1 hour
  @ttl :timer.hours(1)

  @decorate cacheable(key: {User, id}, opts: \[ttl: @ttl\])
  def get\_user!(id) do
    Repo.get!(User, id)
  end

  @decorate cacheable(key: {User, username}, references: & &1.id)
  def get\_user\_by\_username(username) do
    Repo.get\_by(User, \[username: username\])
  end

  @decorate cache\_put(
              key: {User, user.id},
              match: &\_\_MODULE\_\_.match\_update/1,
              opts: \[ttl: @ttl\]
            )
  def update\_user(%User{} \= user, attrs) do
    user
    |> User.changeset(attrs)
    |> Repo.update()
  end

  @decorate cache\_evict(key: {User, user.id})
  def delete\_user(%User{} \= user) do
    Repo.delete(user)
  end

  def create\_user(attrs \\\\ %{}) do
    %User{}
    |> User.changeset(attrs)
    |> Repo.insert()
  end

  def match\_update({:ok, value}), do: {true, value}
  def match\_update({:error, \_}), do: false
end

* * *

🔗 Important Links
------------------

-   Getting Started - Learn how to set up and use Nebulex.
-   Documentation - Complete API reference.
-   Upgrading to v3.0 - Migration guide for v3.0.
-   Declarative caching - Declarative Caching: Patterns and Best Practices.
-   Nebulex Streams - Real-time event streaming for Nebulex caches via `Phoenix.PubSub`.
-   Examples - Example applications.

* * *

🧪 Testing
----------

To run only the tests:

$ mix test

To run all the checks CI runs:

$ mix precommit

The `mix precommit` alias runs the tests, coverage, Credo, Dialyzer, and the other checks. Run it before opening a pull request.

* * *

📊 Benchmarks
-------------

Nebulex provides a set of basic benchmark tests using the library benchee, located in the benchmarks directory.

To run a benchmark test:

$ mix bench

> The benchmark uses the `Nebulex.Adapters.Nil` adapter, so it measures the Nebulex abstraction layer, not a specific adapter.

* * *

🤝 Contributing
---------------

Contributions are welcome.

Use the issue tracker for bug reports or feature requests. Open a pull request when you're ready to contribute.

Please read CONTRIBUTING.md for the full contribution workflow, PR expectations, commit message conventions, and validation steps.

* * *

📄 Copyright and License
------------------------

Copyright (c) 2017, Carlos Bolaños.

Nebulex source code is licensed under the MIT License.
