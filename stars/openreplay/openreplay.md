---
project: openreplay
stars: 12905
description: Session replay, cobrowsing and product analytics you can self-host. Best for reproducing issues and iterating on your product.
url: https://github.com/openreplay/openreplay
---

Français  |  Español  |  Русский  |  العربية

### The open-source experience platform you host yourself

Session replay, cobrowsing, and product analytics — self-hosted, so your users' data never leaves your infrastructure.

OpenReplay is an open-source experience platform you host on your own infrastructure. Replay user sessions, debug with full technical context, analyze product usage, and co-browse with users live — without sending a single session to a third party. Everything OpenReplay captures stays in your cloud, fully under your control.

That makes OpenReplay a fit for teams that can't ship customer data to an external vendor: no third-party processors, no lengthy compliance reviews, and alignment with the strictest regulatory standards. It's used by engineering, product, design, and support teams at large companies in highly regulated industries.

Why OpenReplay
--------------

-   **Own your data.** Self-host on your own infrastructure (AWS, GCP, Azure, and more). Session data never leaves your security perimeter.
-   **Privacy by design.** Mask, obscure, or skip any data at capture time, before it ever reaches your servers. Turn on private mode to redact everything by default.
-   **Everything in one place.** Session replay, DevTools, product analytics, and cobrowsing — instead of stitching together separate tools.
-   **Lightweight.** A lightweight tracker that sends minimal data asynchronously, for very limited impact on performance.
-   **Open-source.** Read the code, self-host it for free, and contribute. No black boxes.

Features
--------

-   **Session Replay.** Relive what your users experience — where they navigate, click, hesitate, or struggle — and catch every error, slowdown, or crash along the way. Search and filter by almost any user action, session attribute, or technical event — no instrumentation required.
-   **DevTools.** Debug as if the bug happened in your own browser. Get the full context — network activity, console logs, JS errors, store actions/state, and 40+ performance metrics — to reproduce and fix issues instantly.
-   **Product Analytics.** Know which journeys convert and where users drop off, with funnels, trends, journeys, heatmaps, and web analytics — all backed by the underlying session replays for full context.
-   **Cobrowsing.** Support users when it matters most. See their live screen, take cursor control with permission, and hop on a WebRTC call — no meeting links, downloads, or third-party screen-sharing software.
-   **Spot.** A free Chrome extension that captures bugs straight from the browser. Each recording bundles the console, network, and environment details developers need to fix the issue.
-   **Mobile.** Native session replay for iOS, Android, and React Native apps.

Own your data
-------------

OpenReplay was built for teams in regulated and security-conscious industries who need full control over user data.

-   **Self-hosted.** Run OpenReplay entirely inside your own cloud or on-prem. No data is shared with any 3rd-party.
-   **Capture-time sanitization.** Choose what to capture, obscure, or ignore so sensitive data never even reaches your servers. Mask by CSS selector, redact inputs, and sanitize network payloads. See Data Sanitization.
-   **Private mode.** Mask all text and inputs by default — ideal for healthcare, banking, and legal applications. See Private Mode.
-   **Ad-blocker resistant.** Because you self-host, tracking is first-party and isn't blocked by ad blockers, so you capture complete data.
-   **GDPR & CCPA.** Built-in tools to sanitize sensitive data, manage exports, and honor deletion requests.
-   **Access control.** Role-based access (Owner, Admin, Member) plus SSO (SAML, OIDC) for enterprise authentication.
-   **SOC 2 Type II.** OpenReplay Cloud is SOC 2 Type II compliant.

How OpenReplay compares
-----------------------

Most session-replay and product-analytics tools are closed-source SaaS: your users' data is captured into a vendor's multi-tenant cloud, and your control ends at a settings page. OpenReplay is open source and gives you the full range of deployment models — including options no other vendor offers — so data security and residency stay your decision.

On top of free self-hosting, you can run OpenReplay three ways: **Serverless** (usage-based, like everyone else), a fully managed **Dedicated** instance with data residency in **50+ regions**, or **Bring-Your-Own-Cloud (BYOC)**, where we deploy and manage OpenReplay inside your _own_ cloud account so session data never leaves it.

Security & privacy

OpenReplay

FullStory

LogRocket

PostHog

Open-source

✅

❌

❌

✅

Self-host in production (free)

✅

❌

Enterprise 1

Deprecated 2

Cloud Serverless (usage based)

✅

✅

✅

✅

Cloud Dedicated

**50+ regions**

❌

❌

❌

Bring-Your-Own-Cloud (BYOC)

✅

❌

❌

❌

Data stays in your infrastructure

✅

❌

Enterprise

Hobby

No 3rd-party processor

✅

❌

⚠️

⚠️

Mask PII at capture

✅

✅

✅

✅

1 LogRocket has a self-hosted version but for enterprise customers only. It's limited and not open-source.  
2 PostHog is open source, but its self-hosted (Kubernetes) deployment is deprecated — only a "hobby" Docker build remains, and new features ship cloud-only.

Deploy anywhere
---------------

OpenReplay can be deployed anywhere. Start with the Getting Started guide. All you need is a single VM on a baseline of 2 vCPUs, 8 GB of RAM, and 50 GB of storage:

-   AWS
-   Google Cloud
-   Azure
-   DigitalOcean
-   Scaleway
-   OVHcloud
-   Kubernetes (Helm)
-   Docker
-   Ubuntu (bare metal)
-   From source

OpenReplay Cloud
----------------

Prefer not to self-host? Run OpenReplay in our Cloud:

-   **Serverless** — usage-based, pay only for the sessions you record.
-   **Dedicated** — a fully managed instance, in a dedicated VPC, with data residency across 50+ regions.
-   **Bring-Your-Own-Cloud (BYOC)** — we run and manage OpenReplay inside your own AWS, GCP, or Azure account.

SDKs
----

-   **Web** — a single JavaScript tracker with guides for React, Next.js, Angular, Vue, Nuxt, Svelte, Gatsby, Remix, Electron, or a drop-in snippet. See the JavaScript SDK reference.
-   **Mobile** — native session replay for iOS, Android, and React Native (currently in beta).

Plugins & integrations
----------------------

Get to the root cause faster by capturing application state and backend context alongside each replay.

-   **State management:** Redux, VueX, Pinia, MobX, NgRx, and Zustand.
-   **Network & performance:** Fetch, Axios, GraphQL (Apollo, Relay), and the Profiler.
-   **Integrations:** Sync backend logs and errors with your replays to see what happened front to back — Sentry, Datadog, Elastic, Dynatrace, and more. Plus ticketing (Jira, GitHub, Zendesk, messaging (Slack, Microsoft Teams), and Google Tag Manager).

Documentation & resources
-------------------------

-   Documentation — guides, SDK references, and deployment instructions.
-   Getting Started — from zero to your first session in ~30 minutes.
-   Blog — tutorials, comparisons, and engineering deep-dives.

Community & support
-------------------

Start with the documentation to troubleshoot common issues. For more help, reach out on any of these channels:

-   Slack — connect with our engineers and community.
-   Forum — ask questions and browse past discussions.
-   YouTube — tutorials and past community calls.

Contributing
------------

We're always on the lookout for contributions, and we're glad you're considering it! Not sure where to start? Look for open issues, preferably those marked as good first issues. See our Contributing Guide for more details, and feel free to join our Slack to ask questions, discuss ideas, or connect with other contributors.

License
-------

This monorepo uses multiple licenses. Most of the codebase is licensed under the **AGPLv3**, some directories are licensed under **MIT**, and everything under the `ee/` directory (the Enterprise Edition) is licensed under a separate commercial license defined in `ee/LICENSE`. Third-party components retain their original licenses.

See LICENSE for the full details. Questions? Reach out to license@openreplay.com.
