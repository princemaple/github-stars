---
project: pgmp
stars: 51
description: Erlang/OTP 25+ PostgreSQL client
url: https://github.com/shortishly/pgmp
---

  

What is PGMP?
=============

An implementation of the PostgreSQL Message Protocol for Erlang/OTP 25+.

Features:

-   Simple Query.
-   Extended Query.
-   Logical Streaming Replication including column lists and row filters.
-   Binary protocol (preferred) and textual when required.
-   Binary protocol for parse, bind and execute during an Extended Query.
-   Asynchronous requests using send\_request. Available for the client to use, and used internally within the implementation.
-   A statement aware connection pool (simple or extended query, outside or within a transaction block).
-   a GitHub Codespace for easy development and evaluation.
-   Support for JSON, JSONB and XML
-   Details of logical replication support.
-   Instrumented with telemetry.

Notes:

-   PGEC is an example OTP Application using PGMP and logical replication.
-   PGMP uses property based testing with PropEr.

Asynchronous Requests
---------------------

The following two sections show how to make an asynchronous request.

### send\_request/2 with receive\_response/1

You can immediately wait for a response (via receive\_response/1). For simplicity, the following examples use this method:

1\> gen\_statem:receive\_response(pgmp\_connection:query(#{sql \=> <<"select 2\*3"\>>})).
{reply, \[{row\_description, \[<<"?column?"\>>\]},
         {data\_row, \[6\]},
         {command\_complete, {select, 1}}\]}

Effectively the above turns an asynchronous call into an asynchronous request that immediately blocks the current process until it receives the reply.

The module `pgmp_connection_sync` wraps the above:

1\> pgmp\_connection\_sync:query(#{sql \=> <<"select 2\*3"\>>}).
\[{row\_description, \[<<"?column?"\>>\]},
 {data\_row, \[6\]},
 {command\_complete, {select, 1}}\]

### send\_request/4 with check\_response/3

The send\_request/4 and check\_response/3 pattern allows you to respond to other messages rather than blocking. Use this option, when writing another `gen_*` behaviour (`gen_server`, `gen_statem`, etc) is calling `pgmp`.

So using another `gen_statem` as an example:

The following `init/1` sets up some state with a request id collection to maintain our outstanding asynchronous requests.

init(\[\]) \->
    {ok, ready, #{requests \=> gen\_statem:reqids\_new()}}.

You can then use the `label` and `requests` parameter to `pgmp` to identify the response to your asynchronous request as follows:

handle\_event(internal, commit \= Label, \_, \_) \-\>
    {keep\_state\_and\_data,
      {next\_event, internal, {query, #{label => Label, sql => <<"commit">>}}}};
     
     
handle\_event(internal, {query, Arg}, \_, #{requests := Requests} = Data) ->
    {keep\_state,
     Data#{requests := pgmp\_connection:query(Arg#{requests => Requests})}};

A call to any of `pgmp_connection` functions: `query/1`, `parse/1`, `bind/1`, `describe/1` or `execute/1` take a map of parameters. If that map includes both a `label` and `requests` then the request is made using send\_request/4. The response will be received as an `info` message as follows:

handle\_event(info, Msg, \_, #{requests :\= Existing} \= Data) \->
    case gen\_statem:check\_response(Msg, Existing, true) of
        {{reply, Reply}, Label, Updated} ->
            %% You have a response with a Label so that you stitch it
            %% back to the original request...
            do\_something\_with\_response(Reply, Label),
            {keep\_state, Data#{requests :\= Updated}};

        ...deal with other cases...
    end.

The internals of `pgmp` use this pattern, pgmp\_rep\_log\_ets being an example that uses `pgmp_connection` itself to manage logical replication into ETS tables.

Simple Query
------------

An asynchronous simple query request using receive\_response to wait for the response:

1\> pgmp\_connection\_sync:query(#{sql \=> <<"select 2\*3"\>>}).
\[{row\_description, \[<<"?column?"\>>\]},
 {data\_row, \[6\]},
 {command\_complete, {select, 1}}\]

Extended Query
--------------

An extended query uses `parse`, `bind` and `execute` functions. A statement created by `parse` can be reused, and rebound with different parameter values and executed repeatedly. Parameters are correctly escaped including quoted strings where appropriate. You can page through results with a maximum number of rows being returned, rather than receiving all rows in one go.

To parse SQL into a prepared statement:

1\> pgmp\_connection\_sync:parse(#{sql \=> <<"select $1 \* 3"\>>}).
\[{parse\_complete, \[\]}\]

Where `$1` is a parameter that will be bound during the `bind` phase.

To `bind` parameters to the prepared statement:

1\> pgmp\_connection\_sync:bind(#{args \=> \[2\]}).
\[{bind\_complete, \[\]}\]

Finally, execute the prepared statement:

1\> pgmp\_connection\_sync:execute(#{}).
\[{row\_description, \[<<"?column?"\>>\]},
 {data\_row, \[6\]},
 {command\_complete, {select, 1}}\]

Execute by default will return all rows. To page the results instead:

create table xy (x integer primary key, y text);
insert into xy values (1, 'abc'), (2, 'foo'), (3, 'bar'), (4, 'baz'), (5, 'bat');

Prepare a statement to return all values:

1\> pgmp\_connection\_sync:parse(#{sql \=> <<"select \* from xy"\>>}).
\[{parse\_complete, \[\]}\]

Bind the statement with no parameters:

1\> pgmp\_connection\_sync:bind(#{args \=> \[\]}).
\[{bind\_complete, \[\]}\]

Finally, execute the prepared statement, returning a maximum of only 2 rows:

1\> pgmp\_connection\_sync:execute(#{max\_rows \=> 2}).
\[{row\_description, \[<<"x"\>>, <<"y"\>>\]},
 {data\_row, \[1, <<"abc"\>>\]},
 {data\_row, \[2, <<"foo"\>>\]},
 {portal\_suspended, \[\]}\]

Note that `portal_suspended` is being returned (rather than `command_complete` previously), which indicates that more rows are available. Repeat the `execute` to get the next page of results:

1\> pgmp\_connection\_sync:execute(#{max\_rows \=> 2}).
\[{row\_description, \[<<"x"\>>, <<"y"\>>\]},
 {data\_row, \[3, <<"bar"\>>\]},
 {data\_row, \[4, <<"baz"\>>\]},
 {portal\_suspended, \[\]}\]

The final execute will return the last row, and `command_complete`:

1\> pgmp\_connection\_sync:execute(#{max\_rows \=> 2}).
\[{row\_description, \[<<"x"\>>, <<"y"\>>\]},
 {data\_row, \[5, <<"bat"\>>\]},
 {command\_complete, {select, 1}}\]

`pgmp` has its own connection pool that is aware of extended query. Extended query connections are reserved by the process that initiated the `parse`. This is to ensure continuity of the unnamed prepared statement or portal, otherwise another process could prepare or bind (and overwrite) another statement or portal.

After an extended query, you can release the connection by:

1\> pgmp\_connection\_sync:sync(#{}).
ok

Alternatively, the initiating process can call `query` to returning back to simple query mode, which will also release the connection in the pool.

Without a call to `sync`, the completion of the transaction, or a simple query, that connection will remain reserved for the initiating process and not returned to the connection pool.

### Named Prepared Statements

A named statement can be created in any connection by using `parse`. However, the named statement is only created in that connection. Once the connection is released, you may not get the same connection back from the pool.

Named prepared statements that are available in all pooled connections, can be setup in Application configuration in dev.config:

 {pgmp, \[...
         {named\_statements,
          #{<<"now"\>> \=> <<"select now()"\>>,
            <<"cursors"\>> \=> <<"select \* from pg\_catalog.pg\_cursors"\>>,
            <<"prepared"\>> \=> <<"select \* from pg\_catalog.pg\_prepared\_statements"\>>,
            <<"yesterday"\>> \=> <<"select timestamp 'yesterday'"\>>,
            <<"allballs"\>> \=> <<"select time 'allballs'"\>>}},
         ...\]}

The named statements can be used in any connection:

pgmp\_connection\_sync:bind(#{name \=> <<"allballs"\>>}).

pgmp\_connection\_sync:execute(#{}).
\[{row\_description, \[<<"time"\>>\]},
 {data\_row, \[{0, 0, 0}\]},
 {command\_complete,{select,1}}\]
