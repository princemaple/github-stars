---
project: love
stars: 7591
description: LÖVE is an awesome 2D game framework for Lua.
url: https://github.com/love2d/love
---

LÖVE is an _awesome_ framework you can use to make 2D games in Lua. It's free, open-source, and works on Windows, macOS, Linux, Android, and iOS.

Documentation
-------------

We use our wiki for documentation. If you need further help, feel free to ask on our forums, our Discord server, or our subreddit.

Repository
----------

We use the 'main' branch for development of the next major release, and therefore it should not be considered stable.

There are also branches for currently released major versions, which may have fixes and changes meant for upcoming patch releases within that major version.

We tag all our releases (since we started using mercurial and git), and have binary downloads available for them.

Experimental changes are sometimes developed in a separate love-experiments repository.

Builds
------

Files for releases are in the releases section on GitHub. The site has links to files and additional platform content for the latest release.

There are also unstable/nightly builds:

-   Builds for some platforms are automatically created after each commit and are available through GitHub's CI interfaces.
-   For ubuntu linux they are in ppa:bartbes/love-unstable
-   For arch linux there's love-git in the AUR.

Test Suite
----------

The test suite in `testing/` covers all the LÖVE APIs, and tests them the same way developers use them. You can view current test coverage from any action.  
You can run the suite locally like you would run a normal LÖVE project, e.g.:  
`love testing`

See the readme in the testing folder for more info.

Contributing
------------

The best places to contribute are through the issue tracker and the official Discord server or IRC channel.

For code contributions, pull requests and patches are welcome. Be sure to read the source code style guide. Changes and new features typically get discussed in the issue tracker or on Discord or the forums before a pull request is made.

Compilation
-----------

### Windows

Follow the instructions at the megasource repository page.

### \*nix

Because in-tree builds are not allowed, the Makefiles needs to be generated in a separate build directory. In this example, folder named `build` is used:

```
$ cmake -B build -S. --install-prefix $PWD/prefix # this will create the directory `build/`.
$ cmake --build build --target install -j$(nproc) # this will build with all cores and put the files in `prefix/`.
```

Note

CMake 3.15 and earlier doesn't support `--install-prefix`. In that case, use `-DCMAKE_INSTALL_PREFIX=` instead.

### macOS

Download or clone this repository and copy, move, or symlink the `macOS/Frameworks` subfolder into love's `platform/xcode/macosx` folder and the `shared` subfolder into love's `platform/xcode` folder.

Then use the Xcode project found at `platform/xcode/love.xcodeproj` to build the `love-macosx` target.

### iOS

Building for iOS requires macOS and Xcode.

Download the `love-apple-dependencies` zip file corresponding to the LÖVE version being used from the Releases page, unzip it, and place the `iOS/libraries` subfolder into love's `platform/xcode/ios` folder and the `shared` subfolder into love's `platform/xcode` folder.

Or, download or clone this repository and copy, move, or symlink the `iOS/libraries` subfolder into love's `platform/xcode/ios` folder and the `shared` subfolder into love's `platform/xcode` folder.

Then use the Xcode project found at `platform/xcode/love.xcodeproj` to build the `love-ios` target.

See `readme-iOS.rtf` for more information.

### Android

Visit the Android build repository for build instructions.

Dependencies
------------

-   SDL3
-   OpenGL 3.3+ / OpenGL ES 3.0+ / Vulkan / Metal
-   OpenAL
-   Lua / LuaJIT / LLVM-lua
-   FreeType
-   harfbuzz
-   ModPlug
-   Vorbisfile
-   Theora
