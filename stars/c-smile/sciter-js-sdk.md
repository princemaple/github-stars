---
project: sciter-js-sdk
stars: 1647
description: Sciter.JS - Sciter but with QuickJS on board instead of my TIScript
url: https://github.com/c-smile/sciter-js-sdk
---

NOTE: sciter-js-sdk is moved to https://gitlab.com/c-smile/sciter-js-sdk/
=========================================================================

Build cross platform desktop applications with HTML, CSS and javascript.

### Tutorials, Documentation and Development logfile.

Script
------

Sciter.JS uses QuickJS in particular QuickJS++.

-   ES6: async/await, classes, modules, destructuring;
-   BigInt, BigFloat, BigDecimal - arbitrary precision IEEE 754 floating point operations and transcendental functions with exact rounding (currency, etc);
-   Node.JS runtime (more or less full) is coming;

Platforms
---------

-   **Windows - i32, i64 and arm64** - published;
-   **Linux - i64, arm32 (Raspberry Pi)** - published;
-   **MacOS - i64** and arm64 - published;
-   Mobiles - pending;

Demos
-----

### Calc demo (universal: Browser and Sciter)

Windows:

Linux (Raspbian on Raspberry Pi in particular)

MacOS:

Path: samples/calc

Browser and Sciter shows the same HTML document.

To run demo start run-calculator-browser.bat or run-calculator-sciter.bat. The later will start bin.win/x32/scapp.exe - standalone Sciter engine.

### Mithril demo (universal: Browser and Sciter)

Path: samples/mithril

Sciter.JS runs mithril as it is. Only basic use cases are thested so far though.
