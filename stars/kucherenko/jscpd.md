---
project: jscpd
stars: 6147
description: Copy/paste detector for source code. 220+ languages, Rust engine, SARIF/HTML/badge reporters, GitHub Action, MCP server for AI agents.
url: https://github.com/kucherenko/jscpd
---

jscpd
=====

> Copy/paste detector for programming source code. 220+ formats, Rust engine, self-contained binary, AI-ready with MCP server and token-efficient reporter.

**Documentation:** https://jscpd.dev

jscpd implements the Rabin-Karp algorithm to find duplicated code blocks across files.

Quick Start
-----------

# macOS / Linux
curl -fsSL https://jscpd.dev/install.sh | bash

# Windows (PowerShell)
irm https://jscpd.dev/install.ps1 | iex

# No install — run once with npx (Node.js)
npx jscpd .

Then scan a project:

jscpd /path/to/code

### Other install methods

Method

Command

Notes

npm

`npm install -g jscpd`

Installs the `jscpd` command; prebuilt binary, no Node.js at runtime

npm (`cpd` command)

`npm install -g cpd`

Same binary, exposed as `cpd`

Cargo

`cargo install jscpd`

Builds from crates.io; installs both `jscpd` and `cpd`

Homebrew

`brew install jscpd`

macOS / Linux

Nix

`nix run github:kucherenko/jscpd -- /path/to/code`

Or `nix profile install github:kucherenko/jscpd`

Docker

`docker run --rm -v "$PWD:/src" ghcr.io/kucherenko/jscpd .`

Multi-arch image built from the release binaries

### GitHub Action

\- uses: kucherenko/jscpd@v5
  with:
    threshold: 5

Uploads SARIF results to GitHub Code Scanning by default. See CI & Pre-Commit Hooks for all inputs and outputs.

Documentation
-------------

Document

Description

Rust engine

Installation, CLI reference, reporters, baseline, summary, blame, config file

AI-Ready

AI reporter, agent skills, MCP server

Programming API

Rust API (`cpd-finder` crate)

CI & Pre-Commit Hooks

GitHub Action, Docker image, pre-commit hooks

Packages

npm packages and crates that make up a release

Supported formats

All 224 formats with their file extensions

Features
--------

jscpd v5 is a Rust engine that ships as a self-contained binary — no runtime required — under two npm names (`jscpd` installs the `jscpd` command, `cpd` installs `cpd`), on crates.io, Homebrew, Nix, Docker, and as a GitHub Action.

-   **224 language formats** with cross-format detection (Vue SFC, Svelte, Astro, Markdown) and `--cross-formats` groups to match clones across JavaScript and TypeScript
-   **Prebuilt for 8 platforms** — macOS arm64/x64, Linux arm64/x64 (glibc and musl), Windows arm64/x64
-   **15 reporters**: `console`, `console-full`, `json`, `xml`, `csv`, `html`, `markdown`, `badge`, `sarif`, `codeclimate`, `openmetrics`, `ai`, `xcode`, `threshold`, `silent`
-   **Clone baseline** — gate CI on _new_ duplication only. `--baseline .jscpd-baseline.json` with `--fail-on-new-clones[=N]` tolerates legacy clones and fails the build on regressions; `--baseline-from-ref origin/main` does the same without a committed file (see docs)
-   **GitLab-ready reporters** — `codeclimate` (`gl-code-quality-report.json`) and `openmetrics` (`jscpd-metrics.txt`) plug into `artifacts:reports`
-   **Git blame** with side-by-side author comparison (`--blame --reporters console-full`)
-   **`--summary`** — codebase summary: top files and folders by tokens, lines, size, and a complexity estimate — refactoring hotspots straight from the scan (see docs)
-   **`--mcp`** — built-in MCP server over stdio: point your AI assistant at the binary and it can check snippets for duplication against your codebase (see docs)
-   **AI reporter** — token-efficient output for LLM pipelines (~79% fewer tokens than console)
-   **`--skip-isolated`** — ignore duplication between monorepo folders owned by different teams
-   **`--workers`** — control parallelism for file tokenization and detection (default: all CPU cores)
-   **Config discovery** — `.jscpd.json`, `.config/jscpd.json`, or the `jscpd` key in `package.json`

See the Rust docs for the full CLI reference and `rust/CHANGELOG.md` for release notes.

### Looking for v4?

jscpd v4 (TypeScript engine, Node.js API, LevelDB/Redis stores) is maintained on the `master-v4` branch and published as `jscpd@4` / the `latest-4` dist-tag. README-v4.md describes it in one page (install, CLI, API, packages, maintenance policy); the same content is at https://jscpd.dev/getting-started/v4.

Packages
--------

Package

Registry

Description

jscpd

npm

Installs the `jscpd` command (prebuilt binary via platform packages)

cpd

npm

Installs the `cpd` command (same binary)

jscpd-<platform>

npm

Platform binary packages pulled in as optional dependencies: `jscpd-darwin-arm64`, `jscpd-darwin-x64`, `jscpd-linux-x64-gnu`, `jscpd-linux-arm64-gnu`, `jscpd-linux-x64-musl`, `jscpd-linux-arm64-musl`, `jscpd-windows-x64-msvc`, `jscpd-windows-arm64-msvc`

jscpd

crates.io

CLI crate; installs both `jscpd` and `cpd` binaries

cpd-core

crates.io

Detection algorithm (Rabin-Karp rolling hash), data models

cpd-tokenizer

crates.io

Source code tokenization (224 formats)

cpd-finder

crates.io

File walking, orchestration, git blame — the library entry point

cpd-reporter

crates.io

Output formatting (15 reporters)

Who Uses jscpd
--------------

The `jscpd` npm package is downloaded **10M+ times per month**, and ~5,000 repositories declare it on GitHub's dependents graph.

**Bundled by analysis platforms:**

-   GitHub Super Linter — official GitHub linter aggregator, bundles jscpd as its copy/paste detector and runs it by default; 15,500+ workflow files on GitHub reference Super Linter (as of Sep 2026)
-   MegaLinter — open-source linter aggregator for CI, ships jscpd in every flavor including `ci_light`
-   Codacy — automated code analysis platform, jscpd powers the duplication engine

**Explicitly enabled in Super Linter** (`VALIDATE_JSCPD: true`) **by dozens of public repositories, including:**

-   A2A — Google's Agent2Agent protocol (25k+ stars)
-   RimSort — mod manager for RimWorld (1.2k+ stars); also runs jscpd directly with its own `.jscpd.json`
-   Contact Center AI samples — official Google Cloud samples, with a dedicated jscpd config
-   Drifty — open-source download manager

**Used in notable projects:**

-   OpenClaw — personal AI assistant, runs jscpd as a duplication gate in its check scripts
-   DeepSeek Harness — DeepSeek's plugin harness, jscpd config in CI
-   degit — Rich Harris's project scaffolder
-   MEGA webclient — the MEGA.nz web client
-   Microsoft TypeAgent
-   Salesforce DX VS Code
-   Alibaba AppWorks — embeds jscpd as a library
-   OVHcloud manager — OVHcloud's customer control panel
-   KiroCrew — self-improving persistent development workspace

Benchmark
---------

Compared against other copy/paste detectors on the `fixtures/` corpus (547 files, 150+ formats), default thresholds, wall-clock time on Apple Silicon:

Tool

Time

Files

Clones

Dup Lines

jscpd

84ms

347

212

9,133

jscpd-rs

111ms

360

222

10,317

Duplo

162ms

319

518

13,049

Fallow dupes

164ms

34

10

3,137

Simian

964ms

547

424

15,351

PMD CPD

35.980s

71

56

2,267

Methodology, cross-format detection and AI-token-efficiency comparisons: benchmark/BENCHMARK.md. Re-run with `benchmark/benchmark.sh`.

AI-Ready Features
-----------------

jscpd integrates into AI-powered workflows through three mechanisms:

### AI Reporter

Token-efficient output for LLM pipelines (~79% fewer tokens than the default console reporter):

jscpd --reporters ai /path/to/source              # compact clone list
jscpd --reporters ai --summary /path/to/source    # + compact codebase summary

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

### MCP Server

`jscpd --mcp /path/to/project` scans once and serves the Model Context Protocol over stdio, so an assistant can check any snippet for duplication against the codebase on demand.

See AI-Ready docs for full details.

Contributing
------------

See CONTRIBUTING.md for the development setup, test policy, and pull request requirements. In short:

cd rust
cargo nextest run --workspace
cargo clippy --workspace --all-targets -- -D warnings
cargo fmt --all --check

Security issues go through the security policy, not public issues.

Backers
-------

Thank you to all our backers! 🙏 \[Become a backer\]

Sponsors
--------

Support this project by becoming a sponsor. Your logo will show up here with a link to your website. \[Become a sponsor\]

License
-------

MIT © Andrey Kucherenko
