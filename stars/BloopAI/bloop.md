---
project: bloop
stars: 9503
description: bloop is a fast code search engine written in Rust.
url: https://github.com/BloopAI/bloop
---

bloop is ChatGPT for your code. Ask questions in natural language, search for code and generate patches using your existing codebase as context.

Engineers are increasing their productivity by using bloop to:

-   Explain how files or features work in simple language
-   Write new features, using their code as context
-   Understand how to use poorly documented open source libraries
-   Pinpoint errors
-   Ask questions about English language codebases in other languages
-   Reduce code duplication by checking for existing functionality

video-search.mp4

Features
--------

-   AI-based conversational search
-   Code Studio, an LLM playground that uses your code as context
-   Blazing fast regex search
-   Sync your local and GitHub repositories
-   Sophisticated query filters so you can narrow down your results
-   Find functions, variables or traits with symbol search
-   Precise code navigation (go-to-reference and go-to-definition) for 10+ of the most popular languages built with Tree-sitter
-   Privacy focussed on-device embedding for semantic search

bloop stands on the shoulders of the Rust ecosystem. Our search indexes are powered by Tantivy and Qdrant, and our multi-platform app is built with Tauri.

video-studio.mp4

Get Started
-----------

The simplest way to get started with bloop is to download the app and follow the onboarding steps. Checkout our getting started guide and our references for conversational and regex search and Code Studio.

For instructions on how to build from source or run bloop from the command line, check out these pages:

-   Build bloop app from source
-   Run bloop from the command line

If you encounter any index issues you can wipe the bloop cache and reindex. Instructions on how to do this on different platforms are here.

Building From Source
--------------------

You can build bloop from source and run it with your own OpenAI API key. Clone the repo, make sure the `oss` branch is checked out, and create a file called `local_config.json` at the top-level of the repo. `local_config.json` should contain the following fields:

{
    "github\_access\_token": "<YOUR\_GITHUB\_ACCESS\_TOKEN>",
    "openai\_api\_key": "<YOUR\_OPENAI\_API\_KEY>"
}

Then follow these installation instructions. If built from source, bloop will not collect any telemetry.

Contributing
------------

We welcome contributions big and small! Before jumping in please read our contributors guide and our code of conduct.

Here's how to find your way around the repo:

-   `apps/desktop`: The Tauri app
-   `server/bleep`: The Rust backend which contains the core search and navigation logic
-   `client`: The React frontend

We use Git LFS for dependencies that are expensive to build.

To make sure you have everything you need to start building, you'll need to install the `git-lfs` package for your favourite operating system, then run the following commands in this repo:

```
git lfs install
git lfs pull
```

If you find a bug or have a feature request, open an issue! You can find the application logs here:

OS

Logs Path

MacOS

`~/Library/Application\ Support/ai.bloop.bloop/bleep/logs`

Windows

`%APPDATA%/bloop/bleep/logs`

Linux

`~/.local/share/bloop/bleep/logs`

Privacy
-------

We store as little data as possible. We use telemetry to helps us identify bugs and make data-driven product decisions. You can read our full privacy policy here.

License
-------

bloop is licensed under the `Apache 2.0` license as defined in LICENSE.
