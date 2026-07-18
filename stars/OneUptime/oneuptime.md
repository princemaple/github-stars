---
project: oneuptime
stars: 7302
description: Complete open-source monitoring and observability platform.
url: https://github.com/OneUptime/oneuptime
---

English · 简体中文 · 繁體中文 · 日本語 · 한국어 · Español · Français · Deutsch · Português · Italiano · Русский · हिन्दी · Nederlands · Dansk · Svenska · Norsk

### Agentic observability — one open-source platform for uptime, incidents, on-call, status pages, logs, traces, metrics & APM.

**When things go wrong, be the first to know — and the fastest to fix.**

OneUptime replaces a whole shelf of SaaS tools with one platform you can self-host for free. It catches the outage, pages the right person, updates your status page, finds the root cause, and even opens the fix PR.

**Website**  •  **Docs**  •  **Quick Start**  •  **Pricing**  •  **Contribute**

**🚀 Try OneUptime Cloud — free forever plan, no credit card →**

  

* * *

Replace your whole observability stack
--------------------------------------

OneUptime brings monitoring, alerting, incident response, and observability into a single open-source app — so you stop paying for (and stitching together) a dozen separate tools.

Instead of…

Use OneUptime for…

Pingdom / UptimeRobot

**Uptime Monitoring** — website, API, ping, port, SSL, DNS & synthetic checks from around the world

StatusPage.io

**Status Pages** — branded public & private status pages with subscribers

PagerDuty / Opsgenie

**On-Call & Alerts** — schedules, escalation policies, SMS / call / push / Slack

Incident.io

**Incident Management** — declare, triage, communicate, and post-mortem

Datadog / New Relic

**APM & Metrics** — traces, dashboards, and service performance

Loggly

**Log Management** — collect, search, and alert on logs

Sentry

**Error Tracking** — exceptions with full stack traces and context

All of it is **100% open source (Apache 2.0)** and free to self-host.

* * *

**🌙 One incident, handled end to end**  

It's 2:47 AM. Checkout starts timing out. Here's what OneUptime does before most tools would even fire the first alert — and what the screenshots below actually show.

### 1 · Detect — _know in seconds_

Probes in multiple regions catch checkout latency blowing past your 5s threshold and open an incident automatically — before your customers hit refresh.

### 2 · Respond — _the right person, paged_

The on-call engineer for the Payments policy is called, texted, and push-notified, escalating to backup automatically until someone acknowledges.

### 3 · Communicate — _customers in the loop_

Your status page updates itself and every subscriber is notified by email and SMS — no one has to hand-write the update.

### 4 · Diagnose — _root cause, found_

Traces, logs, and metrics are correlated down to the exact span: a slow `SELECT … FOR UPDATE` on `orders`, stuck on a missing index.

### 5 · Auto-Fix — _the fix, drafted for you_

The AI agent opens a pull request with the fix, linked to the incident, with tests green — you review and merge. Like an SRE that never sleeps.

* * *

⚡ Quick Start
-------------

### ☁️ OneUptime Cloud — the easy way

Zero setup, always up to date, and it funds the open-source project.

**→ Sign up free at oneuptime.com**

### 🐳 Self-host with Docker Compose

Everything you need on a single server (Debian / Ubuntu / RHEL, Docker + Docker Compose). Great for homelabs and small teams — a Raspberry Pi even works.

# 1. Clone the release branch
git clone --depth 1 --single-branch --branch release https://github.com/OneUptime/oneuptime.git
cd oneuptime

# 2. Create your config (then edit it — set strong, random secrets!)
cp config.example.env config.env

# 3. Start everything
npm start

OneUptime is now running at **http://localhost** — open it and create your first account.

📖 Full guide: Docker Compose install · Sizing & requirements

### ☸️ Kubernetes with Helm — for production

helm repo add oneuptime https://helm-chart.oneuptime.com
helm install oneuptime oneuptime/oneuptime

📖 Full install instructions & values on Artifact Hub →

> **Upgrading an existing install?** See the upgrade guide.

* * *

✨ Everything in the box
-----------------------

Feature

What it does

📊

**Uptime Monitoring**

Website, API, IP, port, SSL, DNS, and synthetic monitors from multiple global regions.

📋

**Status Pages**

Beautiful branded status pages, incident history, scheduled maintenance, and subscriber notifications.

🚨

**Incident Management**

End-to-end incident workflow: declare, assign, communicate, resolve, and run post-mortems.

📞

**On-Call & Alerts**

On-call schedules and escalation policies with SMS, phone call, push, email, and Slack alerts.

📝

**Log Management**

Ingest, store, search, and alert on logs via OpenTelemetry.

🔍

**APM & Traces**

Distributed traces, spans, and performance dashboards to find slow paths and bottlenecks.

📈

**Metrics & Dashboards**

Custom dashboards over your telemetry — build the views your team needs.

🐛

**Error Tracking**

Capture exceptions with full stack traces, context, and release tracking.

⚡

**Workflows**

Automate and integrate with Slack, Jira, GitHub, Microsoft Teams, and 5,000+ apps.

🤖

**AI Copilot**

An always-on agent that finds anomalies across logs, traces & metrics, spots root causes, and opens PRs with fixes.

**⚡ Automate the busywork**  

Wire up escalations, ticketing, and notifications on a visual, no-code canvas — or drop in custom code. The incident above paged on-call, opened a Jira ticket, and posted to Slack without anyone lifting a finger.

### 🖥️ Infrastructure Monitoring

Drop in copy-paste, **OpenTelemetry-based** agents to watch everything your services run on — with ready-made alert templates included:

-   **Servers & VMs** — CPU, memory, disk, network, processes, and logs from Linux, macOS & Windows. Docs →
-   **Kubernetes** — one `helm install` ships node/pod/container/cluster metrics, events, logs, and eBPF traces & service maps. Docs →
-   **Docker** — a single agent auto-discovers every container and ships metrics & logs. Docs →
-   **Podman** — same one-agent auto-discovery via Podman's Docker-compatible socket. Docs →
-   **Proxmox** — nodes, VMs, containers, storage, HA state, backup coverage & replication health. Docs →
-   **Ceph** — cluster health, capacity forecasts, and OSD/pool/PG/monitor visibility. Docs →

* * *

💼 Community vs. Enterprise
---------------------------

**Community**

**Enterprise**

**Best for**

Self-hosters & small teams

Regulated teams needing premium support

**Cost**

Free & open source

Contact sales

**Features**

Full feature set

Full feature set + hardened images, priority support, custom features & data residency

* * *

💡 Why OneUptime?
-----------------

Our mission is simple: **reduce downtime and help more products succeed.** Instead of duct-taping seven vendors together, you get one platform that helps you understand _why_ things break, respond to incidents fast, and cut operational toil — fully open source, so you own your data and your stack.

* * *

🤝 Contributing
---------------

We welcome contributions of every size. Start here:

-   🐛 **Open issues** — pick one up, or file a new one
-   ✅ **Help write tests** for the codebase
-   🧑‍💻 **Local development guide** to get set up
-   📖 Read the **contributing guidelines**
-   💬 Chat with us in the **Developer Slack** or **Community Slack**

❤️ Support the project
----------------------

If OneUptime is useful to you:

-   ⭐ **Star this repo** — it genuinely helps others find us
-   💵 **Sponsor us** — every dollar ships new features
-   🛍️ **Grab some merch** — all proceeds fund open-source development

* * *

📄 License
----------

OneUptime is licensed under the Apache License 2.0.

Made with ❤️ by the OneUptime team and contributors.
