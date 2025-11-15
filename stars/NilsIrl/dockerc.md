---
project: dockerc
stars: 4827
description: container image to single executable compiler
url: https://github.com/NilsIrl/dockerc
---

dockerc - compile docker images to standalone portable binaries
===============================================================

No more

No more `docker run`, no more `pip install`, no more `npm i`, just give your users executables they can run!

Usage
-----

Install dockerc from the latest release.

```
# Image from docker hub
$ dockerc --image docker://oven/bun --output bun
# Image in local docker daemon storage
$ dockerc --image docker-daemon:mysherlock-image:latest --output sherlock_bin
# Specify target instruction set architecture
$ dockerc --image docker://hello-world --arch arm64 --output hello
```

The output binary can then be called as you would with usual binaries. You can also specify `-e`, and `-v` in the same way you would when using `docker run`. Networked services running inside the container can be accessed directly without having to specify `-p`.

Skopeo is used for loading images, for other locations refer to its documentation.

Build from source
-----------------

Please note that this project uses Git submodules. If you clone this repository, you may need to run the following commands to initialize and update the submodules:

```
$ git submodule init
$ git submodule update
```

This will ensure that you download and update all relevant submodule contents.

dockerc uses a patched version of the zig compiler than can be found on the nils-dockerc-version branch of the NilsIrl/zig repository. There is an open PR for the patch to be included in upstream zig.

To compile dockerc use the following commands:

```
$ zig build -Doptimize=ReleaseSafe -Dtarget=x86_64-linux-musl
$ zig build -Doptimize=ReleaseSafe -Dtarget=aarch64-linux-musl
```

Features
--------

-   Compile docker images into portable binaries
-   Rootless containers
-   MacOS and Windows support (using QEMU)
-   x86\_64 support
-   arm64 support
-   Supports arguments
-   Supports specifying environment variables using `-e`
-   Supports specifying volumes using `-v`
-   Support other arguments...
