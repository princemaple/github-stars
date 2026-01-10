---
project: ferron
stars: 1797
description: A fast, memory-safe web server written in Rust.
url: https://github.com/ferronweb/ferron
---

**Ferron** - a fast, memory-safe web server written in Rust

* * *

Features
--------

-   **High performance** - built with Rust’s async capabilities for optimal speed.
-   **Memory-safe** - built with Rust, which is a programming language offering memory safety.
-   **Extensibility** - modular architecture for easy customization.
-   **Secure** - focus on robust security practices and safe concurrency.

Components
----------

Ferron consists of multiple components:

-   **`ferron`** - the main web server.
-   **`ferron-passwd`** - a tool for generating hashed passwords, which can be copied into the web server's configuration file.
-   **`ferron-precompress`** - a tool for precompressing static files for Ferron.
-   **`ferron-yaml2kdl`** - a tool for attempting to convert the Ferron 1.x YAML configuration to Ferron 2.x KDL configuration.

Ferron also consists of:

-   **`build-prepare`** - internal tool for preparation when building Ferron with modules.
-   **`ferron-common`** - code common for Ferron and its modules.
-   **`ferron-dns-builtin`** - built-in Ferron DNS providers.
-   **`ferron-load-modules`** - functions for loading Ferron modules.
-   **`ferron-modules-builtin`** - built-in Ferron modules.
-   **`ferron-yaml2kdl-core`** - the core library behind the `ferron-yaml2kdl` tool.

Building Ferron from source
---------------------------

You can clone the repository and explore the existing code:

git clone https://github.com/ferronweb/ferron.git
cd ferron

You can then build and run the web server using Cargo:

cargo run --manifest-path build-prepare/Cargo.toml
cd build-workspace
cargo update # If you experience crate conflicts
cargo build -r --target-dir ../target
cd ..
cp ferron-test.kdl ferron.kdl
target/release/ferron

You can also, for convenience, use `make`:

make build # Build the web server
make build-dev # Build the web server, for development and debugging
make run # Run the web server
make run-dev # Run the web server, for development and debugging
make smoketest # Perform a smoke test
make smoketest-dev # Perform a smoke test, for development and debugging
make package # Package the web server to a ZIP archive (run it after building it)
make package-deb # Package the web server to a Debian package (run it after building it)
make package-rpm # Package the web server to an RPM package (run it after building it)
make installer # Build installers for Ferron 2

Or a `build.ps1` build script, if you're on Windows:

REM Build the web server
powershell -ExecutionPolicy Bypass .\\build.ps1 Build

REM Build the web server, for development and debugging
powershell -ExecutionPolicy Bypass .\\build.ps1 BuildDev

REM Run the web server
powershell -ExecutionPolicy Bypass .\\build.ps1 Run

REM Run the web server, for development and debugging
powershell -ExecutionPolicy Bypass .\\build.ps1 RunDev

REM Perform a smoke test
powershell -ExecutionPolicy Bypass .\\build.ps1 Smoketest

REM Perform a smoke test, for development and debugging
powershell -ExecutionPolicy Bypass .\\build.ps1 SmoketestDev

REM Package the web server to a ZIP archive (run it after building it)
powershell -ExecutionPolicy Bypass .\\build.ps1 Package

REM Build installers for Ferron 2
powershell -ExecutionPolicy Bypass .\\build.ps1 Installer

You can also create a ZIP archive that can be used by the Ferron installer:

make build-with-package

Or if you're on Windows:

powershell -ExecutionPolicy Bypass .\\build.ps1 BuildWithPackage

The ZIP archive will be located in the `dist` directory.

You can also cross-compile the web server for a different target:

# Replace "i686-unknown-linux-gnu" with the target (as defined by the Rust target triple) you want to build for
make build TARGET="i686-unknown-linux-gnu" CARGO\_FINAL="cross"

It's also possible to use only Cargo to build the web server, although you wouldn't be able to use external modules:

cargo build -r
./target/release/ferron

For compilation notes, see the compilation notes page.

Modules
-------

If you would like to develop Ferron modules, you can find the Ferron module development notes.

Server configuration
--------------------

You can check the Ferron documentation to see configuration properties used by Ferron.

Contributing
------------

See Ferron contribution page for details.

Below is a list of contributors to Ferron. **Thank you to all of them!**

License
-------

Ferron is licensed under the MIT License. See `LICENSE` for details.
