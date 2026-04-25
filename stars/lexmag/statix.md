---
project: statix
stars: 284
description: Fast and reliable Elixir client for StatsD-compatible servers
url: https://github.com/lexmag/statix
---

Statix
======

Statix is an Elixir client for StatsD-compatible servers. It is focused on speed without sacrificing simplicity, completeness, or correctness.

What makes Statix the fastest library around:

-   direct sending to socket \[1\]
-   caching of the UDP packet header
-   connection pooling to distribute the metric sending
-   diligent usage of IO lists

\[1\] In contrast with process-based clients, Statix has lower memory consumption and higher throughput – Statix v1.0.0 does about **876640** counter increments per flush:

It is possible to measure that yourself.

for \_ <- 1..10\_000 do
  Task.start(fn \->
    for \_ <- 1..10\_000 do
      StatixSample.increment("sample", 1)
    end
  end)
end

Make sure you have StatsD server running to get more realistic results.

See the documentation for detailed usage information.

Installation
------------

Add Statix as a dependency to your `mix.exs` file:

defp deps() do
  \[{:statix, ">= 0.0.0"}\]
end

Then run `mix deps.get` in your shell to fetch the dependencies.

License
-------

This software is licensed under the ISC license.
