---
project: openclaw
stars: 384842
description: Your own personal AI assistant. Any OS. Any Platform. The lobster way. 🦞 
url: https://github.com/openclaw/openclaw
---

🦞 OpenClaw — Personal AI Assistant
===================================

**OpenClaw** is a _personal AI assistant_ that learns and grows with you, running on your own devices — developed in the open by the OpenClaw Foundation, a non-profit. It answers you on the channels you already use, can speak and listen on macOS/iOS/Android, and can render a live Canvas you control. The Gateway is just the control plane — the product is the assistant.

If you want a personal, single-user assistant that feels local, fast, and always-on, this is it.

Supported channels: WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, SMS (Twilio), IRC, Microsoft Teams, Matrix, Feishu, LINE, Mattermost, Nextcloud Talk, Nostr, Synology Chat, Tlon, Twitch, Zalo, Zalo Personal, ClickClack, Raft, Reef, QQ, and the built-in WebChat.

Website · Docs · Getting Started · Onboarding · Updating · Showcase · FAQ · Vision · DeepWiki · Docker · Nix · Third-party notices · Discord

Sponsors
--------

Install
-------

Runtime: **Node 24.15+ (recommended), Node 22.22.3+, or Node 25.9+**.

# macOS / Linux
curl -fsSL https://openclaw.ai/install.sh | bash

# Windows (PowerShell)
iwr \-useb https://openclaw.ai/install.ps1 | iex

Or install via a package manager (npm, pnpm, or bun all work):

npm install -g openclaw@latest

Then run onboarding:

openclaw onboard --install-daemon

OpenClaw Onboard guides you step by step through setting up the gateway, workspace, channels, and skills on **macOS, Linux, and Windows**, and installs the Gateway daemon (launchd/systemd user service/Scheduled Task) so it stays running. Windows desktop users can also start with the native Windows Hub companion app for setup, tray status, chat, node mode, and local MCP mode.

Full beginner guide (auth, pairing, channels): Getting started.

Quick start (TL;DR)
-------------------

After onboarding, the Gateway runs as a daemon:

openclaw gateway status   # expect: running on port 18789
openclaw dashboard        # open the Control UI

Send a test message or talk to the assistant:

# Send a message
openclaw message send --target +1234567890 --message "Hello from OpenClaw"

# Talk to the assistant (optionally deliver the reply to any connected channel)
openclaw agent --message "Ship checklist" --thinking high

Foreground/debug mode:

openclaw gateway stop
openclaw gateway --port 18789 --verbose

Upgrading? Run `openclaw update` — see the Updating guide — then `openclaw doctor`.

Models
------

-   Bring the provider you already use: Anthropic, OpenAI, Google (Gemini), xAI (Grok), OpenRouter, GitHub Copilot, MiniMax, and any OpenAI- or Anthropic-compatible endpoint. Details: Model providers.
-   Sign in with a subscription (OAuth) instead of an API key: **Anthropic (Claude Pro/Max)**, **OpenAI (ChatGPT/Codex)**, and **GitHub Copilot**.
-   Model note: prefer a current flagship model from the provider you trust and already use. See Onboarding.
-   Models config + CLI: Models. Auth profile rotation + fallbacks: Model failover.

Security defaults (DM access)
-----------------------------

OpenClaw connects to real messaging surfaces. Treat inbound DMs as **untrusted input**.

Full security guide: Security. Before remote exposure, use the Gateway exposure runbook.

Default behavior on DM-capable channels (Telegram/WhatsApp/Signal/iMessage/Microsoft Teams/Discord/Google Chat/Slack/…):

-   **DM pairing** (`dmPolicy: "pairing"`, e.g. `channels.discord.dmPolicy`): unknown senders receive a short pairing code and the bot does not process their message.
-   Approve with: `openclaw pairing approve <channel> <code>` (then the sender is added to a local allowlist store).
-   Public inbound DMs require an explicit opt-in: set `dmPolicy: "open"` and include `"*"` in the channel allowlist (`allowFrom`, e.g. `channels.discord.allowFrom`).

Run `openclaw doctor` to surface risky/misconfigured DM policies.

### Sandboxing (groups + multi-user surfaces)

-   Default: tools run on the host for the `main` session, so the agent has full access when it is just you.
-   Group/channel safety: set `agents.defaults.sandbox.mode: "non-main"` to run non-`main` sessions inside sandboxes. Docker is the default sandbox backend; SSH and OpenShell backends are also available.
-   Typical sandbox default: allow `bash`, `process`, `read`, `write`, `edit`, and session tools; deny `browser`, `canvas`, `nodes`, `cron`, `gateway`, and channel actions.
-   Before exposing anything remotely, read Security, the Gateway exposure runbook, Sandboxing, and Configuration.

Highlights
----------

-   **Local-first Gateway** — single control plane for sessions, channels, tools, and events.
-   **Multi-channel inbox** — 25+ channels through bundled plugins (see the list above), plus macOS, iOS, and Android nodes.
-   **Multi-agent routing** — route inbound channels/accounts/peers to isolated agents (workspaces + per-agent sessions).
-   **Voice Wake + Talk Mode** — wake words on macOS/iOS and continuous voice on Android (ElevenLabs + system TTS fallback).
-   **Live Canvas** — agent-driven visual workspace with A2UI.
-   **First-class tools** — browser, canvas, nodes, cron, sessions, and Discord/Slack actions.
-   **Companion apps** — Windows Hub, macOS menu bar app, and iOS/Android nodes.
-   **Onboarding + skills** — onboarding-driven setup with bundled/managed/workspace skills.

Operator quick refs
-------------------

-   Chat commands: `/status`, `/new`, `/reset`, `/compact`, `/think <level>`, `/verbose on|off|full`, `/trace on|off|raw`, `/usage off|tokens|full|cost`, `/restart`, `/activation mention|always`
-   Session tools: `sessions_list`, `sessions_history`, `sessions_send`
-   Skills registry: ClawHub
-   Architecture overview: Architecture

Docs by goal
------------

-   New here: Getting started, Onboarding, Updating
-   Channel setup: Channels index, WhatsApp, Telegram, Discord, Slack
-   Apps + nodes: Windows Hub, macOS, iOS, Android, Nodes
-   Config + security: Configuration, Security, Exposure runbook, Sandboxing
-   Remote + web: Gateway, Remote access, Tailscale, Web surfaces
-   Tools + automation: Tools, Skills, Cron jobs, Webhooks, Gmail Pub/Sub
-   Internals: Architecture, Agent, Session model, Gateway protocol
-   Troubleshooting: Channel troubleshooting, Logging, Docs home

Apps (optional)
---------------

The Gateway alone delivers a great experience. All apps are optional and add extra features.

If you plan to build/run companion apps, follow the platform runbooks below.

### macOS (OpenClaw.app) (optional)

-   Menu bar control for the Gateway and health.
-   Voice Wake + push-to-talk overlay.
-   WebChat + debug tools.
-   Remote gateway control over SSH.

Note: signed builds required for macOS permissions to stick across rebuilds (see macOS Permissions).

### iOS node (optional)

-   Pairs as a node over the Gateway WebSocket (device pairing).
-   Voice trigger forwarding + Canvas surface.
-   Controlled via `openclaw nodes …`.

Runbook: iOS connect.

### Android node (optional)

-   Pairs as a WS node via device pairing (`openclaw devices ...`).
-   Exposes Connect/Chat/Voice tabs plus Canvas, Camera, Screen capture, and Android device command families.
-   Runbook: Android connect.

From source (development)
-------------------------

Use `pnpm` for source checkouts. The repository is a pnpm workspace, and bundled plugins load from `extensions/*` during development so their package-local dependencies and your edits are used directly. Plain `npm install` at the repo root is not a supported source setup.

For the dev loop:

git clone https://github.com/openclaw/openclaw.git
cd openclaw

pnpm install

# First run only (or after resetting local OpenClaw config/workspace)
pnpm openclaw setup

# Optional: prebuild Control UI before first startup
pnpm ui:build

# Dev loop (auto-reload on source/config changes)
pnpm gateway:watch

If you need a built `dist/` from the checkout (for Node, packaging, or release validation), run:

pnpm build
pnpm ui:build

`pnpm openclaw setup` writes the local config/workspace needed for `pnpm gateway:watch`. It is safe to re-run, but you normally only need it on first setup or after resetting local state. `pnpm gateway:watch` hands the configured Gateway port from the installed service to a durable tmux pane; run `pnpm openclaw gateway start` when you want the installed service back. It does not rebuild `dist/control-ui`, so rerun `pnpm ui:build` after `ui/` changes or use `pnpm ui:dev` when iterating on the Control UI. If you want this checkout to run onboarding directly, use `pnpm openclaw onboard --install-daemon`.

Note: `pnpm openclaw ...` runs TypeScript directly (via `tsx`). `pnpm build` produces `dist/` for running via Node / the packaged `openclaw` binary, while `pnpm gateway:watch` rebuilds the runtime on demand during the dev loop.

Release channels
----------------

-   **stable**: tagged releases (`vYYYY.M.PATCH` — `PATCH` is a sequential release number, not the calendar day), npm dist-tag `latest`.
-   **extended-stable**: the trailing supported month's maintenance releases, npm dist-tag `extended-stable`.
-   **beta**: prerelease tags (`vYYYY.M.PATCH-beta.N`), npm dist-tag `beta` (macOS app may be missing).
-   **dev**: moving head of `main`, npm dist-tag `dev` (when published).

Switch channels (git + npm): `openclaw update --channel stable|extended-stable|beta|dev`. Details: Release channels.

Agent workspace + skills
------------------------

-   Workspace root: `~/.openclaw/workspace` (configurable via `agents.defaults.workspace`).
-   Injected prompt files: `AGENTS.md`, `SOUL.md`, and other workspace context files.
-   Skills: `~/.openclaw/workspace/skills/<skill>/SKILL.md`.

Configuration
-------------

Minimal `~/.openclaw/openclaw.json` (model + defaults):

{
  agents: {
    defaults: {
      model: "<provider>/<model-id>",
    },
  },
}

Full configuration reference (all keys + examples).

Star History
------------

View OpenClaw's star history.

Molty
-----

OpenClaw was built for **Molty**, a space lobster AI assistant, by Peter Steinberger and the community. 🦞

-   openclaw.ai
-   soul.md
-   steipete.me
-   @openclaw

Community
---------

See CONTRIBUTING.md for guidelines, maintainers, and how to submit PRs. Use the issue chooser for bugs, docs bugs, and feature requests; ask setup/support questions in Discord; and report vulnerabilities through SECURITY.md. Most new features fit best as plugins built on the plugin SDK and shared via ClawHub, keeping core lean. PRs should link the relevant issue when possible and follow the PR template with problem, impact, and evidence. AI/vibe-coded PRs welcome! 🤖

Special thanks to Mario Zechner for his support and for pi. Special thanks to Adam Doppelt for the lobster.bot domain.

Thanks to all clawtributors:
