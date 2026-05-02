---
project: zeroclaw
stars: 30928
description: Fast, small, and fully autonomous AI personal assistant infrastructure, ANY OS, ANY PLATFORM — deploy anywhere, swap anything 🦀
url: https://github.com/zeroclaw-labs/zeroclaw
---

🦀 ZeroClaw — Personal AI Assistant
===================================

**You own the agent. You own the data. You own the machine it runs on.**

Docs · Philosophy · Quick start · Architecture · Discord

* * *

ZeroClaw is an agent runtime — a single Rust binary you configure and run. It talks to LLM providers (Anthropic, OpenAI, Ollama, and ~20 others), reaches the world through 30+ channels (Discord, Telegram, Matrix, email, voice, webhooks, your own CLI), and acts through tools (shell, browser, HTTP, hardware, custom MCP servers). Everything runs on your machine, with your keys, in your workspace.

Read the Philosophy for the four opinions that shape it.

Install
-------

curl -fsSL https://raw.githubusercontent.com/zeroclaw-labs/zeroclaw/master/install.sh | bash

Or clone and run:

git clone https://github.com/zeroclaw-labs/zeroclaw.git
cd zeroclaw
./install.sh

The installer asks whether you want a prebuilt binary (fast, ~seconds) or a source build (slower, customisable). Both end the same way — `zeroclaw onboard` kicks off automatically.

Flags:

```
./install.sh --prebuilt              # always prebuilt; don't ask
./install.sh --source                # always build from source
./install.sh --minimal               # kernel only (~6.6 MB)
./install.sh --source --features agent-runtime,channel-discord  # custom feature set
./install.sh --skip-onboard          # install only, run `zeroclaw onboard` later
./install.sh --list-features         # print available feature flags
```

Platform-specific notes: Linux · macOS · Windows · Docker

Quick start
-----------

zeroclaw onboard                  # wizard: picks a provider, wires channels
zeroclaw agent                    # interactive chat in the terminal
zeroclaw service install          # register as systemd/launchctl/Windows Service
zeroclaw service start            # run it always-on in the background

Full walkthrough: Quick start — or skip the safety gates with YOLO mode for dev boxes.

What ZeroClaw does
------------------

-   **Multi-channel** — one agent answering you across every channel you configure. Inbound messages from Discord, Telegram, Matrix, email, webhooks, CLI — all delivered to the same agent loop.
-   **Provider-agnostic** — model providers are pluggable. Configure Anthropic, OpenAI, local Ollama, or any OpenAI-compatible endpoint. Fallback chains and routing keep the agent running when a provider flakes.
-   **Security-first, with escape hatches** — default autonomy is `supervised`: medium-risk ops require approval, high-risk blocked. Workspace boundaries, command policy, OS-level sandboxes (Landlock / Bubblewrap / Seatbelt / Docker), and cryptographic tool receipts on every action. YOLO mode exists for trusted dev environments.
-   **Hardware-capable** — GPIO / I2C / SPI / USB on Raspberry Pi, STM32, Arduino, and ESP32 via the `Peripheral` trait. See Hardware.
-   **Gateway + dashboard** — HTTP / WebSocket gateway for clients, with a web dashboard for chat, memory browsing, config editing, cron management, and tool inspection.
-   **SOP engine** — event-triggered Standard Operating Procedures (MQTT / webhook / cron / peripheral) with approval gates and resumable runs.
-   **ACP** — IDE / editor integration via Agent Client Protocol (JSON-RPC 2.0 over stdio).

Configuration
-------------

One TOML file at `~/.zeroclaw/config.toml`. Pointers:

-   Provider configuration — the universal `[providers.models.<name>]` schema
-   Channels overview — per-channel `[channels.<name>]` blocks
-   Security overview — autonomy, sandboxing, tool receipts
-   Full config reference — generated from the live schema; every key documented

Architecture
------------

```
┌──────────────────────────────────────────────────────────────┐
│            channels       gateway        ACP                 │
│          (30+ adapters)   (REST/WS)    (JSON-RPC)            │
│                        ↓                                     │
│                   ZeroClaw runtime                           │
│         ┌──────────┬──────────┬──────────┐                   │
│         │  agent   │ security │   SOP    │                   │
│         │   loop   │  policy  │  engine  │                   │
│         └──────────┴──────────┴──────────┘                   │
│              ↓          ↓           ↓                        │
│          providers    tools      memory                      │
│         (Anthropic,  (shell,    (SQLite,                     │
│          OpenAI,     browser,    embeddings)                 │
│          Ollama,     HTTP,                                   │
│          ~20 more)   hardware)                               │
└──────────────────────────────────────────────────────────────┘
```

Full detail with Mermaid diagrams: Architecture overview · Request lifecycle · Crates.

Contributing
------------

Start with how to contribute. Larger changes go through the RFC process. Real-time chat lives on Discord (the best way to reach the team); durable work tracking is on GitHub issues.

Good places to start:

-   New channel → `crates/zeroclaw-channels/`
-   New provider → `crates/zeroclaw-providers/`
-   New tool → `crates/zeroclaw-tools/`
-   Hardware support → `crates/zeroclaw-hardware/`
-   Docs → `docs/book/src/`

AI-assisted PRs are welcome; see Contribution culture (RFC #5615) for the co-authorship norms.

Security
--------

Do not file public issues for security vulnerabilities. Email `security@zeroclaw.dev`. See SECURITY.md for the full policy.

Official repository & impersonation notice
------------------------------------------

This is the only official ZeroClaw repository:

> https://github.com/zeroclaw-labs/zeroclaw

Any other repository, organization, domain, or package claiming to be "ZeroClaw" or implying affiliation with ZeroClaw Labs is **unauthorized and not affiliated with this project**.

License
-------

Dual-licensed: MIT OR Apache 2.0. You may choose either. Contributors automatically grant rights under both — see CLA. The **ZeroClaw** name and logo are trademarks of ZeroClaw Labs.

Credits
-------

Built and maintained by the community — original creator @theonlyhennygod; project lead @JordanTheJet. Full maintainer list in Communication.

Thanks to the communities that incubated early work: **Harvard University**, **MIT**, **Sundai Club**, and every contributor pushing it forward.
