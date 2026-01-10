---
project: posthog
stars: 30774
description: 🦔 PostHog is an all-in-one developer platform for building successful products. We offer product analytics, web analytics, session replay, error tracking, feature flags, experimentation, surveys, data warehouse, a CDP, and an AI product assistant to help debug your code, ship features faster, and keep all your usage and customer data in one stack.
url: https://github.com/PostHog/posthog
---

Docs - Community - Roadmap - Why PostHog? - Changelog - Bug reports

PostHog is an all-in-one, open source platform for building successful products
-------------------------------------------------------------------------------

PostHog provides every tool you need to build a successful product including:

-   Product Analytics: Autocapture or manually instrument event-based analytics to understand user behavior and analyze data with visualization or SQL.
-   Web Analytics: Monitor web traffic and user sessions with a GA-like dashboard. Easily monitor conversion, web vitals, and revenue.
-   Session Replays: Watch real user sessions of interactions with your website or mobile app to diagnose issues and understand user behavior.
-   Feature Flags: Safely roll out features to select users or cohorts with feature flags.
-   Experiments: Test changes and measure their statistical impact on goal metrics. Set up experiments with no-code too.
-   Error Tracking: Track errors, get alerts, and resolve issues to improve your product.
-   Surveys: Ask anything with our collection of no-code survey templates, or build custom surveys with our survey builder.
-   Data warehouse: Sync data from external tools like Stripe, Hubspot, your data warehouse, and more. Query it alongside your product data.
-   Data pipelines: Run custom filters and transformations on your incoming data. Send it to 25+ tools or any webhook in real time or batch export large amounts to your warehouse.
-   LLM analytics: Capture traces, generations, latency, and cost for your LLM-powered app.
-   Workflows: Create workflows that automate actions or send messages to your users.

Best of all, all of this is free to use with a generous monthly free tier for each product. Get started by signing up for PostHog Cloud US or PostHog Cloud EU.

Table of Contents
-----------------

-   PostHog is an all-in-one, open source platform for building successful products
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

The fastest and most reliable way to get started with PostHog is signing up for free to PostHog Cloud or PostHog Cloud EU. Your first 1 million events, 5k recordings, 1M flag requests, 100k exceptions, and 1500 survey responses are free every month, after which you pay based on usage.

### Self-hosting the open-source hobby deploy (Advanced)

If you want to self-host PostHog, you can deploy a hobby instance in one line on Linux with Docker (recommended 4GB memory):

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/posthog/posthog/HEAD/bin/deploy-hobby)"

Open source deployments should scale to approximately 100k events per month, after which we recommend migrating to a PostHog Cloud.

We _do not_ provide customer support or offer guarantees for open source deployments. See our self-hosting docs, troubleshooting guide, and disclaimer for more info.

Setting up PostHog
------------------

Once you've got a PostHog instance, you can set it up by installing our JavaScript web snippet, one of our SDKs, or by using our API.

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

Once you've installed PostHog, see our product docs for more information on how to set up product analytics, web analytics, session replays, feature flags, experiments, error tracking, surveys, data warehouse, and more.

Learning more about PostHog
---------------------------

Our code isn't the only thing that's open source 😳. We also open source our company handbook which details our strategy, ways of working, and processes.

Curious about how to make the most of PostHog? We wrote a guide to winning with PostHog which walks you through the basics of measuring activation, tracking retention, and capturing revenue.

Contributing
------------

We <3 contributions big and small:

-   Vote on features or get early access to beta functionality in our roadmap
-   Open a PR (see our instructions on developing PostHog locally)
-   Submit a feature request or bug report

Open-source vs. paid
--------------------

This repo is available under the MIT expat license, except for the `ee` directory (which has its license here) if applicable.

Need _absolutely 💯% FOSS_? Check out our posthog-foss repository, which is purged of all proprietary code and features.

The pricing for our paid plan is completely transparent and available on our pricing page.

We're hiring!
-------------

Hey! If you're reading this, you've proven yourself as a dedicated README reader.

You might also make a great addition to our team. We're growing fast and would love for you to join us.
