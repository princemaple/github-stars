---
project: entrace
stars: 64
description: null
url: https://github.com/underjord/entrace
---

Entrace
=======

A library to make it easy to use the fantastic Erlang/OTP tracing facilities in an idiomatically Elixir way. Built-in safeties and discoverable function naming. The hope is that this makes a BEAM superpower more well-known in the Elixir community.

Requires OTP 27 or later. Uses isolated trace sessions so multiple tracers can coexist without interfering with each other or other tracing tools.

Quick: paste into a running system
----------------------------------

Don't have Entrace installed? Copy `Entrace.Mini` and paste it into an IEx session on your running node. No dependencies required.

\# Paste the module, then:
pid \= Entrace.Mini.trace({MyApp.SomeModule, :some\_function, 2})

\# Trigger the function however you like, then check your mailbox:
flush()

\# Stop when done:
Entrace.Mini.stop(pid)

It supports wildcard patterns (`{MyApp.SomeModule, :_, :_}`), custom limits (`limit: 500`), and loading onto remote nodes (`Entrace.Mini.load_on(:"node@host")`).

Quick: load pre-compiled into a running system
----------------------------------------------

Paste this one-liner into IEx to download and start the full Entrace library. It fetches pre-compiled `.beam` files matching your OTP version from GitHub releases:

(fn \-> :inets.start(); :ssl.start(); otp \= System.otp\_release(); {:ok, {{\_, 200, \_}, \_, body}} \= :httpc.request(:get, {~c"https://github.com/underjord/entrace/releases/latest/download/entrace-otp-#{otp}.tar.gz", \[\]}, \[ssl: \[verify: :verify\_peer, cacerts: :public\_key.cacerts\_get(), depth: 3, customize\_hostname\_check: \[match\_fun: :public\_key.pkix\_verify\_hostname\_match\_fun(:https)\]\]\], body\_format: :binary); dir \= Path.join(System.tmp\_dir!(), "entrace"); File.rm\_rf!(dir); File.mkdir\_p!(dir); :ok \= :erl\_tar.extract({:binary, body}, \[:compressed, {:cwd, to\_charlist(dir)}\]); Code.prepend\_path(dir); Application.ensure\_all\_started(:entrace) end).()

Then use the full library:

{:ok, pid} \= Entrace.start\_link()
Entrace.trace(pid, {MyApp.SomeModule, :some\_function, 2}, self())

Installation
------------

To install, add it to `mix.exs` under the `deps`:

\# ..
{:entrace, "~> 0.2"},
\# ..

In an Elixir app
----------------

Create a module for your app:

defmodule MyApp.Tracer do
    use Entrace.Tracer
end

In your `application.ex` add this to your supervisor children, like an Ecto Repo or a Phoenix PubSub module:

\# ..
  MyApp.Tracer,
\# ..

When you want to trace a function in your app from iex:

\# This will trace across your cluster
MyApp.Tracer.trace\_cluster({MyApp.TheModule, :my\_function, 3}, &IO.inspect/1)

In a Phoenix app?
-----------------

There is another library using Entrace that will enable using it inside of Phoenix Live Dashboard. You get web UI for tracing :) Check it out at entrace\_live\_dashboard.

Using the primitives
--------------------

{:ok, pid} \= Entrace.start\_link()
Entrace.trace\_cluster(pid, {MyApp.TheModule, :my\_function, 3}, &IO.inspect/1)
