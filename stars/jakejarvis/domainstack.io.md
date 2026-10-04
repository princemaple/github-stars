---
project: domainstack.io
stars: 292
description: 🧰 All-in-one domain name intelligence as a service
url: https://github.com/jakejarvis/domainstack.io
---

**Domainstack** — Domain Intelligence Made Easy

  

Features
--------

-   **Instant domain reports**: WHOIS/RDAP data, DNS, certs, headers, hosting/email providers, and geolocation.
-   **Domain tracking**: Verify ownership, monitor domains, and get important health alerts.
-   **Provider detection**: Matches raw data against a large hosting, email, and DNS provider library.
-   **SEO & metadata analysis**: Titles, meta tags, social previews, Open Graph images, canonicals, and `robots.txt`.
-   **Screenshots & icons**: Server-side screenshots, favicon extraction, and provider logos.
-   **Fast & private**: No sign-up required for reports.
-   **Notifications & calendar sync**: Email/In-app alerts plus iCal feeds for expirations.
-   **Advanced dashboard**: Filtering, sorting, bulk actions, and multiple view modes.
-   **AI chat assistant**: Ask questions about any domain in natural language; powered by durable streaming with automatic reconnection.
-   **MCP server**: AI-assisted domain lookups via Model Context Protocol.
-   **Pro subscription**: Paid plan via Polar for higher tracking limits.
-   **Reliable backend**: SWR caching with cron-based cache warming.

Tech Stack
----------

-   **Next.js 16** (App Router), **React 19**, **TypeScript**
-   **Tailwind CSS v4** + **Base UI**
-   **tRPC** + **TanStack Query** & **TanStack Table**
-   **PlanetScale Postgres** + **Drizzle** + **Upstash Redis** (rate limiting)
-   **Better Auth** (OAuth)
-   **Polar** (subscriptions)
-   **Workflow SDK** (background jobs)
-   **AI SDK** + **Vercel AI Gateway** (Stacky bot)
-   **Resend** (email notifications)
-   **mapcn** + **CARTO Basemaps** (web maps)
-   **Logo.dev** (provider icons)
-   **IPLocate.io** (geolocation)
-   **PostHog** (telemetry)
-   **Vercel** (Edge Config, Blob Storage)
-   **Turborepo** (monorepo)
-   **Vitest** + **Playwright** (testing), **oxlint/oxfmt** (linting)

Development
-----------

This is a **Turborepo monorepo**. You need Node.js 24+, pnpm, and Docker.

### 1\. Clone & install

git clone https://github.com/jakejarvis/domainstack.io.git
cd domainstack.io
pnpm install

### 2\. Start local services and configure env

`compose.yml` runs Postgres and an Upstash-compatible Redis. The top block of `.env.example` already points at them:

docker compose up -d
cp apps/web/.env.example apps/web/.env.local

Maintainers can use `vercel env pull apps/web/.env.local` instead to get real credentials.

### 3\. Set up the database

pnpm db:migrate
pnpm db:seed

The seed creates two users, `free@dev.local` and `pro@dev.local` (password `password123`), with tracked domains in each verification state. It only runs against a local database unless you pass `--force` (`pnpm db:seed -- --force`).

### 4\. Start development

pnpm dev

Open http://localhost:3000/login and use the **Dev sign-in** form. Email/password sign-in only exists when `NODE_ENV=development`.

To fill in report data and change-detection baselines for the seeded domains, trigger the crons by hand:

curl -H "Authorization: Bearer dev" http://localhost:3000/api/cron/warm-domains
curl -H "Authorization: Bearer dev" http://localhost:3000/api/cron/monitor-domains

If you pulled real env vars, replace `dev` with your `CRON_SECRET`.

### Optional services

Every other variable in `.env.example` is optional locally:

Service

Without it (in development)

OAuth (GitHub, GitLab, Google, Vercel)

Sign in as a seeded user with email/password

Resend

Emails are not sent: each send fails with "Resend is not configured"

Vercel Blob

Favicons, screenshots and OG images are stored in `apps/web/public/_dev-blob/`

Vercel Sandbox

Screenshots are skipped (not cached), so the screenshot slot stays empty

Upstash Redis

Rate limiting, session caching and monitor locks are skipped

Polar

Billing is disabled. When a token is set, Polar runs in sandbox outside production

Global Config

Provider detection falls back to "unknown"

Dynadot, IPLocate, PostHog

Pricing, geolocation and analytics are skipped

Logo.dev

Provider logos come from the other logo sources only

License
-------

MIT
