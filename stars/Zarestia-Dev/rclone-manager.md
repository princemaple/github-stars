---
project: rclone-manager
stars: 982
description: RClone Manager is a cross-platform GUI application designed to help users manage Rclone remotes efficiently.
url: https://github.com/Zarestia-Dev/rclone-manager
---

RClone Manager
==============

🇺🇸 English • 🇹🇷 Türkçe • 🇨🇳 简体中文 • 🇫🇷 Français • 🇪🇸 Español • Help to translate • Crowdin

**A powerful, cross-platform GUI for managing Rclone remotes with style and ease.**  
_Built with Angular 22 + Tauri · Linux • Windows • macOS • ARM Support_

* * *

Overview
--------

**RClone Manager** simplifies remote file management and synchronization. Using Rclone as its backbone, it offers a desktop environment with a built-in file manager (**Nautilus**) to transfer, mount, and serve remote files effortlessly.

-   📂 **Nautilus File Manager:** Browse, edit, move, copy, rename, and delete remote files.
-   👁️ **File Viewer:** Inline previews for videos, images, PDFs, audio, and text.
-   ⚙️ **Mount & Serve:** Easy mount controls and serve management (WebDAV, SFTP, HTTP, FTP).
-   🔄 **Job Watcher:** Real-time transfer monitoring and bandwidth control.
-   🌐 **Headless Mode:** Check out RClone Manager Headless to run as a web server on VPS/NAS!

* * *

Screenshot
----------

  
_📖 Want to see more? Check out the **Wiki Gallery** for all features._

* * *

Installation & Downloads
------------------------

Install RClone Manager using your preferred package manager, or download standalone binaries directly from the Releases page.

### Linux

Source

Version

Install Command / Download

**AUR**

`yay -S rclone-manager`

**AUR (Git)**

`yay -S rclone-manager-git`

**Flathub**

`flatpak install io.github.zarestia_dev.rclone-manager`

**Direct Download**

Latest Releases (.deb, .rpm, .AppImage, Portable tar.gz)

> 📚 **Guide:** Wiki: Installation - Linux (troubleshooting Flatpak, snapshots, etc.)

### macOS

Source

Version

Install Command / Download

**Homebrew**

`brew tap Zarestia-Dev/zarestia && brew install --cask rclone-manager`

**Direct Download**

DMG Installer

> 📚 **Guide:** Wiki: Installation - macOS (macFUSE & Gatekeeper fixes)

### Windows

Source

Version

Install Command / Download

**Winget**

`winget install RClone-Manager.rclone-manager`

**Chocolatey**

`choco install rclone-manager`

**Scoop**

`scoop bucket add extras && scoop install rclone-manager`

**Direct Download**

Installer / Portable EXE

> 📚 **Guide:** Wiki: Installation - Windows (WinFsp mounting requirements & SmartScreen)

> 🛠️ **System Requirements:** Mounting drives requires WinFsp (Windows), macFUSE (macOS), or FUSE3 (Linux). Rclone itself is downloaded automatically if missing. See Wiki: System Requirements.

* * *

Development & Support
---------------------

-   **Building from Source:** Refer to the Building Guide.
-   **Code Quality:** Check out LINTING.md for style guidelines.
-   **Troubleshooting:** Visit our Troubleshooting Wiki or read ISSUES.md for platform-specific notes.

* * *

Contributing
------------

We welcome contributions of all forms!

-   🌍 **Translations:** Join the Crowdin Project or read the Translation Guide.
-   🐛 **Bugs & Features:** Open an issue or check the Project Board.
-   🔧 **Code changes:** Please read CONTRIBUTING.md before submitting a Pull Request.

* * *

License & Support
-----------------

-   **License:** Licensed under the GNU GPLv3 – free to use, modify, and distribute.
-   **Support:** If you like this project, please consider leaving a ⭐ on GitHub!
-   **Donate:** If RClone Manager saves you time, consider supporting development ❤️

Made with ❤️ by the Zarestia Dev Team  
Powered by Rclone | Built with Angular & Tauri
