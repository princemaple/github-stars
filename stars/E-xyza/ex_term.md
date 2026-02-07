---
project: ex_term
stars: 78
description: Phoenix LiveView Terminal LiveComponent
url: https://github.com/E-xyza/ex_term
---

ExTerm
======

ExTerm is a terminal `Phoenix.LiveView`. By default, ExTerm provides an IEx terminal usable as a web interface, however, this is customizable and you may use ExTerm for other CLIs.

Under the hood, ExTerm is a generic interface for converting erlang IO protocol messages into web output and translating web input into responses in the IO protocol.

Installation
------------

Add ExTerm to your mix.exs:

def deps do
\[
  \# ...
  {:ex\_term, "~> 0.2"}
  \# ...
\]
end

### How to create a live terminal in your Phoenix router

You must supply a `Phoenix.PubSub` server that is the communication channel to send important updates to the liveview. It's recommended to use the PubSub server associated with your web server.

import ExTerm.Router

scope "/live\_term" do
  pipe\_through :browser

  live\_term "/", pubsub\_server: MyAppWeb.PubSub
end

Documentation
-------------

Documentation is available on hexdocs.pm: https://hexdocs.pm/ex\_term

### Planned (Pro?) features:

-   provenance tracking
-   multiplayer mode
