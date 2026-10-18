---
project: happy
stars: 24195
description: Orchestrate Claude, Codex and Grok in one app. Open-source (MIT), reuses the subscriptions you already pay for.
url: https://github.com/slopus/happy
---

Any Model. Your Subscription.  
_Happy Harness._
================================================

Orchestrate Claude, Codex and Grok in one app

Free and open source

readme-demo.mp4

   

What you get
------------

1.  **Multi-provider.** Astra, Fable, and Grok in one app, each with its vendor's own prompts and tools. Give every task the model that fits, and delegate to subagents on any of them.
2.  **Reuse your subscriptions.** Sign in with the Claude, Codex, and Grok subscriptions you already pay for. Happy adds a harness, not another bill.
3.  **Open source MIT.** It runs on your own hardware and your projects stay ordinary folders. Read the code, fork it, ship your own build.
4.  **End-to-end encrypted mobile app.** Left your desk? The same sessions are already on your phone, and what moves between your devices is encrypted.
5.  **Natively multiplayer.** Invite a colleague or a friend into the session. You both watch the same agent work, and either of you can steer it.

#### Resources

Website · Documentation · Discord · Development guide · MIT License

How Happy fits together
-----------------------

Repository

What it is

**slopus/happy** ← this repository

**The mobile app (iOS, Android, web), the original CLI, and the relay server**

slopus/happy-desktop

The desktop app for macOS, Windows, and Linux

slopus/happy-agent

Happy Agent, the open-source agent runtime the desktop app runs on

slopus/slopus.github.io

The website and docs at happy.engineering

Original Happy CLI
------------------

The original CLI wraps the Claude Code and Codex harnesses directly in your terminal and lets you continue from your phone.

For multi-model sessions and teams, move to the desktop app and Happy Harness.

npm install -g happy

# Start Claude Code
happy claude

# Or start Codex
happy codex

-   happy-app: the Happy mobile app and web client (Expo)
-   happy-cli: the original Happy CLI (`happy` on npm)
-   happy-agent: remote session control for the original Happy CLI (not the Happy Agent runtime)
-   happy-server: the relay server for encrypted sync

Migrated from the `happy-coder` package. Thanks to @franciscop for donating the `happy` package name!
