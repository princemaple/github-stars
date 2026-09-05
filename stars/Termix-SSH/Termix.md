---
project: Termix
stars: 15039
description: Self-hosted SSH and remote desktop management.
url: https://github.com/Termix-SSH/Termix
---

Termix
======

Self-hosted server management, from SSH and remote desktop to automations

English · 中文 · 日本語 · 한국어 · Français · Deutsch · Español · Português · Русский · العربية · हिन्दी · Türkçe · Tiếng Việt · Italiano

  

Termix is free and open source. If you find it useful, consider donating to help cover server costs and development time.

  
  
  

  
Achieved on September 1st, 2025

  

Overview
--------

Termix is a free, open source, self-hosted platform for managing your servers. It puts SSH terminals, remote desktops (RDP, VNC, Telnet), file transfers, tunnels, Docker, metrics, and automations in one place, on web, desktop, and mobile. It is a self-hosted alternative to Termius that stays free forever.

  

Features
--------

**SSH Terminal:** A full terminal with browser-like tabs and split screen, up to 6 panels at once. Pick your theme, font, and colors. A toolbar sits above each session with live CPU, memory, and disk, plus quick links to that host's files, Docker, tunnels, and metrics.

**Remote Desktop:** RDP, VNC, and Telnet in the browser, in tabs and split screen like any other session. Includes a file browser for RDP drives and drag-and-drop upload. On Windows desktop you can also open a host in the native RDP client.

**SSH Tunnels:** Local, remote, and dynamic SOCKS forwarding with auto reconnect and health checks. Client-to-server tunnels on the desktop app are stored on that machine, and you can save presets to the server to move a setup to another client.

**File Manager:** Browse, edit, upload, download, rename, move, and delete files over SFTP, with sudo support. View and edit code, images, audio, and video. Copy files straight from one server to another, with the fastest route picked for you and transfers checked for integrity.

**Docker and Podman:** Start, stop, pause, and remove containers, watch their stats, and open a shell inside one. Works with both Docker and Podman. It is not meant to replace Portainer or Dockge, just to manage containers you already have.

**Host Manager:** Save and organize hosts with tags and nested folders you can name and color. Reuse saved credentials across hosts, deploy SSH keys automatically, group hosts under a parent host, bulk edit and export, and use Quick Connect for one-off connections you do not want to save.

**Host Metrics:** CPU, memory, disk, network, temperature, uptime, processes, ports, logins, and system info on most Linux servers, with history graphs. Manager cards let you handle services, cron jobs, packages, users, firewall rules, WireGuard, Tailscale, SSL certs, logs, and health checks without leaving Termix.

**Automations:** Pick a trigger, then say what should happen. Triggers include a metric crossing a threshold, a host going up or down, a health check changing, a schedule, a container event, or an incoming webhook. Steps can run commands and snippets, control containers and tunnels, wake a host, call a URL, wait, branch on a condition, run another automation, and notify you over ntfy, Discord, or a webhook. Test runs let you try it safely first.

**Fleets:** Group hosts into a fleet by picking them or with tag rules, so new hosts join on their own. Run one command on every host at once, push and pull files across all of them, install packages, and collect an inventory of OS, kernel, arch, and uptime.

**AI Assistant:** Optional, and off until you turn it on. Connect OpenAI, Anthropic, Gemini, Ollama, or any OpenAI compatible endpoint and ask about your setup. It reads hosts, fleets, snippets, and alerts, and proposes changes for you to approve instead of making them. It can never touch credentials, users, or settings. Admins can leave it off for the whole instance, and you can hide it during setup.

**Login and Users:** Local accounts plus OIDC, LDAP, GitHub, and Google sign-in, with 2FA (TOTP), passkeys (WebAuthn), and trusted devices. Admins can manage users, map OIDC groups to roles, see every active session across platforms, and revoke them. Link your local and OIDC accounts together, and read the audit log of what everyone did.

**Roles and Sharing:** Create roles and share hosts with users or roles at four levels: connect, view, edit, and manage. Works with every auth type and every protocol, and you can override the credentials used for a shared host.

**Alerts:** Set rules on host metrics like CPU, memory, and disk, and get notified over ntfy, Discord, or a webhook when they fire. See firing and resolved alerts in a history log, and dismiss the ones you do not care about.

**Homepage:** A drag-and-drop widget grid you build yourself. Widgets for host status, pings, service links, bookmarks, search, clocks, calendars, countdowns, notes, RSS, weather, images, iframes, Docker, tunnels, metrics charts, custom APIs, and even a live terminal.

**Snippets and Tools:** Save commands you run often and fire them off in one click, with variables for the host and your own inputs. Run a single command across every open terminal, and search your command history with autocomplete.

**Session Sharing:** Share a live terminal, RDP, VNC, or Telnet session in real time. Send a link anyone can join without an account, or share with a specific Termix user, in read-only or read-write mode. Shares can expire on their own or be revoked, and can be turned off globally or per host.

**Session Recording and Logs:** Record terminal, RDP, and VNC sessions and play them back later. Download plain text logs of a session, and check the connection log to see exactly what happened during a connection.

**Serial Connections:** Talk to serial devices like routers, switches, and microcontrollers from the browser or desktop app. Set baud rate, data bits, stop bits, and parity. Uses the Web Serial API in supported browsers, or a native backend in the desktop app.

**Tailscale:** Pull devices from your tailnet to add them as hosts in a couple of clicks, and connect with Tailscale SSH so your tailnet ACLs handle access and no credentials are stored. Headscale and custom endpoints work too.

**Proxmox:** Import hosts straight from a Proxmox instance, and watch node and guest stats, including CPU, memory, and storage, in their own tab.

**Workspaces and Tabs:** Save a set of tabs with their split layout and reopen the whole thing in one click. Termix also remembers your last session, so your tabs come back across refreshes and devices.

**Guided Setup:** A short setup walks you through picking an interface preset, your theme, the features you want, and your first host. Simple mode hides what you do not use, and you can rerun setup or switch presets any time.

**Desktop Standalone and Sync:** The desktop app runs on its own with a local backend and database, no server needed. You can also connect it to a Termix server for two-way sync of hosts, credentials, snippets, and more, and choose whether connections start locally or through the server.

**Command Line Interface:** A `termix` CLI for your shell and your scripts. Open terminals, run a command on one host or a whole fleet, move files over SFTP, and manage hosts, snippets, and credentials. Install with `npm install -g @termix-cli/cli` or grab a standalone binary. See the CLI docs.

**Security:** Passwords, keys, and other secrets are encrypted per user, and the database files themselves can be encrypted on disk. See the docs for how it works.

**Languages:** Around 30 languages built in, managed through Crowdin.

  
**More features**  

-   **Dashboard** - Your servers at a glance, with cards you arrange yourself
-   **Network Graph** - See your homelab drawn out from your hosts, with live status
-   **Tmux Monitor** - Browse tmux sessions, windows, and panes, with previews and search
-   **API Keys** - User-scoped keys with expiry dates for scripts and CI
-   **Export and Import** - Move hosts, credentials, and file manager data in and out
-   **Automatic SSL** - Certificates generated and renewed for you, with HTTPS redirects, or bring your own
-   **Databases** - SQLite by default, with PostgreSQL and MySQL supported too
-   **Modern UI** - Clean React interface that works on desktop and mobile, with themes like light, dark, and Dracula. Any connection can open full screen from a URL
-   **Command Palette** - Double tap left shift to jump to a host from the keyboard
-   **Keyboard Shortcuts** - Move between tabs, close tabs, and more, all rebindable
-   **Wake-on-LAN** - Wake a machine from Termix or from an automation step
-   **Trusted Proxy Auth** - Let a reverse proxy handle sign-in and pass the user through
-   **SSH Feature Rich** - Jump hosts, Warpgate, TOTP prompts, SOCKS5, host key verification, password autofill, OPKSSH, tmux, port knocking, terminal logging, agent forwarding, Bitwarden SSH agent, HashiCorp Vault SSH signing, and more
-   **Termix ID** - A built-in take on sshid.io. Claim a handle, publish your public keys at a resolver URL, and issue SSH certificates from the built-in CA

  

Platform Support
----------------

Platform

Distribution

**Web**

Any modern browser (Chrome, Safari, Firefox) · PWA support

**Windows** x64/ia32

Portable · MSI Installer · Chocolatey

**Linux** x64/ia32

Portable · AUR · AppImage · Deb · Flatpak

**macOS** x64/ia32, v12.0+

Apple App Store · DMG · Homebrew

**iOS/iPadOS** v15.1+

Apple App Store · IPA

**Android** v7.0+

Google Play Store · APK

  

Installation
------------

Visit the Termix Docs for full installation instructions across all platforms.

Deploying to Kubernetes? The Helm chart is in `charts/termix`, and setup instructions covering Ingress, Traefik, Argo CD, GitHub Actions, and GitLab CI are at docs.termix.site/install/server/kubernetes.

Sample Docker Compose file (you can omit `guacd` and the network if you don't plan on using remote desktop features):

services:
  termix:
    image: ghcr.io/lukegus/termix:latest
    container\_name: termix
    restart: unless-stopped
    ports:
      - "8080:8080"
    volumes:
      - termix-data:/app/data
    environment:
      PORT: "8080"
    depends\_on:
      - guacd
    networks:
      - termix-net

  guacd:
    image: guacamole/guacd:1.6.0
    container\_name: guacd
    restart: unless-stopped
    ports:
      - "4822:4822"
    networks:
      - termix-net

volumes:
  termix-data:
    driver: local

networks:
  termix-net:
    driver: bridge

### Command Line Interface

Termix also has a CLI, so you can manage your servers from a terminal and use Termix in your own scripts.

npm install -g @termix-cli/cli
termix login --url https://termix.example.com
termix ssh 1

It can open terminals, run a command on one host or a whole fleet, move files over SFTP, and manage hosts, snippets and credentials. Full documentation is at docs.termix.site/cli.

### Cloud Hosting

You can run the Termix server on a VPS instead of inside your own network. If Termix runs on the network it manages, an outage takes Termix down with it, right when you need it to fix things. Running it elsewhere keeps it reachable, gives you a static IP, and lets you get in from anywhere without a VPN or port forward.

GINERNET sponsors Termix, and the docs have a step by step guide for deploying to their VPS platform.

  

Telemetry
---------

Termix sends a small anonymous ping once a day so I can see how many instances are running and which features get used. It contains a random instance ID, how many users and hosts you have, the app version, and which features (terminal, file manager, tunnels, docker, etc.) were used in the last 24 hours. It never contains usernames, hostnames, IP addresses, credentials, or anything else that identifies you or your servers.

It is on by default. Turn it off in Admin Settings under General, or set `ENABLE_TELEMETRY=false` before you ever start Termix.

  

Donate
------

Termix is free and open source with no subscriptions or paid plans. If you find it useful, consider donating to help cover server costs, domains, and development time. Donations also help fund the time to research and learn what's needed to build features like SAML, Kubernetes, and Agent support. Track progress and donate below.

Donate

  

Sponsors
--------

Interested in a paid placement to support development? Email mail@termix.site.

  
                           

  

Support
-------

Need help or want to request a feature? Open a new issue and add as much detail as you can, in English if possible. You can also ask in the support channel on Discord, though replies there can take longer.

  

Screenshots
-----------

  

Watch update overviews on YouTube

  
  

Some videos and images may be out of date or may not perfectly showcase features.

  

Planned Features
----------------

See Projects for all planned features. If you are looking to contribute, see Contributing.

  

License
-------

Distributed under the Apache License Version 2.0. See `LICENSE` for more information.
