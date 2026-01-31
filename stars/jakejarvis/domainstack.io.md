---
project: domainstack.io
stars: 215
description: 🧰 All-in-one domain name intelligence as a service
url: https://github.com/jakejarvis/domainstack.io
---

**Domainstack**: Domain Intelligence Made Easy

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
-   **Postgres** (PlanetScale) + **Drizzle ORM** + **Upstash Redis** (rate limiting)
-   **Better Auth** (OAuth)
-   **Polar** (subscriptions)
-   **Workflow DevKit** (background jobs)
-   **AI SDK** + **AI Gateway**
-   **Resend** + **React Email**
-   **Vercel** (Edge Config, Blob Storage)
-   **mapcn** + **CARTO Basemaps**
-   **Logo.dev**
-   **IPLocate.io**
-   **PostHog** (analytics)
-   **Turborepo** (monorepo)
-   **Vitest** + **Playwright** (testing), **Biome** (linting)

Project Structure
-----------------

This is a **Turborepo monorepo**:

```
domainstack.io/
├── apps/
│   └── web/                 # Next.js application
├── packages/
│   ├── constants/           # Shared constants (enums, TTLs, validation)
│   ├── types/               # Shared TypeScript types
│   ├── typescript-config/   # Shared TypeScript configs
│   └── ui/                  # Shared UI primitives
├── turbo.json               # Turborepo task configuration
├── pnpm-workspace.yaml      # pnpm workspace definition
└── biome.json               # Linting/formatting config
```

Development
-----------

### 1\. Clone & install

git clone https://github.com/jakejarvis/domainstack.io.git
cd domainstack.io
pnpm install

### 2\. Configure environment variables

Create `.env.local` in the `apps/web` directory and populate required variables:

cp apps/web/.env.example apps/web/.env.local

At minimum, you'll need `DATABASE_URL` pointing to a Postgres database.

### 3\. Set up the database

Apply Drizzle migrations to initialize the database schema:

pnpm db:migrate

### 4\. Start development

pnpm dev

Open http://localhost:3000.

License
-------

MIT
