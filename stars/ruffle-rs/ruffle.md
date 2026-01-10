---
project: ruffle
stars: 17614
description: A Flash Player emulator written in Rust
url: https://github.com/ruffle-rs/ruffle
---

  
**website | demo | nightly builds | wiki**

Ruffle
======

Ruffle is an Adobe Flash Player emulator written in the Rust programming language. Ruffle targets both the desktop and the web using WebAssembly.

Table of Contents
-----------------

-   Project status
-   Using Ruffle
-   Building from source
    -   Prerequisites
    -   Linux prerequisites
    -   Desktop
        -   Build
        -   macOS
    -   Web or Extension
    -   Android
    -   Scanner
    -   Exporter
-   Structure
-   Sponsors
-   License
-   Contributing

Project status
--------------

Ruffle supports ActionScript 1, 2 and 3 pretty well, but it's still not finished by any means. Please report any issues in the Issue Tracker.

Using Ruffle
------------

The easiest way to try out Ruffle is to visit the web demo page, then click the "Select File" button to load a SWF file of your choice.

Nightly builds of Ruffle are available for desktop and web platforms.

For more detailed instructions, see our wiki page.

Building from source
--------------------

### Prerequisites

-   Latest stable channel of Rust
-   Java, available on your PATH as `java` (required for building the library containing the builtin Flash classes for ActionScript 3)

### Linux prerequisites

The following are typical dependencies for Linux:

-   Ubuntu/Debian:
    
    sudo apt install pkg-config libasound2-dev libudev-dev default-jre-headless g++
    
-   Fedora/RHEL:
    
    sudo dnf install pkgconf-pkg-config alsa-lib-devel systemd-devel java-latest-openjdk-headless gcc-c++
    

### Desktop

#### Build

Use the following command to build and run the desktop app:

`cargo run --release --package=ruffle_desktop`

To run a specific SWF file, pass the SWF path as an argument:

`cargo run --release --package=ruffle_desktop -- test.swf`

To build in debug mode, simply omit `--release` from the command.

#### macOS

Ruffle desktop can be built from our Homebrew Tap:

`brew install --HEAD ruffle-rs/ruffle/ruffle`

_Note: because it is HEAD-only, you'll need to run `brew upgrade --fetch-HEAD ruffle` each time you want to update._

### Web or Extension

Follow the instructions in the web directory for building either the web or browser extension version of Ruffle.

This project is tested with BrowserStack.

### Android

Follow the instructions in the `ruffle-android` project for building the Android application of Ruffle.

### Scanner

If you have a collection of "real world" SWFs to test against, the scanner may be used to benchmark ruffle's parsing capabilities. Provided with a folder and an output filename, it will attempt to read all of the Flash files and report on the success of such a task.

`cargo run --release --package=ruffle_scanner -- scan folder/with/swfs/ results.csv`

### Exporter

If you have a SWF file and would like to capture an image of it, you may use the exporter tool. This currently requires hardware acceleration, but can be run headless (with no window).

-   `cargo run --release --package=exporter -- path/to/file.swf`
-   `cargo run --release --package=exporter -- path/to/file.swf path/to/screenshots --frames 5`

Structure
---------

-   `core` - core emulator and common code
-   `swf` - SWF and ActionScript parser
-   `desktop` - desktop client (uses `wgpu-rs`)
-   `web` - web client and browser extension (uses `wasm-bindgen`)
-   `render` - various rendering backends for both desktop and web
-   `video` - video decoding backends
-   `flv` - Flash Video decoder
-   `wstr` - a Flash-compatible implementation of strings
-   `scanner` - a utility to bulk parse SWF files
-   `exporter` - a utility to generate PNG screenshots of a SWF file

Sponsors
--------

You can support the development of Ruffle via GitHub Sponsors. Your sponsorship will help to ensure the accessibility of Flash content for the future. Thank you!

Sincere thanks to the diamond level sponsors of Ruffle:

License
-------

Ruffle is licensed under either of

-   Apache License, Version 2.0 (http://www.apache.org/licenses/LICENSE-2.0)
-   MIT License (http://opensource.org/licenses/MIT)

at your option.

Ruffle depends on third-party libraries under compatible licenses. See LICENSE.md for full information.

### Contributing

Ruffle welcomes contribution from everyone. See CONTRIBUTING.md for help getting started.

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the work by you shall be dual licensed as above, without any additional terms or conditions.

The entire Ruffle community, including the chat room and GitHub project, is expected to abide by the Code of Conduct that the Rust project itself follows.
