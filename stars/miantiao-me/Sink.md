---
project: Sink
stars: 7195
description: ⚡ A Simple, Speedy, Secure, and Serverless Link Shortener with Analytics, Running Entirely on Cloudflare.
url: https://github.com/miantiao-me/Sink
---

⚡ Sink
======

**A Simple, Speedy, Secure, and Serverless Link Shortener with Analytics, Running Entirely on Cloudflare.**

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

🔀 Sibling versions
-------------------

Sink and Slite are sibling versions of the same link-management and analytics project. Sink runs on Cloudflare's serverless platform, while Slite runs as a local Node.js 24+/Docker process. They keep features, API contracts, and file organization compatible with each other wherever practical. Neither version is a legacy branch, and Slite is not a fork replacement for Sink.

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

We currently support deployment to Cloudflare Workers (recommended) and Cloudflare Pages (deprecated).

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

Sink serves a built-in MCP endpoint at `POST /api/mcp`, using the official `@modelcontextprotocol/server` SDK v2, serving modern clients over the per-request transport and 2025-era clients over a stateless fallback with JSON responses.

> Replace the domain below with your own instance, and use the `NUXT_SITE_TOKEN` from your instance's environment variables as the bearer token.

claude mcp add --transport http sink https://sink.cool/api/mcp --header "Authorization: Bearer SinkCool"

Any client that supports an HTTP transport with custom headers can connect the same way:

{
  "mcpServers": {
    "sink": {
      "type": "http",
      "url": "https://sink.cool/api/mcp",
      "headers": {
        "Authorization": "Bearer SinkCool"
      }
    }
  }
}

It exposes tools for managing links (list, search, read, count, tag, create, update, upsert, delete) and for reading analytics (counters, views over time, and top values per dimension). See the integrations documentation for the full list.

🙋🏻 FAQs
---------

FAQs

💖 Credits
----------

1.  **Cloudflare**
2.  **NuxtHub**
3.  **Astroship**
4.  **Tailark**

📄 License
----------

AGPL-3.0-only © miantiao-me

☕ Sponsor
---------

1.  Follow Me on X (Twitter).
2.  Become a sponsor on GitHub.
