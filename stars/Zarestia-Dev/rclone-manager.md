---
project: rclone-manager
stars: 449
description: Rclone Manager is a cross-platform GUI application designed to help users manage Rclone remotes efficiently.
url: https://github.com/Zarestia-Dev/rclone-manager
---

  
RClone Manager
=================

**A powerful, cross-platform GUI for managing Rclone remotes with style and ease.**  
_Built with Angular 20 + Tauri 2 · Linux • Windows • macOS • ARM Support_

* * *

🌐 Overview
-----------

**RClone Manager** is a **modern, cross-platform GUI** that makes managing Rclone remotes effortless. Whether you're syncing files across cloud storage providers, mounting remote drives, or performing complex file operations, RClone Manager provides an intuitive interface that simplifies even the most advanced Rclone features.

> ⚠️ **Actively developed** – Regular updates with new features and improvements. Check out our roadmap to see what's coming next!

* * *

🎨 Design Philosophy
--------------------

💡 **Beautiful by design.** A unique blend of **GTK styling**, **Angular Material**, and **FontAwesome icons** creates a clean, minimalist interface that feels at home on any platform while maintaining a modern, responsive experience.

* * *

📸 Screenshots
--------------

Home

Remote Overview

Mount Control

Job Watcher

Serve Control

Responsive

_Seamlessly switches between light and dark modes to match your system preferences._

* * *

🚀 Features
-----------

### 🎯 Core Functionality

-   🛠 **Complete Remote Management** – Add, edit, delete, and clone remotes with an intuitive wizard
-   🔐 **OAuth & Interactive Configuration** – Seamless authentication with providers like OneDrive, Google Drive, and iCloud
-   🔑 **Encrypted Configuration Support** – Secure password storage using system keyring/credential store
-   ⏰ **Scheduled Tasks** – Automate syncs with a built-in scheduler. Create, edit, enable/disable, and monitor scheduled jobs.
-   💾 **Import/Export** – Backup and restore your settings, with optional 7z encryption.

### ⚡ File Operations

-   📁 **Mount Remotes** – Access cloud storage as local drives with multiple mount types (mount, mount2, NFS)
-   🔄 **Sync & Copy** – One-way synchronization and file copying between remotes or local folders
-   ↔️ **Bidirectional Sync (Bisync)** – Keep two locations perfectly synchronized in both directions
-   🚚 **Move Operations** – Transfer files between locations without leaving duplicates
-   🎯 **Primary Actions** – Set up to 3 quick-access actions per remote for instant operations
-   📡 **Serve Remotes** – Expose remotes over HTTP, WebDAV, FTP, SFTP and more.

### 🎨 User Experience

-   🌗 **Adaptive Themes** – Beautiful light and dark modes with GTK-inspired design
-   🖥 **System Tray Integration** – Quick access to mounts and operations from your taskbar
-   📊 **Real-time Monitoring** – Live job status, transfer speeds, and progress tracking
-   🔔 **Smart Notifications** – Stay informed with non-intrusive alerts
-   ⚙️ **Advanced Options** – Full access to VFS settings, bandwidth limits, and flag configurations

### 🌍 Platform Support

-   🐧 **Linux** – Full support including ARM architecture
-   🪟 **Windows** – Native support with WinFsp integration, including ARM
-   🍎 **macOS** – Complete functionality with automatic mount plugin installation
-   📱 **Responsive Design** – Optimized interface for desktop and mobile viewports

### 🔧 Advanced Features

-   🔄 **Auto-Update** – Built-in updater keeps you on the latest version
-   🖥️ **Native Terminal Support** – Open remote config in your preferred terminal
-   📡 **Metered Connection Detection** – Smart warnings when on limited networks
-   🎮 **Global Shortcuts** – Keyboard shortcuts for power users (e.g., Ctrl+Shift+M to force-check mounts)
-   🔍 **Mount Watcher** – Automatic detection and updates of mount status
-   ☁️ **Supported Cloud Providers** – Google Drive, OneDrive, Dropbox, Amazon S3, iCloud, Wasabi, Backblaze B2, and many more

* * *

📦 Installation & Downloads
---------------------------

### 📦 Package Manager Availability

Install RClone Manager from your favorite package manager.

#### 🐧 Linux

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

#### 🍎 macOS

Repository

Version

Install Command

**Homebrew**

`brew install --cask xxxxxxxxxxxxxxxxxxxxxx`

**Direct Download**

> **Note:** For macOS app launch instructions and troubleshooting, check the installation guide: Installation - macOS

#### 🪟 Windows

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
-   **macOS:** Mount plugin – Automatically installed by the app when needed

#### Optional (for encrypted exports)

-   **7-Zip** – For password-protected configuration backups

* * *

🛠️ Development
---------------

### 🔧 Tech Stack

-   **Frontend**: Angular 20 + Angular Material + FontAwesome
-   **Backend**: Tauri 2 (Rust)
-   **Styling**: Custom GTK-inspired theming with responsive design
-   **Architecture**: Modern component-based with reactive state management

### Prerequisites for Building

-   **Node.js** (v18 or later)
-   **Rust** (latest stable)
-   **Cargo** (comes with Rust)
-   Platform-specific build tools (see Tauri prerequisites)

### Development Setup

# Clone the repository
git clone https://github.com/Zarestia-Dev/rclone-manager.git
cd rclone-manager

# Install dependencies
npm install

# Start development server
npm run tauri dev

⚠️ **Important:** Always use `npm run tauri dev` instead of `ng serve`, as the app requires Tauri APIs.

### Building for Production

# Build for your current platform
npm run tauri build

# The built application will be in src-tauri/target/release/

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

We welcome contributions from developers of all skill levels! Here's how you can help:

### Ways to Contribute

-   🐛 **Report Bugs** – Found an issue? Open a bug report
-   💡 **Suggest Features** – Have an idea? Share it with us
-   📖 **Improve Documentation** – Help make our docs clearer and more comprehensive
-   🔧 **Submit Pull Requests** – Fix bugs or implement features (see development setup above)
-   🌍 **Translate** – Help make RClone Manager available in your language (coming soon)
-   ⭐ **Spread the Word** – Star the repo, share with friends, write blog posts

### Contribution Guidelines

1.  Fork the repository and create a feature branch
2.  Follow the existing code style and linting rules
3.  Test your changes thoroughly on your target platform
4.  Write clear commit messages
5.  Submit a pull request with a detailed description

> 📝 See our CONTRIBUTING.md guide (coming soon) for detailed guidelines

* * *

📜 License
----------

Licensed under the **GNU GPLv3**.

You are free to use, modify, and distribute this software under the terms of the GPL v3 license. See the LICENSE file for full details.

* * *

📬 Support & Contact
--------------------

### Get Help

-   💬 GitHub Discussions – Ask questions and chat with the community
-   🐛 Issue Tracker – Report bugs or request features
-   📖 Documentation – Guides and tutorials

### Stay Updated

-   ⭐ Star the repository to get notifications about new releases
-   👀 Watch the repo for all updates and discussions
-   🔔 Enable release notifications to be the first to know about new versions

* * *

Made with ❤️ by the Zarestia Dev Team  
Powered by Rclone | Built with Angular & Tauri
