---
project: domainstack.io
stars: 206
description: 🧰 All-in-one domain name intelligence
url: https://github.com/jakejarvis/domainstack.io
---

📚 Domainstack - Domain Intelligence Tool
=========================================

Domainstack is an all-in-one app for exploring domain names. Search any domain (e.g., `github.com`) and get instant insights including WHOIS/RDAP lookups, DNS records, SSL certificates, HTTP headers, hosting details, geolocation, and SEO signals.

🚀 Features
-----------

-   **Instant domain reports**: Registration, DNS, certificates, HTTP headers, hosting & email, and geolocation.
-   **SEO insights**: Extract titles, meta tags, social previews, canonical data, and `robots.txt` signals.
-   **Screenshots & favicons**: Server-side screenshots and favicon extraction, cached in Postgres with Vercel Blob storage.
-   **Fast, private, no sign-up required for reports**: Live fetches with intelligent multi-layer caching.
-   **Domain tracking dashboard**: Sign in to track domains you own, verify ownership, and receive expiration alerts.
-   **Pro tier subscriptions**: Upgrade via Polar for expanded domain tracking limits (100 vs 5 domains).
-   **Multi-channel notifications**: Configurable alerts via Email and In-App notifications for domain expiry, certificate expiry, and critical record changes.
-   **Calendar integration**: Subscribe to domain expiration dates via iCalendar feed (Google Calendar, Apple Calendar, Outlook, etc.).
-   **Reliable data pipeline**: Postgres persistence with per-table TTLs (Drizzle) and event-driven background revalidation (Inngest).
-   **Advanced dashboard**: Domain filtering by status/health/TLD, URL-persisted filters, bulk archive/delete actions, and sortable table/grid views.
-   **Dynamic configuration**: Vercel Edge Config for runtime-adjustable data and flags without redeployment.

🛠️ Tech Stack
--------------

-   **Next.js 16** (App Router) + **React 19** + **TypeScript**
-   **Tailwind CSS v4** + **shadcn/ui** components (of the **Base UI** variety)
-   **tRPC** API with **TanStack Query** for data fetching and optimistic updates
-   **TanStack Table** for sortable dashboard table view
-   **rdapper** for RDAP lookups with WHOIS fallback
-   **PlanetScale Postgres** + **Drizzle ORM** with connection pooling
-   **Better Auth** for authentication via OAuth
-   **Polar** for subscription payments
-   **Inngest** for scheduled and event-driven background jobs
-   **Workflow DevKit** for durable resource-intensive operations
-   **Resend** + **React Email** for transactional email notifications
-   **Vercel Edge Config** for runtime configuration (domain suggestions, provider detection, and other safeguards)
-   **Vercel Blob** for media storage
-   **PostHog** for analytics and error tracking
-   **mapcn** with **CARTO Basemaps** for beautiful IP geolocation maps
-   **Logo.dev** for provider icons
-   **Puppeteer** for on-demand screenshots
-   **Biome** for linting/formatting and **Vitest** (Browser Mode w/ Playwright) for E2E testing

🌱 Getting Started
------------------

### 1\. Clone & install

git clone https://github.com/jakejarvis/domainstack.io.git
cd domainstack.io
pnpm install

### 2\. Configure environment variables

Create `.env.local` and populate required variables:

cp .env.example .env.local

At minimum, you'll need `DATABASE_URL` pointing to a PostgreSQL database.

### 3\. Set up the database

Apply Drizzle migrations to initialize the database schema:

pnpm db:migrate

### 4\. Start development

pnpm dev

Open http://localhost:3000.

🧰 Useful Commands
------------------

pnpm dev           # start Next.js dev server
pnpm build         # compile production bundle
pnpm start         # serve compiled output for smoke tests
pnpm lint          # Biome lint/format checks
pnpm format        # apply Biome formatting
pnpm typecheck     # tsc --noEmit
pnpm test          # Vitest (watch mode)
pnpm test:run      # Vitest (single run)
pnpm test:coverage # Vitest with coverage report

# Drizzle
pnpm db:generate   # generate SQL migrations from schema
pnpm db:push       # push the current schema to the database
pnpm db:migrate    # apply migrations to the database
pnpm db:studio     # open Drizzle Studio

📜 License
----------

MIT

Toybrick by Ary Prasetyo from Noun Project (CC BY 3.0)
