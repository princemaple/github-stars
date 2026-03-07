---
project: waraft
stars: 600
description: An Erlang implementation of RAFT from WhatsApp
url: https://github.com/WhatsApp/waraft
---

WhatsApp Raft - WARaft
======================

WARaft is a Raft library in Erlang by WhatsApp. It provides an Erlang implementation to obtain consensus among replicated state machines. Consensus is a fundamental problem in fault-tolerant distributed systems. WARaft has been used as consensus provider in WhatsApp message storage, which is a large scale strongly consistent storage system across 5+ datacenters.

Features
--------

-   Full implementation of Raft consensus algorithm defined in https://raft.github.io/
-   Extensible framework. It offers pluggable component interface for log, state machines and transport layer. Users are also allowed provide their own implementation to customize .
-   Performant. It is highly optimized for large volume transactions user cases. It could support up to 200K/s transactions with in a 5 node cluster.
-   Distributed key value store. WARaft provides components needed to build a distributed key-value storage.

Get Started
-----------

The following code snippet gives a quick glance about how WARaft works. It creates a single-node WARaft cluster and writes and reads a record.

% Setup the WARaft application and the host application
rr(wa\_raft\_server).
application:ensure\_all\_started(wa\_raft).
application:set\_env(test\_app, raft\_database, ".").
% Create a spec for partition 1 of the RAFT table "test" and start it.
Spec \= wa\_raft\_sup:child\_spec(test\_app, \[#{table \=> test, partition \=> 1}\]).
% Here we add WARaft to the kernel's supervisor, but you should place WARaft's
% child spec underneath your application's supervisor in a real deployment.
supervisor:start\_child(kernel\_sup, Spec).
% Check that the RAFT server started successfully
wa\_raft\_server:status(raft\_server\_test\_1).
% Make a cluster configuration with the current node as the only member
Config \= wa\_raft\_server:make\_config(\[#raft\_identity{name \= raft\_server\_test\_1, node \= node()}\]).
% Bootstrap the RAFT server to get it started
wa\_raft\_server:bootstrap(raft\_server\_test\_1, #raft\_log\_pos{index \= 1, term \= 1}, Config, #{}).
% Wait for the RAFT server to become the leader
wa\_raft\_server:status(raft\_server\_test\_1).
% Read and write against a key
wa\_raft\_acceptor:commit(raft\_acceptor\_test\_1, {make\_ref(), {write, test, key, 1000}}).
wa\_raft\_acceptor:read(raft\_acceptor\_test\_1, {read, test, key}).

A typical output would look like the following:

1\> % Setup the WARaft application and the host application
   rr(wa\_raft\_server).
\[raft\_application,raft\_identifier,raft\_identity,raft\_log,
 raft\_log\_pos,raft\_options,raft\_state\]
2\> application:ensure\_all\_started(wa\_raft).
{ok,\[wa\_raft\]}
3\> application:set\_env(test\_app, raft\_database, ".").
ok
4\> % Create a spec for partition 1 of the RAFT table "test" and start it.
   Spec \= wa\_raft\_sup:child\_spec(test\_app, \[#{table \=> test, partition \=> 1}\]).
#{id \=> wa\_raft\_sup,restart \=> permanent,shutdown \=> infinity,
  start \=>
      {wa\_raft\_sup,start\_link,
                   \[test\_app,\[#{table \=> test,partition \=> 1}\],#{}\]},
  type \=> supervisor,
  modules \=> \[wa\_raft\_sup\]}
5\> % Here we add WARaft to the kernel's supervisor, but you should place WARaft's
   % child spec underneath your application's supervisor in a real deployment.
   supervisor:start\_child(kernel\_sup, Spec).
{ok,<0.101.0\>}
6\> % Check that the RAFT server started successfully
   wa\_raft\_server:status(raft\_server\_test\_1).
\[{state,stalled},
 {id,nonode@nohost},
 {table,test},
 {partition,1},
 {data\_dir,"./test.1"},
 {current\_term,0},
 {voted\_for,undefined},
 {commit\_index,0},
 {last\_applied,0},
 {leader\_id,undefined},
 {next\_index,#{}},
 {match\_index,#{}},
 {log\_module,wa\_raft\_log\_ets},
 {log\_first,0},
 {log\_last,0},
 {votes,#{}},
 {inflight\_applies,0},
 {disable\_reason,undefined},
 {config,#{version \=> 1,membership \=> \[\],witness \=> \[\]}},
 {config\_index,0},
 {witness,false}\]
7\> % Make a cluster configuration with the current node as the only member
   Config \= wa\_raft\_server:make\_config(\[#raft\_identity{name \= raft\_server\_test\_1, node \= node()}\]).
#{version \=> 1,
  membership \=> \[{raft\_server\_test\_1,nonode@nohost}\],
  witness \=> \[\]}
8\> % Bootstrap the RAFT server to get it started
   wa\_raft\_server:bootstrap(raft\_server\_test\_1, #raft\_log\_pos{index \= 1, term \= 1}, Config, #{}).
ok
9\> % Wait for the RAFT server to become the leader
   wa\_raft\_server:status(raft\_server\_test\_1).
\[{state,leader},
 {id,nonode@nohost},
 {table,test},
 {partition,1},
 {data\_dir,"./test.1"},
 {current\_term,1},
 {voted\_for,nonode@nohost},
 {commit\_index,2},
 {last\_applied,2},
 {leader\_id,nonode@nohost},
 {next\_index,#{}},
 {match\_index,#{}},
 {log\_module,wa\_raft\_log\_ets},
 {log\_first,1},
 {log\_last,2},
 {votes,#{}},
 {inflight\_applies,0},
 {disable\_reason,undefined},
 {config,#{version \=> 1,
           membership \=> \[{raft\_server\_test\_1,nonode@nohost}\],
           witness \=> \[\]}},
 {config\_index,1},
 {witness,false}\]
10\> % Read and write against a key
    wa\_raft\_acceptor:commit(raft\_acceptor\_test\_1, {make\_ref(), {write, test, key, 1000}}).
ok
11\> wa\_raft\_acceptor:read(raft\_acceptor\_test\_1, {read, test, key}).
{ok,1000}

The example directory contains an example generic key-value store built on top of WARaft.

License
-------

WARaft is Apache licensed.
