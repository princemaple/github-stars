---
project: Pake
stars: 43620
description: 🤱🏻 Turn any webpage into a desktop app with one command. 一键打包网页生成轻量桌面应用
url: https://github.com/tw93/Pake
---

#### **English** | 简体中文 | 日本語

Pake
====

**Turn any webpage into a desktop app with one command, supports macOS, Windows, and Linux**

Features
--------

-   🎐 **Lightweight**: Nearly 20 times smaller than Electron packages, typically around 5M
-   🚀 **Fast**: Built with Rust Tauri, much faster than traditional JS frameworks with lower memory usage
-   ⚡ **Easy to use**: One-command packaging via CLI or online building, no complex configuration needed
-   📦 **Feature-rich**: Supports shortcuts, immersive windows, drag & drop, style customization, ad removal

Getting Started
---------------

-   **Beginners**: Download ready-made Popular Packages or use Online Building with no environment setup required
-   **Developers**: Install CLI Tool for one-command packaging of any website with customizable icons, window settings, and more
-   **Advanced Users**: Clone the project locally for Custom Development, or check Advanced Usage for style customization and feature enhancement
-   **Troubleshooting**: Check FAQ for common issues and solutions

Popular Packages
----------------

WeRead Mac Windows Linux

Twitter Mac Windows Linux

Grok Mac Windows Linux

DeepSeek Mac Windows Linux

ChatGPT Mac Windows Linux

Gemini Mac Windows Linux

YouTube Music Mac Windows Linux

YouTube Mac Windows Linux

LiZhi Mac Windows Linux

ProgramMusic Mac Windows Linux

Excalidraw Mac Windows Linux

XiaoHongShu Mac Windows Linux

🏂 You can download more applications from Releases. **Click here to expand the shortcuts reference!**  

Mac

Windows/Linux

Function

⌘ + \[

Ctrl + ←

Return to the previous page

⌘ + \]

Ctrl + →

Go to the next page

⌘ + ↑

Ctrl + ↑

Auto scroll to top of page

⌘ + ↓

Ctrl + ↓

Auto scroll to bottom of page

⌘ + r

Ctrl + r

Refresh Page

⌘ + w

Ctrl + w

Hide window, not quit

⌘ + \-

Ctrl + \-

Zoom out the page

⌘ + +

Ctrl + +

Zoom in the page

⌘ + \=

Ctrl + \=

Zoom in the Page

⌘ + 0

Ctrl + 0

Reset the page zoom

In addition, double-click the title bar to switch to full-screen mode. For Mac users, you can also use the gesture to go to the previous or next page and drag the title bar to move the window.

Command-Line Packaging
----------------------

# Install Pake CLI
pnpm install -g pake-cli

# Basic usage - automatically fetches website icon
pake https://github.com --name GitHub

# Advanced usage with custom options
pake https://weekly.tw93.fun --name Weekly --icon https://cdn.tw93.fun/pake/weekly.icns --width 1200 --height 800 --hide-title-bar

First-time packaging requires environment setup and may be slower, subsequent builds are fast. For complete parameter documentation, see CLI Usage Guide. Don't want to use CLI? Try GitHub Actions Online Building.

Development
-----------

Requires Rust `>=1.85` and Node `>=22`. For detailed installation guide, see Tauri documentation. If unfamiliar with development environment, use the CLI tool instead.

# Install dependencies
pnpm i

# Local development \[right-click to open debug mode\]
pnpm run dev

# Build application
pnpm run build

For style customization, feature enhancement, container communication and other advanced features, see Advanced Usage Documentation.

Developers
----------

Pake's development can not be without these Hackers. They contributed a lot of capabilities for Pake. Also, welcome to follow them! ❤️

Support
-------

1.  I have two cats, TangYuan and Coke. If you think Pake delights your life, you can feed them food 🥩.
2.  If you like Pake, you can star it on GitHub. Also, welcome to recommend Pake to your friends.
3.  You can follow my Twitter to get the latest news of Pake or join our Telegram chat group.
4.  I hope that you enjoy playing with it. Let us know if you find a website that would be great for a Mac App!
