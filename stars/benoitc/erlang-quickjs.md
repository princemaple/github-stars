---
project: erlang-quickjs
stars: 12
description: QuickJS JavaScript engine for Erlang (powered by quickjs-ng). API-compatible replacement for erlang-duktape.
url: https://github.com/benoitc/erlang-quickjs
---

erlang-quickjs
==============

QuickJS JavaScript engine for Erlang.

This library embeds the QuickJS-NG JavaScript engine (v0.16.1) as an Erlang NIF, allowing you to evaluate JavaScript code directly from Erlang.

Features
--------

-   Execute JavaScript code from Erlang
-   Bidirectional type conversion between Erlang and JavaScript
-   Multiple isolated JavaScript contexts
-   CommonJS module support
-   **Execution timeouts to prevent infinite loops**
-   **Event framework for JS ↔ Erlang communication**
-   **Register Erlang functions callable from JavaScript**
-   **console.log/info/warn/error/debug support**
-   **Memory metrics and manual garbage collection**
-   Thread-safe with automatic resource cleanup
-   No external dependencies - QuickJS is embedded

Requirements
------------

-   Erlang/OTP 24 or later
-   CMake 3.10 or later
-   C compiler (gcc, clang, or MSVC)

Installation
------------

Add to your `rebar.config`:

{deps, \[
    {quickjs, {git, "https://github.com/benoitc/erlang-quickjs.git", {branch, "main"}}}
\]}.

Then run:

rebar3 compile

Quick Start
-----------

%% Create a JavaScript context
{ok, Ctx} \= quickjs:new\_context().

%% Evaluate JavaScript code
{ok, 42} \= quickjs:eval(Ctx, <<"21 \* 2"\>>).
{ok, <<"hello"\>>} \= quickjs:eval(Ctx, <<"'hello'"\>>).

%% Evaluate with variable bindings
{ok, 30} \= quickjs:eval(Ctx, <<"x \* y"\>>, #{x \=> 5, y \=> 6}).

%% Define and call functions
{ok, \_} \= quickjs:eval(Ctx, <<"function add(a, b) { return a + b; }"\>>).
{ok, 7} \= quickjs:call(Ctx, add, \[3, 4\]).

%% CommonJS modules
ok \= quickjs:register\_module(Ctx, <<"utils"\>>, <<"
    exports.greet = function(name) {
        return 'Hello, ' + name + '!';
    };
"\>>).
{ok, <<"Hello, World!"\>>} \= quickjs:eval(Ctx, <<"require('utils').greet('World')"\>>).

API Reference
-------------

-   Context Management | Evaluation | Function Calls | CommonJS Modules
-   Event Framework | Erlang Functions | CBOR Encoding/Decoding
-   Utility | Metrics

### Context Management

#### `new_context() -> {ok, context()} | {error, term()}`

Create a new JavaScript context. Contexts are isolated - variables and functions defined in one context are not visible in others.

Contexts are automatically cleaned up when garbage collected, but you can also explicitly destroy them with `destroy_context/1`.

#### `new_context(Opts) -> {ok, context()} | {error, term()}`

Create a new JavaScript context with options.

Options:

-   `handler => pid()`: Process to receive events from JavaScript. The handler will receive messages of the form `{quickjs, Type, Data}` where Type is a binary (e.g., `<<"custom">>`) or atom (for log events: `log`) and Data is the event payload.

{ok, Ctx} \= quickjs:new\_context(#{handler \=> self()}),
{ok, \_} \= quickjs:eval(Ctx, <<"console.log('hello')"\>>),
receive
    {quickjs, log, #{level :\= info, message :\= <<"hello"\>>}} ->
        io:format("Got log message~n")
end.

#### `destroy_context(Ctx) -> ok | {error, term()}`

Explicitly destroy a JavaScript context. This is optional - contexts are automatically cleaned up on garbage collection. Calling destroy on an already-destroyed context is safe (idempotent).

### Evaluation

#### `eval(Ctx, Code) -> {ok, Value} | {error, term()}`

Evaluate JavaScript code and return the result of the last expression. Uses default timeout of 5000ms.

{ok, 3} \= quickjs:eval(Ctx, <<"1 + 2"\>>).
{ok, <<"hello"\>>} \= quickjs:eval(Ctx, <<"'hello'"\>>).
{error, {js\_error, \_}} \= quickjs:eval(Ctx, <<"throw 'oops'"\>>).

#### `eval(Ctx, Code, Timeout) -> {ok, Value} | {error, term()}`

#### `eval(Ctx, Code, Bindings) -> {ok, Value} | {error, term()}`

With an integer or `infinity` as third argument, sets execution timeout in milliseconds. With a map, sets variable bindings.

%% With timeout (100ms)
{error, timeout} \= quickjs:eval(Ctx, <<"while(true){}"\>>, 100).
{ok, 42} \= quickjs:eval(Ctx, <<"21 \* 2"\>>, 1000).
{ok, 42} \= quickjs:eval(Ctx, <<"21 \* 2"\>>, infinity).  %% No timeout

%% With bindings (uses default 5000ms timeout)
{ok, 30} \= quickjs:eval(Ctx, <<"x \* y"\>>, #{x \=> 5, y \=> 6}).

#### `eval(Ctx, Code, Bindings, Timeout) -> {ok, Value} | {error, term()}`

Evaluate with both variable bindings and explicit timeout.

{ok, 30} \= quickjs:eval(Ctx, <<"x \* y"\>>, #{x \=> 5, y \=> 6}, 1000).
{error, timeout} \= quickjs:eval(Ctx, <<"while(x){}"\>>, #{x \=> true}, 100).

### Function Calls

#### `call(Ctx, FunctionName) -> {ok, Value} | {error, term()}`

Call a global JavaScript function with no arguments. Uses default timeout of 5000ms.

{ok, \_} \= quickjs:eval(Ctx, <<"function getTime() { return Date.now(); }"\>>).
{ok, Timestamp} \= quickjs:call(Ctx, <<"getTime"\>>).

#### `call(Ctx, FunctionName, Timeout) -> {ok, Value} | {error, term()}`

#### `call(Ctx, FunctionName, Args) -> {ok, Value} | {error, term()}`

With an integer or `infinity` as third argument, sets execution timeout. With a list, passes arguments to the function.

%% With timeout
{ok, \_} \= quickjs:eval(Ctx, <<"function slow() { while(true){} }"\>>).
{error, timeout} \= quickjs:call(Ctx, slow, 100).

%% With args (uses default 5000ms timeout)
{ok, \_} \= quickjs:eval(Ctx, <<"function add(a, b) { return a + b; }"\>>).
{ok, 7} \= quickjs:call(Ctx, <<"add"\>>, \[3, 4\]).
{ok, 7} \= quickjs:call(Ctx, add, \[3, 4\]).

#### `call(Ctx, FunctionName, Args, Timeout) -> {ok, Value} | {error, term()}`

Call a function with both arguments and explicit timeout.

{ok, 7} \= quickjs:call(Ctx, add, \[3, 4\], 1000).
{ok, 7} \= quickjs:call(Ctx, add, \[3, 4\], infinity).  %% No timeout

### CommonJS Modules

#### `register_module(Ctx, ModuleId, Source) -> ok | {error, term()}`

Register a CommonJS module with source code. The module can then be loaded with `require/2` or via `require()` in JavaScript.

ok \= quickjs:register\_module(Ctx, <<"math"\>>, <<"
    exports.add = function(a, b) { return a + b; };
    exports.multiply = function(a, b) { return a \* b; };
"\>>).

#### `require(Ctx, ModuleId) -> {ok, Exports} | {error, term()}`

Load a CommonJS module and return its exports. Modules are cached - subsequent requires return the same exports object.

{ok, Exports} \= quickjs:require(Ctx, <<"math"\>>).

### Event Framework

The event framework enables bidirectional communication between JavaScript and Erlang.

#### `send(Ctx, Event, Data) -> {ok, Value} | ok | {error, term()}`

Send data to a registered JavaScript callback. If JavaScript code has registered a callback using `Erlang.on(event, fn)`, this function will call that callback with the provided data.

Returns `{ok, Result}` where Result is the return value of the callback, or `ok` if no callback is registered for the event.

{ok, Ctx} \= quickjs:new\_context(),
%% JavaScript registers a callback
{ok, \_} \= quickjs:eval(Ctx, <<"
    var received = null;
    Erlang.on('data', function(d) { received = d; return 'got it'; });
"\>>),
%% Erlang sends data to the callback
{ok, <<"got it"\>>} \= quickjs:send(Ctx, data, #{value \=> 42}),
{ok, #{<<"value"\>> :\= 42}} \= quickjs:eval(Ctx, <<"received"\>>).

#### JavaScript API

The `Erlang` global object provides the following methods:

**`Erlang.emit(type, data)`** - Send an event to the Erlang handler process.

Erlang.emit('custom\_event', {key: 'value', count: 42});

The handler receives: `{quickjs, <<"custom_event">>, #{<<"key">> => <<"value">>, <<"count">> => 42}}`

**`Erlang.log(level, ...args)`** - Send a log message to the Erlang handler.

Erlang.log('info', 'User logged in:', userId);
Erlang.log('warning', 'Rate limit exceeded');
Erlang.log('error', 'Connection failed:', error);
Erlang.log('debug', 'Request details:', request);

The handler receives: `{quickjs, log, #{level => info, message => <<"User logged in: 123">>}}`

**`Erlang.on(event, callback)`** - Register a callback for events from Erlang.

Erlang.on('config\_update', function(config) {
    applyConfig(config);
    return 'applied';
});

**`Erlang.off(event)`** - Unregister a callback.

Erlang.off('config\_update');

#### Console Object

A standard `console` object is available that wraps `Erlang.log`:

console.log('Hello, world!');      // level: info
console.info('Information');        // level: info
console.warn('Warning message');    // level: warning
console.error('Error occurred');    // level: error
console.debug('Debug info');        // level: debug

#### Complete Example

%% Create context with event handler
{ok, Ctx} \= quickjs:new\_context(#{handler \=> self()}),

%% Set up JavaScript callback
{ok, \_} \= quickjs:eval(Ctx, <<"
    var messages = \[\];
    Erlang.on('message', function(msg) {
        messages.push(msg);
        console.log('Received:', msg.text);
        return messages.length;
    });
"\>>),

%% Send from Erlang
{ok, 1} \= quickjs:send(Ctx, message, #{text \=> <<"Hello"\>>}),
{ok, 2} \= quickjs:send(Ctx, message, #{text \=> <<"World"\>>}),

%% Receive console.log events
receive {quickjs, log, #{message :\= <<"Received: Hello"\>>}} -> ok end,
receive {quickjs, log, #{message :\= <<"Received: World"\>>}} -> ok end,

%% Verify messages were stored
{ok, \[#{<<"text"\>> :\= <<"Hello"\>>}, #{<<"text"\>> :\= <<"World"\>>}\]} \=
    quickjs:eval(Ctx, <<"messages"\>>).

### Erlang Functions

Register Erlang functions that can be called synchronously from JavaScript.

#### `register_function(Ctx, Name, Fun) -> ok | {error, term()}`

Register an Erlang function callable from JavaScript. The function receives a list of arguments passed from JavaScript.

Supports both anonymous functions and `{Module, Function}` tuples. The function must accept a single argument (the list of JS arguments).

{ok, Ctx} \= quickjs:new\_context(),

%% Register with anonymous function
ok \= quickjs:register\_function(Ctx, greet, fun(\[Name\]) ->
    <<"Hello, ", Name/binary, "!"\>>
end),
{ok, <<"Hello, World!"\>>} \= quickjs:eval(Ctx, <<"greet('World')"\>>).

%% Register with {Module, Function} tuple
ok \= quickjs:register\_function(Ctx, my\_func, {my\_module, my\_function}).

**Multiple Arguments:**

ok \= quickjs:register\_function(Ctx, add, fun(Args) ->
    lists:sum(Args)
end),
{ok, 10} \= quickjs:eval(Ctx, <<"add(1, 2, 3, 4)"\>>).

**Nested Calls (Erlang functions calling each other):**

ok \= quickjs:register\_function(Ctx, double, fun(\[N\]) -> N \* 2 end),
{ok, \_} \= quickjs:eval(Ctx, <<"function quadruple(n) { return double(double(n)); }"\>>),
{ok, 20} \= quickjs:eval(Ctx, <<"quadruple(5)"\>>).

**Error Handling:**

Erlang exceptions are converted to JavaScript errors:

ok \= quickjs:register\_function(Ctx, fail, fun(\_) ->
    error(something\_bad)
end),
%% JavaScript can catch the error
{ok, \_} \= quickjs:eval(Ctx, <<"
    try {
        fail();
    } catch (e) {
        console.log('Caught:', e.message);
    }
"\>>).

**Note:** Registered functions are stored in the calling process's dictionary. The process that registers the function must also be the one that calls `eval/call`.

### CBOR Encoding/Decoding

QuickJS has built-in CBOR (Concise Binary Object Representation) support.

#### `cbor_encode(Ctx, Value) -> {ok, binary()} | {error, term()}`

Encode an Erlang value to CBOR binary. The value is first converted to a JavaScript value, then encoded to CBOR.

{ok, Ctx} \= quickjs:new\_context(),
{ok, Bin} \= quickjs:cbor\_encode(Ctx, #{name \=> <<"Alice"\>>, age \=> 30}).

#### `cbor_decode(Ctx, Binary) -> {ok, Value} | {error, term()}`

Decode a CBOR binary to an Erlang value. The CBOR is decoded to a JavaScript value, then converted to Erlang.

{ok, Decoded} \= quickjs:cbor\_decode(Ctx, Bin),
%% #{<<"name">> => <<"Alice">>, <<"age">> => 30}

CBOR type mappings follow the same rules as regular Erlang ↔ JavaScript type conversions.

### Utility

#### `info() -> {ok, string()}`

Get NIF information. Used to verify the NIF is loaded correctly.

### Metrics

#### `get_memory_stats(Ctx) -> {ok, Stats} | {error, term()}`

Get memory statistics for a JavaScript context. Returns a map with:

Key

Description

`heap_bytes`

Current allocated bytes in the QuickJS heap

`heap_peak`

Peak memory usage since context creation

`alloc_count`

Total number of allocations

`realloc_count`

Total number of reallocations

`free_count`

Total number of frees

`gc_runs`

Number of garbage collection runs triggered

{ok, Ctx} \= quickjs:new\_context(),
{ok, \_} \= quickjs:eval(Ctx, <<"var x = \[\]; for(var i=0; i<1000; i++) x.push(i);"\>>),
{ok, Stats} \= quickjs:get\_memory\_stats(Ctx),
io:format("Heap: ~p bytes, Peak: ~p bytes~n",
          \[maps:get(heap\_bytes, Stats), maps:get(heap\_peak, Stats)\]).

#### `gc(Ctx) -> ok | {error, term()}`

Trigger garbage collection on a JavaScript context. Forces QuickJS's mark-and-sweep garbage collector to run.

{ok, Ctx} \= quickjs:new\_context(),
{ok, \_} \= quickjs:eval(Ctx, <<"var x = {}; x = null;"\>>),
ok \= quickjs:gc(Ctx),
{ok, #{gc\_runs :\= 1}} \= quickjs:get\_memory\_stats(Ctx).

Type Conversions
----------------

### Erlang to JavaScript

Erlang

JavaScript

`integer()`

number

`float()`

number

`binary()`

string

`true`

true

`false`

false

`null`

null

`undefined`

undefined

other atoms

string

`list()`

array (or string if iolist)

`map()`

object

`tuple()`

array

### JavaScript to Erlang

JavaScript

Erlang

number (integer)

`integer()`

number (float)

`float()`

NaN

`nan` (atom)

Infinity

`infinity` (atom)

\-Infinity

`neg_infinity` (atom)

string

`binary()`

true

`true`

false

`false`

null

`null`

undefined

`undefined`

array

`list()`

object

`map()`

Error Handling
--------------

JavaScript errors are returned as `{error, {js_error, Message}}` where `Message` is a binary containing the error message and stack trace.

{error, {js\_error, <<"ReferenceError: x is not defined", \_/binary\>>}} \=
    quickjs:eval(Ctx, <<"x + 1"\>>).

Contexts remain usable after errors - you can continue to evaluate code in the same context.

Thread Safety
-------------

All context operations are thread-safe. Multiple Erlang processes can share a context, though operations are serialized via a mutex. For maximum parallelism, create separate contexts for concurrent workloads.

Resource Management
-------------------

Contexts are managed as Erlang NIF resources with automatic cleanup:

-   Contexts are garbage collected when no Erlang process holds a reference
-   Multiple processes can share a context safely
-   Explicit `destroy_context/1` is optional but can be used for immediate cleanup
-   Reference counting ensures contexts are not destroyed while in use

Benchmarks
----------

Apple M4 Pro, Erlang/OTP 29, quickjs-ng v0.16.1, release build, 1000 iterations per benchmark after a 100-iteration warmup.

Each iteration creates a context, does the work, and destroys it, so these figures are dominated by context lifecycle rather than by JavaScript execution. Reuse a context and per-call cost drops by roughly an order of magnitude.

### Core operations

Benchmark

Ops/sec

Mean (ms)

P95 (ms)

P99 (ms)

eval\_simple

4,133

0.242

0.301

0.371

eval\_complex

4,076

0.245

0.304

0.356

eval\_bindings\_small (5 vars)

4,201

0.238

0.281

0.336

eval\_bindings\_large (50 vars)

3,363

0.297

0.364

0.422

call\_no\_args

4,122

0.243

0.300

0.353

call\_with\_args (5 args)

4,092

0.244

0.303

0.363

call\_many\_args (20 args)

3,796

0.263

0.336

0.398

type\_convert\_simple

4,182

0.239

0.284

0.348

type\_convert\_array (1000 elem)

3,964

0.252

0.300

0.357

type\_convert\_nested

4,054

0.247

0.293

0.353

context\_create

4,108

0.243

0.297

0.365

module\_require\_cached

3,999

0.250

0.305

0.370

### Erlang function registration

Benchmark

Ops/sec

Mean (ms)

P95 (ms)

P99 (ms)

register\_function\_simple

4,112

0.243

0.288

0.378

register\_function\_complex\_args

3,816

0.262

0.327

0.784

register\_function\_nested (5 calls)

3,791

0.264

0.326

0.408

register\_function\_many\_calls (10)

34,193

0.292

0.370

0.453

### Event framework

Benchmark

Ops/sec

Mean (ms)

P95 (ms)

P99 (ms)

event\_emit

2,619

0.382

0.498

0.608

event\_send

4,078

0.245

0.308

0.365

console\_log

2,672

0.374

0.489

0.601

### CBOR

Benchmark

Ops/sec

Mean (ms)

P95 (ms)

P99 (ms)

cbor\_encode\_simple

3,703

0.270

0.328

0.378

cbor\_encode\_complex

3,306

0.302

0.351

0.387

cbor\_decode\_simple

3,513

0.285

0.337

0.391

cbor\_roundtrip

3,369

0.297

0.357

0.431

The CBOR codec is a JS shim rather than a native C path, so it stays the slowest of these operations. The duktape comparison that used to appear here was measured before the engine was built with optimization and is no longer meaningful; it has not been re-run.

### Concurrency

Benchmark

Ops/sec

Mean (ms)

P95 (ms)

P99 (ms)

concurrent\_same\_context (10 procs)

149,004

0.671

0.995

1.108

concurrent\_many\_contexts (10 procs)

42,368

2.360

2.671

2.852

Run benchmarks yourself:

./run\_bench.sh                  # all
./run\_bench.sh eval\_simple      # one
./run\_bench.sh --smoke          # quick validation

Security Considerations
-----------------------

When running untrusted JavaScript code, be aware of these limitations:

### Execution Timeouts

All `eval` and `call` functions support execution timeouts to prevent infinite loops:

%% Default timeout is 5000ms
{error, timeout} \= quickjs:eval(Ctx, <<"while(true){}"\>>, 100).

%% Use infinity for no timeout (only for trusted code)
{ok, \_} \= quickjs:eval(Ctx, Code, infinity).

After a timeout, the context remains valid and can be reused for subsequent calls.

### Memory Limits

QuickJS does not have built-in memory limits. JavaScript code can allocate unbounded memory.

**Recommendation**: For untrusted code, monitor memory usage via `get_memory_stats/1` and destroy contexts that exceed limits.

### Event Types

Event types from `Erlang.emit()` are returned as binaries to prevent atom table exhaustion. Known log levels (`debug`, `info`, `warning`, `error`) remain atoms for ergonomics.

License
-------

This project is licensed under the Apache License 2.0 - see the LICENSE file for details.

QuickJS-NG is licensed under the MIT License.
