---
project: rambo
stars: 212
description: Run your command. Send input. Get output.
url: https://github.com/jayjun/rambo
---

Rambo
=====

Rambo is the easiest way to run external programs.

-   Run programs that require EOF to produce output
-   No more zombies, even if the VM crashes! No scripts required!
-   No additional installs or compilers (Linux, macOS & Windows only)
-   Stream logs back to your app
-   Chain commands together
-   Kill stalled commands
-   Set timeout or run indefinitely
-   Powered by asynchronous I/O, incredibly efficient!

Usage
-----

Rambo.run("echo")
{:ok, %Rambo{status: 0, out: "\\n", err: ""}}

\# send standard input
Rambo.run("cat", in: "rambo")

\# pass arguments
Rambo.run("ls", \["-l", "-a"\])

\# chain commands
Rambo.run("ls") |> Rambo.run("sort") |> Rambo.run("head")

\# set timeout
Rambo.run("find", "peace", timeout: 1981)

### Logging

Logs to standard error are printed by default, so errors are visible before your command finishes. Change this with the `:log` option.

Rambo.run("ls", log: :stderr) \# default
Rambo.run("ls", log: :stdout) \# log stdout only
Rambo.run("ls", log: true)    \# log both stdout and stderr
Rambo.run("ls", log: false)   \# don’t log output

\# or to any function
Rambo.run("echo", log: &IO.inspect/1)

### Kill

Kill your command from another process, Rambo returns with any gathered results so far.

task \= Task.async(fn \->
  Rambo.run("cat")
end)

Rambo.kill(task.pid)

Task.await(task)
{:killed, %Rambo{status: nil, out: "", err: ""}}

Why?
----

Erlang ports do not work with programs that expect EOF to produce output. The only way to close standard input is to close the port, which also closes standard output, preventing results from coming back to your app. This gotcha is marked Won’t Fix.

### Design

When Rambo is asked to run a command, it starts a shim that spawns your command as a child. After writing to standard input, the file descriptor is closed while output is streamed back to your app.

```
+-----------------+       stdin
|          +------+------+ --> +---------+
|  Erlang  | Port | Shim |     | Command |
|          +------+------+ <-- +---------+
+-----------------+       stdout
```

If your app exits prematurely, the child is automatically killed to prevent orphans.

Caveats
-------

You cannot call `Rambo.run` from a GenServer because Rambo uses `receive`, which interferes with GenServer’s `receive` loop. However, you can wrap the call in a Task.

task \= Task.async(fn \->
  Rambo.run("mission")
end)

Task.await(task)

Comparisons
-----------

Rambo does not spawn any processes nor support bidirectional communication with your commands. It is intentionally kept simple to run transient jobs with minimal overhead, such as calling a Python or Node script to transform some data. For more complicated use cases, see below.

### System.cmd

If you don’t need to pipe standard input or capture standard error, just use `System.cmd`.

### Porcelain

Porcelain cannot send EOF to trigger output by default. The Goon driver must be installed separately to add this capability. Rambo ships with the required native binaries.

Goon is written in Go, a multithreaded runtime with a garbage collector. To be as lightweight as possible, Rambo’s shim is written in Rust using non-blocking, asynchronous I/O only. No garbage collection runtime, no latency spikes.

Most importantly, Porcelain currently leaks processes. Writing a new driver to replace Goon should fix it, but Porcelain appears to be abandoned so effort went into creating Rambo.

### MuonTrap

MuonTrap is designed to run long-running external programs. You can attach the OS process to your supervision tree, and restart it if it crashes. Likewise if your Elixir process crashes, the OS process is terminated too.

You can also limit CPU and memory usage on Linux through cgroups.

### erlexec

erlexec is great if you want fine grain control over external programs.

Each external OS process is mirrored as an Erlang process, so you get asynchronous and bidirectional communication. You can kill your OS processes with any signal or monitor them for termination, among many powerful features.

Choose erlexec if you want a kitchen sink solution.

### ExCmd

ExCmd can stream data with backpressure, wrapped in a convenient `Stream` API. Requires separate install of Odu. By the same author as Exile.

### Exile

Exile is also focused on streaming like ExCmd but implemented with NIFs so it does not require shims.

Installation
------------

Add `rambo` to your list of dependencies in `mix.exs`:

def deps do
  \[
    {:rambo, "~> 0.3"}
  \]
end

Linux, macOS and Windows binaries are bundled (x86-64 architecture only). For other environments, install the Rust compiler or Rambo won’t compile.

To remove unused binaries, set `:purge` to `true` in your configuration.

config :rambo,
  purge: true

Links
-----

-   Documentation
-   Hex

License
-------

Rambo is released under MIT license.
