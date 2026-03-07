---
project: elixometer
stars: 827
description: A light Elixir wrapper around exometer.
url: https://github.com/pinterest/elixometer
---

Elixometer
==========

A light wrapper around exometer.

Elixometer allows you to define metrics and subscribe them automatically to the default reporter for your environment.

Installation
------------

Add the following to your dependencies in mix.exs:

{:elixometer, "~> 1.5"}

Or to track the master development branch:

{:elixometer, github: "pinterest/elixometer"}

Then, add `:elixometer` to your applications. That's it!

Configuration
-------------

In one of your config files, set up an exometer reporter, and then register it to elixometer like this:

config(:exometer\_core, report: \[reporters: \[{:exometer\_report\_tty, \[\]}\]\])
config(:elixometer,
  reporter: :exometer\_report\_tty,
  env: Mix.env,
  metric\_prefix: "myapp")

Metrics are prepended with the `metric_prefix`, the type of metric and the environment name.

The optional `update_frequency` key of the :elixometer config controls the interval between reports. By default this is set to `1000` ms in the `dev` environment and `20` ms in the `test` environment.

You can use an environment variable to set the `env`.

config :elixometer, env: {:system, "ELIXOMETER\_ENV"}

Some reporters know how to handle multiple metrics reported at the same time. Or perhaps you want to write a custom reporter, and would like to receive all data points for a single metric all at once. This can be achieved by adding the `report_bulk: true` option to the _reporter_ configuration, and adding `bulk_subscribe: true` to the _elixometer_ configuration. Like so:

config :exometer\_core,
  report: \[
    reporters: \[
      {My.Custom.Reporter, \[report\_bulk: true\]}
    \]
  \]

config :elixometer,
  \# ...
  bulk\_subscribe: true

By default, metrics are formatted using `Elixometer.Utils.format/2`. This function takes care of composing metric names with prefix, environment and the metric type (e.g. `myapp_prefix.dev.timers.request_time`).

This behaviour can be overridden with a custom formatter module (implementing the `Elixometer.Formatter` behaviour) by adding the following configuration entry:

config :elixometer, Elixometer.Updater,
  formatter: MyApp.Formatter

A formatting module implements the `Elixometer.Formatter` behaviour and implements a single function, `format` as such:

defmodule MyApp.Formatter do
  @behaviour Elixometer.Formatter

  \# If you prefer to hyphen-separate your strings, perhaps
  def format(metric\_type, name) do
    String.split("#{metric\_type}\-#{name}", "-")
  end
end

A formatting function can also be used as the configuration entry, provided it follows the same signature as a formatting module:

config :elixometer, Elixometer.Updater,
  formatter: &MyApp.Formatter.format/2

Elixometer uses `pobox` to prevent overload. A maximum size of message buffer, defaulting to 1000, can be configured with:

config :elixometer, Elixometer.Updater,
  max\_messages: 5000

### Excluding datapoints subscriptions

By default, adding a histogram adds for example 11 subscriptions (`[:n, :mean, :min, :max, :median, 50, 75, 90, 95, 99, 999]`). If you would like to restrict which of these you care about, you can exclude some like so:

config :elixometer, excluded\_datapoints: \[:median, 999\]

Metrics
-------

Defining metrics in elixometer is substantially easier than in exometer. Instead of defining and then updating a metric, just update it. Also, instead of providing a list of terms, a metric is named with a period separated bitstring. Presently, Elixometer supports timers, histograms, gauges, counters, and spirals.

Timings may also be defined by annotating a function with a @timed annotation. This annotation takes a key argument, which tells elixometer what key to use. You can specify `:auto` and a key will be generated from the module name and method name.

Updating a metric is similarly easy:

defmodule ParentModule.MetricsTest do
  use Elixometer

  \# Updating a counter
  def counter\_test(thingie) do
    update\_counter("metrics\_test.\\#{thingie}.count", 1)
  end

  \# Updating a spiral
  def spiral\_test(thingie) do
    update\_spiral("metrics\_test.\\#{thingie}.qps", 1)
  end

  \# Timing a block of code in a function
  def timer\_test do
    timed("metrics\_test.timer\_test.timings") do
      OtherModule.slow\_method
    end
  end

  \# Timing a function. The metric name will be \[:timed, :function\]
  @timed(key: "timed.function") \# key will be: prefix.dev.timers.timed.function
  def function\_that\_is\_timed do
    OtherModule.slow\_method
  end

  \# Timing a function with an auto generated key
  \# The key will be "<prefix>.<env>.timers.parent\_module.metrics\_test.another\_timed\_function"
  \# If the env is prod, the environment is omitted from the key
  @timed(key: :auto)
  def another\_timed\_function do
    OtherModule.slow\_method
  end
end

Additional Reporters
--------------------

By default, Elixometer only requires the `exometer_core` package. However, some reporters (namely OpenTSDB and Statsd) are only available by installing the full `exometer` package. If you need the full package, all you need to do is update your `mix.exs` to include `exometer` as a dependency and start it as an application. For example:

def application do
  \[
    applications: \[:exometer,
    ... other applications go here
    \],
    ...
  \]
end

defp deps do
  \[{:exometer\_core, github: "Feuerlabs/exometer\_core"}\]
end

In case a reporter allows for extra configuration options on subscribe, you can configure them in your `elixometer` config like so:

config(:elixometer,
  ...
  subscribe\_options: \[{:tag, :value1}\])

Custom Reporters
----------------

The documentation on custom reporters in `exometer` is fairly difficult to find, and isn't exactly correct. It is still quite useful though, and can be found here.

Your best bet is to define a module that uses the `:exometer_report` behaviour, and use `@impl` on the functions that you add to conform to that behaviour. That will make sure that each function aligns with the behaviour, and that you haven't missed any required ones.

There is one function that is not included as part of the erlang behaviour, but that you may want, which is `exometer_report_bulk/3`. _If and only if_ you have defined that function in your reporter _and_ you passed `report_bulk: true` as an option to the reporter, it will pass a list of datapoint/value pairs to your `exometer_report_bulk/3`.
