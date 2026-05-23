---
project: 3x-ui
stars: 37960
description: Xray panel supporting multi-protocol multi-user expire day & traffic & IP limit (Vmess, Vless, Trojan, ShadowSocks, Wireguard, Hysteria, Tunnel, Mixed, HTTP, Tun) 
url: https://github.com/MHSanaei/3x-ui
---

English | فارسی | العربية | 中文 | Español | Русский

**3X-UI** — advanced, open-source web-based control panel designed for managing Xray-core server. It offers a user-friendly interface for configuring and monitoring various VPN and proxy protocols.

Important

This project is only for personal usage, please do not use it for illegal purposes, and please do not use it in a production environment.

As an enhanced fork of the original X-UI project, 3X-UI provides improved stability, broader protocol support, and additional features.

Quick Start
-----------

bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)

For full documentation, please visit the project Wiki.

Database Options
----------------

3X-UI supports two backends, chosen during the install:

-   **SQLite** (default) — a single file at `/etc/x-ui/x-ui.db`. Zero setup, ideal for small/medium deployments.
-   **PostgreSQL** — recommended for high client counts or multi-node setups. The installer can install PostgreSQL locally for you, or accept a DSN to an existing server.

At runtime the backend is selected via env vars (the installer writes these to `/etc/default/x-ui` for you):

```
XUI_DB_TYPE=postgres
XUI_DB_DSN=postgres://xui:password@127.0.0.1:5432/xui?sslmode=disable
```

### Migrating an existing SQLite install to PostgreSQL

x-ui migrate-db --dsn "postgres://xui:password@127.0.0.1:5432/xui?sslmode=disable"
# then set XUI\_DB\_TYPE and XUI\_DB\_DSN in /etc/default/x-ui and restart:
systemctl restart x-ui

The source SQLite file is left untouched; remove it manually once you have verified the new backend.

### Docker

The default `docker compose up -d` keeps using SQLite. To run with the bundled PostgreSQL service, uncomment the two `XUI_DB_*` env lines in `docker-compose.yml` and start with the profile:

docker compose --profile postgres up -d

A Special Thanks to
-------------------

-   alireza0

Acknowledgment
--------------

-   Iran v2ray rules (License: **GPL-3.0**): _Enhanced v2ray/xray and v2ray/xray-clients routing rules with built-in Iranian domains and a focus on security and adblocking._
-   Russia v2ray rules (License: **GPL-3.0**): _This repository contains automatically updated V2Ray routing rules based on data on blocked domains and addresses in Russia._

Community Tools
---------------

Tools and integrations built by the community around 3x-ui.

-   terraform-provider-3x-ui (License: **MIT**): _Manage inbounds, clients, panel settings, and Xray configuration as code with Terraform / OpenTofu._

Support project
---------------

**If this project is helpful to you, you may wish to give it a**🌟

  

Stargazers over Time
--------------------
