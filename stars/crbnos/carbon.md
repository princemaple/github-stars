---
project: carbon
stars: 2670
description: Open-source manufacturing ERP, MES and QMS. Quoting, MRP, inventory, shop floor, quality and lot/serial traceability on one Postgres schema, with a REST API and MCP server. Self-host or use Carbon Cloud.
url: https://github.com/crbnos/carbon
---

### Build hardware at the speed of software

Carbon combines ERP, MRP, MES and QMS.  
Plan materials, run the shop floor, manage quality and track actual costs in one system.

**Hard tech unicorns build on Carbon.**

**Start 30-day trial** · **Self-host** · **Docs** · **API** · **MCP** · **Discord** · **Roadmap**

  

**One record from quote to cash.** Link quotes, orders, jobs and invoices.

**Generate configurations from rules.** Control BOMs, routings and revisions.

**Trace every unit to its source.** Follow lot and serial genealogy in both directions.

  

Contents
--------

-   Why Carbon
-   Features
-   Get Carbon
-   API & MCP
-   Architecture
-   Tech Stack
-   Monorepo
-   Local Development
-   Commands
-   Security
-   Contributing
-   License

  

Why Carbon
----------

Manufacturing teams often run planning, production, quality and accounting in separate systems. That creates predictable problems:

-   BOMs and revisions are re-keyed between engineering and production
-   Material shortages surface after work has started
-   Job costs and quality records are reconstructed after the fact
-   Integrations depend on vendor-specific tools and consultants

Carbon puts ERP, MRP, MES and QMS in **one Postgres database you can inspect, own and extend**. Engineering, planning, production, quality and accounting update the same data, without synchronization jobs between separate product databases.

Carbon is an open-source alternative to NetSuite, Epicor, SAP Business One, Plex, Odoo and ERPNext. It supports complex assembly, contract manufacturing, configure-to-order and high-mix, low-volume production. See all comparisons.

  

Features
--------

**ERP — Inventory & Costing**

Quotes, orders, purchasing, inventory, invoicing and actual job costs

**MRP — Planning**

Demand, supply planning, versioned BOMs and routings, finite-capacity scheduling

**MES — Execution**

Digital travelers, operator terminals, 3D instructions, barcode and labor capture

**QMS — Quality**

Inspections, FAI, nonconformance, CAPA, calibration and risk management

**Traceability**

Forward and backward lot and serial genealogy

**Engineering**

Multi-level BOMs, revisions, change orders, supersession and product configuration

**Accounting**

General ledger, journals, multi-entity, multi-currency and accounting integrations

**Workflows**

Rule-based automation with triggers, actions and run history

**Maintenance & Assets**

Scheduled maintenance, fixed assets and kanban replenishment

**API, Webhooks & MCP**

Typed REST operations, event-driven webhooks and a permission-aware MCP server

**Custom Fields**

Extend records without changing the core schema

**Integrations**

Onshape, SolidWorks, Paperless Parts, Linear, Jira, Slack, Ramp, Stripe and Zebra

See the full roadmap for what's next.

**Technical highlights**

-   Generated types shared by the database, application and API
-   Postgres row-level security and tenant-scoped records
-   Role- and attribute-based access for employees, customers and suppliers
-   Realtime database subscriptions
-   Shared identity and permissions across the application, API and MCP server
-   Explicit dependency graphs for manufacturing operations
-   Rust geometry services for STEP conversion and assembly motion planning

  

Get Carbon
----------

**Carbon Cloud**

Managed application, database, updates and backups. Start a 30-day trial without a sales call.

**Self-hosted**

Run Carbon in your VPC, on-prem or air-gapped. See the self-hosting guide.

**Develop locally**

Run the application and supporting services from source. Follow Local Development.

  

API & MCP
---------

The **Carbon API** exposes the same manufacturing operations used by the application. Each operation validates its input, updates dependent records and enforces the authenticated identity's permissions. Operations are available through two interfaces with the same arguments:

-   **HTTP:** `POST https://app.carbon.ms/api/v1/{module}/{operation}`, with a published OpenAPI spec for generating a typed client in any language
-   **MCP:** as tools for hosted or local AI agents, scoped to the permissions of the API key or signed-in user

Create a key under **Settings → API Keys**, then:

curl -X POST https://app.carbon.ms/api/v1/sales/getSalesOrders \\
  -H "Authorization: Bearer $CARBON\_API\_KEY" \\
  -H "Content-Type: application/json" \\
  -d '{ "args": { "limit": 10 } }'

Self-hosted deployments serve the same API at `/api/v1`. The Data API provides direct access to permitted tables and views when an operation is not available in the service layer.

API keys and MCP are included with Business and Enterprise plans. Using them in a self-hosted deployment requires a commercial license.

  

Architecture
------------

ERP and MES are React Router apps over a single Postgres database. Permissions (row-level security), computed totals and change events live in the database itself; background work runs through Inngest, which calls back into the ERP to execute jobs. The architecture guide follows one click all the way down.

  

Tech Stack
----------

Layer

Technology

Apps

React Router 7 on Vite, TypeScript

UI

Tailwind 4, Radix, React Aria, TanStack Table and Query

Forms

Zod with `@carbon/form`

Database

Postgres with row-level security, PostgREST and Kysely

API

oRPC with OpenAPI, MCP server

AI

AI SDK (Anthropic, OpenAI)

Jobs & events

Inngest

Cache

Redis

3D & CAD

three.js / react-three-fiber; Rust with OpenCASCADE and FCL

Documents

React PDF, React Email, TipTap

i18n

Lingui

Tooling

pnpm, Turborepo, Biome, Vitest

Docs

Next.js + Fumadocs

Hosting

AWS via SST, or self-hosted with Docker

  

Monorepo
--------

A pnpm + Turborepo monorepo:

```
carbon
├── apps         # ERP, MES and the Rust assembler
├── packages     # shared TypeScript packages
├── crates       # Rust crates behind the assembler (CAD conversion, collision, motion planning)
└── docs         # docs.carbon.ms, with content and glossary as @carbon/content
```

### `/apps`

App

Description

`erp`

ERP: sales, purchasing, inventory, planning, quality, accounting

`mes`

MES: the shop floor app, run on tablets next to the machines

`assembler`

Rust geometry service: STEP → GLB and assembly motion planning

`academy`

Training

`starter`

Example app built on the API

### `/packages`

Package

Description

`@carbon/database`

Schema, migrations, generated types and database clients

`@carbon/auth`

Authentication, RBAC, sessions, API keys and OAuth

`@carbon/api`

API contract: the generated operation manifest behind the Carbon API and MCP

`@carbon/react`

Shared UI components (Radix, React Aria, Tailwind)

`@carbon/form`

`ValidatedForm` and field components for zod + FormData

`@carbon/jobs`

Inngest background jobs: events, integrations, notifications, workflows

`@carbon/planning`

MRP and scheduling engines

`@carbon/server-functions`

Transactional writes shared by the apps, API and jobs (posting, issuing, converting)

`@carbon/documents`

PDFs, email templates, ZPL labels, QR and barcodes

`@carbon/printing`

Printer routing, label queue and ProxyBox delivery

`@carbon/viewer`

3D models and animated assembly instructions (react-three-fiber)

`@carbon/files`

File handling: images, HEIC, CAD formats

`@carbon/tiptap`

Rich-text editor extensions and components

`@carbon/onboarding`

Implementation Hub: guided company setup

`@carbon/notifications`

Notification event taxonomy shared by apps and jobs

`@carbon/workflows-core`

Community-licensed contracts for workflow triggers

`@carbon/locale`

Lingui i18n runtime for ERP and MES

`@carbon/lib`

Server utilities: event system, Inngest client, SMTP, Slack

`@carbon/kv`

Redis client and rate limiting

`@carbon/env`

Validated environment variables, secrets kept server-side

`@carbon/logger`

Isomorphic logger built on LogTape

`@carbon/utils`

Pure shared utilities (dates, precision, BOM, formatting)

`@carbon/stripe`

Stripe billing (Carbon Cloud only)

`@carbon/ee`

Enterprise features and integrations (commercial license)

`@carbon/checks`

Conformance checks that keep the codebase consistent

`@carbon/dev`

The `crbn` dev CLI: worktrees, Docker stacks, dev URLs

`@carbon/harness`

Harness for AI coding agents working on this repo

`@carbon/config`

Shared Vitest, TypeScript and Tailwind configuration

  

Local Development
-----------------

**Prerequisites:** Docker, Node.js 22 and pnpm (via Corepack). On Windows, use WSL or Git Bash.

git clone https://github.com/crbnos/carbon.git && cd carbon
corepack enable && pnpm install
cp .env.example .env
pnpm dev

`pnpm dev` boots the whole backend in Docker (Postgres, PostgREST, auth, storage, realtime, Inngest, Redis and a mail catcher), applies migrations, generates types and starts the apps:

Surface

URL

ERP

http://localhost:3000

MES

http://localhost:3001

API

http://localhost:54321

Sign in as `test@carbon.ms`: the dev stack seeds that user and skips the magic link. To fill a company with a full demo story (items, BOMs, orders, jobs, inspections, journals), seed one of the industry datasets (`satellite`, `robotics`, `precision`, `motor`):

pnpm db:seed:dev -- --email test@carbon.ms --dataset satellite

No external accounts are needed to run locally. Email, Google/Microsoft sign-in, Stripe, PostHog and AI providers are all optional and configured in `.env`; see environment variables.

### Worktrees and the `crbn` CLI

`pnpm dev` is shorthand for `crbn up --no-portless`. Run `source ./setup.sh` once to put `crbn` on your `PATH` and you get a separate, isolated stack per git worktree, so several branches can run side by side, each on its own HTTPS `.dev` URLs via portless:

crbn checkout -b feat/my-thing   # new branch + worktree off HEAD
crbn up                          # boot this worktree's stack at erp.<branch>.dev
crbn checkout 760                # check out PR #760 into its own worktree
crbn status | down | reset       # ports and health, stop, wipe and reboot

The full command reference is in the local development guide.

### Optional: the `assembler` geometry service

`assembler` is a Rust service (STEP → GLB + assembly motion planning) over C++ FCL and OpenCASCADE. ERP/MES run fine without it — set it up only if you need the 3D `/convert` and `/plan` endpoints.

1.  **Toolchain + native build deps** (macOS):
    
    curl --proto '\=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh   # Rust, if not already installed
    brew install fcl cmake ninja draco                               # collision libs (+ libccd/eigen/octomap), build tools, Draco mesh compression
    
    On Linux, install the equivalents from your package manager: `libfcl-dev libccd-dev libeigen3-dev liboctomap-dev libdraco-dev cmake ninja-build` plus a C/C++ toolchain.
    
    `./setup.sh` already installs Draco on macOS. If yours lives outside the Homebrew keg (`/opt/homebrew/opt/draco` on arm64), point `draco-bridge`'s build at it with `DRACO_PREFIX=/path/to/draco cargo build`.
    
2.  **Build OCCT once** — a patched static OpenCASCADE, cached in `~/.cache/carbon-occt`. Slow (~15–30 min) but one-time per machine; re-running is a no-op once cached:
    
    ./apps/assembler/scripts/build-occt.sh
    
3.  **Build the service** — seconds once OCCT is cached (`build.rs` finds it automatically):
    
    cargo build --release -p assembler
    

`crbn up` spawns the binary when it's present. Verify it's up with `curl -sf "$ASSEMBLER_SERVICE_URL/health"` (the URL is in your worktree's `.env.local`) or by watching the `asm |` lines in the `crbn up` output. Without the binary the rest of the stack still runs — only `/convert` and `/plan` are unavailable.

### Restoring a production snapshot

To restore a production database snapshot locally, use `crbn restore`. It handles both plain-text `.backup` and custom-format `.dump` archives, drops and rebuilds the public schema, realigns internal sequences, resets storage metadata, then applies any migrations the backup predates and regenerates types.

1.  Export a backup of your production database with `pg_dump`.
    
2.  Run it from your worktree root:
    
    crbn restore /path/to/db\_cluster.backup
    # …or for .dump archives:
    crbn restore /path/to/postgres\_YYYYMMDD.dump
    
    It prompts before replacing the database. The stack must already be running (`crbn up`) — a restore rewrites the `auth` and `storage` schemas, which GoTrue and Storage build through their own migrations when those containers boot, so `crbn restore` refuses rather than restore into an uninitialized stack.
    
    To also get local admin access, pass your production email — your account is upgraded to Admin in the companies it already belongs to and the password is reset locally:
    
    crbn restore /path/to/backup.backup --admin-email you@example.com
    # Optional: set a custom local password (default: localpass)
    crbn restore /path/to/backup.backup --admin-email you@example.com --admin-password mypass
    
    Useful flags: `--no-scrub-emails` keeps real addresses (see the warning below), `--mode prod` restores exactly as-is without localizing config/webhooks/integrations, `--no-migrate` / `--no-regen` skip the trailing steps, `--yes` skips the prompt.
    
    > **Emails are scrubbed by default** — every address is rewritten to `@example.test` (your `--admin-email` is preserved so you can still log in). If you pass `--no-scrub-emails`, real production addresses will be present in the local DB; ensure local email sending is disabled or pointed at a sandbox (e.g. Mailpit) before triggering any email flows.
    > 
    > **Note:** `storage.objects` is truncated by default, so a restore does not populate local file storage — kept rows would reference files that only exist in the source environment's backend. Pass `--keep-storage-objects` to retain the metadata (and the backup's buckets) anyway; downloads will still 404, but the rows are there for work that needs realistic storage volume.
    

The underlying script, `scripts/restore-database.sh`, can still be invoked directly — it takes the same options as environment variables (`SCRUB_EMAILS`, `ADMIN_EMAIL`, `ADMIN_PASSWORD`, `RESTORE_MODE`), but note it defaults to **not** scrubbing emails and leaves the trailing `pnpm db:migrate` / `pnpm db:types` to you.

  

Commands
--------

Command

Description

`pnpm dev`

Boot the stack and apps on localhost

`pnpm db:migrate:new <name>`

Create a database migration

`pnpm db:migrate`

Apply pending migrations

`pnpm generate:types`

Regenerate database types after a migration

`pnpm db:seed:dev -- --dataset <key>`

Seed a demo company

`pnpm lint` / `pnpm test`

Biome lint / unit tests

`pnpm exec turbo run typecheck --filter=<pkg>`

Typecheck one package

`pnpm --filter <pkg> <cmd>`

Run a command in one workspace

This project uses Biome for formatting and linting; install the VS Code extension for format-on-save.

  

Security
--------

**Found a vulnerability?** Please email support@carbon.ms instead of opening a public issue. We respond within 3 business days and credit reporters once a fix ships. The full policy is in SECURITY.md.

Security is enforced by the database, not left to application code:

-   **Tenant isolation in Postgres.** Every table is scoped to a company and guarded by row-level security, so a query can only see its own company's rows.
-   **Granular permissions.** Role-based access per module and action for employees, customers and suppliers, applied the same way in the app, the API and MCP.
-   **Scoped API keys.** Keys carry explicit permissions, are stored only as hashes and are rate limited per key.
-   **Sign-in.** Passkeys, SSO, and enforced two-factor authentication on the Business plan.
-   **Audit log.** A record of who changed what and when, on the Business plan.
-   **Your perimeter.** Deploy in your VPC, on-prem or air-gapped to keep CUI inside infrastructure you control while supporting ITAR and CMMC requirements.

  

Contributing
------------

We welcome contributions of all sizes. Read CONTRIBUTING.md to get started, and say hi in Discord. Good first issues are labelled `good first issue`.

### Star history

  

License
-------

Carbon is open core. Everything in this repository is licensed under AGPLv3, except the Enterprise files (`packages/ee` and any file whose name contains `.ee.`), which are under the Carbon Commercial License. See Licensing for what that means in practice.

  

Built by the Carbon team · Join the Discord
