---
project: workerd
stars: 8155
description: The JavaScript / Wasm runtime that powers Cloudflare Workers
url: https://github.com/cloudflare/workerd
---

👷 `workerd`, Cloudflare's JavaScript/Wasm Runtime
==================================================

`workerd` (pronounced: "worker-dee") is a JavaScript / Wasm server runtime based on the same code that powers Cloudflare Workers.

You might use it:

-   **As an application server**, to self-host applications designed for Cloudflare Workers.
-   **As a development tool**, to develop and test such code locally.
-   **As a programmable HTTP proxy** (forward or reverse), to efficiently intercept, modify, and route network requests.

Introduction
------------

### Design Principles

-   **Server-first:** Designed for servers, not CLIs nor GUIs.
    
-   **Standard-based:** Built-in APIs are based on web platform standards, such as `fetch()`.
    
-   **Nanoservices:** Split your application into components that are decoupled and independently-deployable like microservices, but with performance of a local function call. When one nanoservice calls another, the callee runs in the same thread and process.
    
-   **Homogeneous deployment:** Instead of deploying different microservices to different machines in your cluster, deploy all your nanoservices to every machine in the cluster, making load balancing much easier.
    
-   **Capability bindings:** `workerd` configuration uses capabilities instead of global namespaces to connect nanoservices to each other and external resources. The result is code that is more composable -- and immune to SSRF attacks.
    
-   **Always backwards compatible:** Updating `workerd` to a newer version will never break your JavaScript code. `workerd`'s version number is simply a date, corresponding to the maximum "compatibility date" supported by that version. You can always configure your worker to a past date, and `workerd` will emulate the API as it existed on that date.
    

Read the blog post to learn more about these principles.

### WARNING: `workerd` is not a hardened sandbox

`workerd` tries to isolate each Worker so that it can only access the resources it is configured to access. However, `workerd` on its own does not contain suitable defense-in-depth against the possibility of implementation bugs. When using `workerd` to run possibly-malicious code, you must run it inside an appropriate secure sandbox, such as a virtual machine. The Cloudflare Workers hosting service in particular uses many additional layers of defense-in-depth.

With that said, if you discover a bug that allows malicious code to break out of `workerd`, please submit it to Cloudflare's bug bounty program for a reward.

Getting Started
---------------

### Supported Platforms

In theory, `workerd` should work on any POSIX system that is supported by V8 and Windows.

In practice, `workerd` is tested on:

-   Linux and macOS (x86-64 and arm64 architectures)
-   Windows (x86-64 architecture)

On other platforms, you may have to do tinkering to make things work.

### Building `workerd`

To build `workerd`, you need:

-   Bazel
    -   If you use Bazelisk (recommended), it will automatically download and use the right version of Bazel for building workerd.
-   On Linux:
    -   We use the clang/LLVM toolchain to build workerd and support version 19 and higher. Earlier versions of clang may still work, but are not officially supported.
        
    -   Clang 19+ (e.g. package `clang-19` on Debian Trixie). If clang is installed as `clang-<version>` please create a symlink to it in your PATH named `clang`, or use `--repo_env=CC=clang-<version>` on `bazel` command lines to specify the compiler name.
        
    -   libc++ 19+ (e.g. packages `libc++-19-dev` and `libc++abi-19-dev`)
        
    -   LLD 19+ (e.g. package `lld-19`).
        
    -   `python3`, `python3-distutils`, and `tcl8.6`
        
-   On macOS:
    -   Xcode 16.3 installation (available on macOS 15 and higher). Building with just the Xcode Command Line Tools is not being tested, but should work too.
    -   Homebrew installed `tcl-tk` package (provides Tcl 8.6)
-   On Windows:
    -   Install App Installer from the Microsoft Store for the `winget` package manager and then run install-deps.bat from an administrator prompt to install bazelisk, LLVM, and other dependencies required to build workerd on Windows.
    -   Add `startup --output_user_root=C:/tmp` to the `.bazelrc` file in your user directory.
    -   When developing at the command-line, run bazel-env.bat in your shell first to select tools and Windows SDK versions before running bazel.

You may then build `workerd` at the command-line with:

bazel build //src/workerd/server:workerd

You can pass `--config=release` to compile in release mode:

bazel build //src/workerd/server:workerd --config=release

You can also build from within Visual Studio Code using the instructions in docs/vscode.md.

The compiled binary will be located at `bazel-bin/src/workerd/server/workerd`.

If you run a Bazel build before you've installed some dependencies (like clang or libc++), and then you install the dependencies, you must resync locally cached toolchains, or clean Bazel's cache, otherwise you might get strange errors:

bazel fetch --configure --force

If that fails, you can try:

bazel clean --expunge

The cache will now be cleaned and you can try building again.

If you have a fairly recent clang packages installed you can build a more performant release version of workerd:

bazel build --config=thin-lto //src/workerd/server:workerd

### Configuring `workerd`

`workerd` is configured using a config file written in Cap'n Proto text format.

A simple "Hello World!" config file might look like:

using Workerd = import "/workerd/workerd.capnp";

const config :Workerd.Config = (
  services = \[
    (name = "main", worker = .mainWorker),
  \],

  sockets = \[
    # Serve HTTP on port 8080.
    ( name = "http",
      address = "\*:8080",
      http = (),
      service = "main"
    ),
  \]
);

const mainWorker :Workerd.Worker = (
  serviceWorkerScript = embed "hello.js",
  compatibilityDate = "2023-02-28",
  # Learn more about compatibility dates at:
  # https://developers.cloudflare.com/workers/platform/compatibility-dates/
);

Where `hello.js` contains:

addEventListener("fetch", event \=> {
  event.respondWith(new Response("Hello World"));
});

Complete reference documentation is provided by the comments in workerd.capnp.

There is also a library of sample config files.

### Running `workerd`

To serve your config, do:

`workerd serve my-config.capnp`

For more details about command-line usage, use `workerd --help`.

Prebuilt binaries are distributed via `npm`. Run `npx workerd ...` to use these. If you're running a prebuilt binary, you'll need to make sure your system has the right dependencies installed:

-   On Linux:
    -   glibc 2.35 or higher (already included on e.g. Ubuntu 22.04, Debian Bookworm)
-   On macOS:
    -   macOS 13.5 or higher
    -   The Xcode command line tools, which can be installed with `xcode-select --install`
-   x86\_64 CPU with at least SSE4.2 and CLMUL ISA extensions, or arm64 CPU with CRC extension (enabled by default under armv8.1-a). These extensions are supported by all recent x86 and arm64 CPUs.

### Local Worker development with `wrangler`

You can use Wrangler (v3.0 or greater) to develop Cloudflare Workers locally, using `workerd`. First, run the following command to configure Miniflare to use this build of `workerd`.

```
export MINIFLARE_WORKERD_PATH="<WORKERD_REPO_DIR>/bazel-bin/src/workerd/server/workerd"
```

Then, run:

`wrangler dev`

### Serving in production

`workerd` is designed to be unopinionated about how it runs.

One good way to manage `workerd` in production is using `systemd`. Particularly useful is `systemd`'s ability to open privileged sockets on `workerd`'s behalf while running the service itself under an unprivileged user account. To help with this, `workerd` supports inheriting sockets from the parent process using the `--socket-fd` flag.

Here's an example system service file, assuming your config defines two sockets named `http` and `https`:

# /etc/systemd/system/workerd.service
\[Unit\]
Description=workerd runtime
After=local-fs.target remote-fs.target network-online.target
Requires=local-fs.target remote-fs.target workerd.socket
Wants=network-online.target

\[Service\]
Type=exec
ExecStart=/usr/bin/workerd serve /etc/workerd/config.capnp --socket-fd http=3 --socket-fd https=4
Sockets=workerd.socket

# If workerd crashes, restart it.
Restart=always

# Run under an unprivileged user account.
User=nobody
Group=nogroup

# Hardening measure: Do not allow workerd to run suid-root programs.
NoNewPrivileges=true

\[Install\]
WantedBy=multi-user.target

And corresponding sockets file:

# /etc/systemd/system/workerd.socket
\[Unit\]
Description=sockets for workerd
PartOf=workerd.service

\[Socket\]
ListenStream=0.0.0.0:80
ListenStream=0.0.0.0:443

\[Install\]
WantedBy=sockets.target

Once these files are in place you can enable the service -- see the systemd documentation or ask your favorite LLM for details.
