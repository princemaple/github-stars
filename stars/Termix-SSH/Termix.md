---
project: Termix
stars: 15578
description: Self-hosted, plugin-based server management.
url: https://github.com/Termix-SSH/Termix
---

Termix
======

Self-hosted, plugin-based server management

  

Overview
--------

Termix is a free, open source, self-hosted server management platform built on plugins. The core keeps your hosts, credentials, users, sharing and sessions. Everything else, like the SSH terminal, remote desktop, file manager, Docker and metrics, is a plugin you can turn on, off or remove.

It runs on web, desktop and mobile. Think of it as a free, self-hosted Termius.

  

Try the Demo
------------

Try it at demo.termix.site. Any username and password works.

  

Core
----

What every install has, with or without plugins:

-   Hosts: Save hosts in nested folders with tags and parent hosts, bulk edit, import and export, and use Quick Connect for one-off connections
-   Credentials: Reuse saved passwords and keys across hosts, with host defaults you can set for the server, a user or a folder
-   Sharing and Roles: Share hosts, credentials and folders with users or roles at four levels: connect, view, edit and manage
-   Accounts: Local accounts, sessions you can see and revoke, trusted devices, API keys and an audit log
-   Security: Passwords, keys and other secrets are encrypted per user, and the database can be encrypted on disk
-   Desktop Sync: The desktop app runs on its own and can link to a Termix server to keep an offline copy of your account
-   Interface: Tabs and split screen, a command palette (double tap left shift), rebindable shortcuts, themes, branding and around 30 languages
-   Databases: SQLite by default, with PostgreSQL and MySQL supported too

  

Plugins
-------

Plugins add everything else. The official ones ship with Termix, and admins can install, update or remove plugins from the Plugins tab. Each plugin has its own repo.

Plugin

What it does

ACME Certificates

Gets the Termix HTTPS certificate from Let's Encrypt or any ACME provider and renews it for you.

AI Assistant

An AI assistant that reads your setup and proposes changes for you to approve.

Alerts

One inbox for every alert in Termix, with delivery to webhooks, ntfy, Discord and email.

Automations

Run steps on your hosts on a schedule or when something happens.

Docker

Manage Docker and Podman containers on your hosts over SSH, with logs, stats and a console.

File Manager

Browse, edit and move files over SFTP, including straight from one server to another.

Fleets

Group hosts into fleets and run commands, package actions and file transfers on all of them at once.

HashiCorp Vault

Connect to hosts with short-lived SSH certificates signed by HashiCorp Vault.

Homepage

A drag and drop widget page for your servers and services, plus service links for the dashboard.

Host Metrics

Live CPU, memory, disk, network and GPU stats, plus tools to manage your hosts.

LDAP

Sign in with your LDAP or Active Directory username and password.

Network Topology

Draws your hosts and the links between them as a live, interactive graph.

OPKSSH

Connect to hosts with short-lived OpenPubkey SSH certificates after signing in with your identity provider.

Passkeys

Sign in with a passkey or security key instead of a password.

Proxmox

Import Proxmox VE guests as hosts, keep them in sync and watch node stats.

Remote Desktop

RDP, VNC and Telnet sessions in your browser, with clipboard, file transfer, sharing and recording.

Secret Sources

Pull host passwords and keys from 1Password when you connect instead of storing them in Termix.

Serial

Open a serial console to a router, switch or other device plugged into your computer.

Session Recording

Record terminal and remote desktop sessions and play them back or download them later.

Session Sharing

Share live sessions by link or with another user, and present sessions to a group in meeting rooms.

Single sign-on

Sign in with any OpenID Connect provider, GitHub or Google.

Snippets

Save the commands you run often and run them in a terminal or on many hosts in one click.

SSH Terminal

SSH terminal sessions with tabs, split screen, history, macros and a local terminal in the desktop app.

Step CA

Connect to hosts with short-lived SSH certificates from a smallstep step-ca server.

Tailscale

Add tailnet devices as hosts and connect with Tailscale SSH.

Termix Identity

Publish your SSH public keys under a public handle and run your own SSH certificate authority.

Tmux Monitor

Browse and control tmux sessions, windows and panes across your hosts.

TOTP

Two-factor sign in with a code from an authenticator app, with backup codes.

Tunnels

SSH port forwarding that reconnects on its own, plus client tunnels from the desktop app.

Usage Statistics

Sends a small anonymous daily report so we can see how Termix is used.

Wake-on-LAN

Wake sleeping machines by sending a Wake-on-LAN packet to their MAC address.

Warpgate

Connect to hosts through a Warpgate SSH bastion.

Web Endpoint

Open a host's web UI inside Termix, directly or over an SSH tunnel.

Workspaces

Save your open tabs and split layouts and reopen them in one click.

Want to build your own? Start from the plugin template. Plugins you can install are listed in the registry. Turn on the community registry in Plugins, Registries to install plugins made by other people, or add your own registry. See submitting a plugin and hosting your own registry.

  

Platform Support
----------------

Platform

Distribution

**Web**

Any modern browser (Chrome, Safari, Firefox) | PWA support

**Windows** x64/ia32

Portable | EXE and MSI Installer | Chocolatey

**Linux** x64/arm64/armv7l

Portable | AUR | AppImage | Deb | Flatpak

**macOS** Universal/x64/arm64, v12.0+

Apple App Store | DMG | Homebrew

**iOS/iPadOS** v15.1+

Apple App Store | IPA

**Android** v7.0+

Google Play Store | APK

  

Installation
------------

See the docs for install steps on every platform.

Sample Docker Compose file (you can leave out `guacd` and the network if you don't plan to use the Remote Desktop plugin):

services:
  termix:
    image: ghcr.io/termix-ssh/termix:latest
    container\_name: termix
    restart: unless-stopped
    ports:
      - "8080:8080"
    volumes:
      - termix-data:/app/data
    environment:
      PORT: "8080"
      GUACD\_HOST: "guacd"
      GUACD\_TUNNEL\_HOST: "termix"
      GUACD\_RECORDING\_PATH: "/termix-data/session\_recordings/guacamole"
      GUACD\_DRIVE\_PATH: "/termix-data/rdp-drive"
    depends\_on:
      - guacd
    networks:
      - termix-net

  guacd:
    image: guacamole/guacd:1.6.0
    container\_name: guacd
    restart: unless-stopped
    volumes:
      - termix-data:/termix-data
    networks:
      - termix-net

volumes:
  termix-data:
    driver: local

networks:
  termix-net:
    driver: bridge

### Cloud Hosting

If Termix runs on the network it manages, an outage takes it down right when you need it. A VPS keeps it reachable, gives you a static IP and works from anywhere without a VPN or port forward.

GINERNET sponsors Termix and the docs have a setup guide for their VPS.

  

Donate
------

Termix has no paid plans. Donations cover servers, domains and development time.

Donate

  

Sponsors
--------

For a paid sponsor spot, email mail@termix.site.

  
                       

  

Support
-------

Bugs and ideas for Termix itself (login, hosts, credentials, sharing, sync, the app and desktop app) go in this repo: report a bug or request a feature.

Every plugin has its own repo, so a problem with the terminal, file manager, Docker, remote desktop or any other plugin goes in that plugin's repo (see the table above, or use Report an issue on the plugin's page in the app, which fills in your versions for you). Not sure where it goes? Open it here and it will be moved.

You need a GitHub account. Add as much detail as you can, in English if possible.

For discussions and questions, join the Discord server. Update videos are on YouTube.

  

License
-------

Apache License 2.0. See LICENSE.
