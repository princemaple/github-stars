---
project: alacritty
stars: 61520
description: A cross-platform, OpenGL terminal emulator.
url: https://github.com/alacritty/alacritty
---

Alacritty - A fast, cross-platform, OpenGL terminal emulator
============================================================

About
-----

Alacritty is a modern terminal emulator that comes with sensible defaults, but allows for extensive configuration. By integrating with other applications, rather than reimplementing their functionality, it manages to provide a flexible set of features with high performance. The supported platforms currently consist of BSD, Linux, macOS and Windows.

The software is considered to be at a **beta** level of readiness; there are a few missing features and bugs to be fixed, but it is already used by many as a daily driver.

Precompiled binaries are available from the GitHub releases page.

Join `#alacritty` on libera.chat if you have questions or looking for a quick help.

Features
--------

You can find an overview over the features available in Alacritty here.

Further information
-------------------

-   Announcing Alacritty, a GPU-Accelerated Terminal Emulator January 6, 2017
-   A talk about Alacritty at the Rust Meetup January 2017 January 19, 2017
-   Alacritty Lands Scrollback, Publishes Benchmarks September 17, 2018

Installation
------------

Alacritty can be installed by using various package managers on Linux, BSD, macOS and Windows.

Prebuilt binaries for macOS and Windows can also be downloaded from the GitHub releases page.

For everyone else, the detailed instructions to install Alacritty can be found here.

### Requirements

-   At least OpenGL ES 2.0
-   \[Windows\] ConPTY support (Windows 10 version 1809 or higher)

Configuration
-------------

You can find the documentation for Alacritty's configuration in `man 5 alacritty`, or by looking at the website if you do not have the manpages installed.

Alacritty doesn't create the config file for you, but it looks for one in the following locations:

1.  `$XDG_CONFIG_HOME/alacritty/alacritty.toml`
2.  `$XDG_CONFIG_HOME/alacritty.toml`
3.  `$HOME/.config/alacritty/alacritty.toml`
4.  `$HOME/.alacritty.toml`
5.  `/etc/alacritty/alacritty.toml`

On Windows, the config file will be looked for in:

-   `%APPDATA%\alacritty\alacritty.toml`

Contributing
------------

A guideline about contributing to Alacritty can be found in the `CONTRIBUTING.md` file.

FAQ
---

**_Is it really the fastest terminal emulator?_**

Benchmarking terminal emulators is complicated. Alacritty uses vtebench to quantify terminal emulator throughput and manages to consistently score better than the competition using it. If you have found an example where this is not the case, please report a bug.

Other aspects like latency or framerate and frame consistency are more difficult to quantify. Some terminal emulators also intentionally slow down to save resources, which might be preferred by some users.

If you have doubts about Alacritty's performance or usability, the best way to quantify terminal emulators is always to test them with **your** specific usecases.

**_Why isn't feature X implemented?_**

Alacritty has many great features, but not every feature from every other terminal. This could be for a number of reasons, but sometimes it's just not a good fit for Alacritty. This means you won't find things like tabs or splits (which are best left to a window manager or terminal multiplexer) nor niceties like a GUI config editor.

License
-------

Alacritty is released under the Apache License, Version 2.0.
