---
project: jscpd
stars: 5834
description: Copy/paste detector for programming source code, supports 223 formats. AI-ready with token-efficient reporter, skill and MCP server.
url: https://github.com/kucherenko/jscpd
---

jscpd
=====

> Copy/paste detector for programming source code. Supports 224+ formats. AI-ready with MCP server and token-efficient reporter. Now with a Rust-powered engine — 24-37x faster.

jscpd implements the Rabin-Karp algorithm to find duplicated code blocks across files.

Quick Start
-----------

# Install (all platforms — installs the jscpd command)
curl -fsSL https://jscpd.dev/install.sh | bash

# TypeScript engine (Node.js, v4.x)
npm install -g jscpd@4
jscpd /path/to/code
# or use without installing
npx jscpd@4 /path/to/code

# Rust engine (v5.x, 24-37x faster) — installs the jscpd command
npm install -g jscpd@5
jscpd /path/to/code

# Rust engine — cpd command only
npm install -g cpd
cpd /path/to/code

# Rust-native install (exposes both jscpd and cpd)
cargo install jscpd

# Nix (installs both jscpd and cpd)
nix run github:kucherenko/jscpd -- /path/to/code
# or install permanently
nix profile install github:kucherenko/jscpd

# Homebrew (macOS/Linux)
brew install jscpd

Documentation
-------------

Document

Description

TypeScript (v4.x)

Node.js engine — CLI, reporters, config, detection modes

Rust (v5.x)

Rust engine — installation, CLI, reporters, blame, Rust API

AI-Ready

AI reporter, agent skills, MCP server

Programming API

TypeScript and Rust programmatic APIs

CI & Pre-Commit Hooks

GitHub Action, pre-commit hooks

Packages

Monorepo package and crate overview

Two Engines
-----------

TypeScript (v4)

Rust (v5)

**npm package**

`jscpd@4`

`jscpd@5` or `cpd`

**CLI command**

`jscpd`

`jscpd` (from `jscpd@5`) or `cpd` (from `cpd`)

**Speed**

Baseline

24-37x faster

**Formats**

224

223

**Node.js required**

Yes

No (self-contained binary)

**Programming API**

TypeScript (`jscpd()`, `detectClones()`)

Rust (`cpd-finder` crate)

**LevelDB store**

Yes

No

**Reporters**

13

13

`jscpd@5` installs the `jscpd` command. The `cpd` npm package installs the `cpd` command. Both contain the same Rust binary. For both command names from a single install, use crates.io: `cargo install jscpd`.

What's New
----------

### v5.0.x — Rust Engine

jscpd v5 is a ground-up Rust rewrite that ships as `jscpd@5` (installs the `jscpd` command) or `cpd` (installs the `cpd` command). Self-contained binary — no Node.js runtime required.

**Same interface, 24-37x faster:**

-   All CLI options from v4 are preserved — drop-in replacement: `jscpd` → `jscpd@5`
-   Same `.jscpd.json` config file, same detection algorithm, same reporters
-   223 language formats with cross-format detection (Vue SFC, Svelte, Astro, Markdown)

**New in v5:**

-   **24-37x faster** detection on real projects (see benchmark)
    -   Small codebases (548 files): 34x faster
    -   Medium codebases (9K files): 37x faster
    -   Large codebases (17K files, 900 MB): 24x faster
-   **Git blame** with side-by-side author comparison (`--blame --reporters console-full`)
-   **`--workers`** — control parallelism for file tokenization and detection (default: auto, uses all CPU cores; not available in v4)
-   **13 reporters**: `console`, `console-full`, `json`, `xml`, `csv`, `html`, `markdown`, `badge`, `sarif`, `ai`, `xcode`, `threshold`, `silent`
-   **AI reporter** — token-efficient output for LLM pipelines (~79% fewer tokens than console)
-   **Self-contained binary** — prebuilt for 6 platforms (macOS arm64/x64, Linux arm64/x64, Windows x64)

**Not yet in v5** (use v4 for these):

-   LevelDB/Redis stores (`--store leveldb`)
-   Node.js programming API (`jscpd()`, `detectClones()`)

See Rust docs for the full CLI reference and differences from v4.

### v4.2.x — TypeScript Engine

-   **Custom tokenizer backend** — replaced `prismjs` with own backend built on reprism. ~11.5% faster tokenization on real projects
-   **Cross-format detection** — Vue SFC, Svelte, Astro, and Markdown tokenized per-block, enabling detection across file types
-   **New formats**: Apex, CFML/ColdFusion, GDScript, and 70+ additional formats (224 total, up from 152)
-   **Shebang detection** — auto-detect language for extensionless scripts
-   **`--store-path`** — configure LevelDB cache directory for parallel runs
-   **`--skipComments`** — shorthand for `--mode weak`
-   **`--formats-names`** — map filenames (e.g. `Makefile`, `Dockerfile`) to formats
-   **`--noTips`** — suppress tip output in CI
-   **Bug fixes**: entire-file duplicates silently dropped (#728), ReDoS on Lisp/Elisp files (#737), process crash on malformed `package.json` (#739), Vue SFC cross-file detection (#737), Vue SFC column numbers (#737), 50 dependency security vulnerabilities

See TypeScript docs for the full CLI reference.

Packages
--------

Package

Description

jscpd

CLI and Node.js API (v4.x)

jscpd-server

REST API + MCP server

@jscpd/core

Core detection algorithm

@jscpd/finder

File detection, reporters

@jscpd/tokenizer

Source code tokenization

@jscpd/html-reporter

HTML report

@jscpd/badge-reporter

SVG badge

jscpd-sarif-reporter

SARIF (GitHub Code Scanning)

@jscpd/leveldb-store

LevelDB persistent store

@jscpd/redis-store

Redis distributed store

cpd (Rust engine)

Rust-powered engine (v5.x) — also available as `jscpd@5`

Who Uses jscpd
--------------

-   GitHub Super Linter — official GitHub linter aggregator, bundles jscpd as its copy/paste detector
-   Codacy — automated code analysis platform, jscpd powers the duplication engine
-   MegaLinter — 100% open-source linter aggregator for CI, integrates jscpd
-   OpenClaw — personal AI assistant for self-hosted devices
-   Natural — NLP library for Node.js, uses jscpd for code quality

Performance
-----------

Benchmarked on macOS (Apple Silicon), 10 runs per target (3 for CopilotKit). v4 ran with `--no-gitignore -i "node_modules"` to ensure comparable file scanning.

Target

Files

Size

jscpd v4

jscpd v5

Speedup

fixtures

548

1.5 MB

1.03s

0.03s

**34.3x**

svelte

9K

38 MB

15.80s

0.43s

**36.9x**

CopilotKit

17K

159 MB

82.89s

3.44s

**24.1x**

See performance-comparison.md for full methodology and raw data.

AI-Ready Features
-----------------

jscpd integrates into AI-powered workflows through three mechanisms:

### AI Reporter

Token-efficient output for LLM pipelines (~79% fewer tokens than the default console reporter):

jscpd --reporters ai /path/to/source   # v4
cpd --reporters ai /path/to/source      # v5

### Agent Skills

Two installable skills that teach AI coding assistants how to use jscpd and refactor detected duplications:

Skill

Purpose

Install

`jscpd`

Tool reference — CLI options, AI reporter format, config syntax

`npx skills add kucherenko/jscpd --skill jscpd`

`dry-refactoring`

Guided refactoring workflow — read clones, choose strategy, apply, verify

`npx skills add kucherenko/jscpd --skill dry-refactoring`

After installation, ask your agent to "find and fix code duplication" and it will invoke jscpd with the right options and act on the results.

See AI-Ready docs for full details.

Contributing
------------

1.  Fork the repo kucherenko/jscpd
2.  Clone forked version (`git clone https://github.com/{your-id}/jscpd`)
3.  Install dependencies (`pnpm install`)
4.  Run in dev mode: `pnpm dev`
5.  Add your changes
6.  Add tests and check: `pnpm test`
7.  Build: `pnpm build`
8.  Create PR

Backers
-------

Thank you to all our backers! 🙏 \[Become a backer\]

Sponsors
--------

Support this project by becoming a sponsor. Your logo will show up here with a link to your website. \[Become a sponsor\]

License
-------

MIT © Andrey Kucherenko
