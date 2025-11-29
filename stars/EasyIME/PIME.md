---
project: PIME
stars: 1427
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

Development
===========

Tool Requirements
-----------------

-   CMake >= 3.0
-   Visual Studio 2019
-   git

How to Build
------------

-   Get source from github.
    
    ```
    git clone https://github.com/EasyIME/PIME.git
    cd PIME
    git submodule update --init
    ```
    
-   Use the following CMake commands to generate Visual Studio project.
    
    ```
    cmake -G "Visual Studio 16 2019" -A Win32 <path to PIME source folder>
    cmake -G "Visual Studio 16 2019" -A x64 <path to PIME source folder>
    ```
    
-   Open generated project with Visual Studio and build it.
    

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
