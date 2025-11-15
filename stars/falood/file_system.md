---
project: file_system
stars: 278
description: Filesystem monitor for elixir
url: https://github.com/falood/file_system
---

FileSystem
==========

An Elixir file change watcher wrapper based on FS, the native file system listener.

System Support
--------------

-   MacOS - fsevent
-   GNU/Linux, FreeBSD, DragonFly and OpenBSD - inotify
-   Windows - inotify-win

On MacOS 10.14, to compile `mac_listener`, run:

open /Library/Developer/CommandLineTools/Packages/macOS\_SDK\_headers\_for\_macOS\_10.14.pkg

On newer versions this file doesn't exist. But it still should work just fine as long as you have xcode installed.

Usage
-----

Add `file_system` to the `deps` of your mix.exs

defmodule MyApp.Mixfile do
  use Mix.Project

  def project do
  ...
  end

  defp deps do
    \[
      {:file\_system, "~> 1.0", only: :test},
    \]
  end
  ...
end

### Subscription API

You can spawn a worker and subscribe to events from it:

{:ok, pid} \= FileSystem.start\_link(dirs: \["/path/to/some/files"\])
FileSystem.subscribe(pid)

or

{:ok, pid} \= FileSystem.start\_link(dirs: \["/path/to/some/files"\], name: :my\_monitor\_name)
FileSystem.subscribe(:my\_monitor\_name)

The `pid` you subscribed from will now receive messages like:

```
{:file_event, worker_pid, {file_path, events}}
```

and

```
{:file_event, worker_pid, :stop}
```

### Example Using GenServer

defmodule Watcher do
  use GenServer

  def start\_link(args) do
    GenServer.start\_link(\_\_MODULE\_\_, args)
  end

  def init(args) do
    {:ok, watcher\_pid} \= FileSystem.start\_link(args)
    FileSystem.subscribe(watcher\_pid)
    {:ok, %{watcher\_pid: watcher\_pid}}
  end

  def handle\_info({:file\_event, watcher\_pid, {path, events}}, %{watcher\_pid: watcher\_pid} \= state) do
    \# Your own logic for path and events
    {:noreply, state}
  end

  def handle\_info({:file\_event, watcher\_pid, :stop}, %{watcher\_pid: watcher\_pid} \= state) do
    \# Your own logic when monitor stop
    {:noreply, state}
  end
end

Backend Options
---------------

For each platform, you can pass extra options to the underlying listener process.

Each backend supports different extra options, check backend module documentation for more details.

Here is an example to get instant notifications on file changes for MacOS:

FileSystem.start\_link(dirs: \["/path/to/some/files"\], latency: 0, watch\_root: true)
