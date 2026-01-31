---
project: horde
stars: 1459
description: Horde is a distributed Supervisor and Registry backed by Postgres
url: https://github.com/elixir-horde/horde
---

Horde
=====

Distribute your application over multiple servers with Horde.

Horde is comprised of `Horde.DynamicSupervisor`, a distributed supervisor, and `Horde.Registry`, a distributed registry. Horde is built on top of DeltaCrdt.

Read the full documentation on hexdocs.pm.

There is an introductory blog post and a getting started guide. You can also find me in the Elixir slack channel #horde.

Daniel Azuma gave a great talk at ElixirConf US 2018 where he demonstrated Horde's Supervisor and Registry.

Since Horde is built on CRDTs, it is eventually (as opposed to immediately) consistent, although it does sync its state with its neighbours rather aggressively. Cluster membership in Horde is fully dynamic; nodes can be added and removed at any time and Horde will continue to operate as expected. `Horde.DynamicSupervisor` also uses a hash ring to limit any possible race conditions to times when cluster membership is changing.

`Horde.Registry` and `Horde.DynamicSupervisor` are both designed to stay as close as possible to the API and behavior of their counterparts in Elixir’s standard library. For most scenarios, they can be used as drop-in replacements with minimal changes required.

Some differences do exist — such as the current lack of support for keys: :duplicate in Horde.Registry — but these divergences occur only when standard library behavior does not translate well to a system that is inherently distributed.

Our goal is to keep these differences to the absolute minimum necessary, while ensuring that Horde remains reliable, consistent, and optimized for distributed environments. See documentation of Horde.DynamicSupervisor.start\_link/1 for details.

Running a single global process
-------------------------------

If you simply need to run a single process as a singleton in your cluster, I would encourage you to look at Highlander or HighlanderPG instead, as one of these may fit your use case better.

1.0 release
-----------

Help us get to 1.0, please fill out our very short survey and report any issues you encounter when using Horde.

Fault tolerance
---------------

If a node fails (or otherwise becomes unreachable) then Horde.DynamicSupervisor will redistribute processes among the remaining nodes.

You can choose what to do in the event of a network partition by specifying `:distribution_strategy` in the options for `Horde.DynamicSupervisor.start_link/2`. Setting this option to `Horde.UniformDistribution` (which is the default) distributes processes using a hash mechanism among all reachable nodes. In the event of a network partition, both sides of the partition will continue to operate. Setting it to `Horde.UniformQuorumDistribution` will operate in the same way, but will shut down if less than half of the cluster is reachable.

CAP Theorem
-----------

Horde is eventually consistent, which means that Horde can guarantee availability and partition tolerancy. Horde cannot guarantee consistency. This means you may end up with duplicate processes in your cluster. Horde does aggressively synchronize between nodes (this is also tunable), but ultimately, depending on the tuning parameters you choose and the quality of the network, there are conditions under which it is possible to have duplicate processes in your cluster. Horde.Registry terminates duplicate processes as soon as they are discovered with a special exit code, so you'll always know when this is happening. See this page in the docs for more details.

_NOTE: Since Horde 0.6.0, Horde.DynamicSupervisor ignores the `id` of a child spec (as Elixir.DynamicSupervisor does), and therefore does not guarantee that each `id` will be unique in the cluster (as it did pre-0.6.0). If you want to uniquely name your processes in a cluster, use Horde.Registry for this purpose. Having both Horde.DynamicSupervisor and Horde.Registry checking for uniqueness was subject to a race condition where Horde.DynamicSupervisor would choose process A to survive and Horde.Registry would choose process B to survive, resulting in both processes being killed._

Graceful shutdown
-----------------

Using `Horde.DynamicSupervisor.stop/3` will cause the local supervisor to stop and any processes it was running will be shut down and redistributed to remaining supervisors in the horde. (This should happen automatically if `:init.stop()` is called).

Installation
------------

Horde is available in Hex.

The package can be installed by adding `horde` to your list of dependencies in `mix.exs`:

def deps do
  \[
    {:horde, "~> 0.8.5"}
  \]
end

Usage
-----

Here is a small taste of Horde's usage. See the full docs at https://hexdocs.pm/horde for more information and examples. There is also an example application at `examples/hello_world` that you can refer to if you get stuck.

Starting `Horde.DynamicSupervisor`:

defmodule MyApp.Application do
  use Application
  def start(\_type, \_args) do
    children \= \[
      {Horde.DynamicSupervisor, \[name: MyApp.DistributedSupervisor, strategy: :one\_for\_one\]}
    \]
    Supervisor.start\_link(children, strategy: :one\_for\_one)
  end
end

Adding a child to the supervisor:

\# Add a Task
Horde.DynamicSupervisor.start\_child(MyApp.DistributedSupervisor, %{id: :task, start: {Task, :start\_link, \[:infinity\]}})

\# Add an Agent
Horde.DynamicSupervisor.start\_child(MyApp.DistributedSupervisor, %{id: :agent, start: {Agent, :start\_link, \[fn \-> %{} end\]}})

\# Add a GenServer: You need a previously defined GenServer to call the one
\# liner below.  We have a test ("graceful shutdown") in
\# \`test/supervisor\_test.exs\` that exercises and displays that behavior. After
\# defined, it would be very similar to this:
Horde.DynamicSupervisor.start\_child(MyApp.DistributedSupervisor, %{id: :gen\_server, start: {GenServer, :start\_link, \[DefinedGenServer, {500, pid}\]}})

And so on. The public API should be the same as `Elixir.DynamicSupervisor` (and please open an issue if you find a difference).

Joining supervisors into a single distributed supervisor can be done using `Horde.Cluster`:

{:ok, supervisor\_1} \= Horde.DynamicSupervisor.start\_link(name: :distributed\_supervisor\_1, strategy: :one\_for\_one)
{:ok, supervisor\_2} \= Horde.DynamicSupervisor.start\_link(name: :distributed\_supervisor\_2, strategy: :one\_for\_one)
{:ok, supervisor\_3} \= Horde.DynamicSupervisor.start\_link(name: :distributed\_supervisor\_3, strategy: :one\_for\_one)

Horde.Cluster.set\_members(:distributed\_supervisor\_1, \[:distributed\_supervisor\_1, :distributed\_supervisor\_2, :distributed\_supervisor\_3\])
\# supervisor\_1, supervisor\_2 and supervisor\_3 will be joined in a single cluster.

Other projects
==============

Useful libraries that use or extend Horde functionalities.

Horde.Process
-------------

An opinionated but configurable means of quickly creating GenServer modules that are intended to be managed and distributed via Horde.

Contributing
============

Contributions are welcome! Feel free to open an issue if you'd like to discuss a problem or a possible solution. Pull requests are much appreciated.
