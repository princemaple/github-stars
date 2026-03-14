---
project: popcorn
stars: 604
description: Running Elixir in the browser
url: https://github.com/software-mansion/popcorn
---

**Popcorn is a library that allows you to run client-side Elixir in browsers, with JavaScript interoperability**

Popcorn is early stages and may break. Please report an issue if it does. Contributions are very welcome, but please open an issue before committing too much effort.

Under the hood, Popcorn runs AtomVM, a tiny Erlang VM.

Documentation
-------------

The API documentation and guides are available at https://hexdocs.pm/popcorn

Examples
--------

The examples are hosted at popcorn.swmansion.com, and the source code is in the `examples/` directory.

Repository Structure
--------------------

-   **`popcorn/elixir/`** - Elixir library used to patch OTP and Elixir stdlib, create .avm bundles and containing JS interop API.
-   **`popcorn/js/`** - JavaScript library loads the VM in Wasm, manages its isolation, and bridges JS and Elixir.
-   **`examples/`** - Example projects showcasing Popcorn features, hosted at popcorn.swmansion.com. Examples use development version of Popcorn.
-   **`landing-page/`** - Popcorn landing page.
-   **`language-tour/`** - Interactive Elixir language tour running purely in the browser.
-   **`local-live-view/`** - Experimental client-side LiveView implementation.
-   **`scripts/`** - Shell scripts for development, testing, and CI tasks.
-   **`docker/`** - Dockerfiles and nginx configs for CI and deployment.

Development
-----------

We use `mise` to manage tool versions and run tasks. Install it, then:

mise install
mise run dev

This installs all dependencies (Elixir, Node, pnpm) and starts the JS library in watch mode.

To develop with an example or project:

mise run dev --example hello-popcorn
mise run dev --project landing-page
mise run dev --project language-tour

Run `scripts/dev.sh --help` to see all available examples and projects.

### Testing

mise run test               # Elixir unix tests (default)
mise run test --wasm     # Elixir wasm tests
mise run test --js       # JS tests

AtomVM is built automatically if artifacts are missing. Make sure you have AtomVM dependencies installed.

### Other tasks

mise run clean              # Clean build artifacts
mise run clean --all     # Clean everything including examples

All tasks are thin wrappers around `scripts/*.sh` — you can run those directly.

Authors
-------

Popcorn is created by Software Mansion.

Since 2012 Software Mansion is a software agency with experience in building web and mobile apps as well as complex multimedia solutions. We are Core React Native Contributors and experts in live streaming and broadcasting technologies. We can help you build your next dream product – Hire us.

Copyright 2025, Software Mansion

Licensed under the Apache License, Version 2.0
