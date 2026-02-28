---
project: UptimeFlare
stars: 3408
description: ✔ Free and serverless uptime monitoring / status page on Cloudflare Workers, with Geo-specific checks
url: https://github.com/lyc8503/UptimeFlare
---

✔UptimeFlare
============

A more advanced, serverless, and free uptime monitoring & status page solution, powered by Cloudflare Workers, complete with a user-friendly interface.

🎉 **\[UPDATE 2026/01/03\]** I have just migrated UptimeFlare from KV to D1 Database. I also updated the Terraform Cloudflare provider to v5 and improved the deployment process. The data structure has been optimized to resolve long-standing performance issues.

New users can deploy directly, while existing users can have a simple auto migration process (upgrade docs below)! Feel free to open an issue if you run into any trouble deploying.

⭐Features
---------

-   Open-source, easy to deploy (in under 10 minutes, no local tools required), and free
-   Monitoring capabilities
    -   Up to 50 checks at 1-minute intervals
    -   Geo-specific checks from over 310 cities worldwide
    -   Support for HTTP/HTTPS/TCP port monitoring
    -   Up to 90-day uptime history and uptime percentage tracking
    -   Customizable request methods, headers, and body for HTTP(s)
    -   Custom status code & keyword checks for HTTP(s)
    -   Downtime notification supporting 100+ notification channels
    -   Customizable Webhook
    -   Multi-language support (English/Chinese)
-   Status page
    -   Interactive ping (response time) chart for all types of monitors
    -   Scheduled maintenances alerts & Incident history page
    -   Responsive UI that adapts to your system theme
    -   Customizable status page
    -   Use your own domain with CNAME
    -   Optional password authentication (private status page)
    -   JSON API for fetching realtime status data

👀Demo
------

My status page (Online demo): https://uptimeflare.pages.dev/

Some screenshots:

⚡Quickstart / 📄Documentation
-----------------------------

Please refer to Wiki

🚀Upgrade existing deployments
------------------------------

Get the latest features right away with simple upgrade process

⚙️Docs for developer
--------------------

To contribute new features or customize your deployment furthermore, see here.

New features (TODOs)
--------------------

-   Specify region for monitors
-   TCP `opened` promise
-   Use apprise to support various notification channels
-   Telegram example
-   Bark example
-   Email notification via Cloudflare Email Workers
-   Improve docs by providing simple examples
-   Notification grace period
-   SSL certificate checks
-   Self-host Dockerfile
-   Incident history
-   Improve `checkLocationWorkerRoute` and fix possible `proxy failed`
-   Groups
-   Remove old incidents
-   Known issue: `fetch` doesn't support non-standard port (resolved after CF update)
-   Compatibility date update
-   Scheduled Maintenance
-   Add docs for dev
-   Migration to Terraform Cloudflare provider version 5.x
-   Cloudflare D1 database
-   Scheduled maintenances (via IIFE)
-   Simpler config example
-   Upcoming maintenances
-   Universal Webhook upgrade
-   i18n...? (maybe)
-   ICMP via proxy?
-   Add default UA
-   Customizable footer
-   New header logo
-   Improve CPU time usage
-   Local deployment (docs WIP)
