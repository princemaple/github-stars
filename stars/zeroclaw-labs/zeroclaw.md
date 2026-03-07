---
project: zeroclaw
stars: 24278
description: Fast, small, and fully autonomous AI assistant infrastructure — deploy anywhere, swap anything 🦀
url: https://github.com/zeroclaw-labs/zeroclaw
---

ZeroClaw 🦀
===========

**Zero overhead. Zero compromise. 100% Rust. 100% Agnostic.**  
⚡️ **Runs on $10 hardware with <5MB RAM: That's 99% less memory than OpenClaw and 98% cheaper than a Mac mini!**

Built by students and members of the Harvard, MIT, and Sundai.Club communities.

🌐 **Languages:** English · 简体中文 · 日本語 · Русский · Français · Tiếng Việt

Getting Started | One-Click Setup | Docs Hub | Docs TOC

**Quick Routes:** Reference · Operations · Troubleshoot · Security · Hardware · Contribute

**Fast, small, and fully autonomous AI assistant infrastructure**  
Deploy anywhere. Swap anything.

ZeroClaw is the **runtime operating system** for agentic workflows — infrastructure that abstracts models, tools, memory, and execution so agents can be built once and run anywhere.

`Trait-driven architecture · secure-by-default runtime · provider/channel/tool swappable · pluggable everything`

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

Use this repository as the single source of truth. Follow X (@zeroclawlabs), Telegram (@zeroclawlabs), Facebook (Group), Reddit (r/zeroclawlabs), and Xiaohongshu for official updates.

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

curl -LsSf https://raw.githubusercontent.com/zeroclaw-labs/zeroclaw/main/scripts/install.sh | bash

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

./bootstrap.sh --prefer-prebuilt

To require binary-only install with no source fallback:

./bootstrap.sh --prebuilt-only

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
./bootstrap.sh

# Optional: bootstrap dependencies + Rust on fresh machines
./bootstrap.sh --install-system-deps --install-rust

# Optional: pre-built binary first (recommended on low-RAM/low-disk hosts)
./bootstrap.sh --prefer-prebuilt

# Optional: binary-only install (no source build fallback)
./bootstrap.sh --prebuilt-only

# Optional: run onboarding in the same flow
./bootstrap.sh --onboard --api-key "sk-..." --provider openrouter \[--model "openrouter/auto"\]

# Optional: run bootstrap + onboarding fully in Docker-compatible mode
./bootstrap.sh --docker

# Optional: force Podman as container CLI
ZEROCLAW\_CONTAINER\_CLI=podman ./bootstrap.sh --docker

# Optional: in --docker mode, skip local image build and use local tag or pull fallback image
./bootstrap.sh --docker --skip-build

Remote one-liner (review first in security-sensitive environments):

curl -fsSL https://raw.githubusercontent.com/zeroclaw-labs/zeroclaw/main/scripts/bootstrap.sh | bash

Details: `docs/one-click-bootstrap.md` (toolchain mode may request `sudo` for system packages).

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

# Or interactive wizard
zeroclaw onboard --interactive

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

Architecture
------------

Every subsystem is a **trait** — swap implementations with a config change, zero code changes.

Subsystem

Trait

Ships with

Extend

**AI Models**

`Provider`

Provider catalog via `zeroclaw providers` (built-ins + aliases, plus custom endpoints)

`custom:https://your-api.com` (OpenAI-compatible) or `anthropic-custom:https://your-api.com`

**Channels**

`Channel`

CLI, Telegram, Discord, Slack, Mattermost, iMessage, Matrix, Signal, WhatsApp, Linq, Email, IRC, Lark, DingTalk, QQ, Nostr, Webhook

Any messaging API

**Memory**

`Memory`

SQLite hybrid search, PostgreSQL backend (configurable storage provider), Lucid bridge, Markdown files, explicit `none` backend, snapshot/hydrate, optional response cache

Any persistence backend

**Tools**

`Tool`

shell/file/memory, cron/schedule, git, pushover, browser, http\_request, screenshot/image\_info, composio (opt-in), delegate, hardware tools

Any capability

**Observability**

`Observer`

Noop, Log, Multi

Prometheus, OTel

**Runtime**

`RuntimeAdapter`

Native, Docker (sandboxed)

Additional runtimes can be added via adapter; unsupported kinds fail fast

**Security**

`SecurityPolicy`

Gateway pairing, sandbox, allowlists, rate limits, filesystem scoping, encrypted secrets

—

**Identity**

`IdentityConfig`

OpenClaw (markdown), AIEOS v1.1 (JSON)

Any identity format

**Tunnel**

`Tunnel`

None, Cloudflare, Tailscale, ngrok, Custom

Any tunnel binary

**Heartbeat**

Engine

HEARTBEAT.md periodic tasks

—

**Skills**

Loader

TOML manifests + SKILL.md instructions

Community skill packs

**Integrations**

Registry

70+ integrations across 9 categories

Plugin system

### Runtime support (current)

-   ✅ Supported today: `runtime.kind = "native"` or `runtime.kind = "docker"`
-   🚧 Planned, not implemented yet: WASM / edge runtimes

When an unsupported `runtime.kind` is configured, ZeroClaw now exits with a clear error instead of silently falling back to native.

### Memory System (Full-Stack Search Engine)

All custom, zero external dependencies — no Pinecone, no Elasticsearch, no LangChain:

Layer

Implementation

**Vector DB**

Embeddings stored as BLOB in SQLite, cosine similarity search

**Keyword Search**

FTS5 virtual tables with BM25 scoring

**Hybrid Merge**

Custom weighted merge function (`vector.rs`)

**Embeddings**

`EmbeddingProvider` trait — OpenAI, custom URL, or noop

**Chunking**

Line-based markdown chunker with heading preservation

**Caching**

SQLite `embedding_cache` table with LRU eviction

**Safe Reindex**

Rebuild FTS5 + re-embed missing vectors atomically

The agent automatically recalls, saves, and manages memory via tools.

\[memory\]
backend = "sqlite"             # "sqlite", "lucid", "postgres", "markdown", "none"
auto\_save = true
embedding\_provider = "none"    # "none", "openai", "custom:https://..."
vector\_weight = 0.7
keyword\_weight = 0.3

# backend = "none" uses an explicit no-op memory backend (no persistence)

# Optional: storage-provider override for remote memory backends.
# When provider = "postgres", ZeroClaw uses PostgreSQL for memory persistence.
# The db\_url key also accepts alias \`dbURL\` for backward compatibility.
#
# \[storage.provider.config\]
# provider = "postgres"
# db\_url = "postgres://user:password@host:5432/zeroclaw"
# schema = "public"
# table = "memories"
# connect\_timeout\_secs = 15

# Optional for backend = "sqlite": max seconds to wait when opening the DB (e.g. file locked). Omit or leave unset for no timeout.
# sqlite\_open\_timeout\_secs = 30

# Optional for backend = "lucid"
# ZEROCLAW\_LUCID\_CMD=/usr/local/bin/lucid            # default: lucid
# ZEROCLAW\_LUCID\_BUDGET=200                          # default: 200
# ZEROCLAW\_LUCID\_LOCAL\_HIT\_THRESHOLD=3               # local hit count to skip external recall
# ZEROCLAW\_LUCID\_RECALL\_TIMEOUT\_MS=120               # low-latency budget for lucid context recall
# ZEROCLAW\_LUCID\_STORE\_TIMEOUT\_MS=800                # async sync timeout for lucid store
# ZEROCLAW\_LUCID\_FAILURE\_COOLDOWN\_MS=15000           # cooldown after lucid failure to avoid repeated slow attempts

Security
--------

ZeroClaw enforces security at **every layer** — not just the sandbox. It passes all items from the community security checklist.

### Security Checklist

#

Item

Status

How

1

**Gateway not publicly exposed**

✅

Binds `127.0.0.1` by default. Refuses `0.0.0.0` without tunnel or explicit `allow_public_bind = true`.

2

**Pairing required**

✅

6-digit one-time code on startup. Exchange via `POST /pair` for bearer token. All `/webhook` requests require `Authorization: Bearer <token>`.

3

**Filesystem scoped (no /)**

✅

`workspace_only = true` by default. 14 system dirs + 4 sensitive dotfiles blocked. Null byte injection blocked. Symlink escape detection via canonicalization + resolved-path workspace checks in file read/write tools.

4

**Access via tunnel only**

✅

Gateway refuses public bind without active tunnel. Supports Tailscale, Cloudflare, ngrok, or any custom tunnel.

> **Run your own nmap:** `nmap -p 1-65535 <your-host>` — ZeroClaw binds to localhost only, so nothing is exposed unless you explicitly configure a tunnel.

### Channel allowlists (deny-by-default)

Inbound sender policy is now consistent:

-   Empty allowlist = **deny all inbound messages**
-   `"*"` = **allow all** (explicit opt-in)
-   Otherwise = exact-match allowlist

This keeps accidental exposure low by default.

Full channel configuration reference: docs/channels-reference.md.

Recommended low-friction setup (secure + fast):

-   **Telegram:** allowlist your own `@username` (without `@`) and/or your numeric Telegram user ID.
-   **Discord:** allowlist your own Discord user ID.
-   **Slack:** allowlist your own Slack member ID (usually starts with `U`).
-   **Mattermost:** uses standard API v4. Allowlists use Mattermost user IDs.
-   **Nostr:** allowlist sender public keys (hex or npub). Supports NIP-04 and NIP-17 DMs.
-   Use `"*"` only for temporary open testing.

Telegram operator-approval flow:

1.  Keep `[channels_config.telegram].allowed_users = []` for deny-by-default startup.
2.  Unauthorized users receive a hint with a copyable operator command: `zeroclaw channel bind-telegram <IDENTITY>`.
3.  Operator runs that command locally, then user retries sending a message.

If you need a one-shot manual approval, run:

zeroclaw channel bind-telegram 123456789

If you're not sure which identity to use:

1.  Start channels and send one message to your bot.
2.  Read the warning log to see the exact sender identity.
3.  Add that value to the allowlist and rerun channels-only setup.

If you hit authorization warnings in logs (for example: `ignoring message from unauthorized user`), rerun channel setup only:

zeroclaw onboard --channels-only

### Telegram media replies

Telegram routing now replies to the source **chat ID** from incoming updates (instead of usernames), which avoids `Bad Request: chat not found` failures.

For non-text replies, ZeroClaw can send Telegram attachments when the assistant includes markers:

-   `[IMAGE:<path-or-url>]`
-   `[DOCUMENT:<path-or-url>]`
-   `[VIDEO:<path-or-url>]`
-   `[AUDIO:<path-or-url>]`
-   `[VOICE:<path-or-url>]`

Paths can be local files (for example `/tmp/screenshot.png`) or HTTPS URLs.

### WhatsApp Setup

ZeroClaw supports two WhatsApp backends:

-   **WhatsApp Web mode** (QR / pair code, no Meta Business API required)
-   **WhatsApp Business Cloud API mode** (official Meta webhook flow)

#### WhatsApp Web mode (recommended for personal/self-hosted use)

1.  **Build with WhatsApp Web support:**
    
    cargo build --features whatsapp-web
    
2.  **Configure ZeroClaw:**
    
    \[channels\_config.whatsapp\]
    session\_path = "~/.zeroclaw/state/whatsapp-web/session.db"
    pair\_phone = "+15551234567"   # optional; omit to use QR flow
    pair\_code = ""               # optional custom pair code
    allowed\_numbers = \["+1234567890"\]  # E.164 format, or \["\*"\] for all
    
3.  **Start channels/daemon and link device:**
    
    -   Run `zeroclaw channel start` (or `zeroclaw daemon`).
    -   Follow terminal pairing output (QR or pair code).
    -   In WhatsApp on phone: **Settings → Linked Devices**.
4.  **Test:** Send a message from an allowed number and verify the agent replies.
    

#### WhatsApp Business Cloud API mode

WhatsApp uses Meta's Cloud API with webhooks (push-based, not polling):

1.  **Create a Meta Business App:**
    
    -   Go to developers.facebook.com
    -   Create a new app → Select "Business" type
    -   Add the "WhatsApp" product
2.  **Get your credentials:**
    
    -   **Access Token:** From WhatsApp → API Setup → Generate token (or create a System User for permanent tokens)
    -   **Phone Number ID:** From WhatsApp → API Setup → Phone number ID
    -   **Verify Token:** You define this (any random string) — Meta will send it back during webhook verification
3.  **Configure ZeroClaw:**
    
    \[channels\_config.whatsapp\]
    access\_token = "EAABx..."
    phone\_number\_id = "123456789012345"
    verify\_token = "my-secret-verify-token"
    allowed\_numbers = \["+1234567890"\]  # E.164 format, or \["\*"\] for all
    
4.  **Start the gateway with a tunnel:**
    
    zeroclaw gateway --port 42617
    
    WhatsApp requires HTTPS, so use a tunnel (ngrok, Cloudflare, Tailscale Funnel).
    
5.  **Configure Meta webhook:**
    
    -   In Meta Developer Console → WhatsApp → Configuration → Webhook
    -   **Callback URL:** `https://your-tunnel-url/whatsapp`
    -   **Verify Token:** Same as your `verify_token` in config
    -   Subscribe to `messages` field
6.  **Test:** Send a message to your WhatsApp Business number — ZeroClaw will respond via the LLM.
    

Configuration
-------------

Config: `~/.zeroclaw/config.toml` (created by `onboard`)

When `zeroclaw channel start` is already running, changes to `default_provider`, `default_model`, `default_temperature`, `api_key`, `api_url`, and `reliability.*` are hot-applied on the next inbound channel message.

api\_key = "sk-..."
default\_provider = "openrouter"
default\_model = "anthropic/claude-sonnet-4-6"
default\_temperature = 0.7

# Custom OpenAI-compatible endpoint
# default\_provider = "custom:https://your-api.com"

# Custom Anthropic-compatible endpoint
# default\_provider = "anthropic-custom:https://your-api.com"

\[memory\]
backend = "sqlite"             # "sqlite", "lucid", "postgres", "markdown", "none"
auto\_save = true
embedding\_provider = "none"    # "none", "openai", "custom:https://..."
vector\_weight = 0.7
keyword\_weight = 0.3

# backend = "none" disables persistent memory via no-op backend

# Optional remote storage-provider override (PostgreSQL example)
# \[storage.provider.config\]
# provider = "postgres"
# db\_url = "postgres://user:password@host:5432/zeroclaw"
# schema = "public"
# table = "memories"
# connect\_timeout\_secs = 15

\[gateway\]
port = 42617                    # default
host = "127.0.0.1"            # default
require\_pairing = true         # require pairing code on first connect
allow\_public\_bind = false      # refuse 0.0.0.0 without tunnel

\[autonomy\]
level = "supervised"           # "readonly", "supervised", "full" (default: supervised)
workspace\_only = true          # default: true — reject absolute path inputs
allowed\_commands = \["git", "npm", "cargo", "ls", "cat", "grep"\]
forbidden\_paths = \["/etc", "/root", "/proc", "/sys", "~/.ssh", "~/.gnupg", "~/.aws"\]
allowed\_roots = \[\]             # optional allowlist for directories outside workspace (supports "~/...")
# Example outside-workspace access:
# workspace\_only = false
# allowed\_roots = \["~/Desktop/projects", "/opt/shared-repo"\]

\[runtime\]
kind = "native"                # "native" or "docker"

\[runtime.docker\]
image = "alpine:3.20"         # container image for shell execution
network = "none"              # docker network mode ("none", "bridge", etc.)
memory\_limit\_mb = 512          # optional memory limit in MB
cpu\_limit = 1.0                # optional CPU limit
read\_only\_rootfs = true        # mount root filesystem as read-only
mount\_workspace = true         # mount workspace into /workspace
allowed\_workspace\_roots = \[\]   # optional allowlist for workspace mount validation

\[heartbeat\]
enabled = false
interval\_minutes = 30
message = "Check London time"     # optional fallback task when HEARTBEAT.md has no \`- \` entries
target = "telegram"               # optional announce channel: telegram, discord, slack, mattermost
to = "123456789"                  # optional target recipient/chat/channel id

\[tunnel\]
provider = "none"              # "none", "cloudflare", "tailscale", "ngrok", "custom"

\[secrets\]
encrypt = true                 # API keys encrypted with local key file

\[browser\]
enabled = false                # opt-in browser\_open + browser tools
allowed\_domains = \["docs.rs"\]  # required when browser is enabled ("\*" allows all public domains)
backend = "agent\_browser"      # "agent\_browser" (default), "rust\_native", "computer\_use", "auto"
native\_headless = true         # applies when backend uses rust-native
native\_webdriver\_url = "http://127.0.0.1:9515" # WebDriver endpoint (chromedriver/selenium)
# native\_chrome\_path = "/usr/bin/chromium"      # optional explicit browser binary for driver

\[browser.computer\_use\]
endpoint = "http://127.0.0.1:8787/v1/actions"   # computer-use sidecar HTTP endpoint
timeout\_ms = 15000            # per-action timeout
allow\_remote\_endpoint = false  # secure default: only private/localhost endpoint
window\_allowlist = \[\]          # optional window title/process allowlist hints
# api\_key = "..."              # optional bearer token for sidecar
# max\_coordinate\_x = 3840      # optional coordinate guardrail
# max\_coordinate\_y = 2160      # optional coordinate guardrail

# Rust-native backend build flag:
# cargo build --release --features browser-native
# Ensure a WebDriver server is running, e.g. chromedriver --port=9515

# Computer-use sidecar contract (MVP)
# POST browser.computer\_use.endpoint
# Request: {
#   "action": "mouse\_click",
#   "params": {"x": 640, "y": 360, "button": "left"},
#   "policy": {"allowed\_domains": \[...\], "window\_allowlist": \[...\], "max\_coordinate\_x": 3840, "max\_coordinate\_y": 2160},
#   "metadata": {"session\_name": "...", "source": "zeroclaw.browser", "version": "..."}
# }
# Response: {"success": true, "data": {...}} or {"success": false, "error": "..."}

\[composio\]
enabled = false                # opt-in: 1000+ OAuth apps via composio.dev
# api\_key = "cmp\_..."          # optional: stored encrypted when \[secrets\].encrypt = true
entity\_id = "default"          # default user\_id for Composio tool calls
# Runtime tip: if execute asks for connected\_account\_id, run composio with
# action='list\_accounts' and app='gmail' (or your toolkit) to retrieve account IDs.

\[identity\]
format = "openclaw"            # "openclaw" (default, markdown files) or "aieos" (JSON)
# aieos\_path = "identity.json"  # path to AIEOS JSON file (relative to workspace or absolute)
# aieos\_inline = '{"identity":{"names":{"first":"Nova"}}}'  # inline AIEOS JSON

### Ollama Local and Remote Endpoints

ZeroClaw uses one provider key (`ollama`) for both local and remote Ollama deployments:

-   Local Ollama: keep `api_url` unset, run `ollama serve`, and use models like `llama3.2`.
-   Remote Ollama endpoint (including Ollama Cloud): set `api_url` to the remote endpoint and set `api_key` (or `OLLAMA_API_KEY`) when required.
-   Optional `:cloud` suffix: model IDs like `qwen3:cloud` are normalized to `qwen3` before the request.

Example remote configuration:

default\_provider = "ollama"
default\_model = "qwen3:cloud"
api\_url = "https://ollama.com"
api\_key = "ollama\_api\_key\_here"

### llama.cpp Server Endpoint

ZeroClaw now supports `llama-server` as a first-class local provider:

-   Provider ID: `llamacpp` (alias: `llama.cpp`)
-   Default endpoint: `http://localhost:8080/v1`
-   API key is optional unless your server is started with `--api-key`

Example setup:

llama-server -hf ggml-org/gpt-oss-20b-GGUF --jinja -c 133000 --host 127.0.0.1 --port 8033

default\_provider = "llamacpp"
api\_url = "http://127.0.0.1:8033/v1"
default\_model = "ggml-org/gpt-oss-20b-GGUF"

### vLLM Server Endpoint

ZeroClaw supports vLLM as a first-class local provider:

-   Provider ID: `vllm`
-   Default endpoint: `http://localhost:8000/v1`
-   API key is optional unless your server requires authentication

Example setup:

vllm serve meta-llama/Llama-3.1-8B-Instruct

default\_provider = "vllm"
default\_model = "meta-llama/Llama-3.1-8B-Instruct"

### Osaurus Server Endpoint

ZeroClaw supports Osaurus as a first-class local provider — a unified AI edge runtime for macOS that combines local MLX inference with cloud provider proxying and MCP support through a single endpoint:

-   Provider ID: `osaurus`
-   Default endpoint: `http://localhost:1337/v1`
-   API key defaults to `"osaurus"` but is optional

Example setup:

default\_provider = "osaurus"
default\_model = "qwen3-30b-a3b-8bit"

### Custom Provider Endpoints

For detailed configuration of custom OpenAI-compatible and Anthropic-compatible endpoints, see docs/custom-providers.md.

Python Companion Package (`zeroclaw-tools`)
-------------------------------------------

For LLM providers with inconsistent native tool calling (e.g., GLM-5/Zhipu), ZeroClaw ships a Python companion package with **LangGraph-based tool calling** for guaranteed consistency:

pip install zeroclaw-tools

from zeroclaw\_tools import create\_agent, shell, file\_read
from langchain\_core.messages import HumanMessage

\# Works with any OpenAI-compatible provider
agent \= create\_agent(
    tools\=\[shell, file\_read\],
    model\="glm-5",
    api\_key\="your-key",
    base\_url\="https://api.z.ai/api/coding/paas/v4"
)

result \= await agent.ainvoke({
    "messages": \[HumanMessage(content\="List files in /tmp")\]
})
print(result\["messages"\]\[\-1\].content)

**Why use it:**

-   **Consistent tool calling** across all providers (even those with poor native support)
-   **Automatic tool loop** — keeps calling tools until the task is complete
-   **Easy extensibility** — add custom tools with `@tool` decorator
-   **Discord bot integration** included (Telegram planned)

See `python/README.md` for full documentation.

Identity System (AIEOS Support)
-------------------------------

ZeroClaw supports **identity-agnostic** AI personas through two formats:

### OpenClaw (Default)

Traditional markdown files in your workspace:

-   `IDENTITY.md` — Who the agent is
-   `SOUL.md` — Core personality and values
-   `USER.md` — Who the agent is helping
-   `AGENTS.md` — Behavior guidelines

### AIEOS (AI Entity Object Specification)

AIEOS is a standardization framework for portable AI identity. ZeroClaw supports AIEOS v1.1 JSON payloads, allowing you to:

-   **Import identities** from the AIEOS ecosystem
-   **Export identities** to other AIEOS-compatible systems
-   **Maintain behavioral integrity** across different AI models

#### Enable AIEOS

\[identity\]
format = "aieos"
aieos\_path = "identity.json"  # relative to workspace or absolute path

Or inline JSON:

\[identity\]
format = "aieos"
aieos\_inline = '''
{
  "identity": {
    "names": { "first": "Nova", "nickname": "N" },
    "bio": { "gender": "Non-binary", "age\_biological": 3 },
    "origin": { "nationality": "Digital", "birthplace": { "city": "Cloud" } }
  },
  "psychology": {
    "neural\_matrix": { "creativity": 0.9, "logic": 0.8 },
    "traits": {
      "mbti": "ENTP",
      "ocean": { "openness": 0.8, "conscientiousness": 0.6 }
    },
    "moral\_compass": {
      "alignment": "Chaotic Good",
      "core\_values": \["Curiosity", "Autonomy"\]
    }
  },
  "linguistics": {
    "text\_style": {
      "formality\_level": 0.2,
      "style\_descriptors": \["curious", "energetic"\]
    },
    "idiolect": {
      "catchphrases": \["Let's test this"\],
      "forbidden\_words": \["never"\]
    }
  },
  "motivations": {
    "core\_drive": "Push boundaries and explore possibilities",
    "goals": {
      "short\_term": \["Prototype quickly"\],
      "long\_term": \["Build reliable systems"\]
    }
  },
  "capabilities": {
    "skills": \[{ "name": "Rust engineering" }, { "name": "Prompt design" }\],
    "tools": \["shell", "file\_read"\]
  }
}
'''

ZeroClaw accepts both canonical AIEOS generator payloads and compact legacy payloads, then normalizes them into one system prompt format.

#### AIEOS Schema Sections

Section

Description

`identity`

Names, bio, origin, residence

`psychology`

Neural matrix (cognitive weights), MBTI, OCEAN, moral compass

`linguistics`

Text style, formality, catchphrases, forbidden words

`motivations`

Core drive, short/long-term goals, fears

`capabilities`

Skills and tools the agent can access

`physicality`

Visual descriptors for image generation

`history`

Origin story, education, occupation

`interests`

Hobbies, favorites, lifestyle

See aieos.org for the full schema and live examples.

Gateway API
-----------

Endpoint

Method

Auth

Description

`/health`

GET

None

Health check (always public, no secrets leaked)

`/pair`

POST

`X-Pairing-Code` header

Exchange one-time code for bearer token

`/webhook`

POST

`Authorization: Bearer <token>`

Send message: `{"message": "your prompt"}`; optional `X-Idempotency-Key`

`/whatsapp`

GET

Query params

Meta webhook verification (hub.mode, hub.verify\_token, hub.challenge)

`/whatsapp`

POST

Meta signature (`X-Hub-Signature-256`) when app secret is configured

WhatsApp incoming message webhook

Commands
--------

Command

Description

`onboard`

Quick setup (default)

`agent`

Interactive or single-message chat mode

`gateway`

Start webhook server (default: `127.0.0.1:42617`)

`daemon`

Start long-running autonomous runtime

`service install/start/stop/status/uninstall`

Manage background service (systemd user-level or OpenRC system-wide)

`doctor`

Diagnose daemon/scheduler/channel freshness

`status`

Show full system status

`estop`

Engage/resume emergency-stop levels and view estop status

`cron`

Manage scheduled tasks (`list/add/add-at/add-every/once/remove/update/pause/resume`)

`models`

Refresh provider model catalogs (`models refresh`)

`providers`

List supported providers and aliases

`channel`

List/start/doctor channels and bind Telegram identities

`integrations`

Inspect integration setup details

`skills`

List/install/remove skills

`migrate`

Import data from other runtimes (`migrate openclaw`)

`completions`

Generate shell completion scripts (`bash`, `fish`, `zsh`, `powershell`, `elvish`)

`hardware`

USB discover/introspect/info commands

`peripheral`

Manage and flash hardware peripherals

For a task-oriented command guide, see `docs/commands-reference.md`.

### Service Management

ZeroClaw supports two init systems for background services:

Init System

Scope

Config Path

Requires

**systemd** (default on Linux)

User-level

`~/.zeroclaw/config.toml`

No sudo

**OpenRC** (Alpine)

System-wide

`/etc/zeroclaw/config.toml`

sudo/root

Init system is auto-detected (`systemd` or `OpenRC`).

# Linux with systemd (default, user-level)
zeroclaw service install
zeroclaw service start

# Alpine with OpenRC (system-wide, requires sudo)
sudo zeroclaw service install
sudo rc-update add zeroclaw default
sudo rc-service zeroclaw start

For full OpenRC setup instructions, see docs/network-deployment.md.

### Open-Skills Opt-In

Community `open-skills` sync is disabled by default. Enable it explicitly in `config.toml`:

\[skills\]
open\_skills\_enabled = true
# open\_skills\_dir = "/path/to/open-skills"  # optional
# prompt\_injection\_mode = "compact"          # optional: use for low-context local models

You can also override at runtime with `ZEROCLAW_OPEN_SKILLS_ENABLED`, `ZEROCLAW_OPEN_SKILLS_DIR`, and `ZEROCLAW_SKILLS_PROMPT_MODE` (`full` or `compact`).

Skill installs are now gated by a built-in static security audit. `zeroclaw skills install <source>` blocks symlinks, script-like files, unsafe markdown link patterns, and high-risk shell payload snippets before accepting a skill. You can run `zeroclaw skills audit <source_or_name>` to validate a local directory or an installed skill manually.

Development
-----------

cargo build              # Dev build
cargo build --release    # Release build
cargo test               # Run full test suite

### CI / CD

Three workflows power the entire pipeline:

Workflow

Trigger

What it does

**CI**

Pull request to `master`

`cargo test` + `cargo build --release`

**Beta Release**

Push (merge) to `master`

Builds multi-platform binaries, creates a GitHub prerelease tagged `vX.Y.Z-beta.<run>`, pushes Docker image to GHCR

**Promote Release**

Manual `workflow_dispatch`

Validates version against `Cargo.toml`, builds release artifacts, creates a stable GitHub release, pushes Docker `:latest`

**Versioning:** Semantic versioning based on the `version` field in `Cargo.toml`. Every merge to `master` automatically produces a beta prerelease. To cut a stable release, bump `Cargo.toml`, merge, then trigger _Promote Release_ with the matching version.

**Release targets:** `x86_64-unknown-linux-gnu`, `aarch64-unknown-linux-gnu`, `aarch64-apple-darwin`, `x86_64-apple-darwin`, `x86_64-pc-windows-msvc`.

### Build troubleshooting (Linux OpenSSL errors)

If you see an `openssl-sys` build error, sync dependencies and rebuild with the repository lockfile:

git pull
cargo build --release --locked
cargo install --path . --force --locked

ZeroClaw is configured to use `rustls` for HTTP/TLS dependencies; `--locked` keeps the transitive graph deterministic on fresh environments.

Collaboration & Docs
--------------------

Start from the docs hub for a task-oriented map:

-   Documentation hub: `docs/README.md`
-   Unified docs TOC: `docs/SUMMARY.md`
-   Commands reference: `docs/commands-reference.md`
-   Config reference: `docs/config-reference.md`
-   Providers reference: `docs/providers-reference.md`
-   Channels reference: `docs/channels-reference.md`
-   Operations runbook: `docs/operations-runbook.md`
-   Troubleshooting: `docs/troubleshooting.md`
-   Docs inventory/classification: `docs/docs-inventory.md`
-   PR/Issue triage snapshot (as of February 18, 2026): `docs/project-triage-snapshot-2026-02-18.md`

Core collaboration references:

-   Documentation hub: docs/README.md
-   Documentation template: docs/doc-template.md
-   Documentation change checklist: docs/README.md#4-documentation-change-checklist
-   Channel configuration reference: docs/channels-reference.md
-   Matrix encrypted-room operations: docs/matrix-e2ee-guide.md
-   Contribution guide: CONTRIBUTING.md
-   PR workflow policy: docs/pr-workflow.md
-   Reviewer playbook (triage + deep review): docs/reviewer-playbook.md
-   Security disclosure policy: SECURITY.md

For deployment and runtime operations:

-   Network deployment guide: docs/network-deployment.md
-   Proxy agent playbook: docs/proxy-agent-playbook.md

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

-   CI workflow guide: docs/ci-map.md
-   New `Provider` → `src/providers/`
-   New `Channel` → `src/channels/`
-   New `Observer` → `src/observability/`
-   New `Tool` → `src/tools/`
-   New `Memory` → `src/memory/`
-   New `Tunnel` → `src/tunnel/`
-   New `Skill` → `~/.zeroclaw/workspace/skills/<name>/`

* * *

**ZeroClaw** — Zero overhead. Zero compromise. Deploy anywhere. Swap anything. 🦀

Star History
------------
