---
project: Motrix
stars: 50865
description: A full-featured download manager.
url: https://github.com/agalwood/Motrix
---

Motrix
======

A full-featured download manager
--------------------------------

English | 简体中文

Motrix is a full-featured download manager that supports downloading HTTP, FTP, BitTorrent, Magnet, etc.

Motrix has a clean and easy to use interface. I hope you will like it 👻.

✈️ Official Website | 📖 Manual

💽 Installation
---------------

Download from GitHub Releases and install it.

### Windows

It is recommended to install Motrix using the installation package (Motrix-Setup-x.y.z.exe) to ensure a complete experience, such as associating torrent files, capturing magnet links, etc.

If you use package management tools to manage applications on Windows, such as Chocolatey, scoop. You can use them to install Motrix.

#### Chocolatey

Thanks to @Yato for continuing to maintain the Motrix Chocolatey package. To install motrix, run the following command from the `command line` or from `PowerShell`:

# Install
choco install motrix

# Upgrade
choco upgrade motrix

#### scoop

If you prefer the portable version, you can use scoop (need Windows 7+) to install Motrix.

scoop bucket add extras
scoop install motrix

### macOS

The macOS users can install Motrix using `brew`, thanks to PR of @Mitscherlich.

brew update && brew install motrix

#### Auto Update

Since Motrix v1.8.0 and later versions changed the App BundleID ( `net.agalwood.Motrix` => `app.motrix.native` ), the automatic update of Motrix v1.6.11 will fail. Motrix Install Assistant will help you install the latest Motrix application.

### Linux

You can download the `AppImage` (for all Linux distributions) or `snap` to install Motrix, see GitHub/release for more Linux installation package formats.

Motrix may need to run with `sudo` for the first time in Linux because there is no permission to create the download session file (`/var/cache/aria2.session`).

If you want to build from source code, please read the **Build** section.

#### AppImage

The latest version of Motrix AppImage requires you to manually perform desktop integration. Please check the documentation of AppImageLauncher .

> Desktop Integration Since electron-builder 21 desktop integration is not a part of produced AppImage file. AppImageLauncher is the recommended way to integrate AppImages.

Deepin 20 Beta users failed to install Motrix, please follow the steps below:

Open the `Terminal`, paste and run the following command to install Motrix again.

sudo apt --fix-broken install

#### Snap

Motrix has been listed on Snapcraft , Ubuntu users recommend downloading from the Snap Store.

Tips for v1.5.10

The tray may not display the indicator normally, which makes it inconvenient to exit the application.

Please unchecked Preferences--Basic Settings--Hide App Menu (Windows & Linux Only), click Save & Apply. Then click "Exit" in the File menu to exit the application.

Please update to v1.5.12 and above, you can use the keyboard shortcut Ctrl + q to quickly exit the application.

#### AUR

For Arch Linux users, Motrix is available in aur, thanks to the maintainer @weearc.

Run the following command to install:

yay -S motrix

#### Flatpak

Thanks to the PR of @proletarius101, Motrix has been listed Flathub, Linux users who like the Flatpak can try it.

# Install
flatpak install flathub net.agalwood.Motrix

# Run
flatpak run net.agalwood.Motrix

✨ Features
----------

-   🕹 Simple and clear user interface
-   🦄 Supports BitTorrent & Magnet
-   ☑️ BitTorrent selective download
-   📡 Update tracker list every day automatically
-   🔌 UPnP & NAT-PMP Port Mapping
-   🎛 Up to 10 concurrent download tasks
-   🚀 Supports 64 threads in a single task
-   🚥 Supports speed limit
-   🕶 Mock User-Agent
-   🔔 Download completed Notification
-   💻 Ready for Touch Bar (Mac only)
-   🤖 Resident system tray for quick operation
-   📟 Tray speed meter displays real-time speed (Mac only)
-   🌑 Dark mode
-   🗑 Delete related files when removing tasks (optional)
-   🌍 I18n, View supported languages.
-   🛠 More features in development

🖥 User Interface
-----------------

⌨️ Development
--------------

### Clone Code

git clone git@github.com:agalwood/Motrix.git

### Install Dependencies

cd Motrix
yarn

> Error: Electron failed to install correctly, please delete node\_modules/electron and try installing again

`Electron` failed to install correctly, please refer to electron/electron#8466 (comment)

### Dev Mode

yarn run dev

### Build Release

yarn run build

#### Build for Apple Silicon

yarn run build:applesilicon

After building, the application will be found in the project's `release` directory.

🛠 Technology Stack
-------------------

-   Electron
-   Vue + VueX + Element
-   Aria2

☑️ TODO
-------

Development Roadmap see: Trello

🤝 Contribute
-------------

If you are interested in participating in joint development, PR and Forks are welcome!

🌍 Internationalization
-----------------------

Translations into versions for other languages are welcome 🧐! Please read the translation guide before starting translations.

Key

Name

Status

ar

Arabic

✔️ @hadialqattan, @AhmedElTabarani

bg

Българският език

✔️ @null-none

ca

Català

✔️ @marcizhu

de

Deutsch

✔️ @Schloemicher

el

Ελληνικά

✔️ @Likecinema

en-US

English

✔️

es

Español

✔️ @Chofito

fa

فارسی

✔️ @Nima-Ra

fr

Français

✔️ @gpatarin

hu

Hungarian

✔️ @zalnaRs

id

Indonesia

✔️ @aarestu

it

Italiano

✔️ @blackcat-917

ja

日本語

✔️ @hbkrkzk

ko

한국어

✔️ @KOZ39

nb

Norsk Bokmål

✔️ @rubjo

nl

Nederlands

✔️ @nickbouwhuis

pl

Polski

✔️ @KanarekLife

pt-BR

Portuguese (Brazil)

✔️ @andrenoberto

ro

Română

✔️ @alyn3d

ru

Русский

✔️ @bladeaweb

th

แบบไทย

✔️ @nxanywhere

tr

Türkçe

✔️ @abdullah

uk

Українська

✔️ @bladeaweb

vi

Tiếng Việt

✔️ @duythanhvn

zh-CN

简体中文

✔️

zh-TW

繁體中文

✔️ @Yukaii @5idereal

📜 License
----------

MIT Copyright (c) 2018-present Dr\_rOot
