---
project: zeroclaw
stars: 29054
description: Fast, small, and fully autonomous AI personal assistant infrastructure, ANY OS, ANY PLATFORM — deploy anywhere, swap anything 🦀
url: https://github.com/zeroclaw-labs/zeroclaw
---

🦀 ZeroClaw — Personal AI Assistant
===================================

**Zero overhead. Zero compromise. 100% Rust. 100% Agnostic.**  
⚡️ **Runs on $10 hardware with <5MB RAM: That's 99% less memory than OpenClaw and 98% cheaper than a Mac mini!**

Built by students and members of the Harvard, MIT, and Sundai.Club communities.

🌐 **Languages:** 🇺🇸 English · 🇨🇳 简体中文 · 🇯🇵 日本語 · 🇰🇷 한국어 · 🇻🇳 Tiếng Việt · 🇵🇭 Tagalog · 🇪🇸 Español · 🇧🇷 Português · 🇮🇹 Italiano · 🇩🇪 Deutsch · 🇫🇷 Français · 🇸🇦 العربية · 🇮🇳 हिन्दी · 🇷🇺 Русский · 🇧🇩 বাংলা · 🇮🇱 עברית · 🇵🇱 Polski · 🇨🇿 Čeština · 🇳🇱 Nederlands · 🇹🇷 Türkçe · 🇺🇦 Українська · 🇮🇩 Bahasa Indonesia · 🇹🇭 ไทย · 🇵🇰 اردو · 🇷🇴 Română · 🇸🇪 Svenska · 🇬🇷 Ελληνικά · 🇭🇺 Magyar · 🇫🇮 Suomi · 🇩🇰 Dansk · 🇳🇴 Norsk

ZeroClaw is a personal AI assistant you run on your own devices. It answers you on the channels you already use (WhatsApp, Telegram, Slack, Discord, Signal, iMessage, Matrix, IRC, Email, Bluesky, Nostr, Mattermost, Nextcloud Talk, DingTalk, Lark, QQ, Reddit, LinkedIn, Twitter, MQTT, WeChat Work, and more). It has a web dashboard for real-time control and can connect to hardware peripherals (ESP32, STM32, Arduino, Raspberry Pi). The Gateway is just the control plane — the product is the assistant.

If you want a personal, single-user assistant that feels local, fast, and always-on, this is it.

Website · Docs · Architecture · Getting Started · Migrating from OpenClaw · Troubleshoot · Discord

> **Preferred setup:** run `zeroclaw onboard` in your terminal. ZeroClaw Onboard guides you step by step through setting up the gateway, workspace, channels, and provider. It is the recommended setup path and works on macOS, Linux, and Windows (via WSL2). New install? Start here: Getting started

### Subscription Auth (OAuth)

-   **OpenAI Codex** (ChatGPT subscription)
-   **Gemini** (Google OAuth)
-   **Anthropic** (API key or auth token)

Model note: while many providers/models are supported, for the best experience use the strongest latest-generation model available to you. See Onboarding.

Models config + CLI: Providers reference Auth profile rotation (OAuth vs API keys) + failover: Model failover

Install (recommended)
---------------------

Runtime: Rust stable toolchain. Single binary, no runtime dependencies.

### Homebrew (macOS/Linuxbrew)

brew install zeroclaw

### One-click bootstrap

git clone https://github.com/zeroclaw-labs/zeroclaw.git
cd zeroclaw
./install.sh

`zeroclaw onboard` runs automatically after install to configure your workspace and provider.

Quick start (TL;DR)
-------------------

Full beginner guide (auth, pairing, channels): Getting started

# Install + onboard
./install.sh --api-key "sk-..." --provider openrouter

# Start the gateway (webhook server + web dashboard)
zeroclaw gateway                # default: 127.0.0.1:42617
zeroclaw gateway --port 0       # random port (security hardened)

# Talk to the assistant
zeroclaw agent -m "Hello, ZeroClaw!"

# Interactive mode
zeroclaw agent

# Start full autonomous runtime (gateway + channels + cron + hands)
zeroclaw daemon

# Check status
zeroclaw status

# Run diagnostics
zeroclaw doctor

Upgrading? Run `zeroclaw doctor` after updating.

### From source (development)

git clone https://github.com/zeroclaw-labs/zeroclaw.git
cd zeroclaw

cargo build --release --locked
cargo install --path . --force --locked

zeroclaw onboard

> **Dev fallback (no global install):** prefix commands with `cargo run --release --` (example: `cargo run --release -- status`).

Migrating from OpenClaw
-----------------------

ZeroClaw can import your OpenClaw workspace, memory, and configuration:

# Preview what will be migrated (safe, read-only)
zeroclaw migrate openclaw --dry-run

# Run the migration
zeroclaw migrate openclaw

This migrates your memory entries, workspace files, and configuration from `~/.openclaw/` to `~/.zeroclaw/`. Config is converted from JSON to TOML automatically.

Security defaults (DM access)
-----------------------------

ZeroClaw connects to real messaging surfaces. Treat inbound DMs as untrusted input.

Full security guide: SECURITY.md

Default behavior on all channels:

-   **DM pairing** (default): unknown senders receive a short pairing code and the bot does not process their message.
-   Approve with: `zeroclaw pairing approve <channel> <code>` (then the sender is added to a local allowlist).
-   Public inbound DMs require an explicit opt-in in `config.toml`.
-   Run `zeroclaw doctor` to surface risky or misconfigured DM policies.

**Autonomy levels:**

Level

Behavior

`ReadOnly`

Agent can observe but not act

`Supervised` (default)

Agent acts with approval for medium/high risk operations

`Full`

Agent acts autonomously within policy bounds

**Sandboxing layers:** workspace isolation, path traversal blocking, command allowlisting, forbidden paths (`/etc`, `/root`, `~/.ssh`), rate limiting (max actions/hour, cost/day caps).

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

Highlights
----------

-   **Lean Runtime by Default** — common CLI and status workflows run in a few-megabyte memory envelope on release builds.
-   **Cost-Efficient Deployment** — designed for $10 boards and small cloud instances, no heavyweight runtime dependencies.
-   **Fast Cold Starts** — single-binary Rust runtime keeps command and daemon startup near-instant.
-   **Portable Architecture** — one binary across ARM, x86, and RISC-V with swappable providers/channels/tools.
-   **Local-first Gateway** — single control plane for sessions, channels, tools, cron, SOPs, and events.
-   **Multi-channel inbox** — WhatsApp, Telegram, Slack, Discord, Signal, iMessage, Matrix, IRC, Email, Bluesky, Nostr, Mattermost, Nextcloud Talk, DingTalk, Lark, QQ, Reddit, LinkedIn, Twitter, MQTT, WeChat Work, WebSocket, and more.
-   **Multi-agent orchestration (Hands)** — autonomous agent swarms that run on schedule and grow smarter over time.
-   **Standard Operating Procedures (SOPs)** — event-driven workflow automation with MQTT, webhook, cron, and peripheral triggers.
-   **Web Dashboard** — React 19 + Vite web UI with real-time chat, memory browser, config editor, cron manager, and tool inspector.
-   **Hardware peripherals** — ESP32, STM32 Nucleo, Arduino, Raspberry Pi GPIO via the `Peripheral` trait.
-   **First-class tools** — shell, file I/O, browser, git, web fetch/search, MCP, Jira, Notion, Google Workspace, and 70+ more.
-   **Lifecycle hooks** — intercept and modify LLM calls, tool executions, and messages at every stage.
-   **Skills platform** — bundled, community, and workspace skills with security auditing.
-   **Tunnel support** — Cloudflare, Tailscale, ngrok, OpenVPN, and custom tunnels for remote access.

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

cargo build --release
ls -lh target/release/zeroclaw

/usr/bin/time -l target/release/zeroclaw --help
/usr/bin/time -l target/release/zeroclaw status

Everything we built so far
--------------------------

### Core platform

-   Gateway HTTP/WS/SSE control plane with sessions, presence, config, cron, webhooks, web dashboard, and pairing.
-   CLI surface: `gateway`, `agent`, `onboard`, `doctor`, `status`, `service`, `migrate`, `auth`, `cron`, `channel`, `skills`.
-   Agent orchestration loop with tool dispatch, prompt construction, message classification, and memory loading.
-   Session model with security policy enforcement, autonomy levels, and approval gating.
-   Resilient provider wrapper with failover, retry, and model routing across 20+ LLM backends.

### Channels

Channels: WhatsApp (native), Telegram, Slack, Discord, Signal, iMessage, Matrix, IRC, Email, Bluesky, DingTalk, Lark, Mattermost, Nextcloud Talk, Nostr, QQ, Reddit, LinkedIn, Twitter, MQTT, WeChat Work, WATI, Mochat, Linq, Notion, WebSocket, ClawdTalk.

Feature-gated: Matrix (`channel-matrix`), Lark (`channel-lark`), Nostr (`channel-nostr`).

### Web dashboard

React 19 + Vite 6 + Tailwind CSS 4 web dashboard served directly from the Gateway:

-   **Dashboard** — system overview, health status, uptime, cost tracking
-   **Agent Chat** — interactive chat with the agent
-   **Memory** — browse and manage memory entries
-   **Config** — view and edit configuration
-   **Cron** — manage scheduled tasks
-   **Tools** — browse available tools
-   **Logs** — view agent activity logs
-   **Cost** — token usage and cost tracking
-   **Doctor** — system health diagnostics
-   **Integrations** — integration status and setup
-   **Pairing** — device pairing management

### Firmware targets

Target

Platform

Purpose

ESP32

Espressif ESP32

Wireless peripheral agent

ESP32-UI

ESP32 + Display

Agent with visual interface

STM32 Nucleo

STM32 (ARM Cortex-M)

Industrial peripheral

Arduino

Arduino

Basic sensor/actuator bridge

Uno Q Bridge

Arduino Uno

Serial bridge to agent

### Tools + automation

-   **Core:** shell, file read/write/edit, git operations, glob search, content search
-   **Web:** browser control, web fetch, web search, screenshot, image info, PDF read
-   **Integrations:** Jira, Notion, Google Workspace, Microsoft 365, LinkedIn, Composio, Pushover, Weather (wttr.in)
-   **MCP:** Model Context Protocol tool wrapper + deferred tool sets
-   **Scheduling:** cron add/remove/update/run, schedule tool
-   **Memory:** recall, store, forget, knowledge, project intel
-   **Advanced:** delegate (agent-to-agent), swarm, model switch/routing, security ops, cloud ops
-   **Hardware:** board info, memory map, memory read (feature-gated)

### Runtime + safety

-   **Autonomy levels:** ReadOnly, Supervised (default), Full.
-   **Sandboxing:** workspace isolation, path traversal blocking, command allowlists, forbidden paths, Landlock (Linux), Bubblewrap.
-   **Rate limiting:** max actions per hour, max cost per day (configurable).
-   **Approval gating:** interactive approval for medium/high risk operations.
-   **E-stop:** emergency shutdown capability.
-   **129+ security tests** in automated CI.

### Ops + packaging

-   Web dashboard served directly from the Gateway.
-   Tunnel support: Cloudflare, Tailscale, ngrok, OpenVPN, custom command.
-   Docker runtime adapter for containerized execution.
-   CI/CD: beta (auto on push) → stable (manual dispatch) → Docker, crates.io, Scoop, AUR, Homebrew, tweet.
-   Pre-built binaries for Linux (x86\_64, aarch64, armv7), macOS (x86\_64, aarch64), Windows (x86\_64).

Configuration
-------------

Minimal `~/.zeroclaw/config.toml`:

default\_provider = "anthropic"
api\_key = "sk-ant-..."

Full configuration reference: docs/reference/api/config-reference.md.

### Channel configuration

**Telegram:**

\[channels.telegram\]
bot\_token = "123456:ABC-DEF..."

**Discord:**

\[channels.discord\]
token = "your-bot-token"

**Slack:**

\[channels.slack\]
bot\_token = "xoxb-..."
app\_token = "xapp-..."

**WhatsApp:**

\[channels.whatsapp\]
enabled = true

**Matrix:**

\[channels.matrix\]
homeserver\_url = "https://matrix.org"
username = "@bot:matrix.org"
password = "..."

**Signal:**

\[channels.signal\]
phone\_number = "+1234567890"

**LINE:**

\[channels\_config.line\]
channel\_secret = "your-channel-secret"
channel\_access\_token = "your-channel-access-token"
allowed\_users = \["Uxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"\]  # LINE user IDs, or \["\*"\] for all
reply\_mode = "reply\_first"  # reply\_first (default) | push\_only | reply\_only

### Tunnel configuration

\[tunnel\]
kind = "cloudflare"  # or "tailscale", "ngrok", "openvpn", "custom", "none"

Details: Channel reference · Config reference

### Runtime support (current)

-   **`native`** (default) — direct process execution, fastest path, ideal for trusted environments.
-   **`docker`** — full container isolation, enforced security policies, requires Docker.

Set `runtime.kind = "docker"` for strict sandboxing or network isolation.

Subscription Auth (OpenAI Codex / Claude Code / Gemini)
-------------------------------------------------------

ZeroClaw supports subscription-native auth profiles (multi-account, encrypted at rest).

-   Store file: `~/.zeroclaw/auth-profiles.json`
-   Encryption key: `~/.zeroclaw/.secret_key`
-   Profile id format: `<provider>:<profile_name>` (example: `openai-codex:work`)

# OpenAI Codex OAuth (ChatGPT subscription)
zeroclaw auth login --provider openai-codex --device-code

# Gemini OAuth
zeroclaw auth login --provider gemini --profile default

# Anthropic setup-token
zeroclaw auth paste-token --provider anthropic --profile default --auth-kind authorization

# Check / refresh / switch profile
zeroclaw auth status
zeroclaw auth refresh --provider openai-codex --profile default
zeroclaw auth use --provider openai-codex --profile work

# Run the agent with subscription auth
zeroclaw agent --provider openai-codex -m "hello"
zeroclaw agent --provider anthropic -m "hello"

Agent workspace + skills
------------------------

Workspace root: `~/.zeroclaw/workspace/` (configurable via config).

Injected prompt files:

-   `IDENTITY.md` — agent personality and role
-   `USER.md` — user context and preferences
-   `MEMORY.md` — long-term facts and lessons
-   `AGENTS.md` — session conventions and initialization rules
-   `SOUL.md` — core identity and operating principles

Skills: `~/.zeroclaw/workspace/skills/<skill>/SKILL.md` or `SKILL.toml`.

# List installed skills
zeroclaw skills list

# Install from git
zeroclaw skills install https://github.com/user/my-skill.git

# Security audit before install
zeroclaw skills audit https://github.com/user/my-skill.git

# Remove a skill
zeroclaw skills remove my-skill

CLI commands
------------

# Workspace management
zeroclaw onboard              # Guided setup wizard
zeroclaw status               # Show daemon/agent status
zeroclaw doctor               # Run system diagnostics

# Gateway + daemon
zeroclaw gateway              # Start gateway server (127.0.0.1:42617)
zeroclaw daemon               # Start full autonomous runtime

# Agent
zeroclaw agent                # Interactive chat mode
zeroclaw agent -m "message"   # Single message mode

# Service management
zeroclaw service install      # Install as OS service (launchd/systemd)
zeroclaw service start|stop|restart|status

# Channels
zeroclaw channel list         # List configured channels
zeroclaw channel doctor       # Check channel health
zeroclaw channel bind-telegram 123456789

# Cron + scheduling
zeroclaw cron list            # List scheduled jobs
zeroclaw cron add "\*/5 \* \* \* \*" --prompt "Check system health"
zeroclaw cron remove <id\>

# Memory
zeroclaw memory list          # List memory entries
zeroclaw memory get <key\>     # Retrieve a memory
zeroclaw memory stats         # Memory statistics

# Auth profiles
zeroclaw auth login --provider <name\>
zeroclaw auth status
zeroclaw auth use --provider <name\> --profile <profile\>

# Hardware peripherals
zeroclaw hardware discover    # Scan for connected devices
zeroclaw peripheral list      # List connected peripherals
zeroclaw peripheral flash     # Flash firmware to device

# Migration
zeroclaw migrate openclaw --dry-run
zeroclaw migrate openclaw

# Shell completions
source <(zeroclaw completions bash)
zeroclaw completions zsh \> ~/.zfunc/\_zeroclaw

Full commands reference: docs/reference/cli/commands-reference.md

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

### Pre-built binaries

Release assets are published for:

-   Linux: `x86_64`, `aarch64`, `armv7`
-   macOS: `x86_64`, `aarch64`
-   Windows: `x86_64`

Download the latest assets from: https://github.com/zeroclaw-labs/zeroclaw/releases/latest

Docs
----

Use these when you're past the onboarding flow and want the deeper reference.

-   Start with the docs index for navigation and "what's where."
-   Read the architecture overview for the full system model.
-   Use the configuration reference when you need every key and example.
-   Run the Gateway by the book with the operational runbook.
-   Follow ZeroClaw Onboard for a guided setup.
-   Debug common failures with the troubleshooting guide.
-   Review security guidance before exposing anything.

### Reference docs

-   Documentation hub: docs/README.md
-   Unified docs TOC: docs/SUMMARY.md
-   Commands reference: docs/reference/cli/commands-reference.md
-   Config reference: docs/reference/api/config-reference.md
-   Providers reference: docs/reference/api/providers-reference.md
-   Channels reference: docs/reference/api/channels-reference.md
-   Operations runbook: docs/ops/operations-runbook.md
-   Troubleshooting: docs/ops/troubleshooting.md

### Collaboration docs

-   Contribution guide: CONTRIBUTING.md
-   PR workflow policy: docs/contributing/pr-workflow.md
-   CI workflow guide: docs/contributing/ci-map.md
-   Reviewer playbook: docs/contributing/reviewer-playbook.md
-   Security disclosure policy: SECURITY.md
-   Documentation template: docs/contributing/doc-template.md

### Deployment + operations

-   Network deployment guide: docs/ops/network-deployment.md
-   Proxy agent playbook: docs/ops/proxy-agent-playbook.md
-   Hardware guides: docs/hardware/README.md

Smooth Crab 🦀
--------------

ZeroClaw was built for the smooth crab 🦀, a fast and efficient AI assistant. Built by Argenis De La Rosa and the community.

-   zeroclawlabs.ai
-   @zeroclawlabs

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

Contributing
------------

New to ZeroClaw? Look for issues labeled `good first issue` — see our Contributing Guide for how to get started. AI/vibe-coded PRs welcome! 🤖

See CONTRIBUTING.md and CLA.md. Implement a trait, submit a PR:

-   CI workflow guide: docs/contributing/ci-map.md
-   New `Provider` → `src/providers/`
-   New `Channel` → `src/channels/`
-   New `Observer` → `src/observability/`
-   New `Tool` → `src/tools/`
-   New `Memory` → `src/memory/`
-   New `Tunnel` → `src/tunnel/`
-   New `Peripheral` → `src/peripherals/`
-   New `Skill` → `~/.zeroclaw/workspace/skills/<name>/`

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

* * *

**ZeroClaw** — Zero overhead. Zero compromise. Deploy anywhere. Swap anything. 🦀

Contributors
------------

This list is generated from the GitHub contributors graph and updates automatically.

Star History
------------
