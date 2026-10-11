---
project: posthog
stars: 40218
description: :hedgehog: PostHog is the leading platform for building self-driving products. Our developer tools – AI observability, analytics, session replay, flags, experiments, error tracking, logs, and more – capture all the context agents need to diagnose problems, uncover opportunities, and ship fixes. Steer it all from Slack, web, desktop, or the MCP.
url: https://github.com/PostHog/posthog
---

Docs - Community - Roadmap - Why PostHog? - Changelog - Bug reports

PostHog is your product's context layer
---------------------------------------

PostHog ingests and stores your analytics, errors, replays, and business data so you and your agents can query and act on it. It gives you every tool you need to build a successful product, and captures the context agents need to diagnose problems, uncover opportunities, and ship fixes:

**Analytics**

-   Product analytics: Autocapture or manually instrument event-based analytics to understand user behavior. Analyze your data with visualizations or SQL.
-   Web analytics: Monitor web traffic and user sessions with a GA-like dashboard. Track conversion, web vitals, and revenue.
-   Group analytics: Analyze multi-seat accounts and other groups of users.

**Session replay**

-   Session replay: Watch real user sessions from your website or mobile app to diagnose issues and understand user behavior.
-   Replay Vision: Let AI watch your recordings for you and turn them into queryable observations.
-   Heatmaps: See where users click, scroll, and move on your site.

**Observability**

-   Error tracking: Track errors, get alerts, and resolve issues to improve your product.
-   Logs: Ingest, search, and analyze log data alongside the rest of your product data.
-   Tracing: Follow distributed traces straight to the line of code that broke.

**Ship and iterate**

-   Feature flags: Safely roll out features to select users or cohorts.
-   Experiments: Test changes and measure their statistical impact on goal metrics. Set up experiments with no code, too.
-   Early access features (beta): Let users opt into betas and register interest in upcoming features.

**Talk to users**

-   Surveys: Ask anything with our collection of no-code survey templates, or build custom surveys with our survey builder.
-   Support: Run customer support with a chat widget and a unified inbox, next to the product data behind each ticket.
-   Workflows: Automate actions and messages to your users, triggered by your product data.

**Data**

-   Warehouse: Collect, store, transform, and query all the context behind your product. Includes a managed warehouse, 120+ sources, and a SQL editor with BI and data visualization.
-   Data pipelines: Run custom filters and transformations on your incoming data. Send it to 25+ tools or any webhook in real time, or batch export large amounts to your warehouse.
-   Endpoints: Build custom API endpoints powered by your PostHog data.

**AI and agents**

-   AI observability: Capture traces, generations, latency, and cost for your LLM-powered app. Run LLM-as-a-judge evaluations to catch regressions.
-   MCP analytics (beta): See how agents actually use your MCP server.
-   PostHog AI: Ask your product data anything. PostHog AI builds insights, writes SQL, and finds replays for you.
-   Self-driving: Turn signals in your product data (errors, rage clicks, failed queries, and more) into researched reports and pull requests, delivered to your Inbox for you to review and merge.

You can steer it all from Slack, web, desktop (PostHog Desktop), or your own editor via the MCP.

**What is this, a readme for agents?**  

The remote MCP server is `https://mcp.posthog.com/mcp`. It routes to the correct data region (US or EU) when your human logs in. Install it into Claude Code, Cursor, Codex, VS Code, Zed, or PostHog Desktop with:

npx @posthog/wizard mcp add

The docs are indexed for you at posthog.com/llms.txt, the changelog is plain Markdown at posthog.com/changelog.md, and the setup guides for every MCP client are in the docs.

All of this is free to use with a monthly free tier for each product. No card is required, and 97% of users pay $0. Join the 500,000+ teams already shipping with PostHog by signing up for PostHog Cloud US or PostHog Cloud EU.

Table of Contents
-----------------

-   PostHog is your product's context layer
-   Table of Contents
-   Getting started with PostHog
    -   PostHog Cloud (Recommended)
    -   Self-hosting the open-source hobby deploy (Advanced)
-   Setting up PostHog
-   Learning more about PostHog
-   Contributing
-   Open-source vs. paid
-   We’re hiring!

Getting started with PostHog
----------------------------

### PostHog Cloud (Recommended)

The fastest and most reliable way to get started with PostHog is signing up for free to PostHog Cloud or PostHog Cloud EU. Your first 1 million events, 5k recordings, 1M flag requests, 100k exceptions, 10GB of logs, and 1500 survey responses are free every month, after which you pay based on usage.

### Self-hosting the open-source hobby deploy (Advanced)

If you want to self-host PostHog, you can deploy a hobby instance in one line on Linux with Docker (recommended 4GB memory):

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/posthog/posthog/HEAD/bin/deploy-hobby)"

Open source deployments should scale to approximately 100k events per month, after which we recommend migrating to a PostHog Cloud.

We _do not_ provide customer support or offer guarantees for open source deployments. See our self-hosting docs, troubleshooting guide, and disclaimer for more info.

Setting up PostHog
------------------

Once you've got a PostHog instance, the fastest way to set it up is the setup wizard, which installs and configures PostHog in your app for you:

npx -y @posthog/wizard@latest

You can also install our JavaScript web snippet, one of our SDKs, or use our API. You can also connect the MCP to bring PostHog into Claude Code, Cursor, or any MCP-compatible agent.

We have SDKs and libraries for popular languages and frameworks like:

Frontend

Mobile

Backend

JavaScript

React Native

Python

Next.js

Android

Node

React

iOS

PHP

Vue

Flutter

Ruby

Beyond this, we have docs and guides for Go, .NET/C#, Django, Angular, WordPress, Webflow, and more.

Once you've installed PostHog, see our product docs for more information on how to set up product analytics, web analytics, session replays, feature flags, experiments, error tracking, surveys, data sources, and more.

Learning more about PostHog
---------------------------

Our code isn't the only thing that's open source 😳. We also open source our company handbook which details our strategy, ways of working, and processes.

Curious about how to make the most of PostHog? We wrote a guide to winning with PostHog which walks you through the basics of measuring activation, tracking retention, and capturing revenue.

Contributing
------------

We <3 contributions big and small:

-   Vote on features or get early access to beta functionality in our roadmap
-   Open a PR (see our instructions on developing PostHog locally)
-   Submit a feature request on our roadmap or a bug report

For an overview of the codebase structure, see monorepo layout and products.

Open-source vs. paid
--------------------

This repo is available under the MIT expat license, except for the `ee` directory (which has its license here) if applicable.

Need _absolutely 💯% FOSS_? Check out our posthog-foss repository, which is purged of all proprietary code and features.

The pricing for our paid plan is completely transparent and available on our pricing page.

We're hiring!
-------------

Hey! If you're reading this, you've proven yourself as a dedicated README reader.

You might also make a great addition to our team. We're growing fast and would love for you to join us.

* * *

If you're looking for easter eggs or abandoned ideas, please check the trash.
