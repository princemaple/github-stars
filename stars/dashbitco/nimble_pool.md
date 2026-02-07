---
project: nimble_pool
stars: 377
description: A tiny resource-pool implementation for Elixir
url: https://github.com/dashbitco/nimble_pool
---

NimblePool
==========

`NimblePool` is a tiny resource-pool implementation.

Pools in the Erlang VM, and therefore in Elixir, are generally process-based: they manage a group of processes. The downside of said pools is that when they have to manage resources, such as sockets or ports, the additional process leads to overhead.

In such pools, you usually end-up with two scenarios:

-   You invoke the pool manager, which returns the pooled process, which performs the operation on the socket or port for you, returning you the reply. This approach is non-optimal because all of the data sent and returned by the resource needs to be copied between processes
    
-   You invoke the pool manager, which returns the pooled process, which gives you access to the resource. Then you can act directly on the resource, avoiding the data copying, but you need to keep the state of the resource in sync with the process
    

NimblePool allows you to implement the second scenario without the addition of processes, which leads to a simpler and more efficient implementation. You should consider using NimblePool whenever you have to manage sockets, ports, or NIF resources and you want the client to perform one-off operations on them. For example, NimblePool is a good solution to manage HTTP/1 connections, ports that need to communicate with long-running programs, etc.

The downside of NimblePool is that, because all resources are under a single process, any resource management operation will happen on this single process, which is more likely to become a bottleneck. This can be addressed, however, by starting one NimblePool per scheduler and by doing scheduler-based dispatches.

NimblePool may not be a good option to manage processes. After all, the goal of NimblePool is to avoid creating processes for resources. If you already have a process, using a process-based pool such as `poolboy` will provide a better abstraction.

Finally, avoid using NimblePool to manage resources that support multiplexing, such as HTTP/2 connections. In fact, pools are not a good option to manage resources with multiplexing in general, as the pool removes the ability to multiplex.

Types of callbacks
------------------

NimblePool has two types of callbacks. Worker callbacks and pool callbacks. The worker callbacks configure the behaviour of each worker, such as initialization, checkin and checkout. The pool callbacks configure general pool behaviour, such as initialization and queueing.

Examples
--------

To use `NimblePool`, you must define a module that implements the pool worker logic, outlined in the `NimblePool` behaviour.

### Port-based example

The example below keeps ports on the pool and check them out on every command. Please read the docs for `Port` before using the approach below, especially in regards to zombie ports.

defmodule PortPool do
  @behaviour NimblePool

  @doc ~S"""
  Executes a given command against a port kept by the pool.
  First we start a pool of ports:
      iex> child = {NimblePool, worker: {PortPool, :cat}, name: PortPool}
      iex> Supervisor.start\_link(\[child\], strategy: :one\_for\_one)
  Now we can run commands against the ports in the pool:
      iex> PortPool.command(PortPool, "hello\\n")
      "hello\\n"
      iex> PortPool.command(PortPool, "world\\n")
      "world\\n"
  """
  def command(pool, command, opts \\\\ \[\]) do
    pool\_timeout \= Keyword.get(opts, :pool\_timeout, 5000)
    receive\_timeout \= Keyword.get(opts, :receive\_timeout, 15000)

    NimblePool.checkout!(pool, :checkout, fn \_from, port \->
      send(port, {self(), {:command, command}})

      receive do
        {^port, {:data, data}} \->
          try do
            Process.unlink(port)
            {data, :ok}
          rescue
            \_ \-> {data, :close}
          end
      after
        receive\_timeout \->
          exit(:receive\_timeout)
      end
    end, pool\_timeout)
  end

  @impl NimblePool
  def init\_worker(:cat \= pool\_state) do
    path \= System.find\_executable("cat")
    port \= Port.open({:spawn\_executable, path}, \[:binary, args: \["-"\]\])
    {:ok, port, pool\_state}
  end

  @impl NimblePool
  \# Transfer the port to the caller
  def handle\_checkout(:checkout, {pid, \_}, port, pool\_state) do
    Port.connect(port, pid)
    {:ok, port, port, pool\_state}
  end

  @impl NimblePool
  \# We got it back
  def handle\_checkin(:ok, \_from, port, pool\_state) do
    {:ok, port, pool\_state}
  end

  def handle\_checkin(:close, \_from, \_port, pool\_state) do
    {:remove, :closed, pool\_state}
  end

  @impl NimblePool
  \# On terminate, effectively close it
  def terminate\_worker(\_reason, port, pool\_state) do
    Port.close(port)
    {:ok, pool\_state}
  end
end

### HTTP/1-based example

The pool below uses Mint for HTTP/1 connections. It establishes connections eagerly. A better approach may be to establish connections lazily on checkout, as done by Finch, which is built on top of Mint + NimbleOptions.

defmodule HTTP1Pool do
  @behaviour NimblePool

  @doc ~S"""
  Executes a given command against a connection kept by the pool.
  First we start the pool:
      child = {NimblePool, worker: {HTTP1Pool, {:https, "elixir-lang.org", 443}}, name: HTTP1Pool}
      Supervisor.start\_link(\[child\], strategy: :one\_for\_one)
  Then we can use the connections in the pool:
      iex> HTTP1Pool.get(HTTP1Pool, "/")
      {:ok, %{status: 200, ...}}
  """
  def get(pool, path, opts \\\\ \[\]) do
    pool\_timeout \= Keyword.get(opts, :pool\_timeout, 5000)
    receive\_timeout \= Keyword.get(opts, :receive\_timeout, 15000)

    NimblePool.checkout!(
      pool,
      :checkout,
      fn \_from, conn \->
        {{kind, result\_or\_error}, conn} \=
          with {:ok, conn, ref} <- Mint.HTTP1.request(conn, "GET", path, \[\], nil),
               {:ok, conn, result} <- receive\_response(\[\], conn, ref, %{}, receive\_timeout) do
            {{:ok, result}, transfer\_if\_open(conn)}
          end

        {{kind, result\_or\_error}, conn}
      end,
      pool\_timeout
    )
  end

  defp transfer\_if\_open(conn) do
    if Mint.HTTP1.open?(conn) do
      {:ok, conn}
    else
      :closed
    end
  end

  defp receive\_response(\[\], conn, ref, response, timeout) do
    {:ok, conn, entries} \= Mint.HTTP1.recv(conn, 0, timeout)
    receive\_response(entries, conn, ref, response, timeout)
  end

  defp receive\_response(\[entry | entries\], conn, ref, response, timeout) do
    case entry do
      {kind, ^ref, value} when kind in \[:status, :headers\] \->
        response \= Map.put(response, kind, value)
        receive\_response(entries, conn, ref, response, timeout)

      {:data, ^ref, data} \->
        response \= Map.update(response, :data, data, &(&1 <> data))
        receive\_response(entries, conn, ref, response, timeout)

      {:done, ^ref} \->
        {:ok, conn, response}

      {:error, ^ref, error} \->
        {:error, conn, error}
    end
  end

  @impl NimblePool
  def init\_worker({scheme, host, port} \= pool\_state) do
    parent \= self()

    async \= fn \->
      \# TODO: Add back-off
      {:ok, conn} \= Mint.HTTP1.connect(scheme, host, port, \[\])
      {:ok, conn} \= Mint.HTTP1.controlling\_process(conn, parent)
      conn
    end

    {:async, async, pool\_state}
  end

  @impl NimblePool
  \# Transfer the conn to the caller.
  \# If we lost the connection, then we remove it to try again.
  def handle\_checkout(:checkout, \_from, conn, pool\_state) do
    with {:ok, conn} <- Mint.HTTP1.set\_mode(conn, :passive) do
      {:ok, conn, conn, pool\_state}
    else
      \_ \-> {:remove, :closed, pool\_state}
    end
  end

  @impl NimblePool
  \# We got it back.
  def handle\_checkin(state, \_from, \_old\_conn, pool\_state) do
    with {:ok, conn} <- state,
         {:ok, conn} <- Mint.HTTP1.set\_mode(conn, :active) do
      {:ok, conn, pool\_state}
    else
      {:error, \_} \-> {:remove, :closed, pool\_state}
    end
  end

  @impl NimblePool
  \# If it is closed, drop it.
  def handle\_info(message, conn) do
    case Mint.HTTP1.stream(conn, message) do
      {:ok, \_, \_} \-> {:ok, conn}
      {:error, \_, \_, \_} \-> {:remove, :closed}
      :unknown \-> {:ok, conn}
    end
  end

  @impl NimblePool
  \# On terminate, effectively close it.
  \# This will succeed even if it was already closed or if we don't own it.
  def terminate\_worker(\_reason, conn, pool\_state) do
    Mint.HTTP1.close(conn)
    {:ok, pool\_state}
  end
end

Installation
------------

Add `nimble_pool` to your list of dependencies in `mix.exs`:

def deps do
  \[{:nimble\_pool, "~> 1.0"}\]
end

Nimble\*
--------

All nimble libraries by Dashbit:

-   NimbleCSV - simple and fast CSV parsing
-   NimbleOptions - tiny library for validating and documenting high-level options
-   NimbleOwnership - resource ownership tracking
-   NimbleParsec - simple and fast parser combinators
-   NimblePool - tiny resource-pool implementation
-   NimblePublisher - a minimal filesystem-based publishing engine with Markdown support and code highlighting
-   NimbleTOTP - tiny library for generating time-based one time passwords (TOTP)

License
-------

Copyright 2019 Plataformatec  
Copyright 2020 Dashbit

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

```
  http://www.apache.org/licenses/LICENSE-2.0
```

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
