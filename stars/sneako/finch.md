---
project: finch
stars: 1342
description: Elixir HTTP client, focused on performance
url: https://github.com/sneako/finch
---

An HTTP client with a focus on performance, built on top of Mint and NimblePool.

We attempt to achieve this goal by providing efficient connection pooling strategies and avoiding copying of memory wherever possible.

Most developers will most likely prefer to use the fabulous HTTP client Req which takes advantage of Finch's pooling and provides an extremely friendly and pleasant to use API.

Usage
-----

In order to use Finch, you must start it and provide a `:name`. Often in your supervision tree:

children \= \[
  {Finch, name: MyFinch}
\]

Or, in rare cases, dynamically:

Finch.start\_link(name: MyFinch)

Once you have started your instance of Finch, you are ready to start making requests:

Finch.build(:get, "https://hex.pm") |> Finch.request(MyFinch)

When using HTTP/1, Finch will parse the passed in URL into a `{scheme, host, port}` tuple, and maintain one or more connection pools for each `{scheme, host, port}` you interact with.

You can also configure a pool size and count to be used for specific URLs that are known before starting Finch. The passed URLs will be parsed into `{scheme, host, port}`, and the corresponding pools will be started. See `Finch.start_link/1` for configuration options.

children \= \[
  {Finch,
   name: MyConfiguredFinch,
   pools: %{
     :default \=> \[size: 10, count: 2\],
     "https://hex.pm" \=> \[size: 32, count: 8\]
   }}
\]

Pools will be started for each configured `{scheme, host, port}` when Finch is started. For any unconfigured `{scheme, host, port}`, the pool will be started the first time it is requested using the `:default` configuration. This means given the pool configuration above each origin/`{scheme, host, port}` will launch 2 (`:count`) new pool processes. So, if you encountered 10 separate combinations, that'd be 20 pool processes.

Note pools are not automatically terminated by default, if you need to terminate them after some idle time, use the `pool_max_idle_time` option (available only for HTTP1 pools).

Telemetry
---------

Finch uses Telemetry to provide instrumentation. See the `Finch.Telemetry` module for details on specific events.

Logging TLS Secrets
-------------------

Finch supports logging TLS secrets to a file. These can be later used in a tool such as Wireshark to decrypt HTTPS sessions. To use this feature you must specify the file to which the secrets should be written. If you are using TLSv1.3 you must also add `keep_secrets: true` to your pool `:transport_opts`. For example:

{Finch,
 name: MyFinch,
 pools: %{
   default: \[conn\_opts: \[transport\_opts: \[keep\_secrets: true\]\]\]
 }}

There are two different ways to specify this file:

1.  The `:ssl_key_log_file` connection option in your pool configuration. For example:

{Finch,
 name: MyFinch,
 pools: %{
   default: \[
     conn\_opts: \[
       ssl\_key\_log\_file: "/writable/path/to/the/sslkey.log"
     \]
   \]
 }}

1.  Alternatively, you could also set the `SSLKEYLOGFILE` environment variable.

Installation
------------

The package can be installed by adding `finch` to your list of dependencies in `mix.exs`:

def deps do
  \[
    {:finch, "~> 0.20"}
  \]
end

The docs can be found at https://hexdocs.pm/finch.
