---
project: Termix
stars: 14788
description: Self-hosted SSH and remote desktop management.
url: https://github.com/Termix-SSH/Termix
---

Termix
======

Self-hosted SSH management and remote desktop access

English · 中文 · 日本語 · 한국어 · Français · Deutsch · Español · Português · Русский · العربية · हिन्दी · Türkçe · Tiếng Việt · Italiano

  

Termix is free and open source. If you find it useful, consider donating to help cover server costs and development time.

  
  
  

  
Achieved on September 1st, 2025

  

Overview
--------

Termix is an open-source, forever-free, self-hosted all-in-one server management platform. It provides a multi-platform solution for managing your servers and infrastructure through a single, intuitive interface. Termix offers SSH terminal access, remote desktop control (RDP, VNC, Telnet), SSH tunneling capabilities, remote file management, and many other tools. Termix is the perfect free and self-hosted alternative to Termius available for all platforms.

  

Features
--------

**SSH Terminal Access:** Full-featured terminal with split-screen support (up to 4 panels) with a browser-like tab system. Includes support for customizing the terminal including common terminal themes, fonts, and other components.

**Remote Desktop Access:** RDP, VNC, and Telnet support over the browser with complete customization and split screening.

**SSH Tunnel Management:** Create and manage server-to-server SSH tunnels with automatic reconnection, health monitoring, and local, remote, or dynamic SOCKS forwarding. Desktop client-to-server tunnel settings are stored locally per desktop install, optional C2S preset snapshots can be saved to the server, renamed, loaded, or deleted when you want to move a local tunnel configuration between clients.

**Remote File Manager:** Manage files directly on remote servers with support for viewing and editing code, images, audio, and video. Upload, download, rename, delete, and move files seamlessly with sudo support. Includes support for moving files from server to server.

**Docker and Podman Management:** Start, stop, pause, remove containers. View container stats. Control containers using a docker exec terminal. Supports both Docker and Podman as the container runtime. It was not made to replace Portainer or Dockge but rather to simply manage your containers compared to creating them.

**SSH Host Manager:** Save, organize, and manage your SSH connections with tags and folders (folder customization and nested folder support), and easily save reusable login info while being able to automate the deployment of SSH keys.

**Host Metrics:** View CPU, memory, disk usage, network, uptime, system information, firewall, port monitor, log viewer, users/permissions, certificates, and many more which work on most Linux based servers. Includes time-series history graphs and threshold-based alerts with ntfy and webhook support.

**User Authentication:** Secure user management with admin controls (can edit other users information) and OIDC/LDAP/SSO (with access control), 2FA (TOTP), and passkey (WebAuthn) support. View active user sessions across all platforms and revoke permissions. Link your OIDC/Local accounts together. View audit log of all users actions.

**Tailscale Integration:** List devices from your tailnet to quickly add them as hosts, and connect using Tailscale SSH as an authentication method, letting your tailnet ACLs handle authorization without storing credentials.

**RBAC/Sharing:** Create roles and share hosts across users/roles. Supports all auth types and all host protocols.

**Serial Connections:** Connect to serial devices (routers, switches, microcontrollers, etc.) directly from the browser or desktop app. Configure baud rate, data bits, stop bits, and parity. Uses the Web Serial API in supported browsers or a native backend in the Electron app.

**Alerts:** Set threshold-based alert rules on host metrics (CPU, memory, disk, etc.) and get notified via ntfy or webhooks when they fire. View firing and resolved alerts in a history log.

**Homepage:** A fully customizable homepage with a drag-and-drop widget grid. Add widgets for host status, service links, clocks, notes, RSS feeds, weather, Docker containers, host metrics charts, embedded terminals, iframes, and more.

**Database Encryption:** Backend stored as encrypted SQLite database files. View docs for more.

**Network Graph:** Customize your Dashboard to visualize your homelab based off your SSH connections with status support.

**SSH Tools:** Create reusable command snippets that execute with a single click. Run one command simultaneously across multiple open terminals.

**Persistent Tabs:** SSH sessions and tabs stay open across devices/refreshes if enabled in user profile.

**Languages:** Built-in support ~30 languages (managed by Crowdin).

**Session Sharing:** Share a live terminal, RDP, VNC, or Telnet session with others in real time. Share via a link (joined anonymously, no account needed) or with a specific Termix user, and choose read-only or read-write access. Shares can expire automatically or be revoked at any time, and session sharing can be toggled globally or per-host.

**Desktop Standalone + 2-Way Sync:** The Electron desktop app runs fully standalone with its own local backend and database, no server required. Optionally connect it to a remote Termix server for automatic two-way sync of hosts, credentials, snippets, and more, and choose whether SSH connections are started locally or through the remote server.

  
**More features**  

-   **Dashboard** - View server information at a glance on your dashboard
-   **API Keys** - Create user-scoped API keys with expiration dates to be used for automation/CI
-   **Data Export/Import** - Export and import SSH hosts, credentials, and file manager data
-   **Automatic SSL Setup** - Built-in SSL certificate generation and management with HTTPS redirects
-   **Modern UI** - Clean desktop/mobile-friendly interface built with React, Tailwind CSS, and Shadcn. Choose between many different UI themes including light, dark, Dracula, etc. Use URL routes to open any connection in full-screen.
-   **Command History** - Auto-complete and view previously ran SSH commands
-   **Quick Connect** - Connect to a server without having to save the connection data
-   **Command Palette** - Double tap left shift to quickly access SSH connections with your keyboard
-   **Proxmox Integration** - Auto-add hosts into Termix from your Proxmox instance
-   **SSH Feature Rich** - Supports jump hosts, Warpgate, TOTP based connections, SOCKS5, host key verification, password autofill, OPKSSH, tmux, port knocking, terminal logging, SSH agent forwarding, Bitwarden SSH agent, HashiCorp Vault SSH signing, and more.
-   **Termix ID** - A sshid.io equivalent built into Termix. Claim a handle, publish your public SSH keys at a resolver URL, and use a built-in CA to issue SSH certificates.

  

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

### Cloud Hosting

You can also run the Termix server on a cloud VPS instead of inside your own network. If Termix runs on the network it manages, an outage takes Termix with it, and your hosts and saved sessions are stuck inside the system you are trying to fix. Hosting it externally keeps it reachable no matter what happens to your network, and gives you a static IP and access from anywhere without a VPN or port forward.

GINERNET is a sponsor of Termix, and there is a full step by step guide for deploying to their VPS platform in the docs.

  

Telemetry
---------

Termix sends a small anonymous usage ping once every 24 hours to help understand how many instances are running and which features are actually used. This only includes a randomly generated instance ID, a count of users and hosts, the app version, and whether certain features (terminal, file manager, tunnels, docker, etc.) were used in the last 24 hours. It never includes usernames, hostnames, IP addresses, credentials, or any other identifying or connection data.

This is opt-out and enabled by default. You can disable it at any time in Admin Settings under General, or set `ENABLE_TELEMETRY=false` to turn it off before you ever spin-up Termix.

  

Donate
------

Termix is free and open source with no subscriptions or paid plans. If you find it useful, consider donating to help cover server costs, domains, and development time. Donations also help fund the time to research and learn what's needed to build features like SAML, Kubernetes, and Agent support. Track progress and donate below.

Donate

  

Sponsors
--------

Interested in a paid placement to support development? Email mail@termix.site.

  
                           

  

Support
-------

If you need help or want to request a feature with Termix, visit the Issues page, log in, and press `New Issue`. Please be as detailed as possible in your issue, preferably written in English. You can also join the Discord server and visit the support channel, however, response times may be longer.

  

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
