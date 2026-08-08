---
project: openclaw
stars: 385567
description: Your own personal AI assistant. Any OS. Any Platform. The lobster way. 🦞 
url: https://github.com/openclaw/openclaw
---

OpenClaw 🦞 — Your assistant, on your devices, in your chats
============================================================

OpenClaw is a personal AI assistant that runs on your devices and meets you in the channels you already use. It is designed for a single operator and connects models, tools, messaging channels, and optional companion apps through one Gateway.

Website · Docs · Getting started · Showcase · FAQ · Vision · DeepWiki

Install
-------

The installer supports macOS, Linux, and Windows. It provisions a supported Node.js runtime when needed.

# macOS / Linux / WSL2
curl -fsSL https://openclaw.ai/install.sh | bash

# Windows PowerShell
iwr \-useb https://openclaw.ai/install.ps1 | iex

Already manage Node.js? Install the published package instead (Node 22.22.3+, 24.15+, or 25.9+):

npm install -g openclaw@latest

See the installation guide for npm 12 lifecycle-script requirements, Docker, Nix, and other deployment paths.

Quick start
-----------

openclaw onboard --install-daemon
openclaw gateway status
openclaw dashboard

Onboarding verifies model access, creates the workspace, and configures the Gateway. The last command opens the Control UI; send a message there to confirm the assistant is working. See the getting started guide for channel setup and troubleshooting.

How it fits together
--------------------

-   The Gateway is the local control plane for sessions, tools, events, and channel connections.
-   The Control UI, CLI, and TUI connect to the Gateway.
-   Channels bring the assistant to WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, and other messaging services.
-   Companion apps and nodes add voice, Canvas, camera, screen, and device-local actions on supported platforms.

OpenClaw works with hosted and local model providers. Its tools, skills, and plugins extend what an assistant can do.

Security
--------

Treat inbound messages as untrusted input. DM-capable channels pair unknown senders by default; approve a pairing request with `openclaw pairing approve <channel> <code>`.

Tools run on the host for the main session unless you configure sandboxing. Read the security guide, exposure runbook, and sandboxing guide before connecting other users or exposing the Gateway remotely.

Documentation
-------------

Goal

Start here

Configure models and auth

Models · Model providers

Connect a messaging service

Channels

Add tools, skills, and plugins

Tools · Skills · Plugins · ClawHub

Run apps and device nodes

Platforms · Nodes

Use the CLI and chat commands

CLI reference · Slash commands

Configure or operate the Gateway

Configuration · Architecture · Updating · Release channels

Development
-----------

The repository is a pnpm workspace. Plain `npm install` at the repository root is not supported.

git clone https://github.com/openclaw/openclaw.git
cd openclaw
pnpm install
pnpm build
pnpm ui:build

See CONTRIBUTING.md for the contribution workflow and the source setup guide for the development loop.

Community
---------

OpenClaw is developed in the open by the OpenClaw Foundation, a non-profit. See CONTRIBUTING.md for maintainers and contribution guidelines; AI-assisted PRs are welcome.

Use the issue chooser for bugs and feature requests, ask setup questions in Discord, and report vulnerabilities through SECURITY.md. New capabilities usually belong in plugins built on the plugin SDK and shared through ClawHub.

OpenClaw was built for **Molty**, a space lobster AI assistant, by Peter Steinberger and the community. Explore the project lore, soul.md, Peter's site, Star History, and @openclaw.

Special thanks to Mario Zechner for his support and for pi, and to Adam Doppelt for the lobster.bot domain.

Sponsors
--------

Contributors
------------

Thanks to all clawtributors:

License
-------

MIT © OpenClaw Foundation. See THIRD\_PARTY\_NOTICES.md for incorporated or adapted code.
