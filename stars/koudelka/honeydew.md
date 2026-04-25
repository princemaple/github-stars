---
project: honeydew
stars: 727
description: Job Queue for Elixir. Clustered or Local. Straight BEAM. Optional Ecto. 💪🍈
url: https://github.com/koudelka/honeydew
---

Honeydew 💪🏻🍈
===============

Honeydew ("Honey, do!") is a pluggable job queue and worker pool for Elixir, focused on at-least-once execution.

defmodule MyWorker do
  def do\_a\_thing do
    IO.puts "doing a thing!"
  end
end

:ok \= Honeydew.start\_queue(:my\_queue)
:ok \= Honeydew.start\_workers(:my\_queue, MyWorker)

:do\_a\_thing |> Honeydew.async(:my\_queue)

\# => "doing a thing!"

**Isolation**

-   Jobs are run in isolated one-time-use processes.
-   Optionally stores immutable state loaned to each worker (a database connection, for example).
-   Initialized Worker

**Strong Job Custody**

-   Jobs don't leave the queue until either they succeed, are explicitly abandoned or are moved to another queue.
-   Workers are issued only one job at a time, no batching.
-   If a worker crashes while processing a job, the job is reset and a "failure mode" (e.g. abandon, move, retry) is executed. (The default failure mode is to abandon the job.)
-   Job Lifecycle

**Clusterable Components**

-   Queues, workers and your enqueuing processes can exist anywhere in the BEAM cluster.
-   Global Queues

**Plugability**

-   Queues, workers, dispatch strategies, failure modes and success modes are all plugable with user modules.
-   No forced dependency on external queue services.

**Batteries Included**

-   Mnesia Queue, for in-memory/persistence and simple distribution scenarios. (default)
-   Ecto Queue, to turn an Ecto schema into its own work queue, using your database.
-   Fast In-Memory Queue, for fast processing of recreatable jobs without delay requirements.
-   Can optionally heal the cluster after a disconnect or downed node when using a Global Queue.
-   Delayed Jobs
-   Exponential Retry, even works with Ecto queues!

**Easy API**

-   Jobs are enqueued using `async/3` and you can receive replies with `yield/2`, somewhat like Task.
-   API Overview
-   Hex Docs

### Ecto Queue

The Ecto Queue is designed to painlessly turn your Ecto schema into a queue, using your repo as the backing store.

-   You don't need to explicitly enqueue jobs, that's handled for you (for example, sending a welcome email when a new User is inserted).
-   Eliminates the possibility of your database and work queue becoming out of sync
-   As the database is the queue, you don't need to run a separate queue node.
-   You get all of the high-availability, consistency and distribution semantics of your chosen database.

Check out the included example project, and its README.

Getting Started
---------------

In your mix.exs file:

defp deps do
  \[{:honeydew, "~> 1.5.0"}\]
end

Deployment
----------

If you're using the Mnesia queue (the default), you'll need tell your release system to include the `:mnesia` application, and you'll have to decide how you're going to create your on-disk schema files, which needs to be done while mnesia is _not_ running.

If you use mnesia outside of Honeydew, you'll want to use the `:extra_applications` configuration key in your mix.exs file, as well as manually creating your mnesia schema with `:mnesia.create_schema(nodes)` in an iex session in production:

def application do
  \[
    extra\_applications: \[:mnesia\]
  \]
end

Otherwise, if Honeydew is the only user of mnesia, you can let Honeydew manage it by simply using the `:included_applications` key instead.

def application do
  \[
    included\_applications: \[:mnesia\]
  \]
end

### tl;dr

-   Check out the examples.
-   Enqueue jobs with `Honeydew.async/3`, delay jobs by passing `delay_secs: <integer>`.
-   Receive responses with `Honeydew.yield/2`.
-   Emit job progress with `progress/1`
-   Queue/Worker status with `Honeydew.status/1`
-   Suspend and resume with `Honeydew.suspend/1` and `Honeydew.resume/1`
-   List jobs with `Honeydew.filter/2`
-   Move jobs with `Honeydew.move/2`
-   Cancel jobs with `Honeydew.cancel/2`

### README

The rest of the README is broken out into slightly more digestible sections.

Also, check out the README files included with each of the examples.

### CHANGELOG

It's worth keeping abreast with the CHANGELOG
