---
project: OpenSpeedy
stars: 17233
description: 🎮 An open-source game speed modifier.
url: https://github.com/game1024/OpenSpeedy
---

OpenSpeedy
==========

The Best Open-Source Game Speed Controller

  
  
  
  

🌐 English | Deutsch | Français | 日本語 | 한국어 | Português (BR)  
| Русский | Español | Nederlands | हिन्दी | 繁體中文 | 简体中文

🚀 Features
===========

-   Quick speed adjustment
-   Modern UI
-   Supports both x86 and x64 platform processes
-   No kernel intrusion — Ring-3 level hooking, does not tamper with the system kernel

💾 Installation
===============

📦 **Method 1: Winget**

# Install command
winget install openspeedy

# Open a new terminal and run openspeedy
openspeedy

📥 **Method 2: Manual Download**

Visit the Releases page to download the latest version.

💻 System Requirements
======================

-   OS: Windows 10 or later
-   Platform: x86 (32-bit) and x64 (64-bit)

📝 Usage
========

1.  Launch OpenSpeedy
2.  Run the target game you want to speed up

1.  Select the game process and adjust the speed multiplier in the OpenSpeedy interface

1.  Takes effect immediately — see the comparison below

2026-06-20.20-40-21.mp4

🔧 How It Works
===============

Prerequisites:

-   Node.js 18+
-   Rust
-   CMake
-   Visual Studio (with C++ desktop development workload)

Build command:

npm run tauri dev

OpenSpeedy adjusts game speed by hooking the following Windows system time functions:

Function

Library

Purpose

Sleep

user32.dll

Thread sleep

SetTimer

user32.dll

Creates message-based timers

timeGetTime

winmm.dll

Retrieves system uptime in milliseconds

GetTickCount

kernel32.dll

Retrieves system uptime in milliseconds

GetTickCount64

kernel32.dll

Retrieves system uptime in milliseconds (64-bit)

QueryPerformanceCounter

kernel32.dll

High-resolution performance counter

GetSystemTimeAsFileTime

kernel32.dll

Retrieves system time

GetSystemTimePreciseAsFileTime

kernel32.dll

Retrieves high-precision system time

SetWaitableTimer

kernel32.dll

Sets a waitable timer

SetWaitableTimerEx

kernel32.dll

Sets a waitable timer (extended)

⚠️ Warnings
===========

-   This tool is for educational and research purposes only
-   Some online games have anti-cheat systems — using this tool may result in account bans
-   Excessive speed may cause game physics engine glitches or crashes
-   Not recommended for use in competitive online games
-   Open-source software without digital signatures may trigger false positives from antivirus software

🔄 Feedback
===========

If you encounter any issues, please reach out via:

-   FAQ — Check the wiki first for common issues
-   GitHub Issues — Submit bug reports. Please do not submit cloud storage related issues, thank you for your cooperation~ 🙏

License
=======

OpenSpeedy is licensed under the GPL v3 license.

🙏 Acknowledgments
==================

OpenSpeedy uses source code from the following projects. Thanks to the open-source community! If OpenSpeedy helps you, a Star is welcome!

-   minhook: For API hooking
-   tauri: GUI framework
-   MUI: UI component library
-   Ant Design: UI splitter component

Disclaimer: OpenSpeedy is intended for educational and research purposes only. Users assume all risks and liabilities associated with the use of this software. The author is not responsible for any loss or legal liability arising from the use of this software.
