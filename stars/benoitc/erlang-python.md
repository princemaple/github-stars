---
project: erlang-python
stars: 96
description: Execute Python from Erlang using dirty NIFs with GIL-aware execution, rate limiting, and free-threading support
url: https://github.com/benoitc/erlang-python
---

erlang\_python
==============

**Combine Python's ML/AI ecosystem with Erlang's concurrency.**

Run Python code from Erlang or Elixir with true parallelism, async/await support, and seamless integration. Build AI-powered applications that scale.

Overview
--------

erlang\_python embeds Python into the BEAM VM, letting you call Python functions, evaluate expressions, and stream from generators - all without blocking Erlang schedulers.

**Parallelism options:**

-   **Worker mode** (default, recommended) - Works with any Python version. With free-threaded Python (3.13t+), provides true parallelism automatically.
-   **OWN\_GIL sub-interpreters** (Python 3.14+) - Each interpreter has its own GIL, true parallelism.
-   **BEAM processes** - Fan out work across lightweight Erlang processes.

Key features:

-   **Process-bound environments** - Each Erlang process gets isolated Python state, enabling OTP-supervised Python actors
-   **Async/await** - Call Python async functions, gather results, stream from async generators
-   **Dirty NIF execution** - Python runs on dirty schedulers, never blocking the BEAM
-   **Elixir support** - Works seamlessly from Elixir via the `:py` module
-   **Bidirectional calls** - Python can call back into registered Erlang/Elixir functions
-   **Message passing** - Python can send messages directly to Erlang processes via `erlang.send()`
-   **Type conversion** - Automatic conversion between Erlang and Python types (including PIDs)
-   **Streaming** - Iterate over Python generators chunk-by-chunk
-   **Virtual environments** - Activate venvs for dependency isolation
-   **AI/ML ready** - Examples for embeddings, semantic search, RAG, and LLMs
-   **Logging integration** - Python logging forwarded to Erlang logger
-   **Distributed tracing** - Span-based tracing from Python code
-   **Security sandbox** - Blocks fork/exec operations that would corrupt the VM

Requirements
------------

-   Erlang/OTP 27+ (tested on OTP 27, 28, and 29)
-   Python 3.12+ (3.13+ for free-threading)
-   C compiler (gcc, clang)

Building
--------

rebar3 compile

Quick Start
-----------

### Erlang

%% Start the application
application:ensure\_all\_started(erlang\_python).

%% Call a Python function
{ok, 4.0} \= py:call(math, sqrt, \[16\]).

%% With keyword arguments
{ok, Json} \= py:call(json, dumps, \[#{foo \=> bar}\], #{indent \=> 2}).

%% Evaluate an expression
{ok, 45} \= py:eval(<<"sum(range(10))"\>>).

%% Evaluate with local variables
{ok, 25} \= py:eval(<<"x \* y"\>>, #{x \=> 5, y \=> 5}).

%% Async calls with await
Ref \= py:spawn\_call(math, factorial, \[100\]),
{ok, Result} \= py:await(Ref).

%% Fire-and-forget (no result)
ok \= py:cast(erlang, send, \[self(), {done, <<"task1"\>>}\]).

%% Streaming from generators
{ok, \[0,1,4,9,16\]} \= py:stream\_eval(<<"(x\*\*2 for x in range(5))"\>>).

### Elixir

\# Start the application
{:ok, \_} \= Application.ensure\_all\_started(:erlang\_python)

\# Call Python functions
{:ok, 4.0} \= :py.call(:math, :sqrt, \[16\])

\# Evaluate expressions
{:ok, result} \= :py.eval("2 + 2")

\# With variables
{:ok, 100} \= :py.eval("x \* y", %{x: 10, y: 10})

\# Call with keyword arguments
{:ok, json} \= :py.call(:json, :dumps, \[%{name: "Elixir"}\], %{indent: 2})

Erlang/Elixir Functions Callable from Python
--------------------------------------------

Register Erlang or Elixir functions that Python code can call back into:

### Erlang

%% Register a function
py:register\_function(my\_func, fun(\[X, Y\]) -> X + Y end).

%% Call from Python - native import syntax (recommended)
{ok, Result} \= py:exec(<<"
from erlang import my\_func
result = my\_func(10, 20)
"\>>).
%% Result = 30

%% Or use attribute-style access
{ok, 30} \= py:eval(<<"erlang.my\_func(10, 20)"\>>).

%% Legacy syntax still works
{ok, 30} \= py:eval(<<"erlang.call('my\_func', 10, 20)"\>>).

%% Unregister when done
py:unregister\_function(my\_func).

### Elixir

\# Register an Elixir function
:py.register\_function(:factorial, fn \[n\] \->
  Enum.reduce(1..n, 1, &\*/2)
end)

\# Call from Python - native import syntax
{:ok, 3628800} \= :py.exec("""
from erlang import factorial
result = factorial(10)
""")

\# Or use attribute-style access
{:ok, 3628800} \= :py.eval("erlang.factorial(10)")

### Python Calling Syntax

From Python code, registered Erlang functions can be called in three ways:

\# 1. Import syntax (most Pythonic)
from erlang import my\_func
result \= my\_func(10, 20)

\# 2. Attribute syntax
import erlang
result \= erlang.my\_func(10, 20)

\# 3. Explicit call (legacy)
import erlang
result \= erlang.call('my\_func', 10, 20)

All three methods are equivalent. The import and attribute syntaxes provide a more natural Python experience.

### Reentrant Callbacks

Python→Erlang→Python callbacks are fully supported. When Python code calls an Erlang function that in turn calls back into Python, the system handles this transparently without deadlocking:

%% Register an Erlang function that calls Python
py:register\_function(double\_via\_python, fun(\[X\]) ->
    {ok, Result} \= py:call('\_\_main\_\_', double, \[X\]),
    Result
end).

%% Define Python functions
py:exec(<<"
def double(x):
    return x \* 2
def process(x):
    from erlang import call
    # This calls Erlang, which calls Python's double()
    doubled = call('double\_via\_python', x)
    return doubled + 1
"\>>).

%% Test the full round-trip
{ok, 21} \= py:call('\_\_main\_\_', process, \[10\]).
%% 10 → double\_via\_python → double(10)=20 → +1 = 21

The implementation uses a suspension/resume mechanism that frees the dirty scheduler while the Erlang callback executes, preventing deadlocks even with multiple levels of nesting.

Shared State Between Workers
----------------------------

Python workers don't share namespace state, but you can share data via the built-in state API:

### From Python

from erlang import state\_set, state\_get, state\_delete, state\_keys
from erlang import state\_incr, state\_decr

\# Store data (survives across calls, shared between workers)
state\_set('my\_key', {'data': \[1, 2, 3\], 'count': 42})

\# Retrieve data
value \= state\_get('my\_key')  \# {'data': \[1, 2, 3\], 'count': 42}

\# Atomic counters (thread-safe, great for metrics)
state\_incr('requests')       \# returns 1
state\_incr('requests', 10)   \# returns 11
state\_decr('requests')       \# returns 10

\# List keys
keys \= state\_keys()  \# \['my\_key', 'requests', ...\]

\# Delete
state\_delete('my\_key')

### From Erlang/Elixir

%% Store and fetch
py:state\_store(<<"my\_key"\>>, #{value \=> 42}).
{ok, #{value :\= 42}} \= py:state\_fetch(<<"my\_key"\>>).

%% Atomic counters
1 \= py:state\_incr(<<"hits"\>>).
11 \= py:state\_incr(<<"hits"\>>, 10).
10 \= py:state\_decr(<<"hits"\>>).

%% List keys and clear
Keys \= py:state\_keys().
py:state\_clear().

This is backed by ETS with `{write_concurrency, true}`, so counters are atomic and fast.

Process-Bound Python Environments
---------------------------------

Each Erlang process gets its own isolated Python namespace. Variables, imports, and objects defined in one process are invisible to others, even when using the same interpreter.

%% Process A defines state
spawn(fun() \->
    Ctx \= py:context(1),
    ok \= py:exec(Ctx, <<"counter = 0"\>>),
    {ok, 0} \= py:eval(Ctx, <<"counter"\>>)
end).

%% Process B - same context, but isolated namespace
spawn(fun() \->
    Ctx \= py:context(1),
    %% 'counter' is undefined here - different process
    {error, \_} \= py:eval(Ctx, <<"counter"\>>)
end).

This enables OTP-style patterns for Python:

\-module(py\_counter).
-behaviour(gen\_server).

init(\[\]) \->
    Ctx \= py:context(),
    ok \= py:exec(Ctx, <<"
class Counter:
    def \_\_init\_\_(self): self.value = 0
    def incr(self): self.value += 1; return self.value
counter = Counter()
"\>>),
    {ok, #{ctx \=> Ctx}}.

handle\_call(incr, \_From, #{ctx :\= Ctx} \= State) \->
    {ok, Value} \= py:eval(Ctx, <<"counter.incr()"\>>),
    {reply, Value, State}.

Resetting Python state is simple: terminate the process. Supervisors can restart it with a fresh environment. No need for manual cleanup.

See Process-Bound Environments for patterns like ML pipelines, stateful actors, and supervision strategies.

Async/Await Support
-------------------

Call Python async functions without blocking:

%% Call an async function
Ref \= py:async\_call(aiohttp, get, \[<<"https://api.example.com/data"\>>\]),
{ok, Response} \= py:async\_await(Ref).

%% Gather multiple async calls concurrently
{ok, \[Users, Posts, Comments\]} \= py:async\_gather(\[
    {aiohttp, get, \[<<"https://api.example.com/users"\>>\]},
    {aiohttp, get, \[<<"https://api.example.com/posts"\>>\]},
    {aiohttp, get, \[<<"https://api.example.com/comments"\>>\]}
\]).

Parallel Execution with Sub-interpreters
----------------------------------------

True parallelism without GIL contention using Python 3.14+ OWN\_GIL sub-interpreters:

%% Execute multiple calls in parallel across OWN\_GIL sub-interpreters
%% Requires Python 3.14+
{ok, Results} \= py:parallel(\[
    {math, factorial, \[100\]},
    {math, factorial, \[200\]},
    {math, factorial, \[300\]},
    {math, factorial, \[400\]}
\]).
%% Each call runs in its own interpreter with its own GIL

For Python 3.12/3.13 the public modes are `worker` (default) and `owngil` (Python 3.14+ only). Earlier versions run all contexts under the shared main interpreter via dedicated worker threads — namespace isolation between contexts is local-dict based, not via subinterpreters.

Parallel Processing with BEAM Processes
---------------------------------------

Leverage Erlang's lightweight processes for massive parallelism:

%% Register parallel map function
py:register\_function(parallel\_map, fun(\[FuncName, Items\]) ->
    Parent \= self(),
    Refs \= \[begin
        Ref \= make\_ref(),
        spawn(fun() \->
            Result \= execute(FuncName, Item),
            Parent ! {Ref, Result}
        end),
        Ref
    end || Item <- Items\],
    \[receive {Ref, R} -> R after 5000 -> timeout end || Ref <- Refs\]
end).

%% Call from Python - processes 10 items in parallel
{ok, Results} \= py:eval(
    <<"\_\_import\_\_('erlang').call('parallel\_map', 'compute', items)"\>>,
    #{items \=> lists:seq(1, 10)}
).

**Benchmark Results** (from `examples/erlang_concurrency.erl`):

```
Sequential: 10 Python calls × 100ms each = 1.01 seconds
Parallel:   10 BEAM processes calling Python = 0.10 seconds
```

The speedup is linear with the number of items when work is I/O-bound or distributed across sub-interpreters.

Virtual Environment Support
---------------------------

%% Activate a venv
ok \= py:activate\_venv(<<"/path/to/venv"\>>).

%% Use packages from venv
{ok, Model} \= py:call(sentence\_transformers, 'SentenceTransformer', \[<<"all-MiniLM-L6-v2"\>>\]).

%% Deactivate when done
ok \= py:deactivate\_venv().

Logging and Tracing
-------------------

### Python Logging to Erlang Logger

Forward Python `logging` messages to Erlang's `logger`:

%% Configure Python logging
ok \= py:configure\_logging(#{level \=> info}).

%% Python logs now appear in Erlang logger
ok \= py:exec(<<"
import logging
logging.info('Hello from Python!')
logging.warning('Something needs attention')
"\>>).

From Python, you can also set up logging explicitly:

import erlang
erlang.setup\_logging(level\=20)  \# 20 = INFO

### Distributed Tracing

Collect trace spans from Python code:

%% Enable tracing
ok \= py:enable\_tracing().

%% Run Python code with spans
ok \= py:exec(<<"
import erlang
with erlang.Span('process-request', user\_id=123):
    with erlang.Span('query-database'):
        pass  # database work
    with erlang.Span('format-response'):
        pass  # formatting work
"\>>).

%% Retrieve collected spans
{ok, Spans} \= py:get\_traces().
%% Spans = \[#{name => <<"query-database">>, status => ok, duration\_us => 42, ...}, ...\]

%% Clean up
ok \= py:clear\_traces().
ok \= py:disable\_tracing().

Use the `@erlang.trace()` decorator for automatic function tracing:

import erlang

@erlang.trace()
def my\_function():
    return compute\_something()

See docs/logging.md for details.

Examples
--------

The `examples/` directory contains runnable demonstrations:

### Semantic Search

# Setup
python3 -m venv /tmp/ai-venv
/tmp/ai-venv/bin/pip install sentence-transformers numpy

# Run
escript examples/semantic\_search.erl

### RAG (Retrieval-Augmented Generation)

# Setup (also install Ollama and pull a model)
/tmp/ai-venv/bin/pip install sentence-transformers numpy requests
ollama pull llama3.2

# Run
escript examples/rag\_example.erl

### AI Chat

escript examples/ai\_chat.erl

### Erlang Concurrency from Python

# Demonstrates 10x speedup with BEAM processes
escript examples/erlang\_concurrency.erl

### Elixir Integration

elixir --erl "\-pa \_build/default/lib/erlang\_python/ebin" examples/elixir\_example.exs

### Logging and Tracing

escript examples/logging\_example.erl

API Reference
-------------

### Function Calls

{ok, Result} \= py:call(Module, Function, Args).
{ok, Result} \= py:call(Module, Function, Args, KwArgs).
{ok, Result} \= py:call(Module, Function, Args, KwArgs, Timeout).

%% Async with result
Ref \= py:spawn\_call(Module, Function, Args).
{ok, Result} \= py:await(Ref).
{ok, Result} \= py:await(Ref, Timeout).

%% Fire-and-forget (no result returned)
ok \= py:cast(Module, Function, Args).

### Expression Evaluation

{ok, 42} \= py:eval(<<"21 \* 2"\>>).
{ok, 100} \= py:eval(<<"x \* y"\>>, #{x \=> 10, y \=> 10}).
{ok, Result} \= py:eval(Expression, Locals, Timeout).

### Streaming

{ok, Chunks} \= py:stream(Module, GeneratorFunc, Args).
{ok, \[0,1,4,9,16\]} \= py:stream\_eval(<<"(x\*\*2 for x in range(5))"\>>).

### Callbacks

py:register\_function(Name, fun(\[Args\]) -> Result end).
py:register\_function(Name, Module, Function).
py:unregister\_function(Name).

### Memory and GC

{ok, Stats} \= py:memory\_stats().
{ok, Collected} \= py:gc().
ok \= py:tracemalloc\_start().
ok \= py:tracemalloc\_stop().

### Logging

ok \= py:configure\_logging().
ok \= py:configure\_logging(#{level \=> info, format \=> <<"%(name)s: %(message)s"\>>}).

### Tracing

ok \= py:enable\_tracing().
ok \= py:disable\_tracing().
{ok, Spans} \= py:get\_traces().
ok \= py:clear\_traces().

Type Mappings
-------------

### Erlang to Python

Erlang

Python

`integer()`

`int`

`float()`

`float`

`binary()`

`str`

`atom()`

`str`

`true` / `false`

`True` / `False`

`none` / `nil`

`None`

`list()`

`list`

`tuple()`

`tuple`

`map()`

`dict`

### Python to Erlang

Python

Erlang

`int`

`integer()`

`float`

`float()`

`str`

`binary()`

`bytes`

`binary()`

`True` / `False`

`true` / `false`

`None`

`none`

`list`

`list()`

`tuple`

`tuple()`

`dict`

`map()`

Configuration
-------------

%% sys.config
\[
  {erlang\_python, \[
    {num\_contexts, 8},          %% Number of contexts (default: schedulers)
    {context\_mode, worker},     %% worker | owngil
    {max\_concurrent, 17}        %% Max concurrent operations (default: schedulers \* 2 + 1)
  \]}
\].

Execution Modes
---------------

### Context Modes

When creating Python contexts, you can choose the execution mode:

Mode

Python Version

Description

`worker`

Any

Dedicated pthread per context, main interpreter namespace (default)

`owngil`

3.14+

Dedicated pthread + subinterpreter with its own GIL, true parallelism

%% Default: worker mode (recommended)
%% With free-threaded Python (3.13t+), provides true parallelism automatically
{ok, Ctx} \= py\_context:new(#{}).

%% OWN\_GIL mode for true parallelism (Python 3.14+ required)
%% Each context runs in its own pthread with independent GIL
{ok, Ctx} \= py\_context:new(#{mode \=> owngil}).

**Worker mode is recommended** because it works with any Python version and automatically benefits from free-threaded Python (3.13t+) when available. Each context owns a dedicated pthread, providing stable thread affinity for libraries with thread-local state (numpy, torch, tensorflow).

**Why OWN\_GIL requires Python 3.14+**: Some C extensions (e.g., `_decimal`, `numpy`) have global state bugs in sub-interpreters on Python 3.12/3.13. These are fixed in Python 3.14.

### Runtime Detection

Check the current execution mode (mirrors the `context_mode` application env):

py:execution\_mode().  %% => worker | owngil

Mode

Python Version

Parallelism

`worker` (default)

Any

One pthread per context; true parallelism on free-threaded 3.13t+

`owngil`

3.14+

Per-interpreter GIL, true parallelism across contexts

Error Handling
--------------

{error, {'NameError', "name 'x' is not defined"}} \= py:eval(<<"x"\>>).
{error, {'ZeroDivisionError', "division by zero"}} \= py:eval(<<"1/0"\>>).
{error, timeout} \= py:eval(<<"sum(range(10\*\*9))"\>>, #{}, 100).

Documentation
-------------

-   Getting Started
-   Process-Bound Environments - Isolated Python state per Erlang process
-   AI Integration Guide
-   Type Conversion
-   Context Affinity
-   Scalability
-   Streaming
-   Threading
-   Logging and Tracing
-   Asyncio Event Loop - Erlang-native asyncio with TCP/UDP support
-   Reactor - FD-based protocol handling
-   Security - Sandbox and blocked operations
-   Changelog

License
-------

Apache-2.0
