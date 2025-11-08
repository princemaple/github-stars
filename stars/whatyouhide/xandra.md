---
project: xandra
stars: 425
description: Fast, simple, and robust Cassandra/ScyllaDB driver for Elixir.
url: https://github.com/whatyouhide/xandra
---

Xandra
======

> Fast and robust Cassandra driver for Elixir.

Xandra is a Cassandra driver built natively in Elixir and focused on speed, simplicity, and robustness. This driver works exclusively with the Cassandra Query Language v3 (CQL3) and native protocol _v3_, _v4_, and _v5_.

Features
--------

-   🎱 Connection pooling with automatic reconnections
-   🌯 Prepared queries (with local cache of prepared queries on a per-connection basis) and batch queries
-   📃 Page streaming
-   🗜️ LZ4 compression
-   👩‍👩‍👧‍👧 Clustering with support for autodiscovery of nodes in the cluster
-   🔁 Customizable retry strategies for failed queries
-   👩‍💻 User-defined types
-   🔑 Authentication
-   🔐 SSL encryption

See the documentation for detailed explanation of how the supported features work.

Installation
------------

Add the `:xandra` dependency to your `mix.exs` file:

defp deps do
  \[
    {:xandra, "~> 0.19"}
  \]
end

Then, run `mix deps.get` in your shell to fetch the new dependency.

Overview
--------

The documentation is available on HexDocs.

Connections or pool of connections can be started with `Xandra.start_link/1`:

{:ok, conn} \= Xandra.start\_link(nodes: \["127.0.0.1:9042"\])

This connection can be used to perform all operations against the Cassandra server. Executing simple queries looks like this:

statement \= "INSERT INTO users (name, postcode) VALUES ('Priam', 67100)"
{:ok, %Xandra.Void{}} \= Xandra.execute(conn, statement, \_params \= \[\])

Preparing and executing a query:

with {:ok, prepared} <- Xandra.prepare(conn, "SELECT \* FROM users WHERE name = ?"),
     {:ok, %Xandra.Page{}} <- Xandra.execute(conn, prepared, \[\_name \= "Priam"\]),
     do: Enum.to\_list(page)

Xandra supports streaming pages:

prepared \= Xandra.prepare!(conn, "SELECT \* FROM subscriptions WHERE topic = :topic")
page\_stream \= Xandra.stream\_pages!(conn, prepared, \_params \= \[\], page\_size: 1\_000)

\# This is going to execute the prepared query every time a new page is needed:
page\_stream
|> Enum.take(10)
|> Enum.each(fn page \-> IO.puts("Got a bunch of rows: #{inspect(Enum.to\_list(page))}") end)

Scylla support
--------------

Xandra supports Scylla (version `2.x` to `5.x`) without the need to do anything in particular.

License
-------

Xandra is released under the ISC license, see the LICENSE file.
