---
project: zeroclaw
stars: 21138
description: Fast, small, and fully autonomous AI assistant Operating System — deploy anywhere, swap anything 🦀
url: https://github.com/zeroclaw-labs/zeroclaw
---

ZeroClaw 🦀
===========

**Zero overhead. Zero compromise. 100% Rust. 100% Agnostic.**  
⚡️ **Runs on any hardware with <5MB RAM: That's 99% less memory than OpenClaw and 98% cheaper than a Mac mini!**

Built by students and members of the Harvard, MIT, and Sundai.Club communities.

🌐 **Languages:** English · 简体中文 · 日本語 · Русский · Français · Tiếng Việt · Ελληνικά

Getting Started | One-Click Setup | Docs Hub | Docs TOC

**Quick Routes:** Reference · Operations · Troubleshoot · Security · Hardware · Contribute

**Fast, small, and fully autonomous Operating System**  
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
-   🔍 **Research Phase:** Proactive information gathering through tools before response generation — reduces hallucinations by fact-checking first.

### Why teams pick ZeroClaw

-   **Lean by default:** small Rust binary, fast startup, low memory footprint.
-   **Secure by design:** pairing, strict sandboxing, explicit allowlists, workspace scoping.
-   **Fully swappable:** core systems are traits (providers, channels, tools, memory, tunnels).
-   **No lock-in:** OpenAI-compatible provider support + pluggable custom endpoints.

Quick Start
-----------

### Option 1: Homebrew (macOS/Linuxbrew)

brew install zeroclaw

### Option 2: Clone + Bootstrap

git clone https://github.com/zeroclaw-labs/zeroclaw.git
cd zeroclaw
./bootstrap.sh

> **Note:** Source builds require ~2GB RAM and ~6GB disk. For resource-constrained systems, use `./bootstrap.sh --prefer-prebuilt` to download a pre-built binary instead.

### Option 3: Cargo Install

cargo install zeroclaw

### First Run

# Start the gateway daemon
zeroclaw gateway start

# Open the web UI
zeroclaw dashboard

# Or chat directly
zeroclaw chat "Hello!"

For detailed setup options, see docs/one-click-bootstrap.md.

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

**Any hardware**

> Notes: ZeroClaw results are measured on release builds using `/usr/bin/time -l`. OpenClaw requires Node.js runtime (typically ~390MB additional memory overhead), while NanoBot requires Python runtime. PicoClaw and ZeroClaw are static binaries. The RAM figures above are runtime memory; build-time compilation requirements are higher.

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
