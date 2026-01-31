---
project: lufin
stars: 229
description: Read-only mirror of https://git.hloth.dev/hloth/lufin
url: https://github.com/VityaSchel/lufin
---

Lufin — a modern self-hosted file-sharing service
=================================================

Lufin (Let’s Upload that File—Next) is a modern alternative to lufi.

-   ✨ Modern neat design
-   📁 S3 storage support (with Cloudflare R2 compatability)
-   🌄 Rich client-side preview for
    -   🖼️ Images
    -   🎵 Audio
    -   🎥 Video
    -   🗂️ Zip archives
    -   📊 XLSX spreadsheets
    -   📝 Text files
    -   📖 PDF
-   🗣️ Translated to 26 languages: English, Русский, Українська, Беларуская, Български, Čeština, Dansk, Nederlands, Eesti, Suomi, Français, Deutsch, Ελληνικά, Magyar, Italiano, Latviešu, Lietuvių, Norsk, Polski, Português, Română, Slovenčina, Slovenščina, Español, Svenska, Türkçe. See CONTRIBUTING.md for information on how to contibute support for a language.
-   🛡️ Client-side metadata stripping such as EXIF from images
-   🔥 Configurable data retention settings based on files size
-   🔐 Optional end-to-end encryption using AES-GCM allowing user to opt-out to embed files via hotlinks
-   🔑 Password protection
-   👀 Delete at first downlaod
-   🗃️ Client-side archive generation before uploading
-   📸 Client-side image compression
-   ✏️ Automatic file renaming with option to keep original filenames
-   📀 Multiple databases support (MongoDB, PostgreSQL, SQLite)
-   ⚡️ Fully static frontend (no SSR, no Next.js needed running for the website)
-   📦 Docker Compose deployment with automatic HTTPS out of the box
-   💻 Links to uploaded files are stored in LocalStorage
-   💾 Importable/exportable LocalStorage with a button to clean up expired pages

**This app requires JavaScript in order for client-side encryption to work.**

Stack: React, Vite & Rollup, Material UI, SCSS modules, TailwindCSS, MongoDB, PostgreSQL, Drizzle ORM & Kit, Elysia, Bun.

Demo: lufin.hloth.dev

Note

It's a demo website and files get deleted very quickly, it's only purpose is demonstration of the project

-   Lufin — a modern self-hosted file-sharing service
    -   Screenshotter browser extension
    -   Installation
    -   Motivation
    -   License
    -   Donate

Screenshotter browser extension
-------------------------------

See also: a related project — Firefox-based browser extension for taking full-screen, partial, full-screen cropped screenshots, with a built-in image editor and an option to instantly upload to your choosen lufin instance. Free, no ads, no trackers, no metrics, 100% opensource.

Visit screenshotter repository

Installation
------------

Read INSTALL.md for steps to install and run lufin on your machine.

Motivation
----------

I was working on this project in August 2023 - October 2023 as a part of a larger platform for one of my Freelance clients. In late 2024 I had to leave working on them because they were constantly harassing, threatening and abusing me. This is a cleaned up version of filesharing subproject that I made for them, originally built as a microfrontend for Next.js.

I made this project while I was working primarily with React and Next.js as web frameworks and MongoDB as my favorite database. Things have changed and nowadays I only use Svelte and PostgreSQL. First commits were deliberetly offset by exactly -22 months.

Before publishing this project I rewrote the backend from Fastify to Elysia, migrated from Next.js to Vite, from Next router to React Router, from i18next to paraglide js, optimized build size, separated code to dynamic chunks and put everything into Docker Compose containers.

License
-------

MIT

Donate
------

hloth.dev/donate
