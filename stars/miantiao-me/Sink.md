---
project: Sink
stars: 5954
description: ⚡ A Simple / Speedy / Secure Link Shortener with Analytics, 100% run on Cloudflare.
url: https://github.com/miantiao-me/Sink
---

⚡ Sink
======

**A Simple / Speedy / Secure Link Shortener with Analytics, 100% run on Cloudflare.**

* * *

✨ Features
----------

-   **URL Shortening:** Compress your URLs to their minimal length.
-   **Analytics:** Monitor link analytics and gather insightful statistics.
-   **Serverless:** Deploy without the need for traditional servers.
-   **Customizable Slug:** Support for personalized slugs and case sensitivity.
-   **🪄 AI Slug:** Leverage AI to generate slugs.
-   **Link Expiration:** Set expiration dates for your links.

🪧 Demo
-------

Experience the demo at Sink.Cool. Log in using the Site Token below:

Site Token: SinkCool

**Screenshots**

🧱 Technologies Used
--------------------

-   **Framework**: Nuxt
-   **Database**: Cloudflare Workers KV
-   **Analytics Engine**: Cloudflare Workers Analytics Engine
-   **UI Components**: shadcn-vue
-   **Styling:** Tailwind CSS
-   **Deployment**: Cloudflare

🚗 Roadmap \[WIP\]
------------------

We welcome your contributions and PRs.

-   Browser Extension - Sink Tool
-   Raycast Extension - Raycast-Sink
-   Apple Shortcuts - Sink Shortcuts
-   iOS App - Sink
-   Enhanced Link Management (with Cloudflare D1)
-   Analytics Enhancements (Support for merging filter conditions)
-   Dashboard Performance Optimization (Infinite loading)
-   Units Test

🏗️ Deployment
--------------

> Video tutorial: Watch here

We currently support deployment to Cloudflare Workers (recommended) and Cloudflare Pages.

⚒️ Configuration
----------------

Configuration Docs

🔌 API
------

API Docs

🧰 MCP
------

We currently do not support native MCP Server, but we have OpenAPI documentation, and you can use the following method to support MCP.

> Replace the domain name in `OPENAPI_SPEC_URL` with your own domain name.
> 
> The `API_KEY` is the same as the `NUXT_SITE_TOKEN` in the environment variables.

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
        "TOOL\_WHITELIST": "/api/link/create"
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

☕ Sponsor
---------

1.  Follow Me on X(Twitter).
2.  Become a sponsor to on GitHub.
