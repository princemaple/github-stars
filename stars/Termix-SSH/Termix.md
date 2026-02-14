---
project: Termix
stars: 10792
description: Termix is a web-based server management platform with SSH terminal, tunneling, and file editing capabilities.
url: https://github.com/Termix-SSH/Termix
---

Repo Stats
==========

English | 中文

  
Achieved on September 1st, 2025

  

If you would like, you can support the project here!  

Overview
========

Termix is an open-source, forever-free, self-hosted all-in-one server management platform. It provides a multi-platform solution for managing your servers and infrastructure through a single, intuitive interface. Termix offers SSH terminal access, SSH tunneling capabilities, remote file management, and many other tools. Termix is the perfect free and self-hosted alternative to Termius available for all platforms.

Features
========

-   **SSH Terminal Access** - Full-featured terminal with split-screen support (up to 4 panels) with a browser-like tab system. Includes support for customizing the terminal including common terminal themes, fonts, and other components
-   **SSH Tunnel Management** - Create and manage SSH tunnels with automatic reconnection and health monitoring and support for -l or -r connections
-   **Remote File Manager** - Manage files directly on remote servers with support for viewing and editing code, images, audio, and video. Upload, download, rename, delete, and move files seamlessly with sudo support.
-   **Docker Management** - Start, stop, pause, remove containers. View container stats. Control container using docker exec terminal. It was not made to replace Portainer or Dockge but rather to simply manage your containers compared to creating them.
-   **SSH Host Manager** - Save, organize, and manage your SSH connections with tags and folders, and easily save reusable login info while being able to automate the deployment of SSH keys
-   **Server Stats** - View CPU, memory, and disk usage along with network, uptime, system information, firewall, port monitor, on most Linux based servers
-   **Dashboard** - View server information at a glance on your dashboard
-   **RBAC** - Create roles and share hosts across users/roles
-   **User Authentication** - Secure user management with admin controls and OIDC and 2FA (TOTP) support. View active user sessions across all platforms and revoke permissions. Link your OIDC/Local accounts together.
-   **Database Encryption** - Backend stored as encrypted SQLite database files. View docs for more.
-   **Data Export/Import** - Export and import SSH hosts, credentials, and file manager data
-   **Automatic SSL Setup** - Built-in SSL certificate generation and management with HTTPS redirects
-   **Modern UI** - Clean desktop/mobile-friendly interface built with React, Tailwind CSS, and Shadcn. Choose between dark or light mode based UI. Use URL routes to open any connection in full-screen.
-   **Languages** - Built-in support ~30 languages (managed by Crowdin)
-   **Platform Support** - Available as a web app, desktop application (Windows, Linux, and macOS), PWA, and dedicated mobile/tablet app for iOS and Android.
-   **SSH Tools** - Create reusable command snippets that execute with a single click. Run one command simultaneously across multiple open terminals.
-   **Command History** - Auto-complete and view previously ran SSH commands
-   **Quick Connect** - Connect to a server without having to save the connection data
-   **Command Palette** - Double tap left shift to quickly access SSH connections with your keyboard
-   **SSH Feature Rich** - Supports jump hosts, Warpgate, TOTP based connections, SOCKS5, host key verification, password autofill, OPKSSH, etc.
-   **Network Graph** - Customize your Dashboard to visualize your homelab based off your SSH connections with status support

Planned Features
================

See Projects for all planned features. If you are looking to contribute, see Contributing.

Installation
============

Supported Devices:

-   Website (any modern browser on any platform like Chrome, Safari, and Firefox) (includes PWA support)
-   Windows (x64/ia32)
    -   Portable
    -   MSI Installer
    -   Chocolatey Package Manager
-   Linux (x64/ia32)
    -   Portable
    -   AUR
    -   AppImage
    -   Deb
    -   Flatpak
-   macOS (x64/ia32 on v12.0+)
    -   Apple App Store
    -   DMG
    -   Homebrew
-   iOS/iPadOS (v15.1+)
    -   Apple App Store
    -   ISO
-   Android (v7.0+)
    -   Google Play Store
    -   APK

Visit the Termix Docs for more information on how to install Termix on all platforms. Otherwise, view a sample Docker Compose file here:

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

volumes:
  termix-data:
    driver: local

Sponsors
========

                 

Support
=======

If you need help or want to request a feature with Termix, visit the Issues page, log in, and press `New Issue`. Please be as detailed as possible in your issue, preferably written in English. You can also join the Discord server and visit the support channel, however, response times may be longer.

Screenshots
===========

Some videos and images may be out of date or may not perfectly showcase features.

License
=======

Distributed under the Apache License Version 2.0. See LICENSE for more information.
