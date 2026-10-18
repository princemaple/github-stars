---
project: PIME
stars: 1523
description: Develop input methods for Windows easily with Python and node.js
url: https://github.com/EasyIME/PIME
---

PIME
====

Implement input methods easily for Windows via Text Services Framework:

-   LibIME contains a library which aims to be a simple wrapper for Windows Text Service Framework (TSF).
-   PIMETextService contains an backbone implementation of Windows text service for using libIME.
-   The python server part requires python 3.x and pywin32 package.

All parts are licensed under GNU LGPL v2.1 license.

Contributing
============

Contributions using AI coding tools are welcomed! However, to ensure code quality, they must follow the rules in AGENTS.md to be accepted, and AI assistance must be clearly declared in pull requests, git commits, and file headers.

Development
===========

Tool Requirements
-----------------

-   CMake >= 3.0
-   Visual Studio 2019
-   Rust Toolchain (Stable channel with `i686-pc-windows-msvc` target)
-   git
-   Node.js (Required for some backends like McBopomofo)

How to Build
------------

-   Get source from github.
    
    ```
    git clone https://github.com/EasyIME/PIME.git
    cd PIME
    git submodule update --init
    ```
    
-   Ensure the 32-bit Rust target is installed:
    
    ```
    rustup target add i686-pc-windows-msvc
    ```
    
-   Use `build.bat` to build everything, or use the following CMake commands to generate Visual Studio project.
    
    ```
    cmake . -Bbuild -G "Visual Studio 16 2019" -A Win32
    cmake --build build --config Release
    
    # For 64-bit Text Service (Required for 64-bit apps)
    cmake . -Bbuild64 -G "Visual Studio 16 2019" -A x64
    cmake --build build64 --config Release --target PIMETextService
    ```
    
-   The generated installer will be in the `installer` folder after running `makensis`.
    

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

-   Copy `PIMETextService.dll` to C:\\Program Files (X86)\\PIME\\x86.
    
-   Copy `PIMETextService.dll` to C:\\Program Files (X86)\\PIME\\x64.
    
-   Copy the folder `python` to `C:\Program Files (X86)\PIME\`
    
-   Copy the folder `node` to `C:\Program Files (X86)\PIME\`
    
-   Use `regsvr32` to register `PIMETextService.dll`. 64-bit system need to register both 32-bit and 64-bit `PIMETextService.dll`
    
    ```
    regsvr32 "C:\Program Files (X86)\PIME\x86\PIMETextService.dll" (run as administrator)
    regsvr32 "C:\Program Files (X86)\PIME\x64\PIMETextService.dll" (run as administrator)
    ```
    
-   NOTICE: the `regsvr32` command needs to be run as Administrator. Otherwise you'll get access denied error.
    
-   In Windows 8, if you put the dlls in places other than C:\\Windows or C:\\Program Files, they will not be accessible in metro apps.
    

Uninstall
=========

-   Use `regsvr32` to unregister `PIMETextService.dll`. 64-bit system need to unregister both 32-bit and 64-bit `PIMETextService.dll`
    
    ```
    regsvr32 /u "C:\Program Files (X86)\PIME\x86\PIMETextService.dll" (run as administrator)
    regsvr32 /u "C:\Program Files (X86)\PIME\x64\PIMETextService.dll" (run as administrator)
    ```
    
-   Remove `C:\Program Files (X86)\PIME`
    
-   NOTICE: the `regsvr32` command needs to be run as Administrator. Otherwise you'll get access denied error.
    

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
