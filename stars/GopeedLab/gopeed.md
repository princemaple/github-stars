---
project: gopeed
stars: 23395
description:   A fast, modern download manager for HTTP, BitTorrent, Magnet, and ED2K. Cross-platform, built with Golang and Flutter.
url: https://github.com/GopeedLab/gopeed
---

English | 中文 | 日本語 | 正體中文 | Tiếng Việt

🚀 Introduction
---------------

Gopeed (full name Go Speed), a high-speed downloader developed by `Golang` + `Flutter`, supports (HTTP, BitTorrent, Magnet, ED2K) protocol, and supports all platforms. In addition to basic download functions, Gopeed is also a highly customizable downloader that supports implementing more features through integration with APIs or installation and development of extensions.

Visit ✈ Official Website | 📖 Official Docs

⬇️ Download
-----------

🪟 Windows

`EXE`

amd64

📥

arm64

📥

`Portable`

amd64

📥

arm64

📥

🍎 MacOS

`DMG`

universal

📥

amd64

📥

arm64

📥

🐧 Linux

`Flathub`

amd64

📥

`SNAP`

amd64

📥

`DEB`

amd64

📥

arm64

📥

`AppImage`

amd64

📥

arm64

📥

🤖 Android

`APK`

universal

📥

armeabi-v7a

📥

arm64-v8a

📥

x86\_64

📥

📱 iOS

`IPA`

universal

📥

🐳 Docker

\-

universal

📥

💾 Qnap

`QPKG`

amd64

📥

arm64

📥

🌐 Web

`Windows`

amd64

📥

arm64

📥

386

📥

`MacOS`

amd64

📥

arm64

📥

`Linux`

amd64

📥

arm64

📥

386

📥

More about installation, please refer to Installation

### 🛠️ Command tool

use `go install`:

go install github.com/GopeedLab/gopeed/cmd/gopeed@latest

🔌 Browser Extension
--------------------

Gopeed also provides a browser extension to take over browser downloads, supporting browsers such as Chrome, Edge, Firefox, etc., please refer to: https://github.com/GopeedLab/browser-extension

📱 WeChat Official Account
--------------------------

Follow our WeChat Official Account to get the latest updates and news.

💝 Donate
---------

If you like this project, please consider donating to support the development of this project, thank you!

🖼️ Showcase
------------

👨‍💻 Development
-----------------

This project is divided into two parts, the front end uses `flutter`, the back end uses `Golang`, and the two sides communicate through the `http` protocol. On the unix system, `unix socket` is used, and on the windows system, `tcp` protocol is used.

> The front code is located in the `ui/flutter` directory.

### 🌍 Environment

1.  Golang 1.24+
2.  Flutter 3.38+

### 📋 Clone

git clone git@github.com:GopeedLab/gopeed.git

### 🤝 Contributing

Please refer to CONTRIBUTING.md

### 🏗️ Build

#### Desktop

First, you need to configure the environment according to the official Flutter desktop website documention, then you will need to ensure the cgo environment is set up accordingly. For detailed instructions on setting up the cgo environment, please refer to relevant resources available online.

command:

-   windows

go build -tags nosqlite -ldflags="\-w -s" -buildmode=c-shared -o ui/flutter/windows/libgopeed.dll github.com/GopeedLab/gopeed/bind/desktop
cd ui/flutter
flutter build windows

-   macos

go build -tags nosqlite -ldflags="\-w -s" -buildmode=c-shared -o ui/flutter/macos/Frameworks/libgopeed.dylib github.com/GopeedLab/gopeed/bind/desktop
cd ui/flutter
flutter build macos

-   linux

go build -tags nosqlite -ldflags="\-w -s" -buildmode=c-shared -o ui/flutter/linux/bundle/lib/libgopeed.so github.com/GopeedLab/gopeed/bind/desktop
cd ui/flutter
flutter build linux

#### Mobile

Same as before, you also need to prepare the `cgo` environment, and then install `gomobile`:

go install golang.org/x/mobile/cmd/gomobile@latest
go get golang.org/x/mobile/bind
gomobile init

command:

-   android

gomobile bind -tags nosqlite -ldflags="\-w -s -checklinkname=0" -o ui/flutter/android/app/libs/libgopeed.aar -target=android -androidapi 21 -javapkg="com.gopeed" github.com/GopeedLab/gopeed/bind/mobile
cd ui/flutter
flutter build apk

-   ios

gomobile bind -tags nosqlite -ldflags="\-w -s" -o ui/flutter/ios/Frameworks/Libgopeed.xcframework -target=ios github.com/GopeedLab/gopeed/bind/mobile
cd ui/flutter
flutter build ios --no-codesign

#### Web

command:

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
