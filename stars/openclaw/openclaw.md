---
project: openclaw
stars: 367561
description: Your own personal AI assistant. Any OS. Any Platform. The lobster way. 🦞 
url: https://github.com/openclaw/openclaw
---

🦞 OpenClaw — Personal AI Assistant
===================================

**EXFOLIATE! EXFOLIATE!**

**OpenClaw** is a _personal AI assistant_ you run on your own devices. It answers you on the channels you already use. It can speak and listen on macOS/iOS/Android, and can render a live Canvas you control. The Gateway is just the control plane — the product is the assistant.

If you want a personal, single-user assistant that feels local, fast, and always-on, this is it.

Supported channels include: WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, BlueBubbles, IRC, Microsoft Teams, Matrix, Feishu, LINE, Mattermost, Nextcloud Talk, Nostr, Synology Chat, Tlon, Twitch, Zalo, Zalo Personal, WeChat, QQ, WebChat.

Website · Docs · Vision · DeepWiki · Getting Started · Updating · Showcase · FAQ · Onboarding · Nix · Docker · Discord

New install? Start here: Getting started

Preferred setup: run `openclaw onboard` in your terminal. OpenClaw Onboard guides you step by step through setting up the gateway, workspace, channels, and skills. It is the recommended CLI setup path and works on **macOS, Linux, and Windows (via WSL2; strongly recommended)**. Works with npm, pnpm, or bun.

Sponsors
--------

**Subscriptions (OAuth):**

-   **OpenAI** (ChatGPT/Codex)

Model note: while many providers and models are supported, prefer a current flagship model from the provider you trust and already use. See Onboarding.

Install (recommended)
---------------------

Runtime: **Node 24 (recommended) or Node 22.14+**.

npm install -g openclaw@latest
# or: pnpm add -g openclaw@latest

openclaw onboard --install-daemon

OpenClaw Onboard installs the Gateway daemon (launchd/systemd user service) so it stays running.

Quick start (TL;DR)
-------------------

Runtime: **Node 24 (recommended) or Node 22.14+**.

Full beginner guide (auth, pairing, channels): Getting started

openclaw onboard --install-daemon

openclaw gateway --port 18789 --verbose

# Send a message
openclaw message send --target +1234567890 --message "Hello from OpenClaw"

# Talk to the assistant (optionally deliver back to any connected channel: WhatsApp/Telegram/Slack/Discord/Google Chat/Signal/iMessage/BlueBubbles/IRC/Microsoft Teams/Matrix/Feishu/LINE/Mattermost/Nextcloud Talk/Nostr/Synology Chat/Tlon/Twitch/Zalo/Zalo Personal/WeChat/QQ/WebChat)
openclaw agent --message "Ship checklist" --thinking high

Upgrading? Updating guide (and run `openclaw doctor`).

Models config + CLI: Models. Auth profile rotation + fallbacks: Model failover.

Security defaults (DM access)
-----------------------------

OpenClaw connects to real messaging surfaces. Treat inbound DMs as **untrusted input**.

Full security guide: Security

Default behavior on Telegram/WhatsApp/Signal/iMessage/Microsoft Teams/Discord/Google Chat/Slack:

-   **DM pairing** (`dmPolicy="pairing"` / `channels.discord.dmPolicy="pairing"` / `channels.slack.dmPolicy="pairing"`; legacy: `channels.discord.dm.policy`, `channels.slack.dm.policy`): unknown senders receive a short pairing code and the bot does not process their message.
-   Approve with: `openclaw pairing approve <channel> <code>` (then the sender is added to a local allowlist store).
-   Public inbound DMs require an explicit opt-in: set `dmPolicy="open"` and include `"*"` in the channel allowlist (`allowFrom` / `channels.discord.allowFrom` / `channels.slack.allowFrom`; legacy: `channels.discord.dm.allowFrom`, `channels.slack.dm.allowFrom`).

Run `openclaw doctor` to surface risky/misconfigured DM policies.

Highlights
----------

-   **Local-first Gateway** — single control plane for sessions, channels, tools, and events.
-   **Multi-channel inbox** — WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, BlueBubbles (iMessage), iMessage (legacy), IRC, Microsoft Teams, Matrix, Feishu, LINE, Mattermost, Nextcloud Talk, Nostr, Synology Chat, Tlon, Twitch, Zalo, Zalo Personal, WeChat, QQ, WebChat, macOS, iOS/Android.
-   **Multi-agent routing** — route inbound channels/accounts/peers to isolated agents (workspaces + per-agent sessions).
-   **Voice Wake + Talk Mode** — wake words on macOS/iOS and continuous voice on Android (ElevenLabs + system TTS fallback).
-   **Live Canvas** — agent-driven visual workspace with A2UI.
-   **First-class tools** — browser, canvas, nodes, cron, sessions, and Discord/Slack actions.
-   **Companion apps** — macOS menu bar app + iOS/Android nodes.
-   **Onboarding + skills** — onboarding-driven setup with bundled/managed/workspace skills.

Security model (important)
--------------------------

-   Default: tools run on the host for the `main` session, so the agent has full access when it is just you.
-   Group/channel safety: set `agents.defaults.sandbox.mode: "non-main"` to run non-`main` sessions inside sandboxes. Docker is the default sandbox backend; SSH and OpenShell backends are also available.
-   Typical sandbox default: allow `bash`, `process`, `read`, `write`, `edit`, `sessions_list`, `sessions_history`, `sessions_send`, `sessions_spawn`; deny `browser`, `canvas`, `nodes`, `cron`, `discord`, `gateway`.
-   Before exposing anything remotely, read Security, Sandboxing, and Configuration.

Operator quick refs
-------------------

-   Chat commands: `/status`, `/new`, `/reset`, `/compact`, `/think <level>`, `/verbose on|off`, `/trace on|off`, `/usage off|tokens|full`, `/restart`, `/activation mention|always`
-   Session tools: `sessions_list`, `sessions_history`, `sessions_send`
-   Skills registry: ClawHub
-   Architecture overview: Architecture

Docs by goal
------------

-   New here: Getting started, Onboarding, Updating
-   Channel setup: Channels index, WhatsApp, Telegram, Discord, Slack
-   Apps + nodes: macOS, iOS, Android, Nodes
-   Config + security: Configuration, Security, Sandboxing
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

`pnpm openclaw setup` writes the local config/workspace needed for `pnpm gateway:watch`. It is safe to re-run, but you normally only need it on first setup or after resetting local state. `pnpm gateway:watch` does not rebuild `dist/control-ui`, so rerun `pnpm ui:build` after `ui/` changes or use `pnpm ui:dev` when iterating on the Control UI. If you want this checkout to run onboarding directly, use `pnpm openclaw onboard --install-daemon`.

Note: `pnpm openclaw ...` runs TypeScript directly (via `tsx`). `pnpm build` produces `dist/` for running via Node / the packaged `openclaw` binary, while `pnpm gateway:watch` rebuilds the runtime on demand during the dev loop.

Development channels
--------------------

-   **stable**: tagged releases (`vYYYY.M.D` or `vYYYY.M.D-<patch>`), npm dist-tag `latest`.
-   **beta**: prerelease tags (`vYYYY.M.D-beta.N`), npm dist-tag `beta` (macOS app may be missing).
-   **dev**: moving head of `main`, npm dist-tag `dev` (when published).

Switch channels (git + npm): `openclaw update --channel stable|beta|dev`. Details: Development channels.

Agent workspace + skills
------------------------

-   Workspace root: `~/.openclaw/workspace` (configurable via `agents.defaults.workspace`).
-   Injected prompt files: `AGENTS.md`, `SOUL.md`, `TOOLS.md`.
-   Skills: `~/.openclaw/workspace/skills/<skill>/SKILL.md`.

Configuration
-------------

Minimal `~/.openclaw/openclaw.json` (model + defaults):

{
  agent: {
    model: "<provider>/<model-id>",
  },
}

Full configuration reference (all keys + examples).

Star History
------------

Molty
-----

OpenClaw was built for **Molty**, a space lobster AI assistant. 🦞 by Peter Steinberger and the community.

-   openclaw.ai
-   soul.md
-   steipete.me
-   @openclaw

Community
---------

See CONTRIBUTING.md for guidelines, maintainers, and how to submit PRs. AI/vibe-coded PRs welcome! 🤖

Special thanks to Mario Zechner for his support and for pi-mono. Special thanks to Adam Doppelt for the lobster.bot domain.

Thanks to all clawtributors:
