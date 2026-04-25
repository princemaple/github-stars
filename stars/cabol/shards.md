---
project: shards
stars: 296
description: Partitioned ETS tables for Erlang and Elixir
url: https://github.com/cabol/shards
---

Shards
======

> ### ETS tables on steroids!
> 
> Sharding for ETS tables out-of-box.

Why might we need **Sharding/Partitioning** for the ETS tables? The main reason is to keep the lock contention under control enabling ETS tables to scale out and support higher levels of concurrency without lock issues; specially write-locks, which most of the cases might cause significant performance degradation.

Therefore, one of the most common and proven strategies to deal with these problems is Sharding or Partitioning; the principle is pretty similar to DHTs.

This is where shards comes in. Shards is an Erlang/Elixir library fully compatible with the ETS API, but it implements sharding or partitioning on top of the ETS tables, completely transparent and out-of-box.

See the **getting started** guide and the **online documentation**.

Installation
------------

### Erlang

In your `rebar.config`:

{deps, \[
  {shards, "1.1.0"}
\]}.

### Elixir

In your `mix.exs`:

def deps do
  \[{:shards, "~> 1.1"}\]
end

> For more information and examples, see the getting started guide.

Important links
---------------

-   Blog Post - Transparent and out-of-box sharding support for ETS tables in Erlang/Elixir.
    
-   Projects using **shards**:
    
    -   shards\_dist - Distributed version of `shards`. It was moved to a separate repo since `v1.0.0`.
    -   Nebulex – Distributed Caching framework for Elixir.
    -   ExShards – Elixir wrapper for `shards`; with extra and nicer functions.
    -   KVX – Simple Elixir in-memory Key/Value Store using `shards` (default adapter).
    -   Cacherl Distributed Cache using `shards`.

Testing
-------

```
$ make test
```

You can find tests results in `_build/test/logs`, and coverage in `_build/test/cover`.

> **NOTE:** `shards` comes with a helper `Makefile`, but it is just a simple wrapper on top of `rebar3`, therefore, you can do everything using `rebar3` directly as well (e.g.: `rebar3 do ct, cover`).

Generating Edoc
---------------

```
$ make docs
```

> **NOTE:** Once you run the previous command, you will find the generated HTML documentation within `doc` folder; open `doc/index.html`.

Contributing
------------

Contributions to **shards** are very welcome and appreciated!

Use the issue tracker for bug reports or feature requests. Open a pull request when you are ready to contribute.

When submitting a pull request you should not update the CHANGELOG.md, and also make sure you test your changes thoroughly, include unit tests alongside new or changed code.

Before to submit a PR it is highly recommended to run `make check` before and ensure all checks run successfully.

Copyright and License
---------------------

Copyright (c) 2016 Carlos Andres Bolaños R.A.

**Shards** source code is licensed under the MIT License.
