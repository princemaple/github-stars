---
project: gopeed
stars: 26264
description:   A fast, modern download manager for HTTP, BitTorrent, Magnet, and ed2k. Cross-platform, built with Golang and Flutter.
url: https://github.com/GopeedLab/gopeed
---

English | 中文 | 日本語 | 正體中文 | Tiếng Việt

🚀 Introduction
---------------

Gopeed (short for **Go Speed**) is a fast, modern, free, and open-source download manager built with Go and Flutter. It supports HTTP, HTTPS, BitTorrent, magnet links, and ed2k on desktop, mobile, and the web.

Beyond core download management, Gopeed offers browser integration, JavaScript extensions, a REST API, a CLI, and a self-hosted web UI for customization and automation.

Visit ✈ Official Website

✨ Features
----------

-   ⚡ **High-speed downloads** — combine concurrent tasks, multi-connection HTTP transfers, and peer-to-peer BitTorrent downloads to make the most of your bandwidth.
-   🧲 **Multiple protocols** — download HTTP/HTTPS files, torrents, magnet links, and ed2k resources from a single app.
-   🌱 **Full-featured BitTorrent** — use DHT peer discovery, uTP transport, Web Seeds, selective file downloads, tracker management, peer and piece statistics, and ratio- or time-based seeding limits.
-   📋 **Flexible task management** — pause, resume, retry, run batch operations, search, filter by status, organize with categories, and recover tasks after a restart.
-   🪶 **Lightweight native experience** — the main interface is rendered natively with Flutter. No Electron. No WebView shell. Enjoy a smaller footprint, lower overhead, and responsive performance.
-   💻 **Cross-platform** — available for Windows, macOS, Linux, Android, iOS, and the web, with Docker and QNAP deployment options.
-   🎨 **Customizable appearance** — follow your system theme or choose light or dark mode, with eight accent colors.
-   📐 **Responsive interface** — task lists, navigation, settings, and detail views adapt to phones, tablets, and resizable desktop windows.
-   🗣️ **Available in 20+ languages** — including English, Simplified and Traditional Chinese, Japanese, Korean, and many more.
-   🌐 **Browser integration** — send downloads from Chrome, Edge, Firefox, and other compatible browsers directly to Gopeed.
-   🧩 **JavaScript extensions** — add support for video platforms, AI model hubs, cloud storage services, and other download sources.
-   🤖 **AI integration** — use Gopeed's MCP endpoint to connect compatible AI agents and create, inspect, or manage downloads with natural language.
-   🔌 **Automation-ready** — integrate with Gopeed through its REST API, CLI, authenticated web UI, webhooks, and post-download scripts.
-   🛠️ **Built-in essentials** — customize headers and the User-Agent, use proxies and GitHub mirrors, receive notifications, and extract archives automatically.

🤖 AI Integration
-----------------

Connect Gopeed to an AI agent and manage downloads with natural language. For example, you can say:

> Download the latest Gopeed client for Windows.

Tool

Description

`resolve_task`

Resolve a download URL or URI and return its resource metadata and files before creating a task.

`create_task`

Create and start a task from a resolved resource ID or a direct download request.

`list_tasks`

List tasks, optionally filtering them by ID or status.

`get_task`

Get the request, resource, options, and current progress for one task.

`get_task_status`

Get lightweight runtime status and per-file progress for one task.

`get_task_stats`

Get protocol-specific statistics, including HTTP connections or BitTorrent peers and seeding data.

`pause_task`

Pause a task.

`continue_task`

Continue a paused or failed task.

`delete_task`

Delete a task, optionally deleting its downloaded files.

⬇️ Download
-----------

### 🧪 Gopeed 2.0.0 Beta

Gopeed 2.0.0 is currently in public beta, introducing a redesigned interface, a native communication architecture that connects desktop and mobile clients directly to the Go core through FFI, a more consistent cross-platform experience, improved task management, more flexible API support, and MCP-based AI agent integration. Some features may still be incomplete or unstable, so please try it and report any issues you encounter.

-   Download Gopeed 2.0.0 Beta 2

Once the features and stability meet our release standards, we will publish the official Gopeed 2.0.0 release. Beta users will be able to upgrade directly to the final release, while existing stable users will not be automatically moved onto the beta channel.

### Stable release

-   Official Download
-   GitHub Releases

### 🛠️ Command-line tool

Install the CLI with `go install`:

go install github.com/GopeedLab/gopeed/cmd/gopeed@latest

🔌 Browser Extension
--------------------

Use the Gopeed browser extension to send downloads from Chrome, Edge, Firefox, and other compatible browsers directly to Gopeed: GopeedLab/browser-extension

📱 WeChat Official Account
--------------------------

Follow Gopeed's official WeChat account for updates and news.

💝 Donate
---------

If Gopeed is useful to you, please consider supporting its development. Thank you!

👨‍💻 Development
-----------------

Gopeed consists of a Flutter front end and a Go back end. They communicate over HTTP, using Unix sockets on Unix-like systems and TCP on Windows.

> The front-end source is located in the `ui/flutter` directory.

### 🌍 Environment

1.  Go 1.25+
2.  Flutter 3.41+

### 📋 Clone

git clone git@github.com:GopeedLab/gopeed.git

### 🤝 Contributing

See CONTRIBUTING.md.

### 🏗️ Build

#### Desktop

Set up Flutter desktop development using the official Flutter desktop guide, and make sure a working C toolchain is available for cgo. Then run the commands for your platform.

Commands:

-   Windows

go build -tags nosqlite -ldflags="\-w -s" -buildmode=c-shared -o ui/flutter/windows/libgopeed.dll github.com/GopeedLab/gopeed/bind/desktop
cd ui/flutter
flutter build windows

-   macOS

go build -tags nosqlite -ldflags="\-w -s" -buildmode=c-shared -o ui/flutter/macos/Frameworks/libgopeed.dylib github.com/GopeedLab/gopeed/bind/desktop
cd ui/flutter
flutter build macos

-   Linux

go build -tags nosqlite -ldflags="\-w -s" -buildmode=c-shared -o ui/flutter/linux/bundle/lib/libgopeed.so github.com/GopeedLab/gopeed/bind/desktop
cd ui/flutter
flutter build linux

#### Mobile

Mobile builds also require a working cgo toolchain. Install and initialize `gomobile`:

go install golang.org/x/mobile/cmd/gomobile@latest
go get golang.org/x/mobile/bind
gomobile init

Commands:

-   Android

gomobile bind -tags nosqlite -ldflags="\-w -s -checklinkname=0" -o ui/flutter/android/app/libs/libgopeed.aar -target=android -androidapi 21 -javapkg="com.gopeed" github.com/GopeedLab/gopeed/bind/mobile
cd ui/flutter
flutter build apk

-   iOS

gomobile bind -tags nosqlite -ldflags="\-w -s" -o ui/flutter/ios/Frameworks/Libgopeed.xcframework -target=ios github.com/GopeedLab/gopeed/bind/mobile
cd ui/flutter
flutter build ios --no-codesign

#### Web

Build the web app and server:

cd ui/flutter
flutter build web
cd ../../
rm -rf cmd/web/dist
cp -r ui/flutter/build/web cmd/web/dist
go build -tags nosqlite,web -ldflags="\-s -w" -o bin/ github.com/GopeedLab/gopeed/cmd/web

❤️ Credits
----------

### 👥 Contributors

### 🏢 JetBrains

📄 License
----------

GPLv3
