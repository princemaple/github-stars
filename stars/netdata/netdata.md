---
project: netdata
stars: 77911
description: The fastest path to AI-powered full stack observability, even for lean teams.
url: https://github.com/netdata/netdata
---

### X-Ray Vision for your infrastructure!

#### Every Metric, Every Second. No BS.

  

  
  
  

**Visit our Home Page**

* * *

MENU: **WHO WE ARE** | **KEY FEATURES** | **GETTING STARTED** | **HOW IT WORKS** | **FAQ** | **DOCS** | **COMMUNITY** | **CONTRIBUTE** | **LICENSE**

Warning

People **get addicted to Netdata.** Once you use it on your systems, _there's no going back._

* * *

WHO WE ARE
----------

Netdata is an open-source, real-time infrastructure monitoring platform. Monitor, detect, and act across your entire infrastructure.

**Core Advantages:**

-   **Instant Insights** – With Netdata you can access per-second metrics and visualizations.
-   **Zero Configuration** – You can deploy immediately without complex setup.
-   **ML-Powered** – You can detect anomalies, predict issues, and automate analysis.
-   **Efficient** – You can monitor with minimal resource usage and maximum scalability.
-   **Secure & Distributed** – You can keep your data local with no central collection needed.

With Netdata, you get real-time, per-second updates. Clear **insights at a glance**, no complexity.

**All heroes have a great origin story. Click to discover ours.**  

In 2013, at the company where Costa Tsaousis was COO, a significant percentage of their cloud-based transactions failed silently, severely impacting business performance.

Costa and his team tried every troubleshooting tool available at the time. None could identify the root cause. As Costa later wrote:

“_I couldn’t believe that monitoring systems provide so few metrics and with such low resolution, scale so badly, and cost so much to run._”

Frustrated, he decided to build his own monitoring tool, starting from scratch.

That decision led to countless late nights and weekends. It also sparked a fundamental shift in how infrastructure monitoring and troubleshooting are approached, both in method and in cost.

### Most Energy-Efficient Monitoring Tool

According to the University of Amsterdam study, Netdata is the most energy-efficient tool for monitoring Docker-based systems. The study also shows Netdata excels in CPU usage, RAM usage, and execution time compared to other monitoring solutions.

* * *

Key Features
------------

Feature

Description

What Makes It Unique

**Real-Time**

Per-second data collection and processing

Works in a beat – click and see results instantly

**Zero-Configuration**

Automatic detection and discovery

Auto-discovers everything on the nodes it runs

**ML-Powered**

Unsupervised anomaly detection

Trains multiple ML models per metric at the edge

**Long-Term Retention**

High-performance storage

~0.5 bytes per sample with tiered storage for archiving

**Advanced Visualization**

Rich, interactive dashboards

Slice and dice data without query language

**Extreme Scalability**

Native horizontal scaling

Parent-Child centralization with multi-million samples/s

**Complete Visibility**

From infrastructure to applications

Simplifies operations and eliminates silos

**Edge-Based**

Processing at your premises

Distributes code instead of centralizing data

Note

Want to put Netdata to the test against Prometheus? Explore the full comparison.

* * *

Netdata Ecosystem
-----------------

This three-part architecture enables you to scale from single nodes to complex multi-cloud environments:

Component

Description

License

**Netdata Agent**

• Core monitoring engine  
• Handles collection, storage, ML, alerts, exports  
• Runs on servers, cloud, K8s, IoT  
• Zero production impact

GPL v3+

**Netdata Cloud**

• Enterprise features  
• User management, RBAC, horizontal scaling  
• Centralized alerts  
• Free community tier  
• No metric storage centralization

**Netdata UI**

• Dashboards and visualizations  
• Free to use  
• Included in standard packages  
• Latest version via CDN

NCUL1

What You Can Monitor
--------------------

With Netdata you can monitor all these components across platforms:

Component

Linux

FreeBSD

macOS

Windows

**System Resources**  
CPU, Memory and system shared resources

Full

Yes

Yes

Yes

**Storage**  
Disks, Mount points, Filesystems, RAID arrays

Full

Yes

Yes

Yes

**Network**  
Network Interfaces, Protocols, Firewall, etc

Full

Yes

Yes

Yes

**Hardware & Sensors**  
Fans, Temperatures, Controllers, GPUs, etc

Full

Some

Some

Some

**O/S Services**  
Resources, Performance and Status

Yes  
`systemd`

\-

\-

\-

**Processes**  
Resources, Performance, OOM, and more

Yes

Yes

Yes

Yes

System and Application **Logs**

Yes  
`systemd`\-journal

\-

\-

Yes  
`Windows Event Log`, `ETW`

**Network Connections**  
Live TCP and UDP sockets per PID

Yes

\-

\-

\-

**Containers**  
Docker/containerd, LXC/LXD, Kubernetes, etc

Yes

\-

\-

\-

**VMs** (from the host)  
KVM, qemu, libvirt, Proxmox, etc

Yes  
`cgroups`

\-

\-

Yes  
`Hyper-V`

**Synthetic Checks**  
Test APIs, TCP ports, Ping, Certificates, etc

Yes

Yes

Yes

Yes

**Packaged Applications**  
nginx, apache, postgres, redis, mongodb,  
and hundreds more

Yes

Yes

Yes

Yes

**Cloud Provider Infrastructure**  
AWS, GCP, Azure, and more

Yes

Yes

Yes

Yes

**Custom Applications**  
OpenMetrics, StatsD and soon OpenTelemetry

Yes

Yes

Yes

Yes

On Linux, you can continuously monitor all kernel features and hardware sensors for errors, including Intel/AMD/Nvidia GPUs, PCI AER, RAM EDAC, IPMI, S.M.A.R.T, Intel RAPL, NVMe, fans, power supplies, and voltage readings.

* * *

Getting Started
---------------

You can install Netdata on all major operating systems. To begin:

### 1\. Install Netdata

Choose your platform and follow the installation guide:

-   Linux Installation
-   macOS
-   FreeBSD
-   Windows
-   Docker Guide
-   Kubernetes Setup

Note

You can access the Netdata UI at `http://localhost:19999` (or `http://NODE:19999` if remote).

### 2\. Configure Collectors

Netdata auto-discovers most metrics, but you can manually configure some collectors:

-   All collectors
-   SNMP monitoring

### 3\. Configure Alerts

You can use hundreds of built-in alerts and integrate with:

`email`, `Slack`, `Telegram`, `PagerDuty`, `Discord`, `Microsoft Teams`, and more.

Note

Email alerts work by default if there's a configured MTA.

### 4\. Configure Parents

You can centralize dashboards, alerts, and storage with Netdata Parents:

-   Streaming Reference

Note

You can use Netdata Parents for central dashboards, longer retention, and alert configuration.

### 5\. Connect to Netdata Cloud

Sign in to Netdata Cloud and connect your nodes for:

-   Access from anywhere
-   Horizontal scalability and multi-node dashboards
-   UI configuration for alerts and data collection
-   Role-based access control
-   Free tier available

Note

Netdata Cloud is optional. Your data stays in your infrastructure.

Live Demo Sites
---------------

**See Netdata in action**  
**FRANKFURT** | **NEWYORK** | **ATLANTA** | **SANFRANCISCO** | **TORONTO** | **SINGAPORE** | **BANGALORE**  
_These demo clusters run with default configuration and show real monitoring data._  
_Choose the instance closest to you for the best performance._

* * *

How It Works
------------

With Netdata you can run a modular pipeline for metrics collection, processing, and visualization.

flowchart TB
  A\[Netdata Agent\]:::mainNode
  A1(Collect):::green --> A
  A2(Store):::green --> A
  A3(Learn):::green --> A
  A4(Detect):::green --> A
  A5(Check):::green --> A
  A6(Stream):::green --> A
  A7(Archive):::green --> A
  A8(Query):::green --> A
  A9(Score):::green --> A

  classDef green fill:#bbf3bb,stroke:#333,stroke-width:1px,color:#000
  classDef mainNode fill:#f0f0f0,stroke:#333,stroke-width:1px,color:#333

Loading

With each Agent you can:

1.  **Collect** – Gather metrics from systems, containers, apps, logs, APIs, and synthetic checks.
2.  **Store** – Save metrics to a high-efficiency, tiered time-series database.
3.  **Learn** – Train ML models per metric using recent behavior.
4.  **Detect** – Identify anomalies using trained ML models.
5.  **Check** – Evaluate metrics against pre-set or custom alert rules.
6.  **Stream** – Send metrics to Netdata Parents in real time.
7.  **Archive** – Export metrics to Prometheus, InfluxDB, OpenTSDB, Graphite, and others.
8.  **Query** – Access metrics via an API for dashboards or third-party tools.
9.  **Score** – Use a scoring engine to find patterns and correlations across metrics.

Note

Learn more: Netdata's architecture

Agent Capabilities
------------------

With the Netdata Agent, you can use these core capabilities out-of-the-box:

Capability

Description

**Comprehensive Collection**

• 800+ integrations  
• Systems, containers, VMs, hardware sensors  
• OpenMetrics, StatsD, and logs  
• OpenTelemetry support coming soon

**Performance & Precision**

• Per-second collection  
• Real-time visualization with 1-second latency  
• High-resolution metrics

**Edge-Based ML**

• ML models trained at the edge  
• Automatic anomaly detection per metric  
• Pattern recognition based on historical behavior

**Advanced Log Management**

• Direct systemd-journald and Windows Event Log integration  
• Process logs at the edge  
• Rich log visualization

**Observability Pipeline**

• Parent-Child relationships  
• Flexible centralization  
• Multi-level replication and retention

**Automated Visualization**

• NIDL data model  
• Auto-generated dashboards  
• No query language needed

**Smart Alerting**

• Pre-configured alerts  
• Multiple notification methods  
• Proactive detection

**Low Maintenance**

• Auto-detection  
• Zero-touch ML  
• Easy scalability  
• CI/CD friendly

**Open & Extensible**

• Modular architecture  
• Easy to customize  
• Integrates with existing tools

* * *

CNCF Membership
---------------

  
Netdata actively supports and is a member of the Cloud Native Computing Foundation (CNCF).  
It is one of the most starred projects in the CNCF landscape.

* * *

FAQ
---

**Is Netdata secure?**  

Yes. Netdata follows OpenSSF best practices, has a security-first design, and is regularly audited by the community.

-   Security design
-   Security policies and advisories

**Does Netdata use a lot of resources?**  

No. Even with ML and per-second metrics, Netdata uses minimal resources.

-   ~5% CPU and 150MiB RAM by default on production systems
-   <1% CPU and ~100MiB RAM when ML and alerts are disabled and using ephemeral storage
-   Parents scale to millions of metrics per second with appropriate hardware

> You can use the **Netdata Monitoring** section in the dashboard to inspect its resource usage.

**How much data retention is possible?**  

As much as your disk allows.

With Netdata you can use tiered retention:

-   Tier 0: per-second resolution
-   Tier 1: per-minute resolution
-   Tier 2: per-hour resolution

These are queried automatically based on the zoom level.

**Can Netdata scale to many servers?**  

Yes. With Netdata you can:

-   Scale horizontally with many Agents
-   Scale vertically with powerful Parents
-   Scale infinitely via Netdata Cloud

> You can use Netdata Cloud to merge many independent infrastructures into one logical view.

**Is disk I/O a concern?**  

No. Netdata minimizes disk usage:

-   Metrics are flushed to disk every 17 minutes, spread out evenly
-   Uses direct I/O and compression (ZSTD)
-   Can run entirely in RAM or stream to a Parent

> You can use `alloc` or `ram` mode for no disk writes.

**How is Netdata different from Prometheus + Grafana?**  

With Netdata you get a complete monitoring solution—not just tools.

-   No manual setup or dashboards needed
-   Built-in ML, alerts, dashboards, and correlations
-   More efficient and easier to deploy

> Performance comparison

**How is Netdata different from commercial SaaS tools?**  

With Netdata you can store all metrics on your infrastructure—no sampling, no aggregation, no loss.

-   High-resolution metrics by default
-   ML per metric, not shared models
-   Unlimited scalability without skyrocketing cost

**Can Netdata run alongside Nagios, Zabbix, etc.?**  

Yes. You can use Netdata together with traditional tools.

With Netdata you get:

-   Real-time, high-resolution monitoring
-   Zero configuration and auto-generated dashboards
-   Anomaly detection and advanced visualization

**What if I feel overwhelmed?**  

You can start small:

-   Use the dashboard's table of contents and search
-   Explore anomaly scoring ("AR" toggle)
-   Create custom dashboards in Netdata Cloud

> Docs and guides

**Do I have to use Netdata Cloud?**  

No. Netdata Cloud is optional.

Netdata works without it, but with Cloud you can:

-   Access remotely with SSO
-   Save dashboard customizations
-   Configure alerts centrally
-   Collaborate with role-based access

**What telemetry does Netdata collect?**  

Anonymous telemetry helps improve the product. You can disable it:

-   Add `--disable-telemetry` to the installer, or
-   Create `/etc/netdata/.opt-out-from-anonymous-statistics` and restart Netdata

> Telemetry helps us understand usage, not track users. No private data is collected.

**Who uses Netdata?**  

You'll join users including:

-   Major companies (Amazon, ABN AMRO Bank, Facebook, Google, IBM, Intel, Netflix, Samsung)
-   Universities (NYU, Columbia, Seoul National, UCL)
-   Government organizations worldwide
-   Infrastructure-intensive organizations
-   Technology operators
-   Startups and freelancers
-   SysAdmins and DevOps professionals

* * *

📖 Documentation
----------------

Visit Netdata Learn for full documentation and guides.

Note

Includes deployment, configuration, alerting, exporting, troubleshooting, and more.

* * *

🎉 Community
------------

Join the Netdata community:

-   Discord
-   Forum
-   GitHub Discussions

Note

Code of Conduct

Follow us on: Twitter | Reddit | YouTube | LinkedIn

* * *

🙏 Contribute
-------------

We welcome your contributions.

Ways you help us stay sharp:

-   Share best practices and monitoring insights
-   Report issues or missing features
-   Improve documentation
-   Develop new integrations or collectors
-   Help users in forums and chats

Note

Contribution guide

* * *

📜 License
----------

The Netdata ecosystem includes:

-   **Netdata Agent** – Open-source core (GPLv3+). **Includes** data collection, storage, ML, alerting, APIs and **redistributes** several other open-source tools and libraries.
    -   Netdata Agent License
    -   Netdata Agent Redistributed
-   **Netdata UI** – Closed-source but free to use with Netdata Agent and Cloud. Delivered via CDN. It integrates third-party open-source components.
    -   Netdata Cloud UI License
    -   Netdata UI third-party licenses
-   **Netdata Cloud** – Closed-source, with free and paid tiers. Adds remote access, SSO, scalability.
