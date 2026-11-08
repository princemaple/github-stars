---
project: lobehub
stars: 84343
description: 🤯 LobeHub - Super-Agents on Your Team. Add super-agents to the chats your team already uses.They take on work by themselves and get better every week.
url: https://github.com/lobehub/lobehub
---

LobeHub
=======

**Super-Agents on Your Team**

Add super-agents to the chats your team already uses.  
They take on work by themselves and get better every week.

**English** · 简体中文 · Official Site · Changelog · Documents · Blog · Feedback

  
  
  

**Share LobeHub Repository**

Table of contents

#### TOC

-   👋🏻 Getting Started & Join Our Community
-   ✨ Features
    -   From new hire to one of the team
    -   `Day 1` Welcome to the team
    -   `Week 1` Its first task
    -   `Month 1–2` Settling in as the team grows
    -   `Month 3` It passes its review
    -   Bring them onto your team
-   🧩 Marketplace
-   📖 Documentation
-   🛳 Self Hosting
    -   `A` Docker Compose (recommended)
    -   `B` One-click deploy
-   ⌨️ Local Development
-   🤝 Contributing
-   ❤️ Sponsor
-   🔬 Research

  
  
lobehub-cao.webm

👋🏻 Getting Started & Join Our Community
-----------------------------------------

We are a group of e/acc design-engineers, hoping to provide modern design components and tools for AIGC.

Whether for users or professional developers, LobeHub will be your AI Agent playground. Please be aware that LobeHub is currently under active development, and feedback is welcome for any issues encountered.

We are live on Product Hunt! We are thrilled to bring LobeHub to the world. If you believe in a future where humans and agents co-evolve, please support our journey.

Join our Discord community! This is where you can connect with developers and other enthusiastic users of LobeHub.

Important

**Star Us**, You will receive all release notifications from GitHub without any delay ~ ⭐️

Star History

✨ Features
----------

### From new hire to one of the team

See what Lobe AI gets done, from its first day in your team chat onward.

WHAT MAKES A SUPER-AGENT

**🔌 Flexible access**  
Plug in any IM app, agent or model, all in one place.

**⚡ Parallel work**  
Runs several tasks at once, so you don't have to chase each one.

**🙋 Finds its own work**  
Takes on the tasks that suit it, without someone passing messages along.

**📈 Gets more expert**  
The more you use it, the faster an agent builds up its expertise.

### `Day 1` Welcome to the team

You add it to your team chat and ask it to read up. By lunch it has gone through the history and said hello to everyone.

### `Week 1` Its first task

Someone posts a feature request in Discord and nobody assigns it. Lobe AI takes it on, and you only step in once, to accept the result.

### `Month 1–2` Settling in as the team grows

Everyone now has their own agent, and design, releases and docs each have a dedicated one. Lobe AI is still learning when to speak up and when to stay quiet.

### `Month 3` It passes its review

When it started, it got about half of these right. Now it rarely misses, and every correction you gave it has become a lesson it keeps.

### Bring them onto your team

Start with one, and add more when you need them.

**Try LobeHub Cloud** · **Self-host it**

🧩 Marketplace
--------------

Find agents, MCP servers and skills on lobehub.com, add them to your workspace, or publish your own.

Market

What you'll find

**🤖 Agents**

Ready-to-use agents for writing, Q&A, images, video, voice and workflows. Add one to your workspace and adapt it.

**🔌 MCP Servers**

MCP servers rated on activity, stability and community feedback, so you can pick ones you can trust.

**🧠 Skills**

Agent skills in the open `SKILL.md` format. They also work in Claude Code, Codex CLI and ChatGPT.

**🎨 AI / LLM Icons**

A free icon set for major AI brands and models, with SVG, PNG and vector downloads.

**Publish your own**

-   **Agents**: submit one from its settings in LobeHub. The Creator Reward Program features a community agent every two weeks.
    
-   **MCP servers**: ask your agent to `Read https://lobehub.com/publish-mcp/skill.md and follow the instructions to publish my MCP server to the LobeHub Marketplace`, or use the CLI:
    
    npx -y @lobehub/market-cli login
    npx -y @lobehub/market-cli plugin submit https://github.com/OWNER/REPOSITORY
    
-   **Skills**: submit a GitHub repository from the Skills marketplace.
    

📖 Documentation
----------------

All documentation lives at lobehub.com/docs:

Section

What's covered

Get LobeHub

Web, macOS, Windows, Linux and mobile apps, and where work runs

Lobe AI

The built-in agent: chat, code, research and write with no setup

Agents

System role, model, skills, connectors, web search, resources and memory

Agent Team

Several agents working together: sequential, parallel, iterative or debate

Connect External Agents

Bring in Claude Code, Codex, OpenClaw, Hermes and more, with project context and permissions

Tasks

Delegate work, track status, follow up in comments, run once or on a schedule

Memory

Structured memories you can review, edit and delete

Pages

Write long documents with agents, in Markdown

Resource Library

Documents, generated images and drafts your agents can answer from

Channels

Your own bots on Discord, Slack, Telegram, LINE, QQ, WeChat, Feishu and Lark

Messenger

Chat with your agents through LobeHub's bot on Telegram, Slack, Discord and WeChat

GitHub Integration

Track agents' pull requests; merging accepts the work, failed checks go back to the agent

Marketplace

Community agents, MCP servers and skills

Model Providers

Setup guides for 40+ providers, inference platforms and local models

Self-Hosting

Docker Compose, Vercel and other deployment platforms

Environment Variables

Every configuration option, including model providers

Authentication

Sign-in with Better Auth and SSO providers such as Auth0

Development

Tech stack, local setup and contribution guidelines

🛳 Self Hosting
---------------

Run LobeHub on your own infrastructure and keep your data with you. The full guide is in 📘 Build your own LobeHub.

### `A` Docker Compose (recommended)

Starts LobeHub with PostgreSQL, Redis, RustFS file storage, SearXNG search and the agent gateway. Runs on Linux and macOS, or on Windows through WSL 2.

mkdir lobehub && cd lobehub
bash <(curl -fsSL https://lobe.li/setup.sh) -l en
docker compose up -d

Then open http://localhost:3210. Ports, LAN and domain modes, and upgrades are covered in the 📘 Docker Compose guide.

### `B` One-click deploy

Vercel needs a PostgreSQL database, S3-compatible storage and a few secrets before you deploy. The 📘 Vercel guide walks through each one.

Deploy with Vercel

Deploy with Zeabur

Deploy with Sealos

Deploy with RepoCloud

Deploy with Alibaba Cloud

⌨️ Local Development
--------------------

You can use GitHub Codespaces for online development:

Or clone it for local development:

$ git clone https://github.com/lobehub/lobehub.git
$ cd lobehub
$ pnpm install
$ bun run dev       # Full-stack (Next.js + Vite SPA)
$ bun run dev:spa   # SPA frontend only (port 9876)

> **Debug Proxy**: After running `dev:spa`, the terminal prints a proxy URL like `https://app.lobehub.com/_dangerous_local_dev_proxy?debug-host=http%3A%2F%2Flocalhost%3A9876`. Open it to develop locally against the production backend with HMR — a development convenience, not a place to verify a change.

If you would like to learn more details, please feel free to look at our 📘 Development Guide.

🤝 Contributing
---------------

Contributions of all types are more than welcome; if you are interested in contributing code, feel free to check out our GitHub Issues and Projects to get stuck in to show us what you're made of.

Tip

We are creating a technology-driven forum, fostering knowledge interaction and the exchange of ideas that may culminate in mutual inspiration and collaborative innovation.

Help us make LobeHub better. Welcome to provide product design feedback, user experience discussions directly to us.

**Principal Maintainers:** @arvinxx @canisminor1990

  
  
  

❤️ Sponsor
----------

Every bit counts and your one-time donation sparkles in our galaxy of support! You're a shooting star, making a swift and bright impact on our journey. Thank you for believing in us – your generosity guides us toward our mission, one brilliant flash at a time.

🔬 Research
-----------

-   **📊 MCPMark:** A stress-testing benchmark for MCP. Its tasks are realistic, multi-step and verifiable, covering file systems, databases, Playwright browser automation, GitHub and more. Built by EVAL SYS, LobeHub and the National University of Singapore, and open source under Apache-2.0.
-   **📄 Research paper:** Read our research paper on Hugging Face Papers.
-   **🧪 EVAL SYS:** An evaluation systems organization, one of the teams behind MCPMark.

* * *

#### 📝 License

Copyright © 2026 LobeHub.  
This project is LobeHub Community License licensed.
