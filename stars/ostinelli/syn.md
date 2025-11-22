---
project: syn
stars: 685
description: A scalable global Process Registry and Process Group manager for Erlang and Elixir.
url: https://github.com/ostinelli/syn
---

Syn
===

**Syn** (short for _synonym_) is a scalable global Process Registry and Process Group manager for Erlang and Elixir, able to automatically manage dynamic clusters (addition / removal of nodes) and to recover from net splits.

Syn is a replacement for Erlang/OTP global's registry and pg modules. The main differences with these OTP's implementations are:

-   OTP's `global` module chooses Consistency over Availability, therefore it can become difficult to scale when registration rates are elevated and the cluster becomes larger. If eventual consistency is acceptable in your case, Syn can considerably increase the registry's performance.
-   Syn allows to attach metadata to every process, which also gets synchronized across the cluster.
-   Syn implements cluster-wide callbacks on the main events, which are also properly triggered after net splits.

\[Documentation\]

Introduction
------------

### What is a Process Registry?

A global Process Registry allows registering a process on all the nodes of a cluster with a single Key. Consider this the process equivalent of a DNS server: in the same way you can retrieve an IP address from a domain name, you can retrieve a process from its Key.

Typical Use Case: registering on a system a process that handles a physical device (using its serial number).

### What is a Process Group?

A global Process Group is a named group which contains many processes, possibly running on different nodes. With the group Name, you can retrieve on any cluster node the list of these processes, or publish a message to all of them. This mechanism allows for Publish / Subscribe patterns.

Typical Use Case: a chatroom.

### What is Syn?

Syn is a Process Registry and Process Group manager that has the following features:

-   Global Process Registry (i.e. a process is uniquely identified with a Key across all the nodes of a cluster).
-   Global Process Group manager (i.e. a group is uniquely identified with a Name across all the nodes of a cluster).
-   Any term can be used as Key and Name.
-   PubSub mechanism: messages can be published to all members of a Process Group (_globally_ on all the cluster or _locally_ on a single node).
-   Subclusters by using Scopes allows great scalability.
-   Dynamically sized clusters (addition / removal of nodes is handled automatically).
-   Net Splits automatic resolution.
-   Fast writes.
-   Configurable callbacks.
-   Processes are automatically monitored and removed from the Process Registry and Process Groups if they die.

Notes
-----

In any distributed system you are faced with a consistency challenge, which is often resolved by having one master arbiter performing all write operations (chosen with a mechanism of leader election), or through atomic transactions.

Syn was born for applications of the IoT field. In this context, Keys used to identify a process are often the physical object's unique identifier (for instance, its serial or MAC address), and are therefore already defined and unique _before_ hitting the system. The consistency challenge is less of a problem in this case, since the likelihood of concurrent incoming requests that would register processes with the same Key is extremely low and, in most cases, acceptable.

In addition, write speeds were a determining factor in the architecture of Syn.

Therefore, Availability has been chosen over Consistency and Syn implements strong eventual consistency.

Installation
------------

#### Elixir

Add it to your deps:

defp deps do
  \[{:syn, "~> 3.3"}\]
end

#### Erlang

If you're using rebar3, add `syn` as a dependency in your project's `rebar.config` file:

{deps, \[
  {syn, {git, "git://github.com/ostinelli/syn.git", {tag, "3.3.0"}}}
\]}.

Or, if you're using Hex.pm as package manager (with the rebar3\_hex plugin):

{deps, \[
  {syn, "3.3.0"}
\]}.

Ensure that `syn` is started with your application, for example by adding it in your `.app` file to the list of `applications`:

{application, my\_app, \[
    %% ...
    {applications, \[
        kernel,
        stdlib,
        sasl,
        syn,
        %% ...
    \]},
    %% ...
\]}.

Quickstart
----------

### Registry

#### Elixir

iex\> :syn.add\_node\_to\_scopes(\[:users\])
:ok
iex\> pid \= self()
#PID<0.105.0>
iex\> :syn.register(:users, "hedy", pid)
:ok
iex\> :syn.lookup(:users, "hedy")
{#PID<0.105.0>,:undefined}
iex\> :syn.register(:users, "hedy", pid, \[city: "Milan"\])
:ok
iex> :syn.lookup(:users, "hedy")
{#PID<0.105.0>,\[city: "Milan"\]}
iex\> :syn.registry\_count(:users)
1

#### Erlang

1\> syn:add\_node\_to\_scopes(\[users\]).
ok
2\> Pid \= self().
<0.93.0\>
3\> syn:register(users, "hedy", Pid).
ok
4\> syn:lookup(users, "hedy").
{<0.93.0\>,undefined}
5\> syn:register(users, "hedy", Pid, \[{city, "Milan"}\]).
ok
6\> syn:lookup(users, "hedy").
{<0.93.0\>,\[{city, "Milan"}\]}
7\> syn:registry\_count(users).
1

### Process Groups

#### Elixir

iex\> :syn.add\_node\_to\_scopes(\[:users\])
:ok
iex\> pid \= self()
#PID<0.88.0>
iex\> :syn.join(:users, {:italy, :lombardy}, pid)
:ok
iex\> :syn.members(:users, {:italy, :lombardy})
\[{#PID<0.88.0>,:undefined}\]
iex\> :syn.is\_member(:users, {:italy, :lombardy}, pid)
true
iex\> :syn.publish(:users, {:italy, :lombardy}, "hello lombardy!")
{:ok,1}
iex> flush()
Shell got "hello lombardy!"
ok

#### Erlang

1\> syn:add\_node\_to\_scopes(\[users\]).
ok
2\> Pid \= self().
<0.88.0\>
3\> syn:join(users, {italy, lombardy}, Pid).
ok
4\> syn:members(users, {italy, lombardy}).
\[{<0.88.0\>,undefined}\]
5\> syn:is\_member(users, {italy, lombardy}, Pid).
true
6\> syn:publish(users, {italy, lombardy}, "hello lombardy!").
{ok,1}
7\> flush().
Shell got "hello lombardy!"
ok

Contributing
------------

So you want to contribute? That's great! Please follow the guidelines below. It will make it easier to get merged in.

Before implementing a new feature, please submit a ticket to discuss what you intend to do. Your feature might already be in the works, or an alternative implementation might have already been discussed.

Do not commit to master in your fork. Provide a clean branch without merge commits. Every pull request should have its own topic branch. In this way, every additional adjustments to the original pull request might be done easily, and squashed with `git rebase -i`. The updated branch will be visible in the same pull request, so there will be no need to open new pull requests when there are changes to be applied.

Ensure that proper testing is included. To run Syn tests you simply have to be in the project's root directory and run:

$ make test

License
-------

Copyright (c) 2015-2022 Roberto Ostinelli and Neato Robotics, Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
