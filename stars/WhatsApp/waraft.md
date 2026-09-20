---
project: waraft
stars: 607
description: An Erlang implementation of RAFT from WhatsApp
url: https://github.com/WhatsApp/waraft
---

WhatsApp Raft - WARaft
======================

WARaft is an Erlang implementation of the Raft consensus algorithm for building replicated state machines. It has served as a consensus component in WhatsApp's large-scale, strongly consistent message-storage systems.

Features
--------

-   Raft-based consensus with leader election, replicated logs, strongly consistent reads, snapshots, and membership changes, including support for non-voting participants and witnesses.
-   Pluggable implementations for the replicated state machine, log, Raft RPC distribution, snapshot transport, log labels, and metrics.
-   Storage-oriented controls such as command batching, high- and low-priority queues, configurable backpressure, and optional leader read leases.
-   An illustrative partitioned key-value store showing how to build a storage service on WARaft.

The default ETS log and storage providers are intended for examples and tests. They are not durable across VM restarts; production deployments must supply durable providers.

Get Started
-----------

WARaft requires Erlang/OTP 28. Build it and run its checks with Rebar3:

rebar3 compile
rebar3 ct
rebar3 do dialyzer, xref

The following Erlang shell session starts a single-node WARaft cluster, then writes and reads a value. It uses a unique temporary data directory and the non-durable ETS providers, so it is suitable only as a local example.

% Load the WARaft records used below and start the application.
rr(wa\_raft\_server).
application:ensure\_all\_started(wa\_raft).

% Give the host application a unique data directory for this run.
application:set\_env(
    test\_app,
    raft\_database,
    filename:join(
        "/tmp",
        "wa\_raft\_quick\_start\_" ++ integer\_to\_list(erlang:system\_time(microsecond))
    )
).

% Start the WARaft supervisor without partitions, then add partition 1 of
% table "test". Production applications should place the WARaft supervisor
% under their own supervision tree rather than under kernel\_sup.
{ok, RaftSup} \= supervisor:start\_child(
    kernel\_sup,
    wa\_raft\_sup:child\_spec(test\_app, \[\])
).
wa\_raft\_sup:start\_partition(RaftSup, #{table \=> test, partition \=> 1}).

% A new partition remains stalled until it receives its initial configuration.
wa\_raft\_server:status(raft\_server\_test\_1, state).
Config \= wa\_raft\_server:make\_config(\[
    #raft\_identity{name \= raft\_server\_test\_1, node \= node()}
\]).
wa\_raft\_server:bootstrap(
    raft\_server\_test\_1,
    #raft\_log\_pos{index \= 1, term \= 1},
    Config,
    #{}
).

% A successful single-member bootstrap makes this server the leader.
wa\_raft\_server:status(raft\_server\_test\_1, state).

% Commit a write through the leader, then perform a strongly consistent read.
wa\_raft\_acceptor:commit(
    raft\_acceptor\_test\_1,
    {make\_ref(), {write, test, key, 1000}}
).
wa\_raft\_acceptor:read(raft\_acceptor\_test\_1, {read, test, key}).

A run produces output like this (process identifiers vary):

1\> rr(wa\_raft\_server).
\[raft\_application,raft\_identifier,raft\_identity,raft\_log,
 raft\_log\_pos,raft\_options,raft\_state\]
2\> application:ensure\_all\_started(wa\_raft).
{ok,\[wa\_raft\]}
3\> application:set\_env(test\_app, raft\_database, ...).
ok
4\> {ok, RaftSup} \= supervisor:start\_child(kernel\_sup, wa\_raft\_sup:child\_spec(test\_app, \[\])).
{ok,<0.89.0\>}
5\> wa\_raft\_sup:start\_partition(RaftSup, #{table \=> test, partition \=> 1}).
{ok,<0.90.0\>}
6\> wa\_raft\_server:status(raft\_server\_test\_1, state).
stalled
7\> Config \= wa\_raft\_server:make\_config(\[
       #raft\_identity{name \= raft\_server\_test\_1, node \= node()}
   \]).
#{version \=> 1,
  membership \=> \[{raft\_server\_test\_1,nonode@nohost}\],
  witness \=> \[\],
  participants \=> \[{raft\_server\_test\_1,nonode@nohost}\]}
8\> wa\_raft\_server:bootstrap(
       raft\_server\_test\_1,
       #raft\_log\_pos{index \= 1, term \= 1},
       Config,
       #{}
   ).
ok
9\> wa\_raft\_server:status(raft\_server\_test\_1, state).
leader
10\> wa\_raft\_acceptor:commit(
        raft\_acceptor\_test\_1,
        {make\_ref(), {write, test, key, 1000}}
    ).
ok
11\> wa\_raft\_acceptor:read(raft\_acceptor\_test\_1, {read, test, key}).
{ok,1000}

The `wa_raft` application starts services shared by all partitions. A host application owns a `wa_raft_sup` supervisor, and each partition runs a one-for-all process tree containing its queue, storage, log, Raft server, client acceptor, and transport cleanup worker. Applications submit reads and commits through `wa_raft_acceptor`, perform membership and lifecycle operations through `wa_raft_server`, and use `wa_raft_info` for local leader and health lookups.

A multi-node deployment starts the same partition on every participating node, installs the same membership configuration on each replica, and then triggers an election. The key-value store example illustrates partition routing and the storage callbacks; it is a teaching example rather than a production-ready distributed database.

License
-------

WARaft is licensed under the Apache License 2.0.
