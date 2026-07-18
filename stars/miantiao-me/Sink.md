---
project: Sink
stars: 6953
description: ⚡ A Simple / Speedy / Secure Link Shortener with Analytics, 100% run on Cloudflare.
url: https://github.com/miantiao-me/Sink
---

⚡ Sink
======

**A Simple / Speedy / Secure Link Shortener with Analytics, 100% run on Cloudflare.**

Website · Documentation · API Reference

* * *

✨ Features
----------

-   **🔗 URL Shortening:** Compress your URLs to their minimal length.
-   **📈 Analytics:** Monitor link analytics and gather insightful statistics.
-   **☁️ Serverless:** Deploy without the need for traditional servers.
-   **🎨 Customizable Slug:** Support personalized slugs, UTM parameters, and optional case-sensitive slug matching through configuration.
-   **🪄 AI Assistance:** Optionally use Cloudflare Workers AI to generate slugs and OpenGraph metadata from page content.
-   **⏰ Link Control:** Set expirations, passwords, and unsafe-link warning pages.
-   **📱 Smart Routing:** Redirect visitors by device or country.
-   **🖼️ Social Preview:** Customize social previews with titles, descriptions, and images.
-   **📊 Near-real-time Analytics:** Display a live 3D globe and event logs using 10-second analytics polling and client-side replay, not SSE or WebSocket.
-   **🔲 QR Code:** Generate QR codes for your short links.
-   **📦 Import/Export:** Transfer links via JSON and export access analytics via CSV.
-   **🌍 Multi-language:** Full i18n support for dashboard and redirect pages.

Tip

**Who is Sink for?**

Sink focuses on **individuals and small teams** who want a simple, self-hosted shortener on Cloudflare.

For professional / business needs (managed service, multi-user, SLA, and more), use **S.EE**.

🪧 Demo
-------

Experience the demo at Sink.Cool. Log in using the Site Token below:

Site Token: SinkCool

**Screenshots**

🧱 Technologies Used
--------------------

-   **Framework**: Nuxt 4
-   **Database**: Cloudflare D1 is the authoritative link store; Workers KV is a write-through read cache
-   **ORM**: Drizzle ORM
-   **Analytics Engine**: Cloudflare Workers Analytics Engine
-   **Object Storage**: Cloudflare R2 for optional logical JSON snapshots
-   **AI**: Optional Cloudflare Workers AI
-   **UI Components**: shadcn-vue
-   **Styling:** Tailwind CSS
-   **Deployment**: Cloudflare

🚗 Roadmap \[WIP\]
------------------

We welcome your contributions and PRs.

-   Browser Extension - Sink Tool
-   Chrome Extension - Sink Quick Shorten
-   Raycast Extension - Raycast-Sink
-   Apple Shortcuts - Sink Shortcuts
-   iOS App - Sink
-   Enhanced Link Management (with Cloudflare D1)
-   Analytics Enhancements (Multi-link filtering)
-   Dashboard Performance Optimization (Infinite loading)
-   API, migration, backup, and redirect tests

🏗️ Deployment
--------------

> Video tutorial: Watch here

We currently support deployment to Cloudflare Workers (recommended) and Cloudflare Pages.

⚒️ Configuration
----------------

Configuration Docs

🔌 API
------

API Docs · Live Scalar Reference for the public demo instance

🤖 AI Skills
------------

Install Sink AI Skills for enhanced coding assistance:

npx skills add miantiao-me/sink

🧰 MCP
------

We currently do not support native MCP Server, but we have OpenAPI documentation, and you can use the following method to support MCP.

> Replace the domain name in `OPENAPI_SPEC_URL` and the `API_KEY` below with your own instance configuration.
> 
> The `API_KEY` is the same as the `NUXT_SITE_TOKEN` in your instance's environment variables.

{
  "mcpServers": {
    "sink": {
      "command": "uvx",
      "args": \[
        "mcp-openapi-proxy"
      \],
      "env": {
        "OPENAPI\_SPEC\_URL": "https://sink.cool/\_docs/openapi.json",
        "API\_KEY": "SinkCool",
        "TOOL\_WHITELIST": "/api/link"
      }
    }
  }
}

🙋🏻 FAQs
---------

FAQs

💖 Credits
----------

1.  **Cloudflare**
2.  **NuxtHub**
3.  **Astroship**
4.  **Tailark**

☕ Sponsor
---------

1.  Follow Me on X(Twitter).
2.  Become a sponsor to on GitHub.
