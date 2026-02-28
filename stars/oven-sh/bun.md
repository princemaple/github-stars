---
project: bun
stars: 87733
description: Incredibly fast JavaScript runtime, bundler, test runner, and package manager – all in one
url: https://github.com/oven-sh/bun
---

Bun
===

Documentation   •   Discord   •   Issues   •   Roadmap  

### Read the docs →

What is Bun?
------------

Bun is an all-in-one toolkit for JavaScript and TypeScript apps. It ships as a single executable called `bun`.

At its core is the _Bun runtime_, a fast JavaScript runtime designed as **a drop-in replacement for Node.js**. It's written in Zig and powered by JavaScriptCore under the hood, dramatically reducing startup times and memory usage.

bun run index.tsx             # TS and JSX supported out-of-the-box

The `bun` command-line tool also implements a test runner, script runner, and Node.js-compatible package manager. Instead of 1,000 node\_modules for development, you only need `bun`. Bun's built-in tools are significantly faster than existing options and usable in existing Node.js projects with little to no changes.

bun test                      # run tests
bun run start                 # run the \`start\` script in \`package.json\`
bun install <pkg\>             # install a package
bunx cowsay 'Hello, world!'   # execute a package

Install
-------

Bun supports Linux (x64 & arm64), macOS (x64 & Apple Silicon) and Windows (x64 & arm64).

> **Linux users** — Kernel version 5.6 or higher is strongly recommended, but the minimum is 5.1.

> **x64 users** — if you see "illegal instruction" or similar errors, check our CPU requirements

# with install script (recommended)
curl -fsSL https://bun.com/install | bash

# on windows
powershell -c "irm bun.sh/install.ps1 | iex"

# with npm
npm install -g bun

# with Homebrew
brew tap oven-sh/bun
brew install bun

# with Docker
docker pull oven/bun
docker run --rm --init --ulimit memlock=-1:-1 oven/bun

### Upgrade

To upgrade to the latest version of Bun, run:

bun upgrade

Bun automatically releases a canary build on every commit to `main`. To upgrade to the latest canary build, run:

bun upgrade --canary

View canary build

Quick links
-----------

-   Intro
    
    -   What is Bun?
    -   Installation
    -   Quickstart
    -   TypeScript
-   Templating
    
    -   `bun init`
    -   `bun create`
-   CLI
    
    -   `bun upgrade`
-   Runtime
    
    -   `bun run`
    -   File types (Loaders)
    -   TypeScript
    -   JSX
    -   Environment variables
    -   Bun APIs
    -   Web APIs
    -   Node.js compatibility
    -   Single-file executable
    -   Plugins
    -   Watch mode / Hot Reloading
    -   Module resolution
    -   Auto-install
    -   bunfig.toml
    -   Debugger
    -   $ Shell
-   Package manager
    
    -   `bun install`
    -   `bun add`
    -   `bun remove`
    -   `bun update`
    -   `bun link`
    -   `bun unlink`
    -   `bun pm`
    -   `bun outdated`
    -   `bun publish`
    -   `bun patch`
    -   `bun patch-commit`
    -   Global cache
    -   Workspaces
    -   Lifecycle scripts
    -   Filter
    -   Lockfile
    -   Scopes and registries
    -   Overrides and resolutions
    -   `.npmrc`
-   Bundler
    
    -   `Bun.build`
    -   Loaders
    -   Plugins
    -   Macros
    -   vs esbuild
    -   Single-file executable
    -   CSS
    -   HTML
    -   Hot Module Replacement (HMR)
    -   Full-stack with HTML imports
-   Test runner
    
    -   `bun test`
    -   Writing tests
    -   Watch mode
    -   Lifecycle hooks
    -   Mocks
    -   Snapshots
    -   Dates and times
    -   DOM testing
    -   Code coverage
    -   Configuration
    -   Discovery
    -   Reporters
    -   Runtime Behavior
-   Package runner
    
    -   `bunx`
-   API
    
    -   HTTP server (`Bun.serve`)
    -   WebSockets
    -   Workers
    -   Binary data
    -   Streams
    -   File I/O (`Bun.file`)
    -   import.meta
    -   SQLite (`bun:sqlite`)
    -   PostgreSQL (`Bun.sql`)
    -   Redis (`Bun.redis`)
    -   S3 Client (`Bun.s3`)
    -   FileSystemRouter
    -   TCP sockets
    -   UDP sockets
    -   Globals
    -   $ Shell
    -   Child processes (spawn)
    -   Transpiler (`Bun.Transpiler`)
    -   Hashing
    -   Colors (`Bun.color`)
    -   Console
    -   FFI (`bun:ffi`)
    -   C Compiler (`bun:ffi` cc)
    -   HTMLRewriter
    -   Testing (`bun:test`)
    -   Cookies (`Bun.Cookie`)
    -   Utils
    -   Node-API
    -   Glob (`Bun.Glob`)
    -   Semver (`Bun.semver`)
    -   DNS
    -   fetch API extensions

Guides
------

-   Binary
    
    -   Convert a Blob to a string
    -   Convert a Buffer to a blob
    -   Convert a Blob to a DataView
    -   Convert a Buffer to a string
    -   Convert a Blob to a ReadableStream
    -   Convert a Blob to a Uint8Array
    -   Convert a DataView to a string
    -   Convert a Uint8Array to a Blob
    -   Convert a Blob to an ArrayBuffer
    -   Convert an ArrayBuffer to a Blob
    -   Convert a Buffer to a Uint8Array
    -   Convert a Uint8Array to a Buffer
    -   Convert a Uint8Array to a string
    -   Convert a Buffer to an ArrayBuffer
    -   Convert an ArrayBuffer to a Buffer
    -   Convert an ArrayBuffer to a string
    -   Convert a Uint8Array to a DataView
    -   Convert a Buffer to a ReadableStream
    -   Convert a Uint8Array to an ArrayBuffer
    -   Convert an ArrayBuffer to a Uint8Array
    -   Convert an ArrayBuffer to an array of numbers
    -   Convert a Uint8Array to a ReadableStream
-   Ecosystem
    
    -   Use React and JSX
    -   Use Gel with Bun
    -   Use Prisma with Bun
    -   Add Sentry to a Bun app
    -   Create a Discord bot
    -   Run Bun as a daemon with PM2
    -   Use Drizzle ORM with Bun
    -   Build an app with Nuxt and Bun
    -   Build an app with Qwik and Bun
    -   Build an app with Astro and Bun
    -   Build an app with Remix and Bun
    -   Build a frontend using Vite and Bun
    -   Build an app with Next.js and Bun
    -   Run Bun as a daemon with systemd
    -   Deploy a Bun application on Render
    -   Build an HTTP server using Hono and Bun
    -   Build an app with SvelteKit and Bun
    -   Build an app with SolidStart and Bun
    -   Build an HTTP server using Elysia and Bun
    -   Build an HTTP server using StricJS and Bun
    -   Containerize a Bun application with Docker
    -   Build an HTTP server using Express and Bun
    -   Use Neon Postgres through Drizzle ORM
    -   Server-side render (SSR) a React component
    -   Read and write data to MongoDB using Mongoose and Bun
    -   Use Neon's Serverless Postgres with Bun
-   HTMLRewriter
    
    -   Extract links from a webpage using HTMLRewriter
    -   Extract social share images and Open Graph tags
-   HTTP
    
    -   Hot reload an HTTP server
    -   Common HTTP server usage
    -   Write a simple HTTP server
    -   Configure TLS on an HTTP server
    -   Send an HTTP request using fetch
    -   Proxy HTTP requests using fetch()
    -   Start a cluster of HTTP servers
    -   Stream a file as an HTTP Response
    -   fetch with unix domain sockets in Bun
    -   Upload files via HTTP using FormData
    -   Streaming HTTP Server with Async Iterators
    -   Streaming HTTP Server with Node.js Streams
-   Install
    
    -   Add a dependency
    -   Add a Git dependency
    -   Add a peer dependency
    -   Add a trusted dependency
    -   Add a development dependency
    -   Add a tarball dependency
    -   Add an optional dependency
    -   Generate a yarn-compatible lockfile
    -   Configuring a monorepo using workspaces
    -   Install a package under a different name
    -   Install dependencies with Bun in GitHub Actions
    -   Using bun install with Artifactory
    -   Configure git to diff Bun's lockb lockfile
    -   Override the default npm registry for bun install
    -   Using bun install with an Azure Artifacts npm registry
    -   Migrate from npm install to bun install
    -   Configure a private registry for an organization scope with bun install
-   Process
    
    -   Read from stdin
    -   Listen for CTRL+C
    -   Spawn a child process
    -   Listen to OS signals
    -   Parse command-line arguments
    -   Read stderr from a child process
    -   Read stdout from a child process
    -   Get the process uptime in nanoseconds
    -   Spawn a child process and communicate using IPC
-   Read file
    
    -   Read a JSON file
    -   Check if a file exists
    -   Read a file as a string
    -   Read a file to a Buffer
    -   Get the MIME type of a file
    -   Watch a directory for changes
    -   Read a file as a ReadableStream
    -   Read a file to a Uint8Array
    -   Read a file to an ArrayBuffer
-   Runtime
    
    -   Delete files
    -   Run a Shell Command
    -   Import a JSON file
    -   Import a TOML file
    -   Set a time zone in Bun
    -   Set environment variables
    -   Re-map import paths
    -   Delete directories
    -   Read environment variables
    -   Import a HTML file as text
    -   Install and run Bun in GitHub Actions
    -   Debugging Bun with the web debugger
    -   Install TypeScript declarations for Bun
    -   Debugging Bun with the VS Code extension
    -   Inspect memory usage using V8 heap snapshots
    -   Define and replace static globals & constants
    -   Codesign a single-file JavaScript executable on macOS
-   Streams
    
    -   Convert a ReadableStream to JSON
    -   Convert a ReadableStream to a Blob
    -   Convert a ReadableStream to a Buffer
    -   Convert a ReadableStream to a string
    -   Convert a ReadableStream to a Uint8Array
    -   Convert a ReadableStream to an array of chunks
    -   Convert a Node.js Readable to JSON
    -   Convert a ReadableStream to an ArrayBuffer
    -   Convert a Node.js Readable to a Blob
    -   Convert a Node.js Readable to a string
    -   Convert a Node.js Readable to an Uint8Array
    -   Convert a Node.js Readable to an ArrayBuffer
-   Test
    
    -   Spy on methods in `bun test`
    -   Bail early with the Bun test runner
    -   Mock functions in `bun test`
    -   Run tests in watch mode with Bun
    -   Use snapshot testing in `bun test`
    -   Skip tests with the Bun test runner
    -   Using Testing Library with Bun
    -   Update snapshots in `bun test`
    -   Run your tests with the Bun test runner
    -   Set the system time in Bun's test runner
    -   Set a per-test timeout with the Bun test runner
    -   Migrate from Jest to Bun's test runner
    -   Write browser DOM tests with Bun and happy-dom
    -   Mark a test as a "todo" with the Bun test runner
    -   Re-run tests multiple times with the Bun test runner
    -   Generate code coverage reports with the Bun test runner
    -   import, require, and test Svelte components with bun test
    -   Set a code coverage threshold with the Bun test runner
-   Util
    
    -   Generate a UUID
    -   Hash a password
    -   Escape an HTML string
    -   Get the current Bun version
    -   Encode and decode base64 strings
    -   Compress and decompress data with gzip
    -   Sleep for a fixed number of milliseconds
    -   Detect when code is executed with Bun
    -   Check if two objects are deeply equal
    -   Compress and decompress data with DEFLATE
    -   Get the absolute path to the current entrypoint
    -   Get the directory of the current file
    -   Check if the current file is the entrypoint
    -   Get the file name of the current file
    -   Convert a file URL to an absolute path
    -   Convert an absolute path to a file URL
    -   Get the absolute path of the current file
    -   Get the path to an executable bin file
-   WebSocket
    
    -   Build a publish-subscribe WebSocket server
    -   Build a simple WebSocket server
    -   Enable compression for WebSocket messages
    -   Set per-socket contextual data on a WebSocket
-   Write file
    
    -   Delete a file
    -   Write to stdout
    -   Write a file to stdout
    -   Write a Blob to a file
    -   Write a string to a file
    -   Append content to a file
    -   Write a file incrementally
    -   Write a Response to a file
    -   Copy a file to another location
    -   Write a ReadableStream to a file

Contributing
------------

Refer to the Project > Contributing guide to start contributing to Bun.

License
-------

Refer to the Project > License page for information about Bun's licensing.
