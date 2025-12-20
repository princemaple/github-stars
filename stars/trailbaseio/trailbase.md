---
project: trailbase
stars: 4284
description: A blazingly fast, open-source application server with type-safe APIs, built-in WebAssembly runtime, realtime, auth, and admin UI built on Rust, SQLite & Wasmtime.
url: https://github.com/trailbaseio/trailbase
---

An open, blazingly fast, single-executable Firebase alternative with type-safe REST & realtime APIs, built-in WebAssembly runtime, SSR, auth and admin UI built on Rust, SQLite & Wasmtime.

Simplify with fewer moving parts: an easy to self-host, single-executable, extensible backend for your mobile, web or desktop application. Sub-millisecond latencies eliminate the need for dedicated caches, no more stale or inconsistent data.

TrailBase
=========

**Try the demo online**  
Email: _admin@localhost_  
password: _secret_

For more context, documentation, and a live demo, check out the website: trailbase.io. Questions? Thoughts? - Take a look at the FAQ or reach out. If you like TrailBase or want to follow along, consider leaving a ⭐🙏.

Project Structure & Releases
----------------------------

This repository contains all components that make up TrailBase including the server, client libraries, tests, documentation and examples. Only the benchmarks are kept separately due to their external dependencies.

Pre-built binaries are available as GitHub releases for Linux, MacOS and Windows or Docker images.

Client packages for various languages are available via:

-   JavaScript/TypeScript
-   Dart/Flutter
-   Rust
-   C#/.Net
-   Swift
-   Kotlin
-   Go
-   Python

Getting Started
---------------

TrailBase is a **single executable** and therefore very easy to deploy. You can simply download the appropriate pre-built GitHub release bundle for your system (MacOS, Linux or Windows), unpack and run the executable w/o having to worry about dependencies or shared-library skew.

If you want to get started even quicker, install TrailBase with the following command:

# Linux & MacOS
curl -sSL https://trailbase.io/install.sh | bash

# Windows
iwr https://trailbase.io/install.ps1 | iex

Alternatively, run TrailBase using the Docker image:

alias trail='
  mkdir -p traildepot && \\
  docker run \\
      -p 4000:4000 \\
      -e ADDRESS=0.0.0.0:4000 \\
      --mount type=bind,source="$PWD"/traildepot,target=/app/traildepot \\
      trailbase/trailbase /app/trail'

Then execute `trail help` to check that it is properly installed and list all available command line options.

To bring up the server on `localhost:4000`, run:

trail run

On first start, a `./traildepot` folder will be bootstrapped, an admin user created and their credentials printed to the terminal. Afterwards open http://localhost:4000/\_/admin/ in your browser and use the credentials to log into the admin dashboard.

If you want to install the auth UI, you can simply run:

trail components add trailbase/auth\_ui

, which will add a WASM component in `./traildepot/wasm` exposing additional UI endpoints, e.g. http://localhost:4000/\_/auth/login.

Building
--------

If you have all the necessary build dependencies (Rust, protobuf, node.js, pnpm) installed, you can build TrailBase by running:

# Windows only: make sure to enable symlinks (w/o \`mklink\` permissions for your
# user, git will fall back to copies).
git config core.symlinks true && git reset --hard

# Download necessary git sub-modules.
git submodule update --init --recursive

# Install Javascript dependencies first. Required for the next step.
pnpm install

# Build the executable. Adding \`--release\` will yield a more optimized binary
# but slow builds significantly.
cargo build --bin trail

Alternatively, if you want to build a Docker image or don't want to deal with build dependencies, you can simply run:

# Download necessary git sub-modules.
git submodule update --init --recursive

# Build the container as defined in \`Dockerfile\`.
docker build . -t trailbase

Contributing
------------

Contributions are very much appreciated 🙏. For anything beyond bug fixes, let's briefly chat to see how a proposal fits into the overall roadmap and avoid any surprises.

We're not sure yet what the best setup or exact license is for compatibility between OSL-3.0 and more popular licenses or use as a framework. So we'd ask you to sign a simple CLA that retains your copyright, ensures that TrailBase will continue to forever be freely available under an OSI-approved copyleft license, while allowing for some flexibility and sub-licensing as established by much larger, successful projects such as Grafana or Element.

License
-------

TrailBase is free software under the terms of the Open Software License 3.0 (OSL-3.0).

We chose the OSL-3.0 over other, better known copyleft licenses due to its narrower definition of "derivative work" that **only** covers modifications to TrailBase itself. This means that your application's original code is **not** subject to the OSL-3.0's copyleft provisions. This is true whether you connect over the network (e.g. web, mobile, other services, etc.), you're serving static assets, using the runtime to write custom server-side logic or using TrailBase as a framework.

This limited scope is similar to the GPL's classpath or the LGPL's linking exception. The goal is to allow building on top and around of TrailBase without any provisions rubbing off onto your original work, while making sure that fixes and improvements find their way back to the community. These are our intentions - we felt the need to spell them out explicitly because licensing is tricky and we ain't lawyers. Graciously, the license's author provides some more explanations. If you have any concerns, please reach out.

If you require an exception, reach out to contact@trailbase.io.
