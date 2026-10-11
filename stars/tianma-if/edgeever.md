---
project: edgeever
stars: 2181
description: Open-source, AI-native knowledge base & Evernote alternative with native MCP. Zero-cost on Cloudflare or Docker.
url: https://github.com/tianma-if/edgeever
---

EdgeEver
========

**An open-source, AI-native knowledge base & portable Evernote alternative**

简体中文 | 繁體中文 | **English** | 日本語 | Polski

Telegram Group  |  🌐 Live Demo  |  📱 Client Downloads  |  Key Features & Workflows

EdgeEver is a modern, open-source notes and knowledge base workspace. It revives the beloved Evernote-style three-pane layout while offering an open data architecture and seamless AI Agent integration for complete ownership and smart productivity.

> 💡 **Serverless & 100% Free Forever** EdgeEver can run within Cloudflare's free quotas with no server purchase or VPS maintenance. Users who prefer a VPS, NAS, or home server can deploy the same application with Docker.

> ⭐ If EdgeEver is useful to you, consider giving it a Star. Your support helps more people discover the project.

Why EdgeEver
------------

Many long-time **Evernote** users simply want a **reliable, open, and fast** personal knowledge base. However, existing mainstream solutions all present tradeoffs:

-   **Evernote**: A tool that accompanied the author for nearly a decade and holds the deepest affection. Yet as it evolved into a full-featured commercial suite, ads and add-ons multiplied while system overhead climbed. Meanwhile, free-tier quotas tightened, premium AI subscriptions grew expensive, and it remains difficult to integrate into modern self-hosted and private AI workflows.
-   **Obsidian**: Open files, closed-source core. Official Sync is paid and third-party sync is tedious; relying entirely on flat local file scanning causes noticeable cold-start and search lag once notes reach thousands or heavy plugins are loaded; storing images and attachments alongside notes quickly bloats vaults, making mobile sync sluggish and leaving orphaned files behind; and it is overly heavy for lightweight, capture-anywhere use.
-   **Memos & Stream Notes**: Clean and simple, but their social-timeline layouts differ fundamentally from the structured productivity of a classic three-pane workflow.
-   **SiYuan & Block-based PKMs**: Powerful with self-hosting support, but their granular "block-level" architecture imposes noticeable cognitive overhead for quick daily capture and continuous prose writing. Furthermore, they lack a true zero-cost serverless deployment tier, and multi-device sync relies on paid official subscriptions or paying extra to unlock S3/WebDAV sync features with your own storage.

**EdgeEver fills this gap**: The entire stack is open source, including sync and self-hosting. It keeps the three-pane layout you know, stays silky-smooth and lightweight even with 10,000+ notes, and ships native AI agents with zero-cost deployment.

Online Demo
-----------

-   Demo: https://demo.edgeever.org

The public demo resets every day at 3:00 AM (China Standard Time) and restores sample notes. Do not store private content there.

Client Downloads
----------------

           

> The iOS app requires an Apple ID from outside mainland China.

Key Features & Workflows
------------------------

From multi-channel inspiration capture to deep visual expression and team collaboration, EdgeEver delivers frictionless, end-to-end workflows:

### Universal Clipping & Media Storage

-   **Cross-Platform One-Click Clipping**: Browser extension clips Xiaohongshu galleries, X (Twitter) posts & quotes, Zhihu Q&As, Reddit discussions, and GitHub repositories (deep adaptation for more platforms coming soon); one-click mobile system share clipping for photos and WeChat articles.
-   **WeChat Chat History Archiving**: One-click complete transcript import on macOS via WeChat "Forward to Other Apps → EdgeEver", preserving participants, timestamps, quoted replies, and stickers, with images embedded and audio/video files saved as note attachments. See One-Click WeChat Chat History Archiving.
-   **Universal File Attachments & Client-Side Image Compression**: Easily upload and attach PDFs, Office documents, archives, and multimedia files, safely handling up to 1 GiB attachments via chunked streaming; silent client-side image compression in the browser reduces screenshots and large images by 50%-90% for faster loading and minimal storage use.

### Intelligent Visual Notes & Database Collaboration

-   **Visual Diagram Notes & Professional Infographics**: Ditch external diagramming tools—prompt the companion AI assistant to generate interactive, editable mind maps, flowcharts & architecture diagrams (see Visual Diagram Notes Design Guide, with native Mermaid code block rendering); use the built-in template gallery to generate stylized, versatile infographics across all formats (timelines, comparisons, quadrant matrices, etc.) in-place.
-   **AI Multi-Dimensional Tables & Public Forms**: Generate structured multi-dimensional tables for any business workflow (such as project tracking, content banks, and HR rosters) via natural language AI prompts, inferring tags, dates, and rich field types with sample rows; publish public online collection forms with one click without login requirements, syncing submitted responses in real time.
-   **Dual-View Editing & Workspace Organization**: Smoothly toggle between rich-text and raw Markdown views on desktop; classic 3-pane layout, one-click Focus Mode, infinite-depth notebooks, batch note merging/moving, and drag-and-drop sorting; automatic revision history and password-protected public note sharing.

### Creator Publishing & Effortless Distribution

-   **WeChat Official Account & Rich Copy**: Designed for creators, transform notes into beautifully formatted rich text with inline CSS, featuring one-click note copy to WeChat Official Account editor, newsletters, or blogs without extra tools.
-   **Elegant Long-Image Posters & Multi-Format Export**: Turn any note into an elegant image poster card with one click, featuring 8 refined themes, custom typography, and layout options for sharing on social platforms; export individual notes to Markdown, HTML, or PDF effortlessly.
-   **AI RSS Daily Digests**: Built-in official AI RSS subscription plugin that automatically aggregates feeds and blogs, filters out noise with AI, and compiles concise, well-structured daily digest notes.

### Native AI Agents & Open Ecosystem

-   **Native Agent Protocols (MCP & ACP)**: Built-in Model Context Protocol (MCP) enables external AI Agents to read and organize notes; desktop app integrates Agent Client Protocol (ACP) to drive local agents (Codex, Antigravity, Claude Code, WorkBuddy, etc.) directly for collaborative creation.
-   **Bring Your Own AI Models & Extensible Plugin API**: Connect multiple OpenAI, Anthropic, Gemini compatible providers and custom proxies to summarize, extract insights, proofread, translate, and refine writing; customize and extend EdgeEver via comprehensive Plugin Development APIs.

### Open Architecture, Cross-Platform & Security Foundation

-   **Flexible Deployment & Unlocked Data**: Run for free on Cloudflare Serverless (~150k short notes and ~50k images on the free tier), or deploy via Docker to your VPS, NAS, or home server for millions of notes; built on standard SQLite with REST APIs, CLI tooling, and lossless full ZIP export/import to keep your data completely independent.
-   **All-Platform Coverage & Production Security**: Official client support across Web, Android, macOS, Windows, Linux, and iOS, with web clipper extensions for Chrome, Edge, and Firefox; self-hosted synchronization without device limits, lightweight memory footprint on desktop, offline drafts with sync queues, server-side brute-force protection, and isolated multi-user workspaces.

👉 Explore all 14 step-by-step showcases with screenshots: **Complete Showcase & Workflows Guide**

Deployment
----------

Cloudflare is the recommended zero-server deployment. Docker is available for users who prefer a VPS, NAS, or home server.

For Cloudflare, choose either of the following online deployment options:

### Option A: Deploy with an AI Agent (Recommended)

Copy the prompt below directly into an AI Agent (such as Codex, Claude, Cursor, WorkBuddy, Antigravity, OpenClaw, Hermes Agent, etc.). During execution, if access to GitHub or Cloudflare is required, review the requested permissions and follow the prompts to authorize access.

```
Deploy EdgeEver entirely through GitHub and Cloudflare:
1. Fork https://github.com/tianma-if/edgeever.
2. Create D1 `edgeever` and R2 `edgeever-resources` in Cloudflare.
3. In Workers & Pages, create a Worker named `edgeever` from the Fork's `main` branch.
   Use the repository root, keep Cloudflare's default Workers Builds deploy command,
   and ensure its API token can read and edit D1. Select Save and Deploy.
4. After the Worker is created, add the user's chosen password as the runtime Secret
   `EDGE_EVER_AUTH_PASSWORD` (preferably at least 32 characters).
   The username defaults to `admin`.
   If the user specifies another, set `EDGE_EVER_AUTH_USERNAME` as a Workers Builds
   variable before the next build.
5. Run the build again, verify `/api/health` and `/api/openapi.json`, then log in
   with that administrator username and password.
6. Enable and manually run the GitHub Actions workflow named `Update deployed EdgeEver`
   once so the Fork can automatically receive future stable releases and fixes.
```

> Detailed requirements: AI Agent Cloudflare Deployment.

### Option B: Manual Online Deployment

Complete setup in 6 web steps:

1.  **Fork the Repository**: Click **Fork** at the top right of GitHub to fork EdgeEver into your personal account.
2.  **Create Cloudflare Resources**: Create D1 `edgeever` and R2 `edgeever-resources`.
3.  **Import & Configure the Project**: Create a Worker named `edgeever` from the Fork's `main` branch in Cloudflare **Workers & Pages**. Use the repository root and keep Cloudflare's default Workers Builds deploy command, which runs in Cloudflare. Ensure its API token can read and edit D1. The deploy command creates the bindings; do not edit Fork files.
4.  **Choose the Administrator Password**: Choose an administrator password, preferably at least 32 characters. Once the Worker is created, save it as the runtime Secret `EDGE_EVER_AUTH_PASSWORD`.
5.  **Build & Verify**: Save and Deploy creates the Worker and starts a build. If it fails because the administrator Secret is missing, add the runtime Secret from step 4 and retry. The username defaults to `admin`; to use another, set the `EDGE_EVER_AUTH_USERNAME` Workers Builds variable before retrying. Once deployed, confirm `/api/health` returns `200`, then log in with the configured username and password.
6.  **Enable Automatic Updates**: Open the Fork's **Actions** tab, click **I understand my workflows, go ahead and enable them**, then manually run **Update deployed EdgeEver** once so the Fork can automatically receive future stable releases and fixes.

> 📖 For full step-by-step instructions and configuration details, see the Online Deployment Guide.

> 💡 **Custom Domain & Access**: After deployment, you can directly use the default `*.workers.dev` domain assigned by Cloudflare, or attach your own custom domain in the Worker settings under **Settings → Domains & Routes**.

> 💡 **Cloudflare R2 Activation**: Although Cloudflare R2 offers a generous free storage allowance that note-taking workloads remain completely within, you must first activate an R2 subscription and add a payment method. Cloudflare officially supports UnionPay, Visa, Mastercard, and other cards, as well as PayPal, Apple Pay, Google Pay, and other payment methods.

### Option C: Docker on a VPS or NAS

Use the GitHub-hosted installer and the official GHCR image:

curl -fsSL https://edgeever.org/install.sh | bash

The command pulls the latest image, generates an administrator password, and starts EdgeEver with Docker Compose.

See the Docker deployment guide for manual deployment and configuration.

After installation, updates run automatically each day by default. To update manually, run `~/edgeever/update.sh` on the deployment server.

* * *

Multi-Account Login
-------------------

Once deployed, a single instance supports multi-account login.

The instance administrator can create, disable, or reset member accounts in **Profile** -> **User accounts**. Each member gets a fully isolated personal workspace, including notebooks, notes, attachments, Trash, import/export, and MCP tokens.

Browser Web Clipper
-------------------

     

-   **Smart Article Extraction**: Automatically extracts article content and converts it into clean Markdown, preserving the source URL and clipping timestamp.
-   **Selection & Context Menu Clipping**: Save selected text or right-clicked images directly as notes without capturing the entire page.
-   **Deep Social & Community Clipping**: Native support for X (Twitter), Xiaohongshu, Zhihu, Reddit, and GitHub with one-click sending.
-   **Private Self-Hosted Direct Connection**: Sends clipped content directly to your personal EdgeEver instance without third-party relays.

Community and Feedback
----------------------

-   Bugs, feature requests, and deployment issues: GitHub Issues
-   Code contributions: read the Contribution Guide. If your Fork is also used to deploy EdgeEver, keep its `main` branch deployment-only. Create a separate branch from the official `upstream/main` for synchronization, development, and pull requests; do not develop on or Sync fork the deployment `main`.

### Telegram Community

Welcome to the EdgeEver community, bringing together developers and creators exploring vibe coding and AI. Join us to discuss cutting-edge AI productivity and best practices for personal knowledge bases.

👉 Join the EdgeEver Telegram group

Plugins and Themes
------------------

Web and desktop apps support functional plugins and custom themes, installable from the official marketplace, GitHub, or a Manifest URL, with seamless sync across your workspace. Developers can extend capabilities using `@edgeever/plugin-api`; see the plugin development guide and marketplace submission policy.

Tech Stack
----------

-   Bun workspace monorepo with Web, API, official site, and shared type package.
-   Frontend: Vite, React, React Router, TanStack Query, Tailwind CSS, shadcn/ui, and Radix UI.
-   Editor: TipTap / ProseMirror with Markdown support; PWA uses vite-plugin-pwa, Workbox, and Dexie.
-   Android app: Expo + React Native in `apps/mobile`, with SQLite local storage and incremental sync.
-   iOS app: Native SwiftUI in `apps/ios` (iOS 17+), with a packaged TipTap EditorBundle, GRDB local mirror/outbox, and Android-aligned shell chrome.
-   Native desktop app: Electron + Rust sidecar combines a consistent cross-platform experience with high-performance local data services; SQLite enables offline editing, incremental sync when back online, and local backups.
-   Web clipper: Manifest V3, Mozilla Readability, and Turndown for Chrome, Microsoft Edge, and Firefox.
-   Backend: one Hono/Zod business application with REST API and Remote MCP; Cloudflare uses Workers/D1/R2, while Docker uses Bun/SQLite/local files or S3.
-   Official site: Astro static site in `apps/site`, deployable to Cloudflare Pages.

Quick Start
-----------

bun install
bun run dev

Local development signs in automatically; fresh databases use `owner` / `edgeever-local-dev`. Log out to test the login screen.

Project Structure
-----------------

```
apps/web          Vite + React frontend, PWA, offline drafts, and sync queue
apps/extension    Chrome/Edge/Firefox Manifest V3 web clipper
apps/api          Cloudflare Worker + Hono API, MCP endpoint
apps/mobile       Expo + React Native Android app
apps/ios          Native SwiftUI iOS app (TipTap EditorBundle, GRDB)
apps/desktop      Electron desktop shell, preload bridge, and native packaging
apps/site         Astro official website, deployable independently
packages/client   Shared API client for web and mobile apps
packages/shared   Shared types, Zod schemas, TipTap / Markdown conversion
crates/desktop-sidecar
                   Rust sidecar for local SQLite, offline data, backups, and resources
scripts           Wrangler wrapper, password hash, CLI, MCP stdio bridge, Evernote ENEX import
migrations        Shared append-only D1/SQLite database migrations
docs              Architecture, migration, and deployment docs
.github/workflows CI for web, mobile, iOS, desktop packaging, deployment, and releases
wrangler.toml     Cloudflare Workers, Assets, D1, R2 configuration
```

Content Formats
---------------

EdgeEver stores note content in three forms:

```
content_json      TipTap/ProseMirror document, the editor source of truth
content_markdown  API, Agent, import, and export format
content_text      Search, summary, and indexing text
```

Open **Profile** -> **Import and export** to export or import an EdgeEver ZIP. Its `notes/` directory is directly readable and portable as Markdown, while its structured data supports complete recovery between EdgeEver instances. Import preserves unrelated target data and overwrites records with matching EdgeEver IDs.

MCP
---

Create an API token in **Profile** -> **API / MCP** and copy the Remote MCP configuration in one click to let AI Agents such as Claude Code, Cursor, Antigravity, and OpenClaw securely manage your knowledge base within account permissions. EdgeEver supports full CRUD for text notes, visual diagram notes (mind maps, flowcharts, and architecture diagrams), and structured table notes. Agents can also manage notebook hierarchies, tags, attachments, revision history, note templates, and AI instructions.

> 💡 **Inspiration:** Make AI your true knowledge orchestrator and creative co-pilot—instantly turn concepts into interactive mind maps, flowcharts, architecture diagrams, and structured tables, while supplying private context to your AI Agents. Paired with EdgeEver’s powerful rich-text editing and elegant typography, AI-assisted content becomes beautifully structured, polished, and publication-ready knowledge assets.

Image Compression
-----------------

Image compression happens in the Web client before upload and is controlled by the **Compress note images** setting. When enabled, PNG, JPEG, WebP, and AVIF files are converted to WebP when beneficial, with the longest edge limited to `2560px`. If compression does not reduce size, the original file is kept.

EdgeEver avoids Worker-side image processing to reduce compute and image-processing quota usage. REST API and MCP upload paths store the file content provided by the client without additional server-side compression.

Advanced Object Storage
-----------------------

The instance owner can configure S3-compatible object storage under **Settings → Advanced → OSS object storage**. Changing storage does not migrate or affect existing attachments.

Migration
---------

If you want to migrate notes from other platforms to EdgeEver, please refer to the following simple migration guides:

-   **Evernote Migration**: Please refer to docs/evernote-migration-guide.md
-   **flomo Migration**: Please refer to docs/flomo-migration-guide.md
-   **Memos Migration**: Please refer to docs/memos-migration-guide.md
-   **Notion Migration**: Please refer to docs/notion-migration-guide.md

Docker Deployment
-----------------

Docker runs the same frontend, API routes, services, authentication, MCP implementation, and migrations as Cloudflare. The container uses SQLite with local files or S3-compatible attachment storage and supports `amd64` and `arm64`. See Deploy EdgeEver with Docker and Self-hosting and Docker architecture.

Sync Timing
-----------

Web, PWA, and desktop upload memo edits after 30 seconds of inactivity and check for remote changes every 5 minutes while visible; focus and manual refresh remain immediate. Adjust `DEFERRED_MEMO_SYNC_DELAY_MS` and `BACKGROUND_WORKSPACE_REFRESH_INTERVAL_MS` in `apps/web/src/lib/workspace-refresh.ts`.

Sponsor & Support
-----------------

EdgeEver is a free and open-source project. Sustaining cross-platform client development, continuous device testing, code signing, and multi-runtime ecosystem maintenance requires ongoing dedication and resources.

-   Support EdgeEver — Voluntary donation via WeChat Pay or Alipay
-   Sponsors & Partners — Support infrastructure, developer tools, services, or community collaboration

Acknowledgements
----------------

-   EdgeEver's note-taking product design was also informed by the publicly available product experiences of mature note-taking tools such as Evernote and Notion. The related features were independently designed and implemented by EdgeEver.
-   The product design of mind-map and visual-diagram notes was informed by the publicly available product experiences of XMind and ProcessOn. These features were independently designed and implemented by EdgeEver.
-   EdgeEver's poster design workspace draws inspiration from Qiaomu Design by 向阳乔木 (joeseesun), and adapts its templates and typography engine under the MIT license.

Trademark and Brand Use
-----------------------

The EdgeEver name, logo, and other brand identifiers distinguish the official project. Forks and modified versions may state that they are based on EdgeEver, but must not imply official status or mislead users. The open-source license does not grant trademark rights; other uses require prior written permission from the project maintainers.

Disclaimer
----------

EdgeEver is an independent open-source note-taking application developed and maintained by individuals and the community. It is not affiliated with, authorized, sponsored, or endorsed by Evernote Corporation or its affiliates.

EdgeEver is self-hosted software. Except for official demo instances, project maintainers do not host, control, or review user content. Content stored or displayed by an instance is the responsibility of its users or operators and does not represent the maintainers' views.
