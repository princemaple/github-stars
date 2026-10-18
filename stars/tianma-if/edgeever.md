---
project: edgeever
stars: 2319
description: AI-native knowledge base & Evernote/Obsidian alternative with instant sync & native MCP. Free on Cloudflare or self-hosted via Docker.
url: https://github.com/tianma-if/edgeever
---

EdgeEver
========

**AI-native knowledge base & Evernote/Obsidian alternative with instant sync & native MCP. Free on Cloudflare or self-hosted via Docker.**

简体中文 | 繁體中文 | **English** | 日本語 | Polski

Telegram Group  |  🌐 Live Demo  |  📱 Clients & Extension  |  Feature Matrix & Capabilities

EdgeEver is a modern, open-source notes and knowledge base workspace. It preserves the classic, high-efficiency three-pane productivity workflow (Tree View · Note List · Editor) while offering an open data architecture and seamless AI Agent integration for complete ownership and smart productivity.

> 💡 **Serverless & 100% Free Forever** EdgeEver can run within Cloudflare's free quotas with no server purchase or VPS maintenance. Users who prefer a VPS, NAS, or home server can deploy the same application with Docker.

> ⭐ If EdgeEver is useful to you, consider giving it a Star. Your support helps more people discover the project.

Why EdgeEver
------------

Many users of **note-taking apps and personal knowledge bases** simply want a **reliable, open, and fast** personal knowledge base. However, existing mainstream solutions all present tradeoffs:

-   **Evernote**: Offers the smoothest, most seamless multi-device cloud sync experience. Yet as it evolved into a full-featured commercial suite, ads and add-ons multiplied while system overhead climbed. Meanwhile, free-tier quotas tightened, premium AI subscriptions grew expensive, and it remains difficult to integrate into modern self-hosted and private AI workflows.
-   **Obsidian**: Open files, closed-source core. Official Sync is paid and third-party sync is tedious; relying entirely on flat local file scanning causes noticeable cold-start and search lag once notes reach thousands or heavy plugins are loaded; storing images and attachments alongside notes quickly bloats vaults, making mobile sync sluggish and leaving orphaned files behind; and it is overly heavy for lightweight, capture-anywhere use.
-   **Memos & Stream Notes**: Clean and simple, but their social-timeline layouts differ fundamentally from the structured productivity of a classic three-pane workflow.
-   **SiYuan & Block-based PKMs**: Powerful with self-hosting support, but their granular "block-level" architecture imposes noticeable cognitive overhead for quick daily capture and continuous prose writing. Furthermore, they lack a true zero-cost serverless deployment tier, and multi-device sync relies on paid official subscriptions or paying extra to unlock S3/WebDAV sync features with your own storage.

**EdgeEver fills this gap**: The entire stack is open source, delivering truly **seamless, low-latency, instant multi-device cloud sync** with full self-hosting freedom. It keeps the three-pane layout you know, stays silky-smooth and lightweight even with 10,000+ notes, and ships native AI agents with zero-cost deployment.

Online Demo
-----------

-   Demo: https://demo.edgeever.org

The public demo resets every day at 3:00 AM (China Standard Time) and restores sample notes. Do not store private content there.

All-Platform Clients & Browser Extension
----------------------------------------

### Client Downloads

           

> The iOS app requires an Apple ID from outside mainland China.

### Browser Web Clipper Extension

     

-   Extract clean Markdown from web articles or clip selected text and images directly to your self-hosted instance.
-   Deep structured clipping for 20+ platforms: social (X, Xiaohongshu, WeChat, Jike, Douban, Threads, Bluesky), dev & reading communities (Zhihu, Reddit, GitHub, V2EX, Hacker News, Medium, Substack), and media/podcasts (Bilibili, YouTube, Xiaoyuzhou).

Feature Matrix & Capabilities
-----------------------------

An all-in-one workspace connecting inspiration capture, deep creation, and knowledge compounding:

Module

Core Features

Advanced Features

**Writing & Editing**

• Classic 3-pane layout with resizable panel width  
• Seamless toggle between rich-text WYSIWYG & raw Markdown  
• Syntax highlighting, math formulas, task lists & Focus Mode  
• Second-level auto-save, instant multi-device sync & revision history

• **Native Poster Notes**: Canvas-based structured visual card layouts, double-click to edit  
• **WeChat Official Account Formatter**: One-click copy with inline CSS to newsletters/blogs  
• **Poster Image Export**: Curated themes, Monogram avatars; export to MD, HTML, or PDF

**Organization & Search**

• Infinite-depth notebooks & folder tree navigation  
• Tagging system, drag-and-drop sorting, batch note merging/moving  
• Millisecond-level full-text search with historical filtering

• **Standalone Knowledge Base Publishing**: One-click publish entire notebooks as static documentation sites with tree navigation & password protection  
• Multi-user spaces & physical tenant data isolation

**Capture & Media**

• Universal attachment uploads (PDF, Office, audio/video, archives)  
• Browser extension precision clipping for web text & images  
• Mobile system share sheet to save photos & articles

• **Deep Multi-Platform Structured Clipping**: Deeply adapted for Xiaohongshu, X (Twitter), Zhihu, Reddit, GitHub, YouTube, Bilibili, and 20+ sources  
• **WeChat Chat History Archiving**: One-click full transcript import on macOS with timestamps, quotes, emojis, and media  
• **Client-Side Image Compression**: Automatic 50%–90% silent size reduction; chunked streaming safely supports up to 1 GiB files

**Data & Visuals**

• Native table editing & Markdown table rendering  
• Native Mermaid diagrams (flowcharts, sequence diagrams, architecture)

• **AI Multi-Dimensional Tables**: Prompt-to-database with automatic field typing (tags, dates, selects)  
• **Public Online Collection Forms**: One-click shareable forms without login, syncing responses into tables in real time  
• **AI Diagram & Infographic Generation**: In-place creation of timelines, comparison charts, quadrant matrices & mind maps

**AI & Ecosystem**

• Companion sidebar AI assistant for summaries, proofreading & translations  
• BYOK (Bring Your Own Key): compatible with OpenAI, Claude, Gemini & custom endpoints

• **Native Agent Protocols (MCP & ACP)**: Built-in MCP for external agent read/write; ACP in desktop app to drive local coding agents directly  
• **AI RSS Daily Digest**: Automated feed aggregation, AI noise filtering, and structured digest generation  
• Extensible Plugin Development API

**Multi-Device Sync & Foundation**

• Seamless, low-latency sync across desktop, mobile, and web with zero device limits  
• Official client support across Web, macOS, Windows, Linux, iOS, and Android  
• Offline-first with auto-sync queue: write smoothly offline, automatically resume and sync when reconnected  
• Standard SQLite database, lossless ZIP backup & Markdown export/import

• **Zero Server Cost for Life**: 100% runnable on Cloudflare Free tier (~150k short notes & ~50k images)  
• **Flexible Docker Self-Hosting**: One-click deployment for VPS, NAS, or home server with millions of notes & instant sync  
• Server-side brute-force protection and tenant security

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

📖 Click to expand: 6-Step Web Manual Deployment Guide

Complete setup in 6 web steps:

1.  **Fork the Repository**: Click **Fork** at the top right of GitHub to fork EdgeEver into your personal account.
2.  **Create Cloudflare Resources**: Create D1 `edgeever` and R2 `edgeever-resources`.
3.  **Import & Configure the Project**: Create a Worker named `edgeever` from the Fork's `main` branch in Cloudflare **Workers & Pages**. Use the repository root and keep Cloudflare's default Workers Builds deploy command, which runs in Cloudflare. Ensure its API token can read and edit D1. The deploy command creates the bindings; do not edit Fork files.
4.  **Choose the Administrator Password**: Choose an administrator password, preferably at least 32 characters. Once the Worker is created, save it as the runtime Secret `EDGE_EVER_AUTH_PASSWORD`.
5.  **Build & Verify**: Save and Deploy creates the Worker and starts a build. The initial build primarily initializes the Worker instance; if it fails due to missing administrator Secret, this is expected behavior. Simply add the runtime Secret `EDGE_EVER_AUTH_PASSWORD` from Step 4 and click retry. The username defaults to `admin`; to use another, set `EDGE_EVER_AUTH_USERNAME` as a Workers Builds variable before retrying. Once deployed, confirm `/api/health` returns `200`, then log in with the configured username and password.
6.  **Enable Automatic Updates**: Open the Fork's **Actions** tab, click **I understand my workflows, go ahead and enable them**, then manually run **Update deployed EdgeEver** once so the Fork can automatically receive future stable releases and fixes.

> 📖 For full step-by-step instructions and configuration details, see the Online Deployment Guide.

📌 View Cloudflare Deployment Notes (Custom Domain & Free R2 Allowance)

> **Custom Domain & Access**: After deployment, you can directly use the default `*.workers.dev` domain assigned by Cloudflare, or attach your own custom domain in the Worker settings under **Settings → Domains & Routes**.
> 
> **Cloudflare R2 Activation**: Although Cloudflare R2 offers a generous free storage allowance that note-taking workloads remain completely within, you must first activate an R2 subscription and add a payment method. Cloudflare officially supports UnionPay, Visa, Mastercard, and other cards, as well as PayPal, Apple Pay, Google Pay, and other payment methods.

### Option C: Docker on a VPS or NAS

Docker runs the same frontend, API routes, services, authentication, MCP implementation, and migrations as Cloudflare. The container uses SQLite with local files or S3-compatible attachment storage and supports `amd64` and `arm64`. See Deploy EdgeEver with Docker and Self-hosting and Docker architecture.

Use the GitHub-hosted installer and the official GHCR image:

curl -fsSL https://edgeever.org/install.sh | bash

The command pulls the latest image, generates an administrator password, and starts EdgeEver with Docker Compose.

See the Docker deployment guide for manual deployment and configuration.

After installation, updates run automatically each day by default. To update manually, run `~/edgeever/update.sh` on the deployment server.

* * *

Advanced Configuration & Management
-----------------------------------

### Data Backup, Export & Migration

Whether for routine data backups, seamless cross-instance migration, or switching from existing note platforms, EdgeEver provides reliable, complete data mobility:

-   **EdgeEver Native Backup & Restore**: In the app, go to **Profile** -> **Import and export** to export or import an EdgeEver ZIP archive at any time. The extracted `notes/` directory keeps clean plaintext Markdown files and attachments for local archival or direct reading, while internal structured metadata enables lossless full restoration across different EdgeEver instances. Importing preserves existing unrelated data on the target instance and automatically overwrites records with matching IDs.
-   **Smooth Migration from Third-Party Apps**:
    -   **Evernote Migration**: Please refer to docs/evernote-migration-guide.md
    -   **flomo Migration**: Please refer to docs/flomo-migration-guide.md
    -   **Memos Migration**: Please refer to docs/memos-migration-guide.md
    -   **Notion Migration**: Please refer to docs/notion-migration-guide.md

### AI & MCP Protocol Integration

Create an API token in **Profile** -> **API / MCP** and copy the Remote MCP configuration in one click to let AI Agents such as Claude Code, Cursor, Antigravity, and OpenClaw securely manage your knowledge base within account permissions. EdgeEver supports full CRUD for text notes, visual diagram notes (mind maps, flowcharts, and architecture diagrams), structured table notes, and native poster notes. Agents can also manage notebook hierarchies, tags, attachments, revision history, note templates, and AI instructions.

> 💡 **Inspiration:** Make AI your true knowledge orchestrator and creative co-pilot—instantly turn concepts into interactive mind maps, flowcharts, architecture diagrams, and structured tables, while supplying private context to your AI Agents. Paired with EdgeEver’s powerful rich-text editing and elegant typography, AI-assisted content becomes beautifully structured, polished, and publication-ready knowledge assets.

### Multi-Account Login & Storage Management

Once deployed, a single instance supports multi-account login.

The instance administrator can create, disable, or reset member accounts in **Profile** -> **User accounts**. Each member gets a fully isolated personal workspace, including notebooks, notes, attachments, Trash, import/export, and MCP tokens. An intuitive storage usage dashboard provides real-time visibility into attachment storage consumed across the whole instance as well as per account.

### Storage Extension & Third-Party Image Hosting

-   **OSS Object Storage**: The instance owner can configure S3-compatible object storage under **Settings → Advanced → OSS object storage**. Changing storage does not migrate or affect existing attachments.
-   **Desktop PicGo Integration**: The desktop app optionally integrates with a local PicGo client service, uploading inserted images directly to GitHub, SM.MS, Upyun, Qiniu, or custom image hosts to minimize self-hosted storage and bandwidth consumption.

### Plugins and Themes

Web and desktop apps support functional plugins and custom themes, installable from the official marketplace, GitHub, or a Manifest URL, with seamless sync across your workspace. Developers can extend capabilities using `@edgeever/plugin-api`; see the plugin development guide and marketplace submission policy.

* * *

Developer Guide & Contributing
------------------------------

### Quick Start

bun install
bun run dev

Local development signs in automatically; fresh databases use `owner` / `edgeever-local-dev`. Log out to test the login screen.

### Architecture & Tech Stack

#### Tech Stack

-   Bun workspace monorepo with Web, API, official site, and shared type package.
-   Frontend: Vite, React, React Router, TanStack Query, Tailwind CSS, shadcn/ui, and Radix UI.
-   Editor: TipTap / ProseMirror with Markdown support; PWA uses vite-plugin-pwa, Workbox, and Dexie.
-   Android app: Expo + React Native in `apps/mobile`, with SQLite local storage and incremental sync.
-   iOS app: Native SwiftUI in `apps/ios` (iOS 17+), with a packaged TipTap EditorBundle, GRDB local mirror/outbox, and Android-aligned shell chrome.
-   Native desktop app: Electron + Rust sidecar combines a consistent cross-platform experience with high-performance local data services; SQLite enables offline editing, incremental sync when back online, and local backups.
-   Web clipper: Manifest V3, Mozilla Readability, and Turndown for Chrome, Microsoft Edge, and Firefox.
-   Backend: one Hono/Zod business application with REST API and Remote MCP; Cloudflare uses Workers/D1/R2, while Docker uses Bun/SQLite/local files or S3.
-   Official site: Astro static site in `apps/site`, deployable to Cloudflare Pages.

#### Project Structure

📁 Expand to view: Monorepo Project Structure

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

#### Data Storage Model

EdgeEver persists note content simultaneously across three formats to balance editing performance, open portability, and full-text search speed:

```
content_json      TipTap/ProseMirror document, the editor source of truth
content_markdown  API, Agent, export, and external ecosystem interoperability
content_text      Full-text search, summary generation, and indexing
```

### Core Mechanisms & Design Decisions

-   **Client-Side Silent Compression**: To avoid consuming compute quota on serverless runtimes like Cloudflare Workers, image compression occurs in the Web client before upload (converting PNG/JPEG/WebP/AVIF to WebP when beneficial, max edge 2560px; original retained if compression does not reduce size). REST API and MCP endpoints store client-supplied binaries directly without additional server-side transcoding.
-   **Offline-First & Sync Timing**: Web, PWA, and desktop clients automatically upload memo edits after 30 seconds of typing inactivity, and poll for remote changes every 5 minutes while visible; window refocus and manual refresh remain immediate. Configurable via `DEFERRED_MEMO_SYNC_DELAY_MS` and `BACKGROUND_WORKSPACE_REFRESH_INTERVAL_MS` in `apps/web/src/lib/workspace-refresh.ts`.

### Contributing Code

Community contributions are warmly welcome! Please keep the following guidelines in mind:

-   Please review the Contribution Guide before submitting code.
-   **Deployment Isolation**: If your GitHub Fork is also used to deploy EdgeEver, keep its `main` branch clean and deployment-only. Create a dedicated branch from official `upstream/main` for features/fixes and pull requests; do not develop on or run Sync fork directly on the deployment `main`.

* * *

Community and Feedback
----------------------

-   **Issues & Suggestions**: For bugs, feature requests, and deployment questions, please submit to GitHub Issues to help the community build searchable solutions.

### Telegram Community

Welcome to the EdgeEver community, bringing together developers and creators exploring vibe coding and AI. Join us to discuss cutting-edge AI productivity and best practices for personal knowledge bases.

👉 Join the EdgeEver Telegram group

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
-   The visual themes and typography of EdgeEver's image-sharing cards were inspired by Firefly Card (流光卡片). Thank you for the design inspiration.

Trademark and Brand Use
-----------------------

The EdgeEver name, logo, and other brand identifiers distinguish the official project. Forks and modified versions may state that they are based on EdgeEver, but must not imply official status or mislead users. The open-source license does not grant trademark rights; other uses require prior written permission from the project maintainers.

Disclaimer
----------

EdgeEver is an independent open-source note-taking application developed and maintained by individuals and the community. It is not affiliated with, authorized, sponsored, or endorsed by Evernote Corporation or its affiliates.

EdgeEver is self-hosted software. Except for official demo instances, project maintainers do not host, control, or review user content. Content stored or displayed by an instance is the responsibility of its users or operators and does not represent the maintainers' views.
