---
project: transmission
stars: 14529
description: Official Transmission BitTorrent client repository
url: https://github.com/transmission/transmission
---

About
-----

Transmission is a fast, easy, and free BitTorrent client. It comes in several flavors:

-   A native macOS GUI application
-   GTK+ and Qt GUI applications for Linux, BSD, etc.
-   A Qt-based Windows-compatible GUI application
-   A headless daemon for servers and routers
-   A web UI for remote controlling any of the above

Visit https://transmissionbt.com/ for more information.

Documentation
-------------

Transmission's documentation is currently out-of-date, but the team has recently begun a new project to update it and is looking for volunteers. If you're interested, please feel free to submit pull requests!

Command line interface notes
----------------------------

Transmission is fully supported in transmission-remote, the preferred cli client.

Three standalone tools to examine, create, and edit .torrent files exist: transmission-show, transmission-create, and transmission-edit, respectively.

Prior to development of transmission-remote, the standalone client transmission-cli was created. Limited to a single torrent at a time, transmission-cli is deprecated and exists primarily to support older hardware dependent upon it. In almost all instances, transmission-remote should be used instead.

Different distributions may choose to package any or all of these tools in one or more separate packages.

Building
--------

Transmission has an Xcode project file (Transmission.xcodeproj) for building in Xcode.

For a more detailed description, and dependencies, visit How to Build Transmission in docs

### Building a Transmission release from the command line

$ tar xf transmission-4.1.0.tar.xz
$ cd transmission-4.1.0
# Use -DCMAKE\_BUILD\_TYPE=RelWithDebInfo to build optimized binary with debug information. (preferred)
# Use -DCMAKE\_BUILD\_TYPE=Release to build full optimized binary.
$ cmake -B build -DCMAKE\_BUILD\_TYPE=RelWithDebInfo
$ cd build
$ cmake --build .
$ sudo cmake --install .

### Building Transmission from the nightly builds

Download a tarball from https://build.transmissionbt.com/job/trunk-linux/ and follow the steps from the previous section.

If you're new to building programs from source code, this is typically easier than building from Git.

### Building Transmission from Git (first time)

$ git clone --recurse-submodules https://github.com/transmission/transmission Transmission
$ cd Transmission
# Use -DCMAKE\_BUILD\_TYPE=RelWithDebInfo to build optimized binary with debug information. (preferred)
# Use -DCMAKE\_BUILD\_TYPE=Release to build full optimized binary.
$ cmake -B build -DCMAKE\_BUILD\_TYPE=RelWithDebInfo
$ cd build
$ cmake --build .
$ sudo cmake --install .

### Building Transmission from Git (updating)

$ cd Transmission/build
$ cmake --build . -t clean
$ git submodule foreach --recursive git clean -xfd
$ git pull --rebase --prune
$ git submodule update --init --recursive
$ cmake --build .
$ sudo cmake --install .

Contributing
------------

### Code Style

You would want to setup your editor to make use of the .clang-format file located in the root of this repository and the eslint/prettier rules in web/package.json.

If for some reason you are unwilling or unable to do so, there is a shell script which you can use: `./code_style.sh`

### Translations

See language translations.

Sponsors
--------

macOS CI builds are running on a M1 Mac Mini provided by MacStadium

Free code signing on Windows provided by SignPath.io, certificate by SignPath Foundation
