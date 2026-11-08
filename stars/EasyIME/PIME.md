---
project: PIME
stars: 1531
description: Develop input methods for Windows easily with Python and node.js
url: https://github.com/EasyIME/PIME
---

PIME
====

Implement input methods easily for Windows via Text Services Framework:

-   LibIME contains a library which aims to be a simple wrapper for Windows Text Service Framework (TSF).
-   PIMETextService contains an backbone implementation of Windows text service for using libIME.
-   The Python and Node.js backends run on the embedded runtimes in `python/python3/` and `node/`, so input methods are plain Python or JavaScript modules.

All parts are licensed under GNU LGPL v2.1 license.

Contributing
============

Contributions using AI coding tools are welcomed! However, to ensure code quality, they must follow the rules in AGENTS.md to be accepted, and AI assistance must be clearly declared in pull requests, git commits, and file headers.

Development
===========

Tool Requirements
-----------------

-   CMake >= 4.2 (the `Visual Studio 18 2026` generator was added in 4.2)
-   Visual Studio 2026 with the "Desktop development with C++" workload
-   Rust Toolchain (Stable channel with `i686-pc-windows-msvc` target)
-   git
-   Node.js with npm (builds the bundled JavaScript input methods)
-   NSIS 3.x (only needed to build the installer)

How to Build
------------

-   Get source from GitHub.
    
    ```
    git clone --recursive https://github.com/EasyIME/PIME.git
    cd PIME
    ```
    
    If you cloned without `--recursive`, run `git submodule update --init --recursive`.
    
-   Ensure the 32-bit Rust target is installed (the launcher is 32-bit):
    
    ```
    rustup target add i686-pc-windows-msvc
    ```
    
-   Use `build.bat` to build everything. It builds the launcher, the x86, x64 and ARM64 text service DLLs, and bundles the JavaScript input methods.
    
-   To build by hand, use the same generator and policy flag as `build.bat`:
    
    ```
    cmake . -Bbuild -G "Visual Studio 18 2026" -A Win32 -DCMAKE_POLICY_VERSION_MINIMUM=3.5
    cmake --build build --config Release
    
    # For 64-bit Text Service (Required for 64-bit apps)
    cmake . -Bbuild64 -G "Visual Studio 18 2026" -A x64 -DCMAKE_POLICY_VERSION_MINIMUM=3.5
    cmake --build build64 --config Release --target PIMETextService
    
    # For ARM64 Text Service (Required for native ARM64 apps)
    cmake . -Bbuild_arm64 -G "Visual Studio 18 2026" -A ARM64 -DCMAKE_POLICY_VERSION_MINIMUM=3.5
    cmake --build build_arm64 --config Release --target PIMETextService
    ```
    
-   `build.bat` also generates the JavaScript input methods that the installer packages. After it has run, build the installer:
    
    ```
    makensis installer\installer.nsi
    ```
    
    The generated installer is `installer\PIME-<version>-setup.exe`. The manual CMake commands above build only the C++ binaries, so they are not enough on their own.
    

TSF References
--------------

-   Text Services Framework
-   Guidelines and checklist for IME development (Windows Store apps)
-   Input Method Editors (Windows Store apps)
-   Third-party input method editors
-   Strategies for App Communication between Windows 8 UI and Windows 8 Desktop
-   TSF Aware, Dictation, Windows Speech Recognition, and Text Services Framework. (blog)
-   Win32 and COM for Windows Store apps
-   Input Method Editor (IME) sample supporting Windows 8

Windows ACL (Access Control List) references
--------------------------------------------

-   The Windows Access Control Model Part 1
-   The Windows Access Control Model: Part 2
-   Windows 8 App Container Security Notes - Part 1
-   How AccessCheck Works
-   GetAppContainerNamedObjectPath function (enable accessing object outside app containers using ACL)
-   Creating a DACL

Install
=======

-   Download `PIME-<version>-setup.exe` from Releases, or build it as described above.
-   Run the installer; it requests administrator rights. It installs under `C:\Program Files (x86)\PIME` (or `C:\Program Files\PIME` on 32-bit Windows) and registers the text service for the installed architectures (x86, and x64 or ARM64 on 64-bit Windows).
-   Do not copy `PIMETextService.dll` by hand or register it with `regsvr32`; a partially registered copy will not work.

Uninstall
=========

-   Open Settings > Apps > Installed apps, select PIME and choose Uninstall, or run `Uninstall.exe` from the install folder.
-   The uninstaller unregisters the text service and removes the installed files. Files still in use are removed after a reboot.
-   Do not unregister the DLLs with `regsvr32`.

Bug Report
==========

Please report any issue to here.

Debugging
=========

If you encounter issues, you can run `PIMELauncher.exe` with the following debugging options:

-   **Live console output**:
    
    PIMELauncher.exe /console
    
    Opens a console window displaying live `DEBUG` level logs for troubleshooting backend communication and internal events.
    
-   **Log to file (headless)**:
    
    PIMELauncher.exe /log\-file C:\\path\\to\\pime.log
    
    Writes `DEBUG` level logs to the specified file while running silently in the background without popping up a console window.
    
-   **Quit running instance**:
    
    PIMELauncher.exe /quit
    
-   **Show help message**:
    
    PIMELauncher.exe /help
    # or: PIMELauncher.exe /?
    

When run normally without `/console` or `/log-file`, all debug logging is completely suppressed to avoid unnecessary I/O overhead.
