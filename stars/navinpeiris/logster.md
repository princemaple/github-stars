---
project: logster
stars: 206
description: Easily parsable single line, plain text and JSON logger for Plug and Phoenix applications
url: https://github.com/navinpeiris/logster
---

Logster
=======

> **Note**  
> This is the documentation for v2 of Logster. If you're looking for v1, see the v1 branch.

An easy-to-parse, single-line logger for Elixir Phoenix and Plug.Conn, inspired by lograge. Supports logfmt, JSON and custom output formatting.

By default, Phoenix log output for a request looks similar to the following:

```
[info] GET /articles/some-article
[debug] Processing with HelloPhoenix.ArticleController.show/2
  Parameters: %{"id" => "some-article"}
  Pipelines: [:browser]
[info] Sent 200 in 21ms
```

This can be handy for development, but cumbersome for production. The log output is spread across multiple lines, making it difficult to parse and search.

Logster aims to solve this problem by logging the request in a single line:

```
[info] state=sent method=GET path=/articles/some-article format=html controller=HelloPhoenix.ArticleController action=show params={"id":"some-article"} status=200 duration=0.402
```

This is especially handy when integrating with log management services such as Logentries or Papertrail.

Alternatively, Logster can also output JSON formatted logs (see configuration section below):

```
[info] {"state":"sent","method":"GET","path":"/articles/some-article","format":"html","controller":"HelloPhoenix.ArticleController","action":"show","params":{"id":"some-article"},"status":200,"duration":0.402}
```

Installation
------------

Add `:logster` to the list of dependencies in `mix.exs`:

def deps do
  \[{:logster, "~> 2.0.0-rc.1"}\]
end

Upgrading
---------

See Upgrade Guide for more information.

Usage
-----

### Using with Phoenix

Attach the Logster Phoenix logger in the `start` function in your project's `application.ex` file:

\# lib/my\_app/application.ex
def start(\_type, \_args) do
  children \= \[
    \# ...
  \]

  #
  \# Add the line below:
  #
  :ok \= Logster.attach\_phoenix\_logger()

  opts \= \[strategy: :one\_for\_one, name: MyApp.Supervisor\]
  Supervisor.start\_link(children, opts)
end

Next, disable the default Phoenix logger by adding the following line to your `config.exs` file:

config :phoenix, :logger, false

### Using with Plug

Add `Logster.Plug` to your plug pipeline, or in the relevant module:

plug Logster.Plug

### Using standalone logger

Logster provides `debug`, `info`, `warning`, `error` etc convenience functions that mimic those provided by the elixir logger, which outputs messages in your chosen log format.

For example:

Logster.info(service: :payments, event: :received, amount: 1000, customer: 123)

will output the following to the logs:

```
[info] service=payments event=received amount=1000 customer=123
```

You can also provide a function to be called lazily, which will only be called if the log level is enabled:

Logster.debug(fn \->
  \# some potentially expensive operation
  \# won't be called if the log level is not enabled
  customer \= get\_customer\_id()

  \[service: :payments, event: :received, amount: 1000, customer: customer\]
end)

Configuration
-------------

The following configuration options can be set through your `config.exs` file

### Formatter

#### JSON formatter

config :logster, formatter: :json

_Caution:_ There is no guarantee that what reaches your console will be valid JSON. The Elixir `Logger` module has its own formatting which may be appended to your message. See the Logger documentation for more information.

#### Custom formatter

Provide a function that takes one argument, the parameters as input, and returns formatted output

config :logster, formatter: &MyCustomFormatter.format/1

### Filtering parameters

By default, Logster filters parameters named `password`.

To change the filtered parameters:

config :logster, filter\_parameters: \["password", "secret", "token"\]

### Logging HTTP request headers

By default, Logster won't log any request headers. To log specific headers, you can use the `:headers` option:

config :logster, headers: \["my-header-one", "my-header-two"\]

### Changing the log level for a specific controller/action

#### Through Logster.ChangeLogLevel plug

To change the Logster log level for a specific controller and/or action, you use the `Logster.ChangeLogLevel` plug.

For example, to change the logging of all requests in a controller to `debug`, add the following to that controller:

plug Logster.ChangeLogLevel, to: :debug

And to change it only for `index` and `show` actions:

plug Logster.ChangeLogLevel, \[to: :debug\] when action in \[:index, :show\]

This is specially useful for cases such as when you want to lower the log level for a healthcheck endpoint that gets hit every few seconds.

#### Through endpoint configuration

You can set the `Plug.Telemetry` `:log` option to a tuple, `{Mod, Fun, Args}`. `The Plug.Conn.t()` for the request will be prepended to the provided list of arguments.

When invoked, your function must return a `Logger.level()` or `false` to disable logging for the request.

\# lib/my\_app\_web/endpoint.ex
plug Plug.Telemetry,
  event\_prefix: \[:phoenix, :endpoint\],
  log: {\_\_MODULE\_\_, :log\_level, \[\]}

\# Disables logging for routes like /status/\*
def log\_level(%{status: status}) when status \>= 500, do: :error
def log\_level(%{status: status}) when status \>= 400, do: :warning
def log\_level(%{path\_info: \["status" | \_\]}), do: false
def log\_level(\_), do: :info

### Enabling extra fields

One or more of the following fields can be optionally enabled through the `extra_fields` configuration option:

-   host
-   query\_params

Example:

config :logster, extra\_fields: \[:host, :query\_params\]

### Excluding fields

You can exclude fields with `:excludes`:

config :logster, excludes: \[:params, :status, :state\]

Example output:

```
[info] method=GET path=/articles/some-article format=html controller=HelloPhoenix.ArticleController action=show duration=0.402
```

### Renaming default fields

You can rename the default keys passing a map like `%{key: :new_key}`:

config :logster, renames: \[duration: :response\_time, params: :parameters\]

Example output:

```
[info] method=GET path=/articles/some-article format=html controller=HelloPhoenix.ArticleController action=show parameters={"id":"some-article"} status=200 response_time=0.402 state=set
```

### Metadata

Custom metadata can be added to logs using `Logger.metadata` and configuring your logger backend:

\# add metadata for all future logs from this process
Logger.metadata(%{user\_id: "123", foo: "bar"})

\# example for configuring console backend to include metadata in logs.
\# see https://hexdocs.pm/logger/Logger.html#module-console-backend documentation for more
\# config.exs
config :logger, :console, metadata: \[:user\_id, :foo\]

The easiest way to do this app wide is to introduce a new plug which you can include in your Phoenix router pipeline.

For example:

defmodule HelloPhoenix.SetLoggerMetadata do
  def init(opts), do: opts

  def call(conn, \_opts) do
    Logger.metadata user\_id: get\_user\_id(conn),
                    remote\_ip: format\_ip(conn)
    conn
  end

  defp format\_ip(%{remote\_ip: remote\_ip}) when remote\_ip != nil, do: :inet\_parse.ntoa(remote\_ip)
  defp format\_ip(\_), do: nil

  defp get\_user\_id(%{assigns: %{current\_user: %{id: id}}}), do: id
  defp get\_user\_id(\_), do: nil
end

And then add this plug to the relevant pipelines in the router:

pipeline :browser do
  plug :fetch\_session
  plug :fetch\_flash
  plug :put\_secure\_browser\_headers
  \# ...
  plug HelloPhoenix.SetLoggerMetadata
  \# ...
end

Development
-----------

Use the following mix task before pushing commits to run the same checks that are run in CI:

```
mix ci
```

License
-------

The MIT License

Copyright (c) 2016-present Navin Peiris

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.