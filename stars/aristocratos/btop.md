---
project: btop
stars: 30624
description: A monitor of resources
url: https://github.com/aristocratos/btop
---

Index
-----

-   News
-   Documents
-   Description
-   Features
-   Themes
-   Support and funding
-   Prerequisites (Read this if you are having issues!)
-   Screenshots
-   Keybindings
-   Installation Linux/macOS
-   Compilation Linux
-   Compilation macOS
-   Compilation FreeBSD
-   Compilation NetBSD
-   Compilation OpenBSD
-   Testing
-   GPU compatibility
-   Installing the snap
-   Configurability
-   License

If you are considering donating, please first consider donating to:

News
----

##### 4 December 2025

Since there is a increasing amount of AI generated/assisted PR's, the following guidlines have been added to CONTRIBUTING.md:

-   Submissions where the majority of the code is AI generated must be marked with \[AI generated\].
    
-   "Vibe coded" PR's where it seems like the author doesn't understand the generated code will be dismissed.
    

##### 22 September 2024

Btop release v1.4.0

Intel GPU support added, note that only GPU utilization, power usage and clock speed available to monitor. Thanks to @bjia56 for contributions.

NetBSD support added. Thanks to @fraggerfox for contributions.

See CHANGELOG.md and latest release for detailed list of new features, bug fixes and new themes.

##### 7 January 2024

Btop release v1.3.0

Big release with GPU support added for Linux and platform support for OpenBSD. Big thanks to @romner-set (GPU support) and @joske (OpenBSD support) for contributions. And a multitude of bugfixes and small changes, see CHANGELOG.md and latest release for detailed list and attributions.

See news entry below for more information regarding GPU support.

##### 25 November 2023

GPU monitoring added for Linux!

Compile from git main to try it out.

Use keys `5`, `6`, `7` and `0` to show/hide the gpu monitoring boxes. `5` = Gpu 1, `6` = Gpu 2, etc.

Gpu stats/graphs can also be displayed in the "Cpu box" (not as verbose), see the cpu options menu for info and configuration.

Note that the binaries provided on the release page (when released) and the continuous builds will not have gpu support enabled.

Because the GPU support relies on loading of dynamic gpu libraries, gpu support will not work when also static linking.

See Compilation Linux for more info on how to compile with gpu monitoring support.

Many thanks to @romner-set who wrote the vast majority of the implementation for GPU support.

Big update with version bump to 1.3 coming soon.

##### 28 August 2022

First release of btop4win available at https://github.com/aristocratos/btop4win

More...

##### 16 January 2022

Release v1.2.0 with FreeBSD support. No release binaries for FreeBSD provided as of yet.

Again a big thanks to @joske for his porting efforts!

Since compatibility with Linux, macOS and FreeBSD are done, the focus going forward will be on new features like GPU monitoring.

##### 13 November 2021

Release v1.1.0 with macOS support. Binaries in continuous-build-macos are only x86 for now. macOS binaries + installer are included for both x86 and ARM64 (Apple Silicon) in the releases.

Big thank you to @joske who wrote the vast majority of the implementation!

##### 30 October 2021

Work on the OSX \[macOS\] and FreeBSD branches, both initiated and mostly worked on by @joske, will likely be completed in the coming weeks. The OSX \[macOS\] branch has some memory leaks that needs to be sorted out and both have some issues with the processes cpu usage calculation and other smaller issues that needs fixing.

If you want to help out, test for bugs/fix bugs or just try out the branches:

**macOS / OSX**

# Install and use Homebrew or MacPorts package managers for easy dependency installation
brew install coreutils make gcc@11 lowdown
git clone https://github.com/aristocratos/btop.git
cd btop
git checkout OSX
gmake

**FreeBSD**

sudo pkg install gmake gcc11 coreutils git lowdown
git clone https://github.com/aristocratos/btop.git
cd btop
git checkout freebsd
gmake

Note that GNU make (`gmake`) is recommended but not required for macOS/OSX but it is required on FreeBSD.

##### 6 October 2021

macOS development have been started by @joske, big thanks :) See branch OSX for current progress.

##### 18 September 2021

The Linux version of btop++ is complete. Released as version 1.0.0

I will be providing statically compiled binaries for a range of architectures in every release for those having problems compiling.

For compilation GCC 11 is required.

Please report any bugs to the Issues page.

The development plan right now:

-   1.1.0 macOS \[OSX\] support
-   1.2.0 FreeBSD support
-   1.3.0 Support for GPU monitoring
-   1.X.0 Other platforms and features...

Windows support is not in the plans as of now, but if anyone else wants to take it on, I will try to help.

##### 5 May 2021

This project is gonna take some time until it has complete feature parity with bpytop, since all system information gathering will have to be written from scratch without any external libraries. And will need some help in the form of code contributions to get complete support for BSD and macOS/OSX.

Documents
---------

**CHANGELOG.md**

**CONTRIBUTING.md**

**CODE\_OF\_CONDUCT.md**

Description
-----------

Resource monitor that shows usage and stats for processor, memory, disks, network and processes.

C++ version and continuation of bashtop and bpytop.

Features
--------

-   Easy to use, with a game inspired menu system.
-   Full mouse support: all buttons with a highlighted key are clickable and mouse scrolling works in process list and menu boxes.
-   Fast and responsive UI with UP, DOWN key process selection.
-   Function for showing detailed stats for selected process.
-   Ability to filter processes.
-   Easy switching between sorting options.
-   Tree view of processes.
-   Send any signal to selected process.
-   Pause the process list.
-   UI menu for changing all config file options.
-   Auto scaling graph for network usage.
-   Shows IO activity and speeds for disks.
-   Battery meter
-   Selectable symbols for the graphs.
-   Custom presets
-   And more...

Themes
------

Btop++ uses the same theme files as bpytop and bashtop (some color values missing in bashtop themes).

See themes folder for available themes.

Btop searches the following directories for system themes:

-   `../share/btop/themes` (this path is relative to the btop executable)
-   `/usr/local/share/btop/themes`
-   `/usr/share/btop/themes`

The first directory that exists and isn't empty is used as the system themes directory.

The user themes directory depends on which environment variables are set:

-   If `$XDG_CONFIG_HOME` is set, the user themes directory is `$XDG_CONFIG_HOME/btop/themes`
-   Otherwise, if `$HOME` is set, the user themes directory is `$HOME/.config/btop/themes`
-   Otherwise, the user themes directory is `~/.config/btop/themes`

The `make install` command places the default themes in `[$PREFIX or /usr/local]/share/btop/themes`. User created themes should be placed in the user themes directory.

Use the `--themes-dir` command-line option to specify a custom themes directory. When specified, this directory takes priority over the default search paths.

Let me know if you want to contribute with new themes.

The new Process list pausing and Process following features introduce a few new theme attributes. These attributes still need to be added to all of the existing themes (except the default one).

Process list banner attributes:

-   proc\_pause\_bg: background color of the banner when the list is paused.
-   proc\_follow\_bg: background color of the banner when the process following feature is active.
-   proc\_banner\_bg: background color of the banner when the process following feature is active AND the list is paused.
-   proc\_banner\_fg: foreground (text) color of the banner

Process following attributes:

-   followed\_bg: background color of the followed process in the list.
-   followed\_fg: foreground color of the followed process in the list.

Support and funding
-------------------

You can sponsor this project through GitHub. See my sponsors page for options.

Or donate through PayPal or ko-fi.

Any support is greatly appreciated!

Prerequisites
-------------

For the best experience run within a terminal with support for:

-   24-bit truecolor (See list of terminals with truecolor support)
-   256-color terminals are supported through 24-bit to 256-color conversion when setting "truecolor" to False in the options or with "-lc/--low-color" arguments.
-   16 color TTY mode will be activated if a real tty device is detected. Can be forced with "-t/--tty" arguments.
-   Wide characters (Are sometimes problematic in web-based terminals)

Also necessary is a UTF8 locale and a font that includes:

-   Unicode Block “Braille Patterns” U+2800 - U+28FF (Not needed in TTY mode or with graphs set to type: block or tty.)
-   Unicode Block “Geometric Shapes” U+25A0 - U+25FF
-   Unicode Block "Box Drawing" and "Block Elements" U+2500 - U+259F

### **Optional Dependencies (Needed for GPU monitoring) (Only Linux)**

GPU monitoring also requires a btop binary built with GPU support (`GPU_SUPPORT=true` flag).

See GPU compatibility section for more about compiling with GPU support.

-   **NVIDIA**
    
    If you have an NVIDIA GPU you must use an official NVIDIA driver, both the closed-source and open-source ones have been verified to work.
    
    In addition to that you must also have the nvidia-ml dynamic library installed, which should be included with the driver package of your distribution.
    
-   **AMD**
    
    If you have an AMD GPU `rocm_smi_lib` is required, which may or may not be packaged for your distribution.
    
-   **INTEL**
    
    Requires a working C compiler if compiling from source.
    
    Also requires the user to have permission to read from SYSFS.
    
    Can be set with `make setcap` (preferred) or `make setuid` or by running btop with `sudo` or equivalent.
    

### **Notice (Text rendering issues)**

-   If you are having problems with the characters in the graphs not looking like they do in the screenshots, it's likely a problem with your systems configured fallback font not having support for braille characters.
    
-   See Terminess Powerline for an example of a font that includes the braille symbols.
    
-   See comments by @sgleizes link and @XenHat link in issue #100 for possible solutions.
    
-   If text is misaligned and you use Konsole or Yakuake, turning off "Bi-Directional text rendering" is a possible fix.
    
-   Characters clipping into each other or text/border misalignments are not bugs caused by btop, but most likely a fontconfig or terminal problem where the braille characters making up the graphs aren't rendered correctly.
    
-   Look to the creators of the terminal emulator you use to fix these issues if the previously mentioned fixes don't work for you.
    

Screenshots
-----------

#### Main UI showing details for a selected process

#### Main UI in TTY mode

#### Main UI with custom options

#### Main-menu

#### Options-menu

#### Help-menu

Installation
------------

**Binaries for Linux are statically compiled with musl and work on kernel releases 2.6.39 and newer**

1.  **Download btop-(VERSION)-(ARCH)-(PLATFORM).tbz from latest release and unpack to a new folder**
    
    **Notice! Use x86\_64 for 64-bit x86 systems, i486 and i686 are 32-bit!**
    
2.  **Install (from created folder)**
    
    -   **Run:**
    
    # use "make install PREFIX=/target/dir" to set target, default: /usr/local
    # only use "sudo" when installing to a NON user owned directory
    sudo make install
    
3.  **(Optional/Required for Intel GPU and CPU wattage) Set extended capabilities or suid bit to btop**
    
    Enables signal sending to any process without starting with `sudo` and can prevent /proc read permissions problems on some systems.
    
    Is required for Intel GPU support and CPU wattage monitoring.
    
    -   **Run:**
    
    # run after make install and use same PREFIX if any was used at install
    sudo make setcap
    
    -   **or**
    
    # run after make install and use same PREFIX if any was used at install
    # set SU\_USER and SU\_GROUP to select user and group, default is root:root
    sudo make setuid
    

-   **Uninstall**
    
    -   **Run:**
    
    sudo make uninstall
    
-   **Show help**
    
    make help
    

**Binary release (from native os repo)**

-   **openSUSE**
    -   **Tumbleweed:**
        
        sudo zypper in btop
        
    -   For all other versions, see openSUSE Software: btop
-   **Fedora**
    
    sudo dnf install btop
    
-   **RHEL/Rocky/AlmaLinux 8+**
    
    sudo dnf install epel-release
    sudo dnf install btop
    
-   **FreeBSD**
    
     pkg install btop
    
-   **NetBSD**
    
     pkg\_add btop
    

**Binary release on Homebrew (macOS (x86\_64 & ARM64) / Linux (x86\_64))**

-   **Homebrew**
    
    brew install btop
    

Compilation Linux
-----------------

Requires at least GCC 14 or Clang 19.

The Makefile also needs GNU `coreutils` and `sed` (should already be installed on any modern distribution).

### GPU compatibility

Btop++ supports Nvidia and AMD GPUs and Intel IGPUs out of the box on Linux x86\_64, provided you have the correct drivers and libraries.

Gpu support for Nvidia or AMD will not work when static linking glibc (or musl, etc.)!

For x86\_64 Linux the flag `GPU_SUPPORT` is automatically set to `true`, to manually disable gpu support set the flag to false, like:

`make GPU_SUPPORT=false` (or `cmake -DBTOP_GPU=false` with CMake)

-   **NVIDIA**
    
    You must use an official NVIDIA driver, both the closed-source and open-source ones have been verified to work.
    
    In addition to that you must also have the `nvidia-ml` dynamic library installed, which should be included with the driver package of your distribution.
    
-   **AMD**
    
    AMDGPU data is queried using the ROCm SMI library, which may or may not be packaged for your distribution. If your distribution doesn't provide a package, btop++ is statically linked to ROCm SMI with the `RSMI_STATIC=true` make flag.
    
    This flag expects the ROCm SMI source code in `lib/rocm_smi_lib`, and compilation will fail if it's not there. The latest tested version is 5.6.x, which can be obtained with the following command:
    
    git clone https://github.com/rocm/rocm\_smi\_lib.git --depth 1 -b rocm-5.6.x lib/rocm\_smi\_lib
    

### With Make

1.  **Install dependencies (example for Ubuntu 24.04 Noble)**
    
    sudo apt install coreutils sed git build-essential lowdown
    
2.  **Clone repository**
    
    git clone https://github.com/aristocratos/btop.git
    cd btop
    
3.  **Compile**
    
    make
    
    Options for make:
    
    Flag
    
    Description
    
    `VERBOSE=true`
    
    To display full compiler/linker commands
    
    `STATIC=true`
    
    For static compilation
    
    `QUIET=true`
    
    For less verbose output
    
    `STRIP=true`
    
    To force stripping of debug symbols (adds `-s` linker flag)
    
    `DEBUG=true`
    
    Sets OPTFLAGS to `-O0 -g` and enables more verbose debug logging
    
    `ARCH=<architecture>`
    
    To manually set the target architecture
    
    `GPU_SUPPORT=<true|false>`
    
    Enable/disable GPU support (Enabled by default on X86\_64 Linux)
    
    `RSMI_STATIC=true`
    
    To statically link the ROCm SMI library used for querying AMDGPU
    
    `ADDFLAGS=<flags>`
    
    For appending flags to both compiler and linker
    
    `CXX=<compiler>`
    
    Manually set which compiler to use
    
    Example: `make ADDFLAGS=-march=native` might give a performance boost if compiling only for your own system.
    
    Notice! If using LDAP Authentication, usernames will show as UID number for LDAP users if compiling statically with glibc.
    
4.  **Install**
    
    sudo make install
    
    Append `PREFIX=/target/dir` to set target, default: `/usr/local`
    
    Notice! Only use "sudo" when installing to a NON user owned directory.
    
5.  **(Optional/Required for Intel GPU support and CPU wattage) Set extended capabilities or suid bit to btop**
    
    No need for `sudo` to enable signal sending to any process and to prevent /proc read permissions problems on some systems.
    
    Also required for Intel GPU monitoring and CPU wattage monitoring.
    
    Run after make install and use same PREFIX if any was used at install.
    
    sudo make setcap
    
    or
    
    Set `SU_USER` and `SU_GROUP` to select user and group, default is `root` and `root`
    
    sudo make setuid
    

-   **Uninstall**
    
    sudo make uninstall
    
-   **Remove any object files from source dir**
    
    make clean
    
-   **Remove all object files, binaries and created directories in source dir**
    
    make distclean
    
-   **Show help**
    
    make help
    

### With CMake (Community maintained)

1.  **Install build dependencies**
    
    Requires Clang / GCC, CMake, Ninja, Lowdown and Git
    
    For example, with Debian Bookworm:
    
    sudo apt install cmake git g++ ninja-build lowdown
    
2.  **Clone the repository**
    
    git clone https://github.com/aristocratos/btop.git && cd btop
    
3.  **Compile**
    
    # Configure
    cmake -B build -G Ninja
    # Build
    cmake --build build
    
    This will automatically build a release version of btop.
    
    Some useful options to pass to the configure step:
    
    Configure flag
    
    Description
    
    `-DBTOP_STATIC=<ON|OFF>`
    
    Enables static linking (OFF by default)
    
    `-DBTOP_LTO=<ON|OFF>`
    
    Enables link time optimization (ON by default)
    
    | `-DBTOP_GPU=<ON\|OFF>` | Enable GPU support (ON by default) | | `-DBTOP_RSMI_STATIC=<ON\|OFF>` | Build and link the ROCm SMI library statically (OFF by default) | | `-DCMAKE_INSTALL_PREFIX=<path>` | The installation prefix ('/usr/local' by default) |
    
    To force any other compiler, run `CXX=<compiler> cmake -B build -G Ninja`
    
4.  **Install**
    
    cmake --install build
    
    May require root privileges
    
5.  **Uninstall**
    
    CMake doesn't generate an uninstall target by default. To remove installed files, run
    
    ```
    cat build/install_manifest.txt | xargs rm -irv
    ```
    
6.  **Cleanup build directory**
    
    cmake --build build -t clean
    

Compilation macOS OSX
---------------------

Requires at least GCC 14 or Clang 19.

The Makefile also needs GNU coreutils and `sed`.

Install and use Homebrew or MacPorts package managers for easy dependency installation

### With Make

1.  **Install dependencies (example for Homebrew)**
    
    brew install coreutils make gcc@15 lowdown
    
2.  **Clone repository**
    
    git clone https://github.com/aristocratos/btop.git
    cd btop
    
3.  **Compile**
    
    gmake
    
    Options for make:
    
    Flag
    
    Description
    
    `VERBOSE=true`
    
    To display full compiler/linker commands
    
    `STATIC=true`
    
    For static compilation (only libgcc and libstdc++)
    
    `QUIET=true`
    
    For less verbose output
    
    `STRIP=true`
    
    To force stripping of debug symbols (adds `-s` linker flag)
    
    `DEBUG=true`
    
    Sets OPTFLAGS to `-O0 -g` and enables more verbose debug logging
    
    `ARCH=<architecture>`
    
    To manually set the target architecture
    
    `ADDFLAGS=<flags>`
    
    For appending flags to both compiler and linker
    
    `CXX=<compiler>`
    
    Manually set which compiler to use
    
    Example: `gmake ADDFLAGS=-march=native` might give a performance boost if compiling only for your own system.
    
4.  **Install**
    
    sudo gmake install
    
    Append `PREFIX=/target/dir` to set target, default: `/usr/local`
    
    Notice! Only use "sudo" when installing to a NON user owned directory.
    
5.  **(Recommended) Set suid bit to make btop always run as root (or other user)**
    
    sudo gmake setuid
    
    No need for `sudo` to see information for non user owned processes and to enable signal sending to any process.
    
    Run after make install and use same PREFIX if any was used at install.
    
    Set `SU_USER` and `SU_GROUP` to select user and group, default is `root` and `wheel`
    

-   **Uninstall**
    
    sudo gmake uninstall
    
-   **Remove any object files from source dir**
    
    gmake clean
    
-   **Remove all object files, binaries and created directories in source dir**
    
    gmake distclean
    
-   **Show help**
    
    gmake help
    

### With CMake (Community maintained)

1.  **Install build dependencies**
    
    Requires Clang, CMake, Ninja, Lowdown and Git
    
    brew update --quiet
    brew install cmake git llvm ninja lowdown
    
2.  **Clone the repository**
    
    git clone https://github.com/aristocratos/btop.git && cd btop
    
3.  **Compile**
    
    # Configure
    export LLVM\_PREFIX="$(brew --prefix llvm)"
    export CXX="$LLVM\_PREFIX/bin/clang++"
    export CPPFLAGS="\-I$LLVM\_PREFIX/include"
    export LDFLAGS="\-L$LLVM\_PREFIX/lib -L$LLVM\_PREFIX/lib/c++ -Wl,-rpath,$LLVM\_PREFIX/lib/c++ -fuse-ld=$LLVM\_PREFIX/bin/ld64.lld"
    cmake -B build -G Ninja
    # Build
    cmake --build build
    
    This will automatically build a release version of btop.
    
    Some useful options to pass to the configure step:
    
    Configure flag
    
    Description
    
    `-DBTOP_LTO=<ON|OFF>`
    
    Enables link time optimization (ON by default)
    
    | `-DCMAKE_INSTALL_PREFIX=<path>` | The installation prefix ('/usr/local' by default) |
    
    To force any specific compiler, run `CXX=<compiler> cmake -B build -G Ninja`
    
4.  **Install**
    
    cmake --install build
    
    May require root privileges
    
5.  **Uninstall**
    
    CMake doesn't generate an uninstall target by default. To remove installed files, run
    
    ```
    cat build/install_manifest.txt | xargs rm -irv
    ```
    
6.  **Cleanup build directory**
    
    cmake --build build -t clean
    

Compilation FreeBSD
-------------------

Requires at least Clang 19 (default) or GCC 14.

Note that GNU make (`gmake`) is required to compile on FreeBSD.

### With gmake

1.  **Install dependencies**
    
    sudo pkg install gmake coreutils git lowdown
    
2.  **Clone repository**
    
    git clone https://github.com/aristocratos/btop.git
    cd btop
    
3.  **Compile**
    
    gmake
    
    Options for make:
    
    Flag
    
    Description
    
    `VERBOSE=true`
    
    To display full compiler/linker commands
    
    `STATIC=true`
    
    For static compilation (only libgcc and libstdc++)
    
    `QUIET=true`
    
    For less verbose output
    
    `STRIP=true`
    
    To force stripping of debug symbols (adds `-s` linker flag)
    
    `DEBUG=true`
    
    Sets OPTFLAGS to `-O0 -g` and enables more verbose debug logging
    
    `ARCH=<architecture>`
    
    To manually set the target architecture
    
    `ADDFLAGS=<flags>`
    
    For appending flags to both compiler and linker
    
    `CXX=<compiler>`
    
    Manually set which compiler to use
    
    Example: `gmake ADDFLAGS=-march=native` might give a performance boost if compiling only for your own system.
    
4.  **Install**
    
    sudo gmake install
    
    Append `PREFIX=/target/dir` to set target, default: `/usr/local`
    
    Notice! Only use "sudo" when installing to a NON user owned directory.
    
5.  **(Recommended) Set suid bit to make btop always run as root (or other user)**
    
    sudo gmake setuid
    
    No need for `sudo` to see information for non user owned processes and to enable signal sending to any process.
    
    Run after make install and use same PREFIX if any was used at install.
    
    Set `SU_USER` and `SU_GROUP` to select user and group, default is `root` and `wheel`
    

-   **Uninstall**
    
    sudo gmake uninstall
    
-   **Remove any object files from source dir**
    
    gmake clean
    
-   **Remove all object files, binaries and created directories in source dir**
    
    gmake distclean
    
-   **Show help**
    
    gmake help
    

### With CMake (Community maintained)

1.  **Install build dependencies**
    
    Requires Clang / GCC, CMake, Ninja, Lowdown and Git
    
    pkg install cmake ninja lowdown
    
2.  **Clone the repository**
    
    git clone https://github.com/aristocratos/btop.git && cd btop
    
3.  **Compile**
    
    # Configure
    cmake -B build -G Ninja
    # Build
    cmake --build build
    
    This will automatically build a release version of btop.
    
    Some useful options to pass to the configure step:
    
    Configure flag
    
    Description
    
    `-DBTOP_STATIC=<ON|OFF>`
    
    Enables static linking (OFF by default)
    
    `-DBTOP_LTO=<ON|OFF>`
    
    Enables link time optimization (ON by default)
    
    | `-DCMAKE_INSTALL_PREFIX=<path>` | The installation prefix ('/usr/local' by default) |
    
    _**Note:** Static linking does not work with GCC._
    
    To force any other compiler, run `CXX=<compiler> cmake -B build -G Ninja`
    
4.  **Install**
    
    cmake --install build
    
    May require root privileges
    
5.  **Uninstall**
    
    CMake doesn't generate an uninstall target by default. To remove installed files, run
    
    ```
    cat build/install_manifest.txt | xargs rm -irv
    ```
    
6.  **Cleanup build directory**
    
    cmake --build build -t clean
    

Compilation NetBSD
------------------

Requires at least GCC 14.

Note that GNU make (`gmake`) is required to compile on NetBSD.

### With gmake

1.  **Install dependencies**
    
    /usr/sbin/pkg\_add pkgin
    pkgin install -y coregutils gcc14 git gmake
    
2.  **Clone repository**
    
    git clone https://github.com/aristocratos/btop.git
    cd btop
    
3.  **Compile**
    
    CXX=/usr/pkg/gcc14/bin/g++ gmake CXXFLAGS="\-DNDEBUG"
    
    Options for make:
    
    Flag
    
    Description
    
    `VERBOSE=true`
    
    To display full compiler/linker commands
    
    `STATIC=true`
    
    For static compilation (only libgcc and libstdc++)
    
    `QUIET=true`
    
    For less verbose output
    
    `STRIP=true`
    
    To force stripping of debug symbols (adds `-s` linker flag)
    
    `DEBUG=true`
    
    Sets OPTFLAGS to `-O0 -g` and enables more verbose debug logging
    
    `ARCH=<architecture>`
    
    To manually set the target architecture
    
    `ADDFLAGS=<flags>`
    
    For appending flags to both compiler and linker
    
    `CXX=<compiler>`
    
    Manually set which compiler to use
    
    Example: `gmake ADDFLAGS=-march=native` might give a performance boost if compiling only for your own system.
    
4.  **Install**
    
    sudo gmake install
    
    Append `PREFIX=/target/dir` to set target, default: `/usr/local`
    
    Notice! Only use "sudo" when installing to a NON user owned directory.
    
5.  **(Recommended) Set suid bit to make btop always run as root (or other user)**
    
    sudo gmake setuid
    
    No need for `sudo` to see information for non user owned processes and to enable signal sending to any process.
    
    Run after make install and use same PREFIX if any was used at install.
    
    Set `SU_USER` and `SU_GROUP` to select user and group, default is `root` and `wheel`
    

-   **Uninstall**
    
    sudo gmake uninstall
    
-   **Remove any object files from source dir**
    
    gmake clean
    
-   **Remove all object files, binaries and created directories in source dir**
    
    gmake distclean
    
-   **Show help**
    
    gmake help
    

### With CMake (Community maintained)

1.  **Install build dependencies**
    
    Requires GCC, CMake, Ninja and Git
    
    /usr/sbin/pkg\_add pkgin
    pkgin install cmake ninja-build gcc14 git
    
2.  **Clone the repository**
    
    git clone https://github.com/aristocratos/btop.git && cd btop
    
3.  **Compile**
    
    # Configure
    CXX="/usr/pkg/gcc14/bin/g++" cmake -B build -G Ninja
    # Build
    cmake --build build
    
    This will automatically build a release version of btop.
    
    Some useful options to pass to the configure step:
    
    Configure flag
    
    Description
    
    `-DBTOP_LTO=<ON|OFF>`
    
    Enables link time optimization (ON by default)
    
    | `-DCMAKE_INSTALL_PREFIX=<path>` | The installation prefix ('/usr/local' by default) |
    
    To force any other compiler, run `CXX=<compiler> cmake -B build -G Ninja`
    
4.  **Install**
    
    cmake --install build
    
    May require root privileges
    
5.  **Uninstall**
    
    CMake doesn't generate an uninstall target by default. To remove installed files, run
    
    ```
    cat build/install_manifest.txt | xargs rm -irv
    ```
    
6.  **Cleanup build directory**
    
    cmake --build build -t clean
    

Compilation OpenBSD
-------------------

Note that GNU make (`gmake`) is required to compile on OpenBSD.

### With gmake

1.  **Install dependencies**
    
    pkg\_add coreutils git gmake lowdown
    
2.  **Clone repository**
    
    git clone https://github.com/aristocratos/btop.git
    cd btop
    
3.  **Compile**
    
    gmake
    
    Options for make:
    
    Flag
    
    Description
    
    `VERBOSE=true`
    
    To display full compiler/linker commands
    
    `STATIC=true`
    
    For static compilation (only libgcc and libstdc++)
    
    `QUIET=true`
    
    For less verbose output
    
    `STRIP=true`
    
    To force stripping of debug symbols (adds `-s` linker flag)
    
    `DEBUG=true`
    
    Sets OPTFLAGS to `-O0 -g` and enables more verbose debug logging
    
    `ARCH=<architecture>`
    
    To manually set the target architecture
    
    `ADDFLAGS=<flags>`
    
    For appending flags to both compiler and linker
    
    `CXX=<compiler>`
    
    Manually set which compiler to use
    
    Example: `gmake ADDFLAGS=-march=native` might give a performance boost if compiling only for your own system.
    
4.  **Install**
    
    sudo gmake install
    
    Append `PREFIX=/target/dir` to set target, default: `/usr/local`
    
    Notice! Only use "sudo" when installing to a NON user owned directory.
    
5.  **(Recommended) Set suid bit to make btop always run as root (or other user)**
    
    sudo gmake setuid
    
    No need for `sudo` to see information for non user owned processes and to enable signal sending to any process.
    
    Run after make install and use same PREFIX if any was used at install.
    
    Set `SU_USER` and `SU_GROUP` to select user and group, default is `root` and `wheel`
    

-   **Uninstall**
    
    sudo gmake uninstall
    
-   **Remove any object files from source dir**
    
    gmake clean
    
-   **Remove all object files, binaries and created directories in source dir**
    
    gmake distclean
    
-   **Show help**
    
    gmake help
    

### With CMake (Community maintained)

1.  **Install build dependencies**
    
    Requires GCC, CMake, Ninja, Lowdown and Git
    
    _**Note:** LLVM's libc++ shipped with OpenBSD 7.4 is too old and cannot compile btop._
    
    pkg\_add cmake git ninja lowdown
    
2.  **Clone the repository**
    
    git clone https://github.com/aristocratos/btop.git && cd btop
    
3.  **Compile**
    
    # Configure
    cmake -B build -G Ninja
    # Build
    cmake --build build
    
    This will automatically build a release version of btop.
    
    Some useful options to pass to the configure step:
    
    Configure flag
    
    Description
    
    `-DBTOP_LTO=<ON|OFF>`
    
    Enables link time optimization (ON by default)
    
    `-DCMAKE_INSTALL_PREFIX=<path>`
    
    The installation prefix ('/usr/local' by default)
    
    To force any other compiler, run `CXX=<compiler> cmake -B build -G Ninja`
    
4.  **Install**
    
    cmake --install build
    
    May require root privileges
    
5.  **Uninstall**
    
    CMake doesn't generate an uninstall target by default. To remove installed files, run
    
    ```
    cat build/install_manifest.txt | xargs rm -irv
    ```
    
6.  **Cleanup build directory**
    
    cmake --build build -t clean
    

Testing
-------

Testing requires CMake. Tests are build by default and can be run with `ctest --test-dir <build>`.

If you want to disable building tests, pass `-DBUILD_TESTING=OFF` to the configure step.

Installing the snap
-------------------

### Note: there are now two snaps available: `btop` and `btop-desktop`. The desktop version is much larger and includes the desktop entries needed to allow for launching `btop` with a click.

-   **Install the snap**
    
    sudo snap install btop
    or
    sudo snap install btop-desktop
    
-   **Install the latest snap from the edge channel**
    
    ```
    sudo snap install btop --edge
    or
    sudo snap install btop-desktop --edge
    ```
    
-   **Connect the interface**
    
    sudo snap connect btop:removable-media
    or
    sudo snap connect btop-desktop:removable-media
    

Configurability
---------------

All options changeable from within UI. Config and log files stored in `$XDG_CONFIG_HOME/btop` or `$HOME/.config/btop` folder

#### btop.conf: (auto generated if not found)

#? Config file for btop v.1.4.5

#\* Name of a btop++/bpytop/bashtop formatted ".theme" file, "Default" and "TTY" for builtin themes.
#\* Themes should be placed in "../share/btop/themes" relative to binary or "$HOME/.config/btop/themes"
color\_theme = "Default"

#\* If the theme set background should be shown, set to False if you want terminal background transparency.
theme\_background = true

#\* Sets if 24-bit truecolor should be used, will convert 24-bit colors to 256 color (6x6x6 color cube) if false.
truecolor = true

#\* Set to true to force tty mode regardless if a real tty has been detected or not.
#\* Will force 16-color mode and TTY theme, set all graph symbols to "tty" and swap out other non tty friendly symbols.
force\_tty = false

#\* Define presets for the layout of the boxes. Preset 0 is always all boxes shown with default settings. Max 9 presets.
#\* Format: "box\_name:P:G,box\_name:P:G" P=(0 or 1) for alternate positions, G=graph symbol to use for box.
#\* Use whitespace " " as separator between different presets.
#\* Example: "cpu:0:default,mem:0:tty,proc:1:default cpu:0:braille,proc:0:tty"
presets = "cpu:1:default,proc:0:default cpu:0:default,mem:0:default,net:0:default cpu:0:block,net:0:tty"

#\* Set to True to enable "h,j,k,l,g,G" keys for directional control in lists.
#\* Conflicting keys for h:"help" and k:"kill" is accessible while holding shift.
vim\_keys = false

#\* Rounded corners on boxes, is ignored if TTY mode is ON.
rounded\_corners = true

#\* Use terminal synchronized output sequences to reduce flickering on supported terminals.
terminal\_sync = true

#\* Default symbols to use for graph creation, "braille", "block" or "tty".
#\* "braille" offers the highest resolution but might not be included in all fonts.
#\* "block" has half the resolution of braille but uses more common characters.
#\* "tty" uses only 3 different symbols but will work with most fonts and should work in a real TTY.
#\* Note that "tty" only has half the horizontal resolution of the other two, so will show a shorter historical view.
graph\_symbol = "braille"

# Graph symbol to use for graphs in cpu box, "default", "braille", "block" or "tty".
graph\_symbol\_cpu = "default"

# Graph symbol to use for graphs in cpu box, "default", "braille", "block" or "tty".
graph\_symbol\_mem = "default"

# Graph symbol to use for graphs in cpu box, "default", "braille", "block" or "tty".
graph\_symbol\_net = "default"

# Graph symbol to use for graphs in cpu box, "default", "braille", "block" or "tty".
graph\_symbol\_proc = "default"

#\* Manually set which boxes to show. Available values are "cpu mem net proc" and "gpu0" through "gpu5", separate values with whitespace.
shown\_boxes = "cpu mem net proc"

#\* Update time in milliseconds, recommended 2000 ms or above for better sample times for graphs.
update\_ms = 2000

#\* Processes sorting, "pid" "program" "arguments" "threads" "user" "memory" "cpu lazy" "cpu direct",
#\* "cpu lazy" sorts top process over time (easier to follow), "cpu direct" updates top process directly.
proc\_sorting = "cpu lazy"

#\* Reverse sorting order, True or False.
proc\_reversed = false

#\* Show processes as a tree.
proc\_tree = false

#\* Use the cpu graph colors in the process list.
proc\_colors = true

#\* Use a darkening gradient in the process list.
proc\_gradient = true

#\* If process cpu usage should be of the core it's running on or usage of the total available cpu power.
proc\_per\_core = false

#\* Show process memory as bytes instead of percent.
proc\_mem\_bytes = true

#\* Show cpu graph for each process.
proc\_cpu\_graphs = true

#\* Use /proc/\[pid\]/smaps for memory information in the process info box (very slow but more accurate)
proc\_info\_smaps = false

#\* Show proc box on left side of screen instead of right.
proc\_left = false

#\* (Linux) Filter processes tied to the Linux kernel(similar behavior to htop).
proc\_filter\_kernel = false

#\* Should the process list follow the selected process when detailed view is open.
proc\_follow\_detailed = true

#\* In tree-view, always accumulate child process resources in the parent process.
proc\_aggregate = false

#\* Should cpu and memory usage display be preserved for dead processes when paused.
keep\_dead\_proc\_usage = false

#\* Sets the CPU stat shown in upper half of the CPU graph, "total" is always available.
#\* Select from a list of detected attributes from the options menu.
cpu\_graph\_upper = "Auto"

#\* Sets the CPU stat shown in lower half of the CPU graph, "total" is always available.
#\* Select from a list of detected attributes from the options menu.
cpu\_graph\_lower = "Auto"

#\* Toggles if the lower CPU graph should be inverted.
cpu\_invert\_lower = true

#\* Set to True to completely disable the lower CPU graph.
cpu\_single\_graph = false

#\* Show cpu box at bottom of screen instead of top.
cpu\_bottom = false

#\* Shows the system uptime in the CPU box.
show\_uptime = true

#\* Shows the CPU package current power consumption in watts. Requires running \`make setcap\` or \`make setuid\` or running with sudo.
show\_cpu\_watts = true

#\* Show cpu temperature.
check\_temp = true

#\* Which sensor to use for cpu temperature, use options menu to select from list of available sensors.
cpu\_sensor = "Auto"

#\* Show temperatures for cpu cores also if check\_temp is True and sensors has been found.
show\_coretemp = true

#\* Set a custom mapping between core and coretemp, can be needed on certain cpus to get correct temperature for correct core.
#\* Use lm-sensors or similar to see which cores are reporting temperatures on your machine.
#\* Format "x:y" x=core with wrong temp, y=core with correct temp, use space as separator between multiple entries.
#\* Example: "4:0 5:1 6:3"
cpu\_core\_map = ""

#\* Which temperature scale to use, available values: "celsius", "fahrenheit", "kelvin" and "rankine".
temp\_scale = "celsius"

#\* Use base 10 for bits/bytes sizes, KB = 1000 instead of KiB = 1024.
base\_10\_sizes = false

#\* Show CPU frequency.
show\_cpu\_freq = true

#\* How to calculate CPU frequency, available values: "first", "range", "lowest", "highest" and "average".
freq\_mode = "first"

#\* Draw a clock at top of screen, formatting according to strftime, empty string to disable.
#\* Special formatting: /host = hostname | /user = username | /uptime = system uptime
clock\_format = "%X"

#\* Update main ui in background when menus are showing, set this to false if the menus is flickering too much for comfort.
background\_update = true

#\* Custom cpu model name, empty string to disable.
custom\_cpu\_name = ""

#\* Optional filter for shown disks, should be full path of a mountpoint, separate multiple values with whitespace " ".
#\* Only disks matching the filter will be shown. Prepend exclude= to only show disks not matching the filter. Examples: disk\_filter="/boot /home/user", disks\_filter="exclude=/boot /home/user"
disks\_filter = ""

#\* Show graphs instead of meters for memory values.
mem\_graphs = true

#\* Show mem box below net box instead of above.
mem\_below\_net = false

#\* Count ZFS ARC in cached and available memory.
zfs\_arc\_cached = true

#\* If swap memory should be shown in memory box.
show\_swap = true

#\* Show swap as a disk, ignores show\_swap value above, inserts itself after first disk.
swap\_disk = true

#\* If mem box should be split to also show disks info.
show\_disks = true

#\* Filter out non physical disks. Set this to False to include network disks, RAM disks and similar.
only\_physical = true

#\* Read disks list from /etc/fstab. This also disables only\_physical.
use\_fstab = true

#\* Setting this to True will hide all datasets, and only show ZFS pools. (IO stats will be calculated per-pool)
zfs\_hide\_datasets = false

#\* Set to true to show available disk space for privileged users.
disk\_free\_priv = false

#\* Toggles if io activity % (disk busy time) should be shown in regular disk usage view.
show\_io\_stat = true

#\* Toggles io mode for disks, showing big graphs for disk read/write speeds.
io\_mode = false

#\* Set to True to show combined read/write io graphs in io mode.
io\_graph\_combined = false

#\* Set the top speed for the io graphs in MiB/s (100 by default), use format "mountpoint:speed" separate disks with whitespace " ".
#\* Example: "/mnt/media:100 /:20 /boot:1".
io\_graph\_speeds = ""

#\* Set fixed values for network graphs in Mebibits. Is only used if net\_auto is also set to False.
net\_download = 100

net\_upload = 100

#\* Use network graphs auto rescaling mode, ignores any values set above and rescales down to 10 Kibibytes at the lowest.
net\_auto = true

#\* Sync the auto scaling for download and upload to whichever currently has the highest scale.
net\_sync = true

#\* Starts with the Network Interface specified here.
net\_iface = ""

#\* "True" shows bitrates in base 10 (Kbps, Mbps). "False" shows bitrates in binary sizes (Kibps, Mibps, etc.). "Auto" uses base\_10\_sizes.
base\_10\_bitrate = "Auto"

#\* Show battery stats in top right if battery is present.
show\_battery = true

#\* Which battery to use if multiple are present. "Auto" for auto detection.
selected\_battery = "Auto"

#\* Show power stats of battery next to charge indicator.
show\_battery\_watts = true

#\* Set loglevel for "~/.local/state/btop.log" levels are: "ERROR" "WARNING" "INFO" "DEBUG".
#\* The level set includes all lower levels, i.e. "DEBUG" will show all logging info.
log\_level = "WARNING"

#### Command line options

```
Usage: btop [OPTIONS]

Options:
  -c, --config <file>     Path to a config file
  -d, --debug             Start in debug mode with additional logs and metrics
  -f, --filter <filter>   Set an initial process filter
      --force-utf         Override automatic UTF locale detection
  -l, --low-color         Disable true color, 256 colors only
  -p, --preset <id>       Start with a preset (0-9)
  -t, --tty               Force tty mode with ANSI graph symbols and 16 colors only
      --no-tty            Force disable tty mode
  -u, --update <ms>       Set an initial update rate in milliseconds
      --default-config    Print default config to standard output
  -h, --help              Show this help message and exit
  -V, --version           Show a version message and exit (more with --version)
```

LICENSE
-------

Apache License 2.0
