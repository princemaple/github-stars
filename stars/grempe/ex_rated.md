---
project: ex_rated
stars: 457
description: ExRated, the Elixir OTP GenServer with the naughty name that allows you to rate-limit calls to any service that requires it.
url: https://github.com/grempe/ex_rated
---

ExRated
=======

ExRated is:

1.  A port of the Erlang 'raterlimiter' project to Elixir.
2.  An OTP GenServer process that allows you to rate limit calls to something like an external API.
3.  The Hex.pm package with the naughty name.

You can learn more about the concept for this rate limiter in the Token Bucket article on Wikipedia

If you use the PhoenixFramework there is also a great blog post on Rate Limiting a Phoenix API by danielberkompas describing how to write a plug to use ExRated in your own API. Its fast and its easy.

Usage
-----

Call the ExRated application with `ExRated.check_rate/3`. This function takes three arguments:

1.  A `bucket name` (Erlang term, typically String). You can have as many buckets as you need.
2.  A `scale` (Integer). The time scale in milliseconds that the bucket is valid for.
3.  A `limit` (Integer). How many actions you want to limit your app to in the time scale provided.

For example, if you have to enforce a rate limit of no more than 5 calls in 10 seconds to your API:

iex\> ExRated.check\_rate("my-rate-limited-api", 10\_000, 5)
{:ok, 1}

The `ExRated.check_rate` function will return an `{:ok, Integer}` tuple if its OK to proceed with your rate limited function. The Integer returned is the current value of the incrementing counter showing how many times in the time scale window your function has already been called. If you are over limit a `{:error, Integer}` tuple will be returned where the Integer is always the limit you have specified in the function call.

Call the ExRated application with `ExRated.inspect_bucket/3`. This function takes the same three arguments as `check_rate`:

For example, if you want to inspect the bucket for your API:

iex\> ExRated.inspect\_bucket("my-rate-limited-api", 10\_000, 5)
{0, 5, 2483, nil, nil}
iex\> ExRated.check\_rate("my-rate-limited-api", 10\_000, 5)
{:ok, 1}
iex\> ExRated.inspect\_bucket("my-rate-limited-api", 10\_000, 5)
{1, 4, 723, 1450282268397, 1450282268397}

The `ExRated.inspect_bucket` function will return a `{count, count_remaining, ms_to_next_bucket, created_at, updated_at}` tuple, count and count\_remaining are integers, ms\_to\_next\_bucket is the number of milliseconds before the bucket resets, created\_at and updated\_at are timestamps in milliseconds.

Call the ExRated application with `ExRated.delete_bucket/1`. This function takes one argument:

1.  A `bucket name` (String). You can have as many buckets as you need.

For example, if you want to reset the counter for your API:

iex\> ExRated.delete\_bucket("my-rate-limited-api")
:ok

The `ExRated.delete_bucket` function will return an `:ok` on success or `:error` if the bucket doesn't exist

Installation
------------

You can use ExRated in your projects in two steps:

1.  Add ExRated to your `mix.exs` dependencies:
    
    def deps do
      \[{:ex\_rated, "~> 2.0"}\]
    end
    
2.  List `:ex_rated` in your application dependencies:
    
    def application do
      \[applications: \[:ex\_rated\]\]
    end
    

You can also start the GenServer manually, and pass it custom config, with something like:

{:ok, pid} \= GenServer.start\_link(ExRated, \[ {:timeout, 10\_000}, {:cleanup\_rate, 10\_000}, {:persistent, false} \], \[name: :ex\_rated\])

Alternatively, you can configure them in your `config/config.exs` (or other config) file like

config :ex\_rated,
  timeout: 10\_000,
  cleanup\_rate: 10\_000,
  persistent: false,
  name: :ex\_rated,
  ets\_table\_name: :ets\_rated\_test\_buckets

These args and their defaults are:

`{:timeout, 90_000_000}` : buckets older than this in milliseconds will be automatically pruned.

`{:cleanup_rate, 60_000}` : how often, in milliseconds, the bucket pruning process will be run.

`{:ets_table_name, :ex_rated_buckets}` : The atom name of the ETS table. This can be configured within your `config` files but not when starting the GenServer manually.

`{:persistent, false}` : Whether to persist ETS table to disk with DETS on server stop/restart.

`[name: :ex_rated]` : The registered name of the ExRated GenServer.

Contributing
------------

Please run the following commands before pushing a pull request to ensure your code has been properly formatted and static analysis run.

mix format
mix credo --strict

Testing
-------

It is important that the OTP doesn't get automatically started by Mix.

mix test \--no\-start

Is it fast?
-----------

You can use the `Benchfella` library to do a quick performance test.

On a 2019 Macbook Pro (2.3 GHz 8-Core Intel Core i9, 64GB RAM) the lib can do 10,000,000 checks in less than 10s, averaging 0.89 µs/op (microseconds).

```
$ mix bench
Compiling 1 file (.ex)
Settings:
  duration:      1.0 s

## BasicBench
[10:45:54] 1/1: Basic Bench

Finished in 9.87 seconds

## BasicBench
benchmark na iterations   average time
Basic Bench    10000000   0.89 µs/op
```

Changes
-------

### v2.1.0

-   Fix compilation issues with latest Elixir
-   Update dependencies
-   Update test targets, dropping 1.6

### v2.0.1

-   Add matrix tests for Elixir/OTP versions for Elixir >= 1.6. \[@jechol\]
-   Remove deprecated `Supervisor.Spec.worker` usage. \[@jechol\]
-   Remove `init/1` from generated docs. \[@jechol\]
-   Update config example in README.md

### v2.0.0

-   \[BREAKING\] Fixes #24 (Avoid GenServer Serialization) \[@nabaskes, @benwilson512\]
    -   Improves performance from 2.26 µs/op to 0.89 µs/op (same hardware)
    -   Breaking due to changed method for configuring `ets_table_name` if overriding.
-   Bucket names can be any Erlang term. Fixes #17 \[@denvera\]
-   Update `ex_doc` and `ex2ms` dependencies.
-   `_` prefix unused variables to avoid compilation warnings.
-   Fix compilation warning with `ets_table_name()`
-   Added GitHub Elixir test action.

### v1.3.3

-   Eliminate `warning: function timestamp/1 is unused`. \[@brianberlin\]

### v1.3.2

-   Automatic application inference
-   Update ex\_doc dependency
-   Update minimum Elixer to 1.6+
-   Update "Rate Limiting" blogpost URL reference

### v1.3.1

-   Update `ex2ms` to v1.5

### v1.3.0

-   Fix compilation warnings. \[@walkr\]
-   Start app properly with no args \[@walkr\]
-   Modify start\_link to be callable by `Supervisor.Spec.worker` fun \[@walkr\]

### v1.2.2

-   Update Elixir to v1.2
-   Update `ex2ms` to v1.4

### v1.2.1

-   Change ETS Table to private.
-   Change ETS table name to a non-test name.

### v1.2.0

-   Added `{:persistent, false}` option to server config to allow persisting data to disk.
-   Fixed minor compilation warning.

### v1.1.0

-   Added `delete_bucket/1` function. Takes a bucket name and removes it now instead of waiting for pruning (Nick Sanders).
-   Added `inspect_bucket/3` function. Returns metadata about buckets (Nick Sanders).

### v1.0.0

-   \[BREAKING\] Return {:error, limit} instead of {:fail, limit} to be a bit more idiomatic. Requires semver major version number change.
-   Support Elixir version 1.1 in addition to 1.0

### v0.0.6

-   ExRated internally calls `:erlang.system_time(:milli_seconds)` provided by the new Time API in OTP 18 and greater if available, and will fall back gracefully to the old `:erlang.now()` in older versions. Thanks to Mitchell Henke (mitchellhenke) for the enhancement.

License
-------

ExRated source code is released under Apache 2 License. Check LICENSE file for more information.
