---
project: carbon
stars: 2049
description: Carbon is an open source ERP, MES and QMS for manufacturing. Perfect for complex assembly, contract manufacturing, and configure to order manufacturing.
url: https://github.com/crbnos/carbon
---

The operating system for manufacturing  
  
Discord · Website · Documentation

Does the world need another ERP?
--------------------------------

We built Carbon after years of building end-to-end manufacturing systems with off-the-shelf solutions. We realized that:

-   Modern, API-first tooling didn't exist
-   Vendor lock-in bordered on extortion
-   There is no "perfect ERP" because each company is unique

We built Carbon to solve these problems ☝️

Architecture
------------

Carbon is designed to make it easy for you to extend the platform by building your own apps through our API. We provide some examples to get you started in the examples folder.

Features:

-   ERP
-   MES
-   QMS
-   Custom Fields
-   Nested BoM
-   Traceability
-   MRP
-   Configurator
-   MCP Client/Server
-   API
-   Webhooks
-   Accounting
-   Capacity Planning
-   Simulation
-   Full Roadmap

Technical highlights:

-   Unified auth and permissions across apps
-   Full-stack type safety (Database → UI)
-   Realtime database subscriptions
-   Attribute-based access control (ABAC)
-   Role-based access control (Customer, Supplier, Employee)
-   Row-level security (RLS)
-   Composable user groups
-   Dependency graph for operations
-   Third-party integrations

Techstack
---------

-   React Router – framework
-   Typescript – language
-   Tailwind – styling
-   Radix UI - behavior
-   Supabase - database
-   Supabase – auth
-   Redis - cache
-   Inngest - jobs
-   Resend – email
-   Lingui - i18n
-   Novu – notifications
-   Vercel – hosting
-   Stripe - billing

Codebase
--------

The monorepo follows the Turborepo convention of grouping packages into one of two folders.

1.  `/apps` for applications
2.  `/packages` for shared code

### `/apps`

Package Name

Description

Local Command

`erp`

ERP Application

`npm run dev`

`mes`

MES

`npm run dev:mes`

`academy`

Academy

`npm run dev:academy`

`starter`

Starter

`npm run dev:starter`

### `/packages`

Package Name

Description

`@carbon/database`

Database schema, migrations and types

`@carbon/documents`

Transactional PDFs and email templates

`@carbon/ee`

Integration definitions and configurations

`@carbon/config`

Shared configuration (vitest, tsconfig, tailwind) across apps and packages

`@carbon/jobs`

Background jobs and workers

`@carbon/logger`

Shared logger used across apps

`@carbon/react`

Shared web-based UI components

`@carbon/kv`

Redis cache client

`@carbon/lib`

Third-party client libraries (slack, resend)

`@carbon/stripe`

Stripe integration

`@carbon/utils`

Shared utility functions used across apps and packages

Development
-----------

### Setup

1.  Clone the repo into a public GitHub repository (or fork https://github.com/crbnos/carbon/fork). If want to make the repo private, you should acquire a commercial license to comply with the AGPL license.
    
    git clone https://github.com/crbnos/carbon.git
    
2.  Go to the project folder
    
    cd carbon
    

Make sure that you have Docker installed on your system since this monorepo uses the Docker for local development.

In addition you must configure the following external services:

Service

Purpose

URL

Posthog

Product analytics platform

https://us.posthog.com/signup

Stripe

Payments service

https://dashboard.stripe.com/login

Resend

Email service

https://resend.com

Novu

Notifications service

https://dashboard.novu.co/auth/sign-in

Posthog has a free tier which should be plenty to support local development. If you're self hosting and you don't want to use Posthog, it's pretty easy to remove the analytics.

### Installation

First download and initialize the repository dependencies.

$ nvm use           # use node v20
$ npm install       # install dependencies
$ npm run db:start  # pull and run the containers

Create an `.env` file and copy the contents of `.env.example` file into it

$ cp ./.env.example ./.env

1.  **Social Sign In**: Signing in requires you to setup one of two methods:

-   Email requires a Resend API key (you'll set this up later on)
-   Sign-in with Google requires a Google auth client with these variables. See the Supabase docs for instructions on how to set this up:
    -   Set `Authorized JavaScript origins` to only `http://127.0.0.1:54321`
    -   Set `Authorized redirect URIs` to `http://127.0.0.1:54321/auth/v1/callback`
-   You should set environment variables like the following.
    -   `SUPABASE_AUTH_EXTERNAL_GOOGLE_CLIENT_ID="******.apps.googleusercontent.com"`
    -   `SUPABASE_AUTH_EXTERNAL_GOOGLE_CLIENT_SECRET="GOCSPX-****************"`

1.  **Supabase**: Start up the backend services using `npm run db:start`. Find the following values in its output to set the supabase entries:

-   `SUPABASE_SERVICE_ROLE_KEY=[service_role key]`
-   `SUPABASE_ANON_KEY=[anon key]`

1.  **Redis** (Caching): Set up a Redis instance (local or cloud) and add the connection URL. You can set one up in the cloud easily using Upstash:

-   `REDIS_URL=[redis://user:password@host:port]`

1.  **Posthog** (Analytics): In Posthog go to https://\[region\].posthog.com/project/\[project-id\]/settings/project-details to find your Project ID and Project API key:

-   `POSTHOG_API_HOST=[https://[region].posthog.com]`
-   `POSTHOG_PROJECT_PUBLIC_KEY=[Project API Key starting 'phc*']`

1.  **Stripe** (Payment service) - Create a stripe account, add a `STRIPE_SECRET_KEY` from the Stripe `Settings > Developers` interface

-   `STRIPE_SECRET_KEY="sk_test_*************"`

1.  **Resend** (Email service) - Create a Resend account and configure:

-   `RESEND_API_KEY="re_**********"`
-   `RESEND_DOMAIN="carbon.ms"` (or your domain, no trailing slashes or protocols)
-   `RESEND_AUDIENCE_ID="*****"` (Optional - required for contact management in `packages/jobs`)

Resend is used for transactional emails (user invitations, email verification, onboarding). All three variables are stored in `packages/auth/src/config/env.ts`.

1.  **Novu** (In-app notifications) - Create a Novu account and configure:

-   `NOVU_APPLICATION_ID="********************"` (Client-side, public)
-   `NOVU_SECRET_KEY="********************"` (Server-side secret, backend only)

Novu is used for in-app notifications and notification workflows. After standing up the application and tunnelling port 3000, sync your Novu workflows:

npm run novu:sync

This command syncs your Novu workflows with the Carbon application using the bridge URL.

Finally, start the apps and packages:

$ npm run dev
$ npm run dev:mes        # npm run dev in all apps & packages

After installation you should be able run the apps locally.

Application

URL

ERP

http://localhost:3000

MES

http://localhost:3001

Academy

http://localhost:4111

Starter

http://localhost:4000

Background Jobs

http://localhost:8288

Postgres

postgresql://postgres:postgres@localhost:54322/postgres

Supabase Studio

http://localhost:54323/project/default

Mailpit

http://localhost:54324

Edge Functions

http://localhost:54321/functions/v1/

### Code Formatting

This project uses Biome for code formatting and linting. To set up automatic formatting on save in VS Code:

1.  Install the Biome VS Code extension
    
2.  Add the following to your VS Code settings (`.vscode/settings.json` or global settings):
    

"editor.codeActionsOnSave": {
  "source.organizeImports.biome": "explicit",
  "source.fixAll.biome": "explicit"
},
"editor.defaultFormatter": "biomejs.biome"

### Commands

To add an edge function

$ npm run db:function:new <name\>

To add a database migration

$ npm run db:migrate:new <name\>

To add an AI agent

$ npm run agent:new <name\>

To add an AI tool

$ npm run tool:new <name\>

To kill the database containers in a non-recoverable way, you can run:

$ npm run db:kill   # stop and delete all database containers

To restart and reseed the database, you can run:

$ npm run db:build # runs db:kill, db:start, and setup

To run a particular application, use the `-w workspace` flag.

For example, to run test command in the `@carbon/react` package you can run:

```
$ npm run test -w @carbon/react
```

To restore a production database locally:

1.  Download the production database as a .backup file
2.  Rename the `migrations` folder to `_migrations`
3.  Restore the database with the following command:

$ npm run db:build # this should error out at the seed step
$ PGPASSWORD=postgres psql -h localhost -p 54322 -U supabase\_admin -d postgres < ~/Downloads/db\_cluster-17-11-2025@09-03-36.backup
$ npm run dev

1.  Rename the `_migraitons` folder back to `migrations`

API
---

The API documentation is located in the ERP app at `${ERP}/x/api/js/intro`. It is auto-generated based on changes to the database.

There are two ways to use the API:

1.  From another codebase using a supabase client library:

-   Javascript
-   Flutter
-   Python
-   C#
-   Swift
-   Kotlin

1.  From within the codebase using our packages.

### From another Codebase

First, set up the necessary credentials in environment variables. For the example below:

1.  Navigate to settings in the ERP to generate an API key. Set this in `CARBON_API_KEY`
2.  Get the Supabase URL to call (this is `SUPABASE_URL` in your `.env` if hosting locally, e.g. http://localhost:54321). Set this as `CARBON_API_URL`.
3.  Get the `SUPABASE_ANON_KEY` e.g. from your .env file. Set this as `CARBON_PUBLIC_KEY`.

If you're self-hosting you can also use the supabase service key instead of the public key for root access. In that case you don't need to include the `carbon-key` header.

import { Database } from "@carbon/database";
import { createClient } from "@supabase/supabase-js";

const apiKey \= process.env.CARBON\_API\_KEY;
const apiUrl \= process.env.CARBON\_API\_URL;
const publicKey \= process.env.CARBON\_PUBLIC\_KEY;

const carbon \= createClient<Database\>(apiUrl, publicKey, {
  global: {
    headers: {
      "carbon-key": apiKey,
    },
  },
});

// returns items from the company associated with the api key
const { data, error } \= await carbon.from("item").select("\*");

### From the Monorepo

import { getCarbonServiceRole } from "@carbon/auth/client.server";
const carbon \= getCarbonServiceRole();

// returns all items across companies
const { data, error } \= await carbon.from("item").select("\*");

// returns items from a specific company
const companyId \= "xyz";
const { data, error } \= await carbon
  .from("item")
  .select("\*")
  .eq("companyId", companyId);

Translations
------------

In order to run `npm run translate` you must first run:

brew install ollama
brew services start ollama
ollama pull llama3.2
curl http://localhost:11434/api/tags
npx linguito config set \\
  llmSettings.provider=ollama \\
  llmSettings.url=http://127.0.0.1:11434/api

Migration Notes
---------------

### Trigger.dev to Inngest

Background jobs have been migrated from Trigger.dev to Inngest. Key changes:

-   **Job definitions** moved from `packages/jobs/trigger/` to `packages/jobs/src/inngest/functions/`
-   **Triggering jobs** from app code uses `trigger()` and `batchTrigger()` from `@carbon/jobs` instead of `tasks.trigger()` from `@trigger.dev/sdk`
-   **Inngest dev server** runs via `npx inngest-cli@latest dev -u http://localhost:3000/api/inngest`
-   **Environment variables**: `TRIGGER_SECRET_KEY`, `TRIGGER_API_URL`, and `TRIGGER_PROJECT_ID` are no longer needed. Set `INNGEST_EVENT_KEY` and `INNGEST_SIGNING_KEY` instead (not required for local dev).

### Upstash to Local Redis

The caching layer (`@carbon/kv`) no longer depends on Upstash. A standard Redis instance is used instead. The `REDIS_URL` environment variable still applies, but you can point it at any Redis-compatible server (including a local Docker container).
