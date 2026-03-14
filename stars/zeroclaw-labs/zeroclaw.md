---
project: zeroclaw
stars: 27048
description: Fast, small, and fully autonomous AI assistant infrastructure — deploy anywhere, swap anything 🦀
url: https://github.com/zeroclaw-labs/zeroclaw
---

ZeroClaw 🦀
===========

**Zero overhead. Zero compromise. 100% Rust. 100% Agnostic.**  
⚡️ **Runs on $10 hardware with <5MB RAM: That's 99% less memory than OpenClaw and 98% cheaper than a Mac mini!**

Built by students and members of the Harvard, MIT, and Sundai.Club communities.

🌐 **Languages:** 🇺🇸 English · 🇨🇳 简体中文 · 🇯🇵 日本語 · 🇰🇷 한국어 · 🇻🇳 Tiếng Việt · 🇵🇭 Tagalog · 🇪🇸 Español · 🇧🇷 Português · 🇮🇹 Italiano · 🇩🇪 Deutsch · 🇫🇷 Français · 🇸🇦 العربية · 🇮🇳 हिन्दी · 🇷🇺 Русский · 🇧🇩 বাংলা · 🇮🇱 עברית · 🇵🇱 Polski · 🇨🇿 Čeština · 🇳🇱 Nederlands · 🇹🇷 Türkçe · 🇺🇦 Українська · 🇮🇩 Bahasa Indonesia · 🇹🇭 ไทย · 🇵🇰 اردو · 🇷🇴 Română · 🇸🇪 Svenska · 🇬🇷 Ελληνικά · 🇭🇺 Magyar · 🇫🇮 Suomi · 🇩🇰 Dansk · 🇳🇴 Norsk

Getting Started | One-Click Setup | Docs Hub | Docs TOC

**Quick Routes:** Reference · Operations · Troubleshoot · Security · Hardware · Contribute

**Fast, small, and fully autonomous AI assistant infrastructure**  
Deploy anywhere. Swap anything.

ZeroClaw is the **runtime operating system** for agentic workflows — infrastructure that abstracts models, tools, memory, and execution so agents can be built once and run anywhere.

`Trait-driven architecture · secure-by-default runtime · provider/channel/tool swappable · pluggable everything`

### 🚀 What's New in v0.3.0-beta.196 (March 2026)

Area

Highlights

General

Incremental improvements and polish

### 📢 Announcements

Use this board for important notices (breaking changes, security advisories, maintenance windows, and release blockers).

Date (UTC)

Level

Notice

Action

2026-02-19

_Critical_

We are **not affiliated** with `openagen/zeroclaw`, `zeroclaw.org` or `zeroclaw.net`. The `zeroclaw.org` and `zeroclaw.net` domains currently points to the `openagen/zeroclaw` fork, and that domain/repository are impersonating our official website/project.

Do not trust information, binaries, fundraising, or announcements from those sources. Use only this repository and our verified social accounts.

2026-02-21

_Important_

Our official website is now live: zeroclawlabs.ai. Thanks for your patience while we prepared the launch. We are still seeing impersonation attempts, so do **not** join any investment or fundraising activity claiming the ZeroClaw name unless it is published through our official channels.

Use this repository as the single source of truth. Follow X (@zeroclawlabs), Facebook (Group), and Reddit (r/zeroclawlabs) for official updates.

2026-02-19

_Important_

Anthropic updated the Authentication and Credential Use terms on 2026-02-19. Claude Code OAuth tokens (Free, Pro, Max) are intended exclusively for Claude Code and Claude.ai; using OAuth tokens from Claude Free/Pro/Max in any other product, tool, or service (including Agent SDK) is not permitted and may violate the Consumer Terms of Service.

Please temporarily avoid Claude Code OAuth integrations to prevent potential loss. Original clause: Authentication and Credential Use.

### ✨ Features

-   🏎️ **Lean Runtime by Default:** Common CLI and status workflows run in a few-megabyte memory envelope on release builds.
-   💰 **Cost-Efficient Deployment:** Designed for low-cost boards and small cloud instances without heavyweight runtime dependencies.
-   ⚡ **Fast Cold Starts:** Single-binary Rust runtime keeps command and daemon startup near-instant for daily operations.
-   🌍 **Portable Architecture:** One binary-first workflow across ARM, x86, and RISC-V with swappable providers/channels/tools.

### Why teams pick ZeroClaw

-   **Lean by default:** small Rust binary, fast startup, low memory footprint.
-   **Secure by design:** pairing, strict sandboxing, explicit allowlists, workspace scoping.
-   **Fully swappable:** core systems are traits (providers, channels, tools, memory, tunnels).
-   **No lock-in:** OpenAI-compatible provider support + pluggable custom endpoints.

Benchmark Snapshot (ZeroClaw vs OpenClaw, Reproducible)
-------------------------------------------------------

Local machine quick benchmark (macOS arm64, Feb 2026) normalized for 0.8GHz edge hardware.

OpenClaw

NanoBot

PicoClaw

ZeroClaw 🦀

**Language**

TypeScript

Python

Go

**Rust**

**RAM**

\> 1GB

\> 100MB

< 10MB

**< 5MB**

**Startup (0.8GHz core)**

\> 500s

\> 30s

< 1s

**< 10ms**

**Binary Size**

~28MB (dist)

N/A (Scripts)

~8MB

**~8.8 MB**

**Cost**

Mac Mini $599

Linux SBC ~$50

Linux Board $10

**Any hardware $10**

> Notes: ZeroClaw results are measured on release builds using `/usr/bin/time -l`. OpenClaw requires Node.js runtime (typically ~390MB additional memory overhead), while NanoBot requires Python runtime. PicoClaw and ZeroClaw are static binaries. The RAM figures above are runtime memory; build-time compilation requirements are higher.

### Reproducible local measurement

Benchmark claims can drift as code and toolchains evolve, so always measure your current build locally:

cargo build --release
ls -lh target/release/zeroclaw

/usr/bin/time -l target/release/zeroclaw --help
/usr/bin/time -l target/release/zeroclaw status

Example sample (macOS arm64, measured on February 18, 2026):

-   Release binary size: `8.8MB`
-   `zeroclaw --help`: about `0.02s` real time, ~`3.9MB` peak memory footprint
-   `zeroclaw status`: about `0.01s` real time, ~`4.1MB` peak memory footprint

Prerequisites
-------------

**Windows**

#### Required

1.  **Visual Studio Build Tools** (provides the MSVC linker and Windows SDK):
    
    winget install Microsoft.VisualStudio.2022.BuildTools
    
    During installation (or via the Visual Studio Installer), select the **"Desktop development with C++"** workload.
    
2.  **Rust toolchain:**
    
    winget install Rustlang.Rustup
    
    After installation, open a new terminal and run `rustup default stable` to ensure the stable toolchain is active.
    
3.  **Verify** both are working:
    
    rustc \--version
    cargo \--version
    

#### Optional

-   **Docker Desktop** — required only if using the Docker sandboxed runtime (`runtime.kind = "docker"`). Install via `winget install Docker.DockerDesktop`.

**Linux / macOS**

#### Required

1.  **Build essentials:**
    
    -   **Linux (Debian/Ubuntu):** `sudo apt install build-essential pkg-config`
    -   **Linux (Fedora/RHEL):** `sudo dnf group install development-tools && sudo dnf install pkg-config`
    -   **macOS:** Install Xcode Command Line Tools: `xcode-select --install`
2.  **Rust toolchain:**
    
    curl --proto '\=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    
    See rustup.rs for details.
    
3.  **Verify** both are working:
    
    rustc --version
    cargo --version
    

#### One-Line Installer

Or skip the steps above and install everything (system deps, Rust, ZeroClaw) in a single command:

curl -LsSf https://raw.githubusercontent.com/zeroclaw-labs/zeroclaw/master/install.sh | bash

#### Compilation resource requirements

Building from source needs more resources than running the resulting binary:

Resource

Minimum

Recommended

**RAM + swap**

2 GB

4 GB+

**Free disk**

6 GB

10 GB+

If your host is below the minimum, use pre-built binaries:

./install.sh --prefer-prebuilt

To require binary-only install with no source fallback:

./install.sh --prebuilt-only

#### Optional

-   **Docker** — required only if using the Docker sandboxed runtime (`runtime.kind = "docker"`). Install via your package manager or docker.com.

> **Note:** The default `cargo build --release` uses `codegen-units=1` to lower peak compile pressure. For faster builds on powerful machines, use `cargo build --profile release-fast`.

Quick Start
-----------

### Homebrew (macOS/Linuxbrew)

brew install zeroclaw

### One-click bootstrap

# Recommended: clone then run local bootstrap script
git clone https://github.com/zeroclaw-labs/zeroclaw.git
cd zeroclaw
./install.sh

# Optional: bootstrap dependencies + Rust on fresh machines
./install.sh --install-system-deps --install-rust

# Optional: pre-built binary first (recommended on low-RAM/low-disk hosts)
./install.sh --prefer-prebuilt

# Optional: binary-only install (no source build fallback)
./install.sh --prebuilt-only

# Optional: run onboarding in the same flow
./install.sh --api-key "sk-..." --provider openrouter \[--model "openrouter/auto"\]

# Optional: run bootstrap + onboarding fully in Docker-compatible mode
./install.sh --docker

# Optional: force Podman as container CLI
ZEROCLAW\_CONTAINER\_CLI=podman ./install.sh --docker

# Optional: in --docker mode, skip local image build and use local tag or pull fallback image
./install.sh --docker --skip-build

Remote one-liner (review first in security-sensitive environments):

curl -fsSL https://raw.githubusercontent.com/zeroclaw-labs/zeroclaw/master/install.sh | bash

Details: `docs/setup-guides/one-click-bootstrap.md` (toolchain mode may request `sudo` for system packages).

### Pre-built binaries

Release assets are published for:

-   Linux: `x86_64`, `aarch64`, `armv7`
-   macOS: `x86_64`, `aarch64`
-   Windows: `x86_64`

Download the latest assets from: https://github.com/zeroclaw-labs/zeroclaw/releases/latest

Example (ARM64 Linux):

curl -fsSLO https://github.com/zeroclaw-labs/zeroclaw/releases/latest/download/zeroclaw-aarch64-unknown-linux-gnu.tar.gz
tar xzf zeroclaw-aarch64-unknown-linux-gnu.tar.gz
install -m 0755 zeroclaw "$HOME/.cargo/bin/zeroclaw"

git clone https://github.com/zeroclaw-labs/zeroclaw.git
cd zeroclaw
cargo build --release --locked
cargo install --path . --force --locked

# Ensure ~/.cargo/bin is in your PATH
export PATH="$HOME/.cargo/bin:$PATH"

# Quick setup (no prompts, optional model specification)
zeroclaw onboard --api-key sk-... --provider openrouter \[--model "openrouter/auto"\]

# Or guided wizard
zeroclaw onboard

# If config.toml already exists and you intentionally want to overwrite it
zeroclaw onboard --force

# Or quickly repair channels/allowlists only
zeroclaw onboard --channels-only

# Chat
zeroclaw agent -m "Hello, ZeroClaw!"

# Interactive mode
zeroclaw agent

# Start the gateway (webhook server)
zeroclaw gateway                # default: 127.0.0.1:42617
zeroclaw gateway --port 0       # random port (security hardened)

# Start full autonomous runtime
zeroclaw daemon

# Check status
zeroclaw status
zeroclaw auth status

# Generate shell completions (stdout only, safe to source directly)
source <(zeroclaw completions bash)
zeroclaw completions zsh \> ~/.zfunc/\_zeroclaw

# Run system diagnostics
zeroclaw doctor

# Check channel health
zeroclaw channel doctor

# Bind a Telegram identity into allowlist
zeroclaw channel bind-telegram 123456789

# Get integration setup details
zeroclaw integrations info Telegram

# Note: Channels (Telegram, Discord, Slack) require daemon to be running
# zeroclaw daemon

# Manage background service
zeroclaw service install
zeroclaw service status
zeroclaw service restart

# On Alpine (OpenRC): sudo zeroclaw service install

# Migrate memory from OpenClaw (safe preview first)
zeroclaw migrate openclaw --dry-run
zeroclaw migrate openclaw

> **Dev fallback (no global install):** prefix commands with `cargo run --release --` (example: `cargo run --release -- status`).

Subscription Auth (OpenAI Codex / Claude Code)
----------------------------------------------

ZeroClaw now supports subscription-native auth profiles (multi-account, encrypted at rest).

-   Store file: `~/.zeroclaw/auth-profiles.json`
-   Encryption key: `~/.zeroclaw/.secret_key`
-   Profile id format: `<provider>:<profile_name>` (example: `openai-codex:work`)

OpenAI Codex OAuth (ChatGPT subscription):

# Recommended on servers/headless
zeroclaw auth login --provider openai-codex --device-code

# Browser/callback flow with paste fallback
zeroclaw auth login --provider openai-codex --profile default
zeroclaw auth paste-redirect --provider openai-codex --profile default

# Check / refresh / switch profile
zeroclaw auth status
zeroclaw auth refresh --provider openai-codex --profile default
zeroclaw auth use --provider openai-codex --profile work

Claude Code / Anthropic setup-token:

# Paste subscription/setup token (Authorization header mode)
zeroclaw auth paste-token --provider anthropic --profile default --auth-kind authorization

# Alias command
zeroclaw auth setup-token --provider anthropic --profile default

Run the agent with subscription auth:

zeroclaw agent --provider openai-codex -m "hello"
zeroclaw agent --provider openai-codex --auth-profile openai-codex:work -m "hello"

# Anthropic supports both API key and auth token env vars:
# ANTHROPIC\_AUTH\_TOKEN, ANTHROPIC\_OAUTH\_TOKEN, ANTHROPIC\_API\_KEY
zeroclaw agent --provider anthropic -m "hello"

Collaboration & Docs
--------------------

Start from the docs hub for a task-oriented map:

-   Documentation hub: `docs/README.md`
-   Unified docs TOC: `docs/SUMMARY.md`
-   Commands reference: `docs/reference/cli/commands-reference.md`
-   Config reference: `docs/reference/api/config-reference.md`
-   Providers reference: `docs/reference/api/providers-reference.md`
-   Channels reference: `docs/reference/api/channels-reference.md`
-   Operations runbook: `docs/ops/operations-runbook.md`
-   Troubleshooting: `docs/ops/troubleshooting.md`
-   Docs inventory/classification: `docs/maintainers/docs-inventory.md`
-   PR/Issue triage snapshot (as of February 18, 2026): `docs/maintainers/project-triage-snapshot-2026-02-18.md`

Core collaboration references:

-   Documentation hub: docs/README.md
-   Documentation template: docs/contributing/doc-template.md
-   Documentation change checklist: docs/README.md#4-documentation-change-checklist
-   Channel configuration reference: docs/reference/api/channels-reference.md
-   Matrix encrypted-room operations: docs/security/matrix-e2ee-guide.md
-   Contribution guide: CONTRIBUTING.md
-   PR workflow policy: docs/contributing/pr-workflow.md
-   Reviewer playbook (triage + deep review): docs/contributing/reviewer-playbook.md
-   Security disclosure policy: SECURITY.md

For deployment and runtime operations:

-   Network deployment guide: docs/ops/network-deployment.md
-   Proxy agent playbook: docs/ops/proxy-agent-playbook.md

Support ZeroClaw
----------------

If ZeroClaw helps your work and you want to support ongoing development, you can donate here:

### 🙏 Special Thanks

A heartfelt thank you to the communities and institutions that inspire and fuel this open-source work:

-   **Harvard University** — for fostering intellectual curiosity and pushing the boundaries of what's possible.
-   **MIT** — for championing open knowledge, open source, and the belief that technology should be accessible to everyone.
-   **Sundai Club** — for the community, the energy, and the relentless drive to build things that matter.
-   **The World & Beyond** 🌍✨ — to every contributor, dreamer, and builder out there making open source a force for good. This is for you.

We're building in the open because the best ideas come from everywhere. If you're reading this, you're part of it. Welcome. 🦀❤️

### 🌟 Recent Contributors (v0.3.0-beta.196)

0 0 contributors shipped features, fixes, and improvements in this release cycle:

Thank you to everyone who opened issues, reviewed PRs, translated docs, and helped test. Every contribution matters. 🦀

⚠️ Official Repository & Impersonation Warning
----------------------------------------------

**This is the only official ZeroClaw repository:**

> https://github.com/zeroclaw-labs/zeroclaw

Any other repository, organization, domain, or package claiming to be "ZeroClaw" or implying affiliation with ZeroClaw Labs is **unauthorized and not affiliated with this project**. Known unauthorized forks will be listed in TRADEMARK.md.

If you encounter impersonation or trademark misuse, please open an issue.

* * *

License
-------

ZeroClaw is dual-licensed for maximum openness and contributor protection:

License

Use case

MIT

Open-source, research, academic, personal use

Apache 2.0

Patent protection, institutional, commercial deployment

You may choose either license. **Contributors automatically grant rights under both** — see CLA.md for the full contributor agreement.

### Trademark

The **ZeroClaw** name and logo are trademarks of ZeroClaw Labs. This license does not grant permission to use them to imply endorsement or affiliation. See TRADEMARK.md for permitted and prohibited uses.

### Contributor Protections

-   You **retain copyright** of your contributions
-   **Patent grant** (Apache 2.0) shields you from patent claims by other contributors
-   Your contributions are **permanently attributed** in commit history and NOTICE
-   No trademark rights are transferred by contributing

Contributing
------------

New to ZeroClaw? Look for issues labeled `good first issue` — see our Contributing Guide for how to get started.

See CONTRIBUTING.md and CLA.md. Implement a trait, submit a PR:

-   CI workflow guide: docs/contributing/ci-map.md
-   New `Provider` → `src/providers/`
-   New `Channel` → `src/channels/`
-   New `Observer` → `src/observability/`
-   New `Tool` → `src/tools/`
-   New `Memory` → `src/memory/`
-   New `Tunnel` → `src/tunnel/`
-   New `Skill` → `~/.zeroclaw/workspace/skills/<name>/`

* * *

**ZeroClaw** — Zero overhead. Zero compromise. Deploy anywhere. Swap anything. 🦀

Contributors
------------

Star History
------------
