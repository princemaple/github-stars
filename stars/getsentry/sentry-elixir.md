---
project: sentry-elixir
stars: 672
description: The official Elixir SDK for Sentry (sentry.io)
url: https://github.com/getsentry/sentry-elixir
---

_Bad software is everywhere, and we're tired of it. Sentry is on a mission to help developers write better software faster, so we can get back to enjoying technology. If you want to join us **Check out our open positions**_

This is the official Sentry SDK for Sentry.

_💁: This README documents unreleased features (from the `master` branch). For documentation on the current release, see the official documentation._

Getting Started
---------------

### Install

To use Sentry in your project, add it as a dependency in your `mix.exs` file.

Sentry does not install a JSON library nor an HTTP client by itself. Sentry will default to the built-in `JSON` for JSON and Finch for HTTP requests, but can be configured to use other ones. To use the default ones, do:

defp deps do
  \[
    \# ...

    {:sentry, "~> 11.0"},
    {:jason, "~> 1.4"},
    {:finch, "~> 0.17.0"}
  \]
end

Warning

If you're using an Elixir version before 1.18, the Sentry SDK will default to Jason as the JSON library. However, you **must** add it to your dependencies:

defp deps do
  \[
    \# ...
    {:sentry, "~> 10.8.1"},
    {:jason, "~> 1.4"}
  \]
end

### Configuration

Sentry has a range of configuration options, but most applications will have a configuration that looks like the following:

\# config/config.exs
config :sentry,
  dsn: "https://public\_key@app.getsentry.com/1",
  environment\_name: config\_env(),
  enable\_source\_code\_context: true,
  root\_source\_code\_paths: \[File.cwd!()\]

### Usage

This library comes with a `:logger` handler to capture error messages coming from process crashes. To enable this, add `Sentry.LoggerHandler` to your production configuration:

\# config/prod.exs
config :my\_app, :logger, \[
  {:handler, :my\_sentry\_handler, Sentry.LoggerHandler, %{
    config: %{
      metadata: \[:file, :line\],
      rate\_limiting: \[max\_events: 10, interval: \_1\_second \= 1\_000\],
      \# Logs all messages with level \`:error\` and above to Sentry.
      \# Remove :capture\_log\_messages and :level if you only want to report crashes.
      capture\_log\_messages: true,
      level: :error
    }
  }}
\]

And then add your logger when your application starts:

\# lib/my\_app/application.ex
def start(\_type, \_args) do
  Logger.add\_handlers(:my\_app)

  \# ...
end

Alternatively, you can skip the `:logger` configuration and add the handler directly to your application's `start/2` callback:

\# lib/my\_app/application.ex
def start(\_type, \_args) do
  :logger.add\_handler(:my\_sentry\_handler, Sentry.LoggerHandler, %{
    config: %{
      metadata: \[:file, :line\],
      rate\_limiting: \[max\_events: 10, interval: \_1\_second \= 1\_000\],
      capture\_log\_messages: true,
      level: :error
    }
  })

  \# ...
end

See all logger configuration options here.

#### Capture exceptions manually

Sometimes you want to capture specific exceptions manually. To do so, use `Sentry.capture_exception/2`.

try do
  ThisWillError.really()
rescue
  my\_exception \->
    Sentry.capture\_exception(my\_exception, stacktrace: \_\_STACKTRACE\_\_)
end

Sometimes you want to capture **messages** that are not exceptions. To do that, use `Sentry.capture_message/2`:

Sentry.capture\_message("custom\_event\_name", extra: %{extra: information})

To learn more about how to use this SDK, refer to the documentation.

#### Testing Your Configuration

To ensure you've set up your configuration correctly we recommend running the included Mix task. It can be tested on different Mix environments and will tell you if it is not currently configured to send events in that environment:

MIX\_ENV=dev mix sentry.send\_test\_event

### Testing with Sentry

In some cases, you may want to _test_ that certain actions in your application cause a report to be sent to Sentry. Sentry itself does this by using Bypass. It is important to note that when modifying the environment configuration the test case should not be run asynchronously, since you are modifying **global configuration**. Not returning the environment configuration to its original state could also affect other tests depending on how the Sentry configuration interacts with them. A good way to make sure to revert the environment is to use the `on_exit/2` callback that ships with ExUnit.

For example:

test "add/2 does not raise but sends an event to Sentry when given bad input" do
  bypass \= Bypass.open()

  Bypass.expect(bypass, fn conn \->
    assert {:ok, \_body, conn} \= Plug.Conn.read\_body(conn)
    Plug.Conn.resp(conn, 200, ~s<{"id": "340"}\>)
  end)

  Sentry.put\_config(:dsn, "http://public:secret@localhost:#{bypass.port}/1")
  Sentry.put\_config(:send\_result, :sync)

  on\_exit(fn \->
    Sentry.put\_config(:dsn, nil)
    Sentry.put\_config(:send\_result, :none)
  end)

  MyModule.add(1, "a")
end

When testing, you will also want to set the `:send_result` type to `:sync`, so that sending Sentry events blocks until the event is sent.

Integrations
------------

-   Phoenix and Plug

Contributing to the SDK
-----------------------

Please make sure to read the CONTRIBUTING.md before making a pull request.

Thanks to everyone who has contributed to this project so far.

Getting Help/Support
--------------------

If you need help setting up or configuring the Elixir SDK (or anything else in the Sentry universe) please head over to the Sentry Community on Discord. There is a ton of great people in our Discord community ready to help you!

Resources
---------

-   
-   
-   
-   
-   

License
-------

Licensed under the MIT license, see `LICENSE`.
