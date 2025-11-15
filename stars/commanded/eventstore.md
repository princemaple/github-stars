---
project: eventstore
stars: 1129
description: Event store using PostgreSQL for persistence
url: https://github.com/commanded/eventstore
---

EventStore
==========

Event store implemented in Elixir. Uses PostgreSQL as the underlying storage engine.

Requires Elixir v1.10 and PostgreSQL v9.5 or newer.

EventStore supports running on a cluster of nodes.

-   Changelog
-   Wiki
-   Frequently asked questions
-   Getting help
-   Latest published Hex package & documentation

MIT License

* * *

### Overview

> This README and the following guides follow the `master` branch which may not be the currently published version. Read docs for the latest published version of EventStore on Hex.

-   Getting started
    -   Using an existing database
    -   Reset an existing database
    -   Initialize a database using an Elixir release
    -   Using Postgres schemas
    -   Event data and metadata data type
        -   Using the `jsonb` data type
    -   Using with PgBouncer
-   Using the EventStore
    -   Writing to a stream
        -   Appending events to an existing stream
    -   Reading from a stream
    -   Reading from all streams
    -   Stream from all streams
    -   Linking events between streams
    -   Deleting streams
-   Subscriptions
    -   Transient subscriptions
    -   Persistent subscriptions
        -   Acknowledge received events
        -   Subscription concurrency
        -   Example persistent subscriber
        -   Deleting a persistent subscription
-   Running on a cluster
-   Event serialization
-   Upgrading an EventStore
-   Used in production?
-   Backup and administration
-   Benchmarking performance
-   Contributing
    -   Contributors
-   Need help?

* * *

Example usage
-------------

Define an event store module:

defmodule MyEventStore do
  use EventStore, otp\_app: :my\_app
end

Start the event store:

{:ok, \_pid} \= MyEventStore.start\_link()

Create one or more event structs to be persisted (serialized to JSON by default):

defmodule ExampleEvent do
  defstruct \[:key\]
end

Append events to a stream:

stream\_uuid \= EventStore.UUID.uuid4()
expected\_version \= 0

events \= \[
  %EventStore.EventData{
    event\_type: "Elixir.ExampleEvent",
    data: %ExampleEvent{key: "value"},
    metadata: %{user: "someuser@example.com"}
  }
\]

:ok \= MyEventStore.append\_to\_stream(stream\_uuid, expected\_version, events)

Read all events from a single stream, starting at the stream's first event:

{:ok, events} \= MyEventStore.read\_stream\_forward(stream\_uuid)

More: Usage guide

Subscribe to events appended to all streams:

{:ok, subscription} \= MyEventStore.subscribe\_to\_all\_streams("example\_subscription", self())

\# Wait for the subscription confirmation
receive do
  {:subscribed, ^subscription} \->
    IO.puts("Successfully subscribed to all streams")
end

\# Receive a batch of events appended to the event store
receive do
  {:events, events} \->
    IO.puts("Received events: #{inspect events}")

    \# Acknowledge successful receipt of events
    :ok \= MyEventStore.ack(subscription, events)
end

In production use you would use a `GenServer` subscriber process and the `handle_info/2` callback to receive events.

More: Subscriptions guide

Used in production?
-------------------

Yes, this event store is being used in production.

PostgreSQL is used for the underlying storage. Providing guarantees to store data securely. It is ACID-compliant and transactional. PostgreSQL has a proven architecture. A strong reputation for reliability, data integrity, and correctness.

Backup and administration
-------------------------

You can use any standard PostgreSQL tool to manage the event store data:

-   Backup and restore.
-   Continuous archiving and Point-in-Time Recovery (PITR).

Benchmarking performance
------------------------

Run the benchmark suite using mix with the `bench` environment, as configured in `config/bench.exs`. Logging is disabled for benchmarking.

MIX\_ENV=bench mix do es.reset, app.start, bench

Example output:

```
## AppendEventsBench
benchmark name                         iterations   average time
append events, single writer                  100   20288.68 µs/op
append events, 10 concurrent writers           10   127416.90 µs/op
append events, 20 concurrent writers            5   376836.60 µs/op
append events, 50 concurrent writers            2   582350.50 µs/op
## ReadEventsBench
benchmark name                         iterations   average time
read events, single reader                    500   3674.93 µs/op
read events, 10 concurrent readers             50   44653.98 µs/op
read events, 20 concurrent readers             20   73927.55 µs/op
read events, 50 concurrent readers             10   188244.80 µs/op
## SubscribeToStreamBench
benchmark name                         iterations   average time
subscribe to stream, 1 subscription           100   27687.97 µs/op
subscribe to stream, 10 subscriptions          50   56047.72 µs/op
subscribe to stream, 20 subscriptions          10   194164.40 µs/op
subscribe to stream, 50 subscriptions           5   320435.40 µs/op
```

After running two benchmarks you can compare the runs:

MIX\_ENV=bench mix bench.cmp -d percent

You can also produce an HTML page containing a graph comparing benchmark runs:

MIX\_ENV=bench mix bench.graph

Taking the above example output, the append events benchmark is for writing 100 events in a single batch. That's what the µs/op average time is measuring. For a single writer it takes on average 0.02s per 100 events appended (4,929 events/sec) and for 50 concurrent writers it's 50 x 100 events in 0.58s (8,586 events/sec).

For reading events it takes a single reader 3.67ms to read 100 events (27,211 events/sec) and for 50 concurrent readers it takes 0.19s (26,561 events/sec).

### Using the benchmark suite

The purpose of the benchmark suite is to measure the performance impact of proposed changes, as opposed to looking at the raw numbers. The above figures are taken when run against a local PostgreSQL database. You can run the benchmarks against your own hardware to get indicative performance figures for the Event Store.

The benchmark suite is configured to use Erlang's external term format serialization. Using another serialization format, such as JSON, will likely have a negative impact on performance.

Testing
-------

Tests can be run using any Postgres database instance, including via Docker.

To use Docker, first pull the latest Postgres image:

docker pull postgres

A tmpfs mount can be used to run the Docker container with the Postgres data directory stored in memory.

docker run --rm \\
  --name postgres \\
  --tmpfs=/pgtmpfs \\
  -e PGDATA=/pgtmpfs \\
  -e POSTGRES\_PASSWORD=postgres \\
  -e POSTGRES\_USER=postgres \\
  -p 5432:5432 \\
  postgres

Alternatively, use Docker Compose

docker compose up

### Running tests

Create and initialize the test event store databases:

```
MIX_ENV=test mix event_store.setup
```

Run the test suite:

```
mix test
```

Contributing
------------

Pull requests to contribute new or improved features, and extend documentation are most welcome.

Please follow the existing coding conventions, or refer to the Elixir style guide.

You should include unit tests to cover any changes.

### Contributors

EventStore exists thanks to the following people who have contributed.

-   Andreas Riemer
-   Andrey Akulov
-   Basile Nouvellet
-   Ben Smith
-   Bruce Williams
-   Chris Brodt
-   Chris Martin
-   Christian Green
-   Craig Savolainen
-   Damir Vandic
-   David Soff
-   Derek Kraan
-   Diogo Scudelletti
-   Dominik Guzei
-   Douglas Vought
-   Eamon Taaffe
-   Floris Huetink
-   Fredrik Teschke
-   Ilya Suzdalnitskiy
-   Jan Vereecken
-   Kai Kuchenbecker
-   Kaz Walker
-   Morten Berg Nissen
-   Nicholas Henry
-   Olafur Arason
-   Ole Michaelis
-   Paul Iannazzo
-   Piotr Szmielew
-   Raphaël Lustin
-   Ryan Young
-   Samuel Roze
-   Simon Harris
-   Stuart Corbishley
-   Thomas Coopman
-   Victor Oliveira Nascimento
-   Yamil Díaz Aguirre
-   Yannis Weishaupt
-   Yordis Prieto

Need help?
----------

Please open an issue if you encounter a problem, or need assistance. You can also seek help in the #commanded channel in the official Elixir Slack.
