---
project: popcorn
stars: 592
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

The examples are hosted at popcorn.swmansion.com, and the source code is in the `examples` directory.

Development
-----------

We use `mise` to manage dependencies. Install it and install deps and dev tools with:

mise install

Then, you should setup pre-commit hooks using lefthook:

lefthook install

### Testing

Popcorn tests can be run either on WASM via Playwright or natively on UNIX. To run them on WASM, run

TARGET=wasm mix test

To run tests on UNIX, use

mix popcorn.build\_runtime --target unix

to build AtomVM from source. Make sure you have AtomVM dependencies installed. Then, run

mix test

Authors
-------

Popcorn is created by Software Mansion.

Since 2012 Software Mansion is a software agency with experience in building web and mobile apps as well as complex multimedia solutions. We are Core React Native Contributors and experts in live streaming and broadcasting technologies. We can help you build your next dream product – Hire us.

Copyright 2025, Software Mansion

Licensed under the Apache License, Version 2.0
