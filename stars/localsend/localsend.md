---
project: localsend
stars: 74944
description: An open-source cross-platform alternative to AirDrop
url: https://github.com/localsend/localsend
---

LocalSend
=========

Homepage • Discord • GitHub • Codeberg

English (Default) • Español • فارسی • Filipino • Français • Indonesia • Italiano • 日本語 • ភាសាខ្មែរ • 한국어 • Polski • Português Brasil • Русский • ภาษาไทย • Türkçe • Українська • Tiếng Việt • 中文

LocalSend is a free, open-source app that allows you to securely share files and messages with nearby devices over your local network without needing an internet connection.

-   About
-   Sponsors
-   Screenshots
-   Download
-   How It Works
-   Getting Started
-   Contributing
    -   Translation
    -   Bug Fixes and Improvements
-   Troubleshooting
-   Building
    -   Android
    -   iOS
    -   macOS
    -   Windows
    -   Linux

About
-----

LocalSend is a cross-platform app that enables secure communication between devices using a REST API and HTTPS encryption. Unlike other messaging apps that rely on external servers, LocalSend doesn't require an internet connection or third-party servers, making it a fast and reliable solution for local communication.

Sponsors
--------

Browser testing via

Screenshots
-----------

Download
--------

It is recommended to download the app either from an app store or from a package manager because the app does not have an auto-update.

Windows

macOS

Linux

Android

iOS

Fire OS

Winget

App Store

Flathub

Play Store

App Store

Amazon

Scoop

Homebrew

Nixpkgs

F-Droid

Chocolatey

DMG Installer

Snap

APK

EXE Installer

AUR

Portable ZIP

TAR

DEB

AppImage

Read more about distribution channels.

Caution

**Unofficial MSIX preview:** you can try builds from the latest commits at localsend.ob-buff.dev. Stability is not guaranteed and all custom code tweaks are listed on that site.

**Compatibility**

Platform

Minimum Version

Note

Android

5.0

\-

iOS

12.0

\-

macOS

11 Big Sur

Use OpenCore Legacy Patcher 2.0.2 (See #1005)

Windows

10

The last version to support Windows 7 is v1.15.4. There might be backports of newer versions for Windows 7 in the future.

Linux

N.A.

Deps: Gnome: `xdg-desktop-portal` and `xdg-desktop-portal-gtk`, KDE: `xdg-desktop-portal` and `xdg-desktop-portal-kde`

Setup
-----

In most cases, LocalSend should work out of the box. However, if you are having trouble sending or receiving files, you may need to configure your firewall to allow LocalSend to communicate over your local network.

Traffic Type

Protocol

Port

Action

Incoming

TCP, UDP

53317

Allow

Outgoing

TCP, UDP

Any

Allow

Also make sure to disable AP isolation on your router. It should be usually disabled by default but some routers may have it enabled (especially guest networks). See troubleshooting for more information.

**Portable Mode**

(Introduced in v1.13.0)

Create a file named `settings.json` located in the same directory as the executable. This file can be empty. The app will use this file to store settings instead of the default location.

**Start hidden**

(Updated in v1.15.0)

To start the app hidden (only in tray), use the `--hidden` flag (example: `localsend_app.exe --hidden`).

On v1.14.0 and earlier, the app starts hidden if `autostart` flag is set, and the hidden setting is enabled.

How It Works
------------

LocalSend uses a secure communication protocol that allows devices to communicate with each other using a REST API. All data is sent securely over HTTPS, and the TLS/SSL certificate is generated on the fly on each device, ensuring maximum security.

For more information on the LocalSend Protocol, see the documentation.

Getting Started
---------------

To compile LocalSend from the source code, follow these steps:

1.  Install Flutter directly or using fvm (see version required)
2.  Install Rust
3.  Clone the `LocalSend` repository
4.  Run `cd app` to enter the app directory
5.  Run `flutter pub get` to download dependencies
6.  Run `flutter run` to start the app

Note

LocalSend currently requires an older Flutter version (specified in .fvmrc) and thus build issues may be caused by a mismatch between the required and the (system-wide) installed Flutter version.  
To make development more consistent, LocalSend uses fvm to manage the project Flutter version. After installing `fvm`, run `fvm flutter` instead of `flutter`.

Contributing
------------

We welcome contributions from anyone interested in helping improve LocalSend. If you'd like to contribute, there are a few ways to get involved:

### Translation

You can help translate LocalSend into other languages. We use the Weblate platform to manage translations.

Alternatively, you can also contribute by forking this repository and adding translations manually.

The translations are located in the app/assets/i18n directory. Edit the `_missing_translations_<locale>.json` or `strings_<locale>.i18n.json` file to add or update translations.

**_Take note:_ Fields decorated with `@` are not meant to be translated; they are not used in the app in any way, being merely informative text about the file or to give context to the translator.**

### Bug Fixes and Improvements

-   **Bug Fixes:** If you find a bug, please create a pull request with a clear description of the issue and how to fix it.
-   **Improvements:** Have an idea for how to improve LocalSend? Please create an issue first to discuss why the improvement is needed.

For more information, see the contributing guide.

Troubleshooting
---------------

Issue

Platform (Sending)

Platform (Receiving)

Solution

Device not visible

Any

Any

Make sure to disable AP-Isolation on your router. If it is enabled, connections between devices are forbidden.

Device not visible

Any

Windows

Make sure to configure your network as a "private" network. Windows might be more restrictive when the network is configured as public.

Device not visible

macOS, iOS

Any

You can try to toggle the "Local Network" permission under "Privacy" in the OS settings.

Speed too slow

Any

Any

Use 5 Ghz; Disable encryption on both devices

Speed too slow

Any

Android

Known issue. flutter-cavalry/saf\_stream#4

Building
--------

These commands are intended for maintainers only. Make sure to run them from the `app` directory.

### Android

Traditional APK

flutter build apk

AppBundle for Google Play

flutter build appbundle

### iOS

flutter build ipa

### macOS

flutter build macos

### Windows

**Traditional**

flutter build windows

**Local MSIX App**

flutter pub run msix:create

**Store ready**

flutter pub run msix:create --store

### Linux

**Traditional**

flutter build linux

**AppImage**

appimage-builder --recipe AppImageBuilder.yml

**Snap**

Instructions in localsend/snap/README.md

Contributors
------------
