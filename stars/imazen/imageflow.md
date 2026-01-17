---
project: imageflow
stars: 4362
description: High-performance image manipulation for web servers. Includes imageflow_server, imageflow_tool, and libimageflow
url: https://github.com/imazen/imageflow
---

optimal images at incredible speeds
-----------------------------------

Download blazing fast and safer tools for a modern image workflow.

-   **`imageflow_tool`** is a command-line tool for experimenting, running batch jobs, JSON jobs, or when you want process isolation. Up to 17x faster than ImageMagick. Also produces smaller files at higher quality. Download or `docker run imazen/imageflow_tool`.
-   **`libimageflow`** is for direct (in-process) use from _your_ programming language. See our **Node bindings**, **Go bindings**, **Scala bindings**, **Elixir bindings**, or **.NET bindings**. If we don't already have bindings for your language, consider spending a day to add them. Imageflow has a simple C-compatible ABI, of which only 4 methods are needed to implement bindings.
-   **Imageflow.Server** is cross-platform and can manipulate images in-flight (e.g.`/bucket/img.jpg?w=200`) for direct use from HTML. Source images can reside in blob storage, on another server, or on the filesystem. It's a production ready server with excellent hybrid disk caching, support for Azure and Amazon blob storage, and can be easily customized. You can deploy it easily via Docker, on a VM, or via any cloud host. It's also backwards compatible with the ImageResizer API - which is useful, as ImageResizer as been integrated into more than a thousand different CMSes and applications in the last decade.

**Open an issue to share ideas, feedback, or ask questions. We believe in feedback-driven design, and streamlining real-world usage is the fastest way to a great product.**

Querystring API Documentation

JSON API Documentation

libimageflow and imageflow\_tool are available as self-contained binaries for Windows, Ubuntu, and Mac. We also offer Docker images for Linux (where glibc and OpenSSL are required).

We thank our backers on Kickstarter and the many supporters of ImageResizer for making this project a reality. Visit Imageresizing.net if you need an AGPLv3 exception for commercial use.

Start with imageflow\_tool (recommended)
----------------------------------------

`imageflow_tool examples --generate` - creates an _examples_ directory with JSON jobs and invocation scripts.

You can use command strings that are compatible with ImageResizer 4 querystrings:

`imageflow_tool v1/querystring --in source.jpg --out thumb.jpg --command "width=50&height=50&mode=crop&format=jpg"`

Or submit a JSON job file. JSON jobs can have multiple inputs and outputs, and can represent any kind of operation graph.

The following generates multiple sizes of an image from an example job file:

```
imageflow_tool v1/build --json examples/export_4_sizes/export_4_sizes.json
        --in waterhouse.jpg
        --out 1 waterhouse_w1600.jpg
              2 waterhouse_w1200.jpg
              3 waterhouse_w800.jpg
              4 waterhouse_w400.jpg
        --response operation_result.json
```

By default, imageflow\_tool prints a JSON response to stdout. You write this to disk with `--response`.

`--debug-package` will create a .zip file to reproduce problematic behavior with both `v1/build` and `v1/querystring`. Please submit bug reports; we try to make it easy.

Using Imageflow.Server for dynamic imaging
------------------------------------------

NOTE: imageflow\_server has been removed as the underlying web framework (iron) is abandoned and no longer secure. For the last few years we have suggested moving to the production-ready Imageflow.Server product, which also offers docker deployment (but we suggest your own dockerfile to permit configuration)

Now you can edit images from HTML... and use srcset without headache.

```
<img src="http://localhost:39876/demo_images/u3.jpg?w=300" />

<img src="" srcset="    http://localhost:39876/demo_images/u3.jpg?w=300 300w
                        http://localhost:39876/demo_images/u3.jpg?w=800 800w
                        http://localhost:39876/demo_images/u3.jpg?w=1600 1600w" />

```

Using libimageflow from your language
-------------------------------------

-   .NET Standard bindings can be found at https://github.com/imazen/imageflow-dotnet
-   Node bindings available at https://github.com/imazen/imageflow-node
-   Ruby - Basic bindings can be found at https://github.com/imazen/imageflow-ruby
-   C and C++ interface is stable - use bindings/headers/imageflow\_default.h or one of the many alternate conventions provided with each release.
-   Rust - Imageflow is written in Rust, so you can use the `imageflow_core` crate, althogh the interfaces are not stable or semver in line with tagged releases (those version numbers are for the C ABI, not the Rust API)
-   other languages - Use an FFI binding-generation tool for your language, and feed it whichever header file it likes best.

You also may find that `imageflow_tool` is quite fast enough for your needs.

### Crates within this project

-   imageflow\_abi - The stable API of libimageflow/imageflow.dll. Headers for libimageflow are located in `bindings/headers`
-   imageflow\_tool - The command-line tool
-   c\_components - A rust crate containing C source
-   c\_components/tests - Tests for the C components
-   imageflow\_types - Shared types used by most crates, with JSON serialization
-   imageflow\_helpers - Common helper functions and utilities
-   imageflow\_riapi - RIAPI and ImageResizer4 compatibility parsing/layout
-   imageflow\_core - The main library and execution engine

Building from Source without Docker
===================================

You'll need more than just Rust to compile Imageflow, as it has a couple C dependencies.

1.  **Install platform-specific prerequisites (find the right section below).**
    
2.  Clone and cd into this repository E.g., `git clone git@github.com:imazen/imageflow.git && cd imageflow`)
    
3.  Run `cargo build --release --all`
    
4.  Look in `./target/release` for the binaries
    

If you are on Windows, only run build commands in the window created by `win_enter_env.bat`.

### Build using `cargo` directly, although this will place binaries in `./target/release` instead.

```
* `cargo test --all` to test Imageflow in debug (slooow) mode
* `cargo build --package imageflow_abi --release` to compile `libimageflow/imageflow.dll`
* `cargo build --package imageflow_tool --release` to compile `imageflow_tool(.exe)`
* `cargo build --all --release` to compile everything in release mode
* `cargo doc --no-deps --all --release` to generate documentation.
```

Linux Pre-requisites
--------------------

(tested on Ubuntu 20.04 and 22.04.)

#Install Rust by running
curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain stable
#Ensure build tools are installed (git, curl, wget, gcc, g++, nasm, pkg-config, openssl, ca-certificates)
sudo apt-get install --no-install-recommends -y \\
  sudo build-essential nasm dh-autoreconf pkg-config ca-certificates \\
  git zip curl libpng-dev libssl-dev wget libc6-dbg  \\
  libcurl4-openssl-dev libelf-dev libdw-dev apt-transport-https

Mac OS Pre-requisites
---------------------

1.  Install XCode Command-Line Tools if you haven't already
2.  Install Homebrew if you haven't already.
3.  Install nasm, pkg-config, and wget `brew install nasm pkg-config wget`
4.  Install Rust

Windows WSL (Ubuntu) Pre-requisites
-----------------------------------

1.  Install Ubuntu from the Windows Store
2.  Run Ubuntu 22.04 and create your username/password
3.  `sudo apt-get update` to update available packages.
4.  Install Rust by running `curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain stable`
5.  Ensure build tools are installed (git, curl, wget, gcc, g++, nasm, pkg-config, openssl, ca-certificates) `sudo apt-get install git wget curl build-essential pkg-config libssl-dev libpng-dev nasm`
6.  (optional) To use a graphical text editor, you'll need to download imageflow to a "Windows" directory, then map it to a location in Ubuntu. For example, if you cloned imageflow to Documents/imageflow, you would run: `ln -s /mnt/c/Users/[YourWindowsUserName]/Documents/imageflow ~/win_imageflow`
7.  Close and re-open Ubuntu

Windows 10 Pre-requisites
-------------------------

1.  Install Visual Studio 2017 Build Tools (separately or as a VS component)
2.  Install Git 64-bit.
3.  `Run As Administrator` the NASM 64-bit installer - it will not prompt.
4.  Install Rust 64-bit if you want 64-bit Imageflow or Rust 32-bit if you don't. Install toolchain `stable` as the default, and confirm adding it to `PATH`.
5.  Open the command line and switch to this repository's root directory
6.  Edit `ci/wintools/SETUP_PATH.bat` to ensure that rust/cargo, nasm, git, and Git/mingw64/bin are all in `%PATH%`.
7.  Run `win_enter_env.bat` to start a sub-shell (edit it if you want a 32-bit build)
8.  All build commands should be run in the sub-shell. Run `cmd.exe /c "ci\wintools\win_verify_tools.bat"` to check tools are present.

How does one learn image processing for the web?
------------------------------------------------

First, read High Performance Images for context.

There are not many great textbooks on the subject. Here are some from my personal bookshelf. Between them (and Wikipedia) I was able to put together about 60% of the knowledge I needed; the rest I found by reading the source code to many popular image processing libraries.

I would start by reading Principles of Digital Image Processing: Core Algorithms front-to-back, then Digital Image Warping. Wikipedia is also a useful reference, although the relevant pages are not linked or categorized together - use specific search terms, like "bilinear interpolation" and "Lab color space".

-   Digital Image Warping
-   Computer Graphics: Principles and Practice in C (2nd Edition)
-   Principles of Digital Image Processing: Fundamental Techniques
-   Principles of Digital Image Processing: Core Algorithms
-   Principles of Digital Image Processing: Advanced Methods

I have found the source code for OpenCV, LibGD, FreeImage, Libvips, Pixman, Cairo, ImageMagick, stb\_image, Skia, and FrameWave is very useful for understanding real-world implementations and considerations. Most textbooks assume an infinite plane, ignore off-by-one errors, floating-point limitations, color space accuracy, and operational symmetry within a bounded region. I cannot recommend any textbook as an accurate reference, only as a conceptual starting point. I made some notes regarding issues to be aware of when creating an imaging library.

Also, keep in mind that computer vision is very different from image creation. In computer vision, resampling accuracy matters very little, for example. But in image creation, you are serving images to photographers, people with far keener visual perception than the average developer. The images produced will be rendered side-by-side with other CSS and images, and the least significant bit of inaccuracy is quite visible. You are competing with Lightroom; with offline tools that produce visually perfect results. End-user software will be discarded if photographers feel it is corrupting their work.
