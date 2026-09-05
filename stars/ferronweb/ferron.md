---
project: ferron
stars: 2129
description: A fast, modern web server built for production debugging.
url: https://github.com/ferronweb/ferron
---

**Ferron** - a fast, modern web server built for production debugging.
======================================================================

Why Ferron?
-----------

Built to set up quickly, behave predictably, and hold up reliably in production.

-   **Readable configuration** - set up websites and reverse proxies with a clear, compact config that avoids sprawl and hidden surprises.
-   **Automatic TLS** - certificates are issued and renewed automatically. You get clear signals when it works (or doesn't).
-   **First-class observability** - see exactly what happened with any request. Traces cover every layer and link directly to the relevant logs.
-   **Predictable performance** - fast and consistent under load, right out of the box. No runtime tuning required.
-   **Memory-safe** - entire categories of memory-related security holes simply don't exist in Ferron (it's built with Rust).
-   **Reliable in production** - handles messy real-world traffic, upstream failures, and protocol edge cases predictably.

Tip

Ferron is designed around two core principles: **ease of setup** (get a working config in minutes) and **ease of debugging** (when something goes wrong, find the root cause fast).

Configuration examples
----------------------

### Static file serving

```
example.com {
    root "/var/www/html"

    # If uncommented, directory listing is enabled.
    #directory_listing
}
```

### Reverse proxy

```
api.example.com {
    proxy http://localhost:8080
}
```

More examples are available in the configuration documentation.

Installing Ferron (pre-built)
-----------------------------

The most convenient way to get started with Ferron is to use the installer script for Linux:

sudo bash -c "$(curl -fsSL https://get.ferron.sh/v3)"

See the full instructions in the Linux installation documentation.

Building from source
--------------------

git clone https://github.com/ferronweb/ferron -b develop-3.x
cd ferron
git submodule update --init --recursive
cargo build --workspace

Run the server:

cargo run -p ferron -- run -c ferron.conf
cargo run -p ferron -- run -c ferron.conf --verbose  # with debug logging

Other CLI commands:

cargo run -p ferron -- validate -c ferron.conf   # validate without starting
cargo run -p ferron -- adapt -c ferron.conf      # output config as JSON
cargo run -p ferron -- daemon -c ferron.conf --pid-file /var/run/ferron.pid  # Unix daemon

Run tests and checks:

cargo test --workspace
cargo fmt --all --check
cargo clippy --workspace --all-targets -- -D warnings

Package Ferron for distribution (requires `just`):

just package # Archive (.zip for Windows, .tar.gz for Unix)
just package-deb # Debian package
just package-rpm # RPM package
just package-windows # Windows installer
just installer # Linux installer

Cross-build optimized binaries for Ferron (see README for the build files; available on Linux only):

just cross-build

Configuration
-------------

The full directive reference is in docs/configuration/.

Contributing
------------

Feedback, bug reports, and testing are welcome. When reporting issues, include your configuration file, `--verbose` output, and steps to reproduce.

License
-------

MIT. See `LICENSE` for details.
