---
project: cachex
stars: 1737
description: A powerful caching library for Elixir with support for transactions, fallbacks and expirations
url: https://github.com/whitfin/cachex
---

Cachex
======

Cachex is an extremely fast in-memory key/value store with support for many useful features:

-   Time-based key expirations
-   Maximum size protection
-   Pre/post execution hooks
-   Proactive/reactive cache warming
-   Transactions and row locking
-   Asynchronous write operations
-   Distribution across app nodes
-   Syncing to a local filesystem
-   Idiomatic cache streaming
-   Batched write operations
-   User command invocation
-   Statistics gathering

All of these features are optional and are off by default so you can pick and choose those you wish to enable.

Setting Up
----------

To get started, please add Cachex to your `mix.exs` list of dependencies and then pull it using `mix deps.get`:

def deps do
  \[{:cachex, "~> 4.0"}\]
end

Depending on what you're trying to do, there are a couple of different ways you might want to go about starting a cache. If you're testing out Cachex inside `iex`, you can call `Cachex.start_link/2` manually:

Cachex.start\_link(:my\_cache)     \# with default options
Cachex.start\_link(:my\_cache, \[\]) \# with custom options

In other cases, you might want to start a cache within an existing supervision tree. If you created your project via `mix` with the `--sup` flag, this should be available to you inside `lib/my_app/application.ex`:

children \= \[
  {Cachex, \[:my\_cache\]},     \# with default options
  {Cachex, \[:my\_cache, \[\]\]}  \# with custom options
\]

Both of these approaches work the same way; your options are parsed and your cache is started as a child under the appropriate parent process. The latter is recommended for production applications, as it will ensure your cache is managed correctly inside your application.

Basic Examples
--------------

Working with a cache is pretty straightforward, and basically everything is provided by the core `Cachex` module. You can make calls to a cache using the name you registered it under at startup time.

Let's take a quick look at some basic calls you can make to a cache in a quick `iex` session:

\# create a default cache in our shell session
{:ok, \_pid} \= Cachex.start\_link(:my\_cache)

\# place a "my\_value" string against the key "my\_key"
:ok \= Cachex.put(:my\_cache, "my\_key", "my\_value")

\# verify that the key exists under the key name
true \= Cachex.exists?(:my\_cache, "my\_key")

\# verify that "my\_value" is returned when we retrieve
"my\_value" \= Cachex.get(:my\_cache, "my\_key")

\# remove the "my\_key" key from the cache
:ok \= Cachex.del(:my\_cache, "my\_key")

\# verify that the key no longer exists
false \= Cachex.exists?(:my\_cache, "my\_key")

\# verify that "my\_value" is no longer returned
nil \= Cachex.get(:my\_cache, "my\_key")

For cache actions which are fallible and can return an error tuple, the Cachex API provides an automatically generated "unsafe" equivalent (i.e. appended with `!`). These options will unpack the returned tuple, and return values directly:

\# write a non-numeric value to the table
:ok \= Cachex.put(:my\_cache, "one", "one")

\# attempt to increment a non-numeric value and get an error
{:error, :non\_numeric\_value} \= Cachex.incr(:my\_cache, "one")

\# but calling with \`!\` raises the error
Cachex.incr!(:my\_cache, "one")
\*\* (Cachex.Error) Attempted arithmetic operations on a non\-numeric value
    (cachex) lib/cachex.ex:1439: Cachex.unwrap/1

The `!` version of functions exists for convenience, in particular to make chaining and assertions easier in unit testing. For production use cases it's recommended to avoid `!` wrappers, and instead explicitly handle the different response types.

Advanced Examples
-----------------

Beyond the typical get/set semantics of a cache, Cachex offers many additional features to help with typical use cases and access patterns a developer may meet during their day-to-day.

While the list is too long to properly cover everything in detail here, let's take a look at some of the most common cache actions:

\# create a default cache in our shell session
{:ok, \_pid} \= Cachex.start\_link(:my\_cache)

\# place some values in a single batch call
:ok \= Cachex.put\_many(:my\_cache, \[
    {"key1", 1},
    {"key2", 2},
    {"key3", 3}
\])

\# now let's do an atomic update operation against the key in the cache
{:commit, 2} \= Cachex.get\_and\_update(:my\_cache, "key1", fn value \->
    value + 1
end)

\# we can also do this via \`Cachex.incr/2\`
2 \= Cachex.incr(:my\_cache, "key2")

\# and of course the inverse via \`Cachex.decr/2\`
0 \= Cachex.decr(:my\_cache, "key3")

\# we can also lazily compute keys if they're missing from the cache
{:commit, "nazrat"} \= Cachex.fetch(:my\_cache, "tarzan", fn key \->
  {:commit, String.reverse(key)}
end)

\# we can also write keys with a time expiration (in milliseconds)
:ok \= Cachex.put(:my\_cache, "secret\_mission", "...", expire: 1)

\# and if we pull it back after expiration, it's not there!
nil \= Cachex.get(:my\_cache, "secret\_mission")

These are just some of the conveniences made available by Cachex's API, but there's still a bunch of other fun stuff in the `Cachex` API, covering a broad range of patterns and use cases.

For further information or examples on supported features and options, please see the Cachex documentation where there are several guides on specific features and workflows.

All of the hosted documentation is also available in raw form in the repository.

Benchmarks
----------

There are some very trivial benchmarks available using Benchee in the `benchmarks/` directory. You can run the benchmarks using the following command:

# default benchmarks
$ mix bench

# enable benchmarks for compressed tests
$ CACHEX\_BENCH\_COMPRESS=true mix bench

# enable benchmarks for transactional tests
$ CACHEX\_BENCH\_TRANSACTIONS=true mix bench

Any combination of these environment variables is also possible, to allow you to test and benchmark your specific workflows.

Contributions
-------------

If you feel something can be improved, or have any questions about certain behaviours or pieces of implementation, please feel free to file an issue. Proposed changes should be taken to issues before any PRs to avoid wasting time on code which might not be merged upstream.

If you _do_ make changes to the codebase, please make sure you test your changes thoroughly, and include any unit tests alongside new or changed behaviours. Cachex currently uses the excellent excoveralls to track code coverage.

$ mix test # --exclude=distributed to skip slower tests
$ mix credo
$ mix coveralls
$ mix coveralls.html && open cover/excoveralls.html

Thank you to everyone who has contributed to the codebase, and to everyone who has taken the time to open an issue or PR to help improve the project!
