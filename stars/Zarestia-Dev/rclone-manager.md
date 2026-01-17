---
project: rclone-manager
stars: 578
description: RClone Manager is a cross-platform GUI application designed to help users manage Rclone remotes efficiently.
url: https://github.com/Zarestia-Dev/rclone-manager
---

RClone Manager
==============

**A powerful, cross-platform GUI for managing Rclone remotes with style and ease.**  
_Built with Angular 20 + Tauri · Linux • Windows • macOS • ARM Support_

* * *

Overview
--------

**RClone Manager** is a **modern, cross-platform GUI** that makes managing Rclone remotes effortless. Whether you're syncing files across cloud storage providers, mounting remote drives, or performing complex file operations, RClone Manager provides an intuitive interface that simplifies even the most advanced Rclone features.

> ### 🌐 **Looking for Headless Mode?**
> 
> Check out **RClone Manager Headless** – Run as a web server on Linux servers without a GUI!  
> Perfect for NAS, VPS, and remote systems. Access from any browser. 🚀

> Regular updates with new features and improvements. Check out our roadmap to see what's coming next!

* * *

🎨 Design Philosophy
--------------------

A unique blend of **GTK styling**, **Angular Material**, and **FontAwesome icons** creates a clean, minimalist interface that feels at home on any platform while maintaining a modern, responsive experience.

* * *

📸 Screenshots
--------------

Home

Remote Overview

Mount Control

Job Watcher

Serve Control

Dark Mode

_Seamlessly switches between light and dark modes to match your system preferences._

* * *

🚀 Features
-----------

### 🎯 Core

-   🛠 Manage remotes end-to-end (add/edit/delete/clone) with OAuth or interactive config
-   🔑 Secure by default (keyring storage, encrypted exports) plus scheduled jobs and quick import/export
-   📡 Works with all major clouds (Drive, OneDrive, Dropbox, S3, iCloud, Wasabi, B2, …)

### ⚡ Operations

-   📁 Mount and serve remotes; sync, copy, move and bisync between any two locations
-   🎯 One-tap primary actions per remote; monitor jobs live with speeds and progress

### 🎨 Experience

-   🌗 Adaptive light/dark theming with GTK-inspired Material UI
-   🖥 Tray controls, smart notifications, and full VFS/flag tuning when you need it

### 🌍 Platforms

-   Linux, Windows, macOS; responsive layout for desktop and mobile

* * *

📦 Downloads
------------

Install RClone Manager from your favorite package manager.

#### Linux

Repository

Version

Install Command

**AUR**

`yay -S rclone-manager`

**AUR (Git)**

`yay -S rclone-manager-git`

**Direct Download**

**Flathub**

`flatpak install io.github.zarestia_dev.rclone-manager`

> **Note:** For Linux installation instructions and troubleshooting, check the installation guide: Installation - Linux

#### macOS

Repository

Version

Install Command

**Homebrew**

`brew install --cask xxxxxxxxxxxxxxxxxxxxxx`

**Direct Download**

> **Note:** For macOS app launch instructions and troubleshooting, check the installation guide: Installation - macOS

#### Windows

Repository

Version

Install Command

**Chocolatey**

`choco install rclone-manager`

**Scoop**

`scoop bucket add extras` then `scoop install rclone-manager`

**Winget**

`winget install RClone-Manager.rclone-manager`

**Direct Download**

* * *

### 🛠️ Runtime Requirements

**RClone Manager** will guide you through installing any missing dependencies on first run. However, you can pre-install:

#### Required

-   **Rclone** – The core tool for remote management (can be installed via the app)

#### Optional (for mounting)

-   **Linux/macOS:** FUSE – Usually pre-installed on most distributions
-   **Windows:** WinFsp – Automatically prompted for installation if missing
-   **macOS:** FUSE (macFUSE or FUSE-T) – Automatically installed by the app when needed

* * *

🛠️ Development
---------------

For detailed building instructions, please refer to our Wiki.

### Linting & Formatting

-   See **LINTING.md** for detailed instructions on linting and formatting the codebase.

* * *

🐞 Known Issues
---------------

Known bugs and technical limitations are tracked in two places:

-   📄 See **ISSUES.md** for detailed explanations of platform-specific issues (e.g. MacOS App Damaged)
-   📌 Visit our **GitHub Project Board** for open bugs and upcoming fixes

* * *

🗺️ Roadmap
-----------

We organize development on our **GitHub Project Board** — track features, bugs, and long-term goals.

> 🧠 **Want to influence the direction?** Star the repo, watch the project board, and share your ideas in Discussions or Issues!

* * *

🤝 Contributing
---------------

We welcome contributions! Here's how you can help:

-   🐛 **Report Bugs** – Open a bug report
-   💡 **Suggest Features** – Share your ideas
-   📖 **Improve Docs** – Help make our documentation clearer
-   🔧 **Submit PRs** – Fix bugs or implement features (see development setup above)
-   🌍 **Translate** – Help localize RClone Manager (coming soon)
-   💬 **Discuss** – Join GitHub Discussions

* * *

📜 License
----------

Licensed under **GNU GPLv3** – free to use, modify, and distribute.

* * *

⭐ Support the Project
---------------------

-   **Star** and **Watch** the repo to stay updated on releases
-   Share with friends and spread the world!

* * *

Made with ❤️ by the Zarestia Dev Team  
Powered by Rclone | Built with Angular & Tauri
