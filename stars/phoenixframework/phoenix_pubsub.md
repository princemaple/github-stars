---
project: phoenix_pubsub
stars: 747
description: Distributed PubSub and Presence platform for the Phoenix Framework
url: https://github.com/phoenixframework/phoenix_pubsub
---

Phoenix.PubSub
==============

> Distributed PubSub and Presence platform for the Phoenix Framework

Usage
-----

Add `phoenix_pubsub` to your list of dependencies in `mix.exs`:

def deps do
  \[{:phoenix\_pubsub, "~> 2.0"}\]
end

Then start your PubSub instance:

defmodule MyApp do
  use Application

  def start(\_type, \_args) do
    children \= \[
      {Phoenix.PubSub, name: MyApp.PubSub}
    \]

    opts \= \[strategy: :one\_for\_one, name: MyApp.Supervisor\]
    Supervisor.start\_link(children, opts)
  end
end

Now broadcast and subscribe:

Phoenix.PubSub.subscribe(MyApp.PubSub, "user:123")
Phoenix.PubSub.broadcast(MyApp.PubSub, "user:123", :hello\_world)

Testing
-------

Testing by default spawns nodes internally for distributed tests. To run tests that do not require clustering, exclude the `clustered` tag:

$ mix test --exclude clustered

If you have issues running the clustered tests try running:

$ epmd -daemon

before running the tests.
