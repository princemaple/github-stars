---
project: plug_attack
stars: 448
description: A plug building toolkit for blocking and throttling abusive requests
url: https://github.com/michalmuskala/plug_attack
---

PlugAttack
==========

A plug building toolkit for blocking and throttling abusive requests.

This is inspired by the Kickstarter's Rack::Attack middleware for Ruby.

Installation
------------

Add `plug_attack` to your list of dependencies in `mix.exs`:

def deps do
  \[{:plug\_attack, "~> 0.4.3"}\]
end

Basic usage
-----------

We first need to construct a plug that will list various rules we want to apply:

defmodule MyApp.PlugAttack do
  use PlugAttack

  rule "allow local", conn do
    allow conn.remote\_ip \== {127, 0, 0, 1}
  end
end

The `MyApp.PlugAttack` module is now a regular plug that can be used, for example, in a phoenix endpoint.

_WARNING_: if you're behind a proxy, like nginx or heroku's router, you need to make sure you have a plug that respects the `X-Forwarded-For` headers, for example: remote\_ip.

Throttling
----------

Before we implement throttling in our attack plug, we need to add a storage to our supervision tree. This can be achieved by adding following to the supervision tree:

children \= \[
  {PlugAttack.Storage.Ets, name: MyApp.PlugAttack.Storage, clean\_period: 60\_000}
\]

We've configured the table to be cleaned of stale data every minute. The usage patterns of the table by the throttling rules means no stale data will be ever accessed. This is only a measure used to control the memory usage.

Now we can add a rule to our plug allowing 10 requests every minute from a single ip address:

rule "throttle by ip", conn do
  throttle conn.remote\_ip,
    period: 60\_000, limit: 10,
    storage: {PlugAttack.Storage.Ets, MyApp.PlugAttack.Storage}
end

Rate limiting headers
---------------------

We can customize the actions taken by `PlugAttack` on blocked or allowed requests, by adding rate limiting headers for well behaved clients.

To do this, we can define two functions in our plug - `allow_action/3` and `block_action/3`. Those are similar to regular plugs - accepting a connection as the first argument and opts as the last one. The middle argument represents the blocking or allowing data returned by the rule. The throttling rule returns data in the form of `{:throttle, data}`, where `data` is a keyword with various useful data we can use to construct rate limiting headers.

import Plug.Conn
def allow\_action(conn, {:throttle, data}, opts) do
  conn
  |> add\_throttling\_headers(data)
  |> allow\_action(true, opts)
end

def allow\_action(conn, \_data, \_opts) do
  conn
end

def block\_action(conn, {:throttle, data}, opts) do
  conn
  |> add\_throttling\_headers(data)
  |> block\_action(false, opts)
end

def block\_action(conn, \_data, \_opts) do
  conn
  |> send\_resp(:forbidden, "Forbidden\\n")
  |> halt \# It's important to halt connection once we send a response early
end

defp add\_throttling\_headers(conn, data) do
  \# The expires\_at value is a unix time in milliseconds, we want to return one
  \# in seconds
  reset \= div(data\[:expires\_at\], 1\_000)
  conn
  |> put\_resp\_header("x-ratelimit-limit", to\_string(data\[:limit\]))
  |> put\_resp\_header("x-ratelimit-remaining", to\_string(data\[:remaining\]))
  |> put\_resp\_header("x-ratelimit-reset", to\_string(reset))
end

License
-------

Copyright 2015 Michał Muskała

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

```
http://www.apache.org/licenses/LICENSE-2.0
```

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
