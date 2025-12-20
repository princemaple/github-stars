---
project: utoo
stars: 2259
description: An unified toolchain for web development.
url: https://github.com/utooland/utoo
---

> 🌖 **Notice**: We are building a next-generation toolchain on top of Turbopack. Check out our progress.

Utoo
====

**Unified Toolchain: Open & Optimized**

* * *

Utoo is a modern, high-performance frontend toolchain designed to provide a unified and optimized experience. It combines a fast package manager, a powerful bundler, and a flexible command system into a single, cohesive ecosystem.

💡 Why Utoo?
------------

Feature

Description

**Unified**

One tool for package management, building, and workflow automation.

**Performance**

Core logic in Rust + Turbopack for extreme speed.

**Compatible**

Seamless migration with Webpack compatibility mode.

**Universal**

Run anywhere: Local, CI, or Browser (via WASM).

📦 Core Components
------------------

-   **`utoo`** (alias **`ut`**): High-performance Rust package manager (Fast, Parallel, `npm` compatible).
-   **`@utoo/pack`**: Next-gen bundler powered by **Turbopack** (HMR, TS/JSX, Less/Sass, and more).
-   **`@utoo/web`**: Web-compatible version of the toolchain (WASM, Browser-based bundling).

🚀 Quick Start
--------------

### 1\. Install

# Install the core toolchain
npm install -g utoo

# Install the bundler (optional)
npm install -g @utoo/pack

# Install the web version (optional)
npm install @utoo/web

### 2\. Use

#### Package Management

utoo install          # Install dependencies (or use \`ut install\`)
utoo add lodash       # Add a package (or use \`ut add\`)
utoo x create-react   # Execute a package (npx style, or use \`ut x\`)

#### Bundling

utoopack dev          # Start dev server with HMR
utoopack build        # Production build
utoopack build --webpack # Build using webpack.config.js

✨ Key Features
--------------

-   ⚡ **Rust Powered**: Maximum performance for dependency resolution and bundling.
-   🛠️ **Turbopack Inside**: Incremental builds and instant HMR.
-   🔌 **Webpack Friendly**: Partial support for existing Webpack configurations.
-   📦 **Monorepo First**: Built-in workspace management.
-   🌐 **Web Ready**: Run the entire toolchain in the browser via WASM.

🗺️ Roadmap
-----------

We are actively working on expanding Utoo's capabilities:

-   **Persistent Caching**: Disk-based caching for even faster restarts.
-   **SSR & RSC**: Full support for modern React architectures.
-   **Plugin System**: Extensible hooks for custom build logic.
-   **Mobile Support**: Unified tooling for mobile frontend development.

📂 Project Structure
--------------------

-   **crates/**: Rust core (Package Manager, Bundler Core, WASM/NAPI bindings).
-   **packages/**: TypeScript packages (CLI, Web version, Shared utilities).
-   **next.js/**: Turbopack source integration (Git submodule).
-   **examples/**: Demo projects (React, Ant Design, Webpack-compat, etc.).

🤝 Contributing
---------------

We love contributions! Check out CONTRIBUTING.md to get started.

📄 License
----------

Utoo is licensed under the MIT License.
