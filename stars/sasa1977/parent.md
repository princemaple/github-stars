---
project: parent
stars: 276
description: Custom parenting of processes in Elixir
url: https://github.com/sasa1977/parent
---

Parent
======

Support for custom parenting of processes. See docs for reference.

Parent is a toolkit for building processes which parent other children and manage their life cycles. The library provides features similar to `Supervisor`, such as the support for automatic restarts and failure escalation (maximum restart intensity), with some additional benefits that can help flattening the supervision tree, reduce the amount of custom process monitors, and simplify the process structure. The most important differences from `Supervisor` are:

-   No supervision strategies (one\_for\_one, rest\_for\_one, etc). Instead, Parent uses bindings and shutdown groups to achieve the similar behaviour.
-   No distinction between static and dynamic supervisors. Instead, a per-child option called `:ephemeral?` is used to achieve dynamic behaviour.
-   Basic registry-like capabilities for simple children discovery baked-in directly into parent.
-   Exposed lower level plumbing modules, such as `Parent.GenServer` and `Parent`, which can be used to build custom parent processes (i.e. supervisors with custom logic).

Examples
--------

### Basic supervisor

Parent.Supervisor.start\_link(
  \# child spec is a superset of supervisor child specification
  child\_specs,

  \# parent options, note that there's no \`:strategy\`
  max\_restarts: 3,
  max\_seconds: 5,

  \# std. Supervisor/GenServer options
  name: \_\_MODULE\_\_
)

### Binding lifecycles

Parent.Supervisor.start\_link(
  \[
    Parent.child\_spec(Child1),
    Parent.child\_spec(Child2, binds\_to: \[Child1\]),
    Parent.child\_spec(Child3, binds\_to: \[Child1\]),
    Parent.child\_spec(Child4, shutdown\_group: :children4\_to\_6),
    Parent.child\_spec(Child5, shutdown\_group: :children4\_to\_6),
    Parent.child\_spec(Child6, shutdown\_group: :children4\_to\_6),
    Parent.child\_spec(Child7, binds\_to: \[Child1\]),
  \]
)

-   if `Child1` is restarted, `Child2`, `Child3`, and `Child7` will be restarted too
-   if `Child2`, `Child3`, or `Child7` is restarted, nothing else is restarted
-   if any of `Child4`, `Child5`, or `Child6` is restarted, all other processes from the shutdown group are restarted too

### Discovering siblings during startup

Parent.Supervisor.start\_link(
  \[
    Parent.child\_spec(Child1),
    Parent.child\_spec(Child2, binds\_to: \[Child1\]),
    \# ...
  \]
)

defmodule Child2 do
  def start\_link do
    \# can be safely invoked inside the parent process
    child1 \= Parent.child\_pid(:child1)

    \# ...
  end
end

### Pausing and resuming a part of the system

\# stops child1 and all children depending on it, removing it from the parent
stopped\_children \= Parent.Client.shutdown\_child(some\_parent, :child1)

\# ...

\# returns all stopped children back to the parent
Parent.Client.return\_children(some\_parent, stopped\_children)

### Dynamic supervisor with anonymous children

Parent.Supervisor.start\_link(\[\], name: MySup)

\# set \`ephemeral?: true\` for dynamic children if child is temporary/transient
{:ok, pid1} \= Parent.Client.start\_child(MySup, Parent.child\_spec(Child, id: nil, ephemeral?: true))
{:ok, pid2} \= Parent.Client.start\_child(MySup, Parent.child\_spec(Child, id: nil, ephemeral?: true))
\# ...

Parent.Client.shutdown\_child(MySup, pid1)
Parent.Client.restart\_child(MySup, pid2)

### Dynamic supervisor with child discovery

Parent.Supervisor.start\_link(\[\], name: MySup)

\# meta is an optional value associated with the child
Parent.Client.start\_child(MySup, Parent.child\_spec(Child, id: id1, ephemeral?: true, meta: some\_meta))
Parent.Client.start\_child(MySup, Parent.child\_spec(Child, id: id2, ephemeral?: true, meta: another\_meta))
\# ...

\# synchronous calls into the parent process
pid \= Parent.Client.child\_pid(MySup, id1)
meta \= Parent.Client.child\_meta(MySub, id1)
all\_children \= Parent.Client.children(MySup)

Optional ETS-powered registry:

Parent.Supervisor.start\_link(\[\], registry?: true)

\# start some children

\# ETS lookup, no call into parent involved
Parent.Client.child\_pid(my\_sup, id1)
Parent.Client.children(my\_sup)

### Per-child max restart frequency

Parent.Supervisor.start\_link(
  \[
    Parent.child\_spec(Child1, max\_restarts: 10, max\_seconds: 10),
    Parent.child\_spec(Child2, max\_restarts: 3, max\_seconds: 5)
  \],

  \# Per-parent max restart frequency can be disabled, or a parent-wide limit can be used. In the
  \# former case make sure that this limit is higher than the limit of any child.
  max\_restarts: :infinity
)

### Module-based supervisor

defmodule MySup do
  use Parent.GenServer

  def start\_link(init\_arg),
    do: Parent.GenServer.start\_link(\_\_MODULE\_\_, init\_arg, name: \_\_MODULE\_\_)

  @impl GenServer
  def init(\_init\_arg) do
    Parent.start\_all\_children!(children)
    {:ok, initial\_state}
  end
end

### Restarting with a delay

defmodule MySup do
  use Parent.GenServer

  def start\_link(init\_arg),
    do: Parent.GenServer.start\_link(\_\_MODULE\_\_, init\_arg, name: \_\_MODULE\_\_)

  @impl GenServer
  def init(\_init\_arg) do
    \# Make sure that children are temporary and ephemeral b/c otherwise \`handle\_stopped\_children/2\`
    \# won't be invoked.
    Parent.start\_all\_children!(children)
    {:ok, initial\_state}
  end

  @impl Parent.GenServer
  def handle\_stopped\_children(stopped\_children, state) do
    \# invoked when a child stops and is not restarted
    Process.send\_after(self, {:restart, stopped\_children}, delay)
    {:noreply, state}
  end

  def handle\_info({:restart, stopped\_children}, state) do
    \# Returns the child to the parent preserving its place according to startup order and bumping
    \# its restart count. This is basically a manual restart.
    Parent.return\_children(stopped\_children)
    {:noreply, state}
  end
end

### Starting additional children after a child stops

defmodule MySup do
  use Parent.GenServer

  def start\_link(init\_arg),
    do: Parent.GenServer.start\_link(\_\_MODULE\_\_, init\_arg, name: \_\_MODULE\_\_)

  @impl GenServer
  def init(\_init\_arg) do
    Parent.start\_child(first\_child\_spec)
    {:ok, initial\_state}
  end

  @impl Parent.GenServer
  def handle\_stopped\_children(%{child1: info}, state) do
    Parent.start\_child(other\_children)
    {:noreply, state}
  end

  def handle\_stopped\_children(\_other, state), do: {:noreply, state}
end

### Building a custom parent process or behaviour from scratch

defp init\_process do
  Parent.initialize(parent\_opts)
  start\_some\_children()
  loop()
end

defp loop() do
  receive do
    msg \->
      case Parent.handle\_message(msg) do
        \# parent handled the message
        :ignore \-> loop()

        \# parent handled the message and returned some useful information
        {:stopped\_children, stopped\_children} \-> handle\_stopped\_children(stopped\_children)

        \# not a parent message
        nil \-> custom\_handle\_message(msg)
      end
  end
end

Status
------

This library has seen production usage in a couple of different projects. However, features such as automatic restarts and ETS registry are pretty fresh (aded in late 2020) and so they haven't seen any serious production testing yet.

Based on a very quick & shallow test, Parent is about 3x slower and consumes about 2x more memory than DynamicSupervisor.

The API is prone to significant changes.

Compared to supervisor crash reports, the error logging is very basic and probably not sufficient.

License
-------

MIT
