---
project: ImageGlass
stars: 14769
description: 🏞 A fast, open-source, modern image viewer for 90+ formats – including WEBP, GIF, SVG, AVIF, JXL, HEIC and more – built for smooth browsing across Windows, macOS, and Linux.
url: https://github.com/d2phap/ImageGlass
---

🖼️ ImageGlass
==============

### A Fast, Seamless Photo Viewer

ImageGlass is a fast, modern, open-source image viewer for Windows, macOS, and Linux. It pairs high-performance rendering with a smooth, immersive viewing experience and powerful tools for everyday users and designers alike, with seamless navigation across 90+ image formats, including `WEBP`, `JXL`, `SVG`, `HEIC`, `AVIF`, `HDR`, and raw images.

Built enterprise-ready, ImageGlass Pro supports managed deployment through preset config files that work across every platform and package. IT teams can roll out a preconfigured app config, enforce admin-locked settings, and lock individual features on every managed device.

  

  

**🌐 Website**  •  **📥 Pricing**  •  **🧩 Plugins**  •  **📐 Tools**  •  **📚 Docs**  •  **💬 Support**

  

  

👉 Compare all plans and features at imageglass.org/pricing.

  

Caution

### Security Alert: Beware of Fake ImageGlass Downloads

Malicious campaigns are using AI tools to impersonate trusted software through fake GitHub profiles, forks, and Gists that spread malware. Download ImageGlass only from its official sources:

-   Website: **imageglass.org**
-   GitHub: **github.com/d2phap/ImageGlass** and the **github.com/ImageGlass**

Any other repo, fork, or Gist offering ImageGlass builds is not mine. Always check the URL before downloading.

  

Features
--------

Primarily a photo viewer, ImageGlass offers a wide array of features geared toward image viewing, along with some focused editing capabilities. Here are some of the key features:

-   Supports 90+ image formats out of the box
-   Hardware-aware smart caching
-   Super-fast image browsing with Turbo mode
-   Slideshow with random interval and sound notification
-   Native SVG and SVGZ vector rendering
-   Animated GIF, WEBP, and SVG playback
-   Color management and basic HDR support
-   Different cursor-precise zoom modes with flexible image interpolations
-   Different window modes: Frameless, Window Fit, Full screen
-   Built-in Tools: Rotate, Flip, Crop, Resize, Color Picker, Frame Navigation, Lossless compression...
-   EXIF metadata viewing through the ExifGlass tool
-   Touch gestures for zoom and pan
-   Themes, layouts, and custom hotkeys
-   Custom action binding for toolbar, mouse...
-   Plugins and external tools support via ImageGlass.SDK
-   Managed deployment with preset app config, admin-locked settings, and feature lock, for all platforms and packages (Available for Pro only)
-   Windows: Explorer sort order support
-   Windows: Custom file type icon pack (Not available for Store release)

👉 Visit https://imageglass.org/docs/features to explore all features of ImageGlass.

  

Plugins & Tools
---------------

Extend ImageGlass with codec plugins that open more image formats, and with tools that work alongside it.

Plugin

Author

Description

Platforms

AVIF Codec

aplefull

Opens still and animated `.avif` files, using libavif, dav1d and libyuv

Windows, macOS, Linux

WIC Codec

d2phap

Brings the Windows Imaging Component in as a native codec, including JPEG XR (`.jxr`, `.hdp`, `.wdp`)

Windows

APNG Codec

d2phap

Plays animated `.apng` files

Windows, macOS, Linux

ITHMB Codec

B67687

Decodes `.ithmb` thumbnail files using Ithmb-Codec

Windows, macOS, Linux

Tool

Author

Description

Platforms

ExifGlass

d2phap

Reads the camera settings, lens, location, and color profile in any photo

Windows, macOS, Linux

FewerPhotos

d2phap

Cleans up the photo folders you already have: duplicates, blurry shots, and sorting by date

Windows, macOS

👉 Browse the plugins and tools, or build your own with ImageGlass.SDK.

  

System Requirements
-------------------

**Version 10**

-   Windows 10/11 x64 or arm64, version 1809 (build 17763) or later
-   macOS 14+, Apple Silicon arm64
-   Linux Desktop X11 x64: Ubuntu 20.04+, Linux Mint 20+, Debian 11+, Fedora 30+, RHEL/Alma/Rocky 9+,...

**Version 9**

-   Windows 10/11 x64 or arm64, version 1809 (build 17763) or later
-   Optional: WebView2 Runtime 64-bit v119.0.2151 or later

  

Development
-----------

The `develop` branch contains the latest commits, while the `prod` branch holds the final stable release.

**Version 10**: Located in `source` folder

-   Visual Studio 2026 for Windows build
-   VS Code for macOS, Linux build
-   Run a task from VS Code to build, publish, or pack the app
    -   Note: for debug builds, copy the contents of `source/__assets/__app/` into the build output folder, beside the ImageGlass executable, before launching it.

**Version 9**: Located in `v9` folder

-   Visual Studio 2026 on Windows 11
-   VS Code for `WebUI`

  

Roadmap
-------

  

This project needs your help!
-----------------------------

If you find ImageGlass useful and would like to support its ongoing development, please consider making a donation or purchase Pro edition. Your support — whether financial or simply sharing ImageGlass with others — means the world to me. Every bit helps keep the project alive for everyone.

#### 👉 Explore the ways to support at imageglass.org/donate.
