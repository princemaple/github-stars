---
project: memories
stars: 3745
description: Fast, modern and advanced photo management suite. Runs as a Nextcloud app.
url: https://github.com/pulsejet/memories
---

Memories: Photo Management for Nextcloud
========================================

Memories is a _batteries-included_ photo management solution for Nextcloud with advanced features

🎁 Features
-----------

-   **📸 Timeline**: Sort photos and videos by date taken, parsed from Exif data.
-   **⏪ Rewind**: Jump to any time in the past instantly and relive your memories.
-   **🤖 AI Tagging**: Group photos by people and objects, powered by recognize and facerecognition.
-   **🖼️ Albums**: Create albums to group photos and videos together. Then share these albums with others.
-   **🫱🏻‍🫲🏻 External Sharing**: Share photos and videos with people outside of your Nextcloud instance.
-   **📱 Mobile Support**: Work from any device, of any shape and size through the web app.
-   **✏️ Edit Metadata**: Edit dates and other metadata on photos quickly and in bulk.
-   **📦 Archive**: Store photos you don't want to see in your timeline in a separate folder.
-   **📹 Video Transcoding**: Transcode videos and use HLS for maximal performance.
-   **🗺️ Map**: View your photos on a map, tagged with accurate reverse geocoding.
-   **📦 Migration**: Migrate easily from Nextcloud Photos and Google Takeout.
-   **⚡️ Performance**: Do all this very fast. Tested on instances with over a million photos.

🚀 Installation
---------------

1.  Install the app from the Nextcloud app store.
2.  Perform the recommended configuration steps.
3.  Run `php occ memories:index` to generate metadata indices for existing photos.
4.  Open the 📷 Memories app in Nextcloud and set the directory containing your photos.

📱 Mobile Apps
--------------

-   An Android client for Memories is available in early access on Google Play, F-Droid or GitHub Releases.
-   For automatic uploads, you can use the official Nextcloud mobile apps.
    -   Android: Google Play, F-Droid
    -   iOS: App Store.

🏗 Development Setup
--------------------

You can use the dev container to quickly fire up an instance of Nextcloud with Memories pre-installed. See `.devcontainer/README.md` for more information.

To set up a development instance manually, follow these steps:

1.  ☁ Clone this monorepo into the `custom_apps` folder of your Nextcloud.
2.  📥 Install Composer and Node.js 18
3.  👩‍💻 In a terminal, run the command `make dev-setup` to install the dependencies.
4.  🏗 To build/watch the UI, run `make watch-js`.
5.  ✅ Enable the app through the app management of your Nextcloud.
6.  ⚒️ (Strongly recommended) use VS Code for development and install these extensions (`Ctrl+Shift+P` > `Show Recommended Extensions`).
    -   PHP Intelephense: For PHP intellisense and static analysis
    -   PHP-CS-Fixer: For PHP formatting (alternatively, `make php-cs-fixer`)
    -   Psalm: For PHP static analysis (alternatively, `make psalm`)
    -   Prettier: For autoformatting Vue and Typescript
    -   Volar: For Vue intellisense and static analysis
7.  If using PHP Intelephense, search for `@builtin php-language-features` in the extensions tab and disable it.

This monorepo is organized into the following packages:

-   lib: Backend and database migrations (PHP).
-   src: Frontend for all platforms (Vue)
-   go-vod: On-demand video transcoder (Go)
-   android: Android implemention of NativeX (Kotlin)
-   l10n: Translations (Transifex)

Releases are organized with these tags:

-   `v*`: overall releases (e.g. `v1.0.0` or `v1.0.0-beta.1`)
-   `go-vod/*`: transcoder releases (e.g. `go-vod/1.0.0`)
-   `android/*`: Android releases (e.g. `android/1.0.0`)

🤝 Support the project
----------------------

1.  **🌟 Star this repository**: This is the easiest way to support Memories and costs nothing.
2.  **🪲 Report bugs**: Report any bugs you find on the issue tracker.
3.  **📖 Translate**: Help translate Memories into your language on Transifex.
4.  **📝 Contribute**: Read and file or comment on an issue and ask for guidance.
5.  **🪙 Sponsorship**: You can support the project financially at GitHub Sponsors.

A shout out to the current and past financial backers of Memories! See the sponsors page for a full list.

📝 Changelog
------------

For the full changelog, see CHANGELOG.md.

🙏 Special Thanks
-----------------

To the great folks building Nextcloud, PHP, Vue and all the other dependencies that make this project possible.

Thanks to GitHub, CircleCI and BrowserStack for sponsorship for Open Source projects for CI / testing on different devices.

📄 License
----------

Memories is licensed under the AGPLv3. Subpackages such as go-vod are licensed under their respective licenses. See the directory of the subpackage for more information.
