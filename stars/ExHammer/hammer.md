---
project: hammer
stars: 892
description: An Elixir rate-limiter with pluggable backends
url: https://github.com/ExHammer/hammer
---

Hammer
======

**Hammer** is a rate-limiter for Elixir with pluggable storage backends. Hammer enables users to set limits on actions performed within specified time intervals, applying per-user or global limits on API requests, file uploads, and more.

* * *

Note

This README is for the unreleased master branch, please reference the official documentation on hexdocs for the latest stable release.

* * *

Installation
------------

Hammer is available in Hex. Install by adding `:hammer` to your list of dependencies in `mix.exs`:

def deps do
  \[
    {:hammer, "~> 7.0"}
  \]
end

Available Backends
------------------

Atomic backends are single-node rate limiting but will be the fastest option.

-   Hammer.ETS (default, can be distributed)
-   Hammer.Atomic
-   Hammer.Redis
-   Hammer.Mnesia

Available Algorithms:
---------------------

Each backend supports multiple algorithms. Not all of them are available for all backends. The following table shows which algorithms are available for which backends.

Algorithm

Backend

Hammer.Atomic.FixWindow

Hammer.Atomic

Hammer.Atomic.LeakyBucket

Hammer.Atomic

Hammer.Atomic.TokenBucket

Hammer.Atomic

Hammer.ETS.FixWindow

Hammer.ETS

Hammer.ETS.LeakyBucket

Hammer.ETS

Hammer.ETS.TokenBucket

Hammer.ETS

Hammer.ETS.SlidingWindow

Hammer.ETS

Hammer.Redis.FixedWindow

Hammer.Redis

Hammer.Redis.LeakyBucket

Hammer.Redis

Hammer.Redis.TokenBucket

Hammer.Redis

Hammer.Mnesia.FixedWindow

Hammer.Mnesia

Hammer.Mnesia.LeakyBucket

Hammer.Mnesia

Hammer.Mnesia.TokenBucket

Hammer.Mnesia

Default Algorithm
-----------------

By default, Hammer backends use the **fixed window counter** to track actions within set time windows, resetting the count at the start of each new window. For example, with a limit of 10 uploads per minute, a user could upload up to 10 files between 12:00:00 and 12:00:59, and up to 10 more between 12:01:00 and 12:01:59. Notice that the user can upload 20 videos in a second if the uploads are timed at the window edges. If this is an issue, it can be worked around with a "bursty" counter which can be implemented with the current API by making two checks, one for the original interval with the total limit, and one for a shorter interval with a fraction of the limit. That would smooth out the number of requests allowed.

Algorithm Comparison
--------------------

Here's a comparison of the different rate limiting algorithms to help you choose:

### Fixed Window

-   Simplest implementation with lowest overhead
-   Good for basic rate limiting with clear time boundaries
-   Potential edge case: Up to 2x requests possible at window boundaries
-   Best for: Basic API limits where occasional bursts are acceptable

### Leaky Bucket

-   Provides smooth, consistent request rate
-   Requests "leak" out at constant rate
-   Good for traffic shaping and steady throughput
-   Best for: Network traffic control, queue processing

### Token Bucket

-   Allows controlled bursts while maintaining average rate
-   Tokens regenerate at fixed rate
-   More flexible than fixed windows
-   Best for: APIs needing burst tolerance, gaming mechanics

### Sliding Window

-   Most precise rate limiting
-   No boundary conditions like fixed windows
-   Higher overhead than other algorithms
-   Best for: Strict rate enforcement, critical systems

Selection Guide:

-   Need simple implementation? → Fixed Window
-   Need smooth output rate? → Leaky Bucket
-   Need burst tolerance? → Token Bucket
-   Need precise limits? → Sliding Window

How to use Hammer
-----------------

-   Basic usage is covered in the Tutorial.
-   Distributed usage is covered in the Distributed ETS guide.

The quick start
---------------

-   **Limit:** Maximum number of actions allowed in a window.
-   **Scale:** Duration of the time window (in milliseconds).
-   **Key:** Unique identifier (e.g., user ID) to scope the rate limiting.

Example Usage
-------------

defmodule MyApp.RateLimit do
  use Hammer, backend: :ets
end

MyApp.RateLimit.start\_link()

user\_id \= 42
key \= "upload\_video:#{user\_id}"
scale \= :timer.minutes(1)
limit \= 3

case MyApp.RateLimit.hit(key, scale, limit) do
  {:allow, \_count} \->
    \# upload the video
    :ok

  {:deny, retry\_after} \->
    \# deny the request
    {:error, :rate\_limit, \_message \= "try again in #{retry\_after}ms"}
end

Benchmarks
----------

See the BENCHMARKS.md for more details.

Acknowledgements
----------------

Hammer was originally inspired by the ExRated library, by grempe.

License
-------

Copyright (c) 2023 June Kelly Copyright (c) 2023-2024 See CONTRIBUTORS.md

This library is MIT licensed. See the LICENSE for details.
