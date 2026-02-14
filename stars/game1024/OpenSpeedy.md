---
project: OpenSpeedy
stars: 15112
description: 🎮 An open-source game speed modifier.[一款开源的游戏变速器]
url: https://github.com/game1024/OpenSpeedy
---

OpenSpeedy
==========

OpenSpeedy is an open-source and free game speed tool that helps you break frame rate limitations and provides a smoother, silkier gaming acceleration experience.

Offcial Website  
  
  
  
  
  

简体中文 · 日本語 · English

🚀 Features
===========

-   Completely free and open-source
-   Easy-to-use interface
-   Customizable speed multiplier
-   Good compatibility with various game engines
-   Low system resource consumption
-   Supports accelerating both x86 and x64 processes
-   Non-invasive to the kernel: Ring3 level Hook, does not compromise the system kernel

💾 Installation
===============

📦 **Method1: Winget**

# install 
winget install openspeedy

# open a new terminal, you can run openspeedy by following command
speedy

📥 **Method2: Manual Download**

Visit the Installation Page to download the latest version

💻 System Requirements
======================

-   OS: Windows 10 or later
-   Platform: x86 (32-bit) and x64 (64-bit)

📝 Usage Instructions
=====================

1.  Start OpenSpeedy
2.  Launch the target game you want to speed up

1.  Select the game process, and adjust the speed multiplier in the OpenSpeedy interface

1.  The effect takes effect immediately. Compare the results below

default.mp4

🔧 Technical Principle
======================

OpenSpeedy achieves game speed adjustment by hooking the following Windows system time functions:

Function Name

Library

Description

Sleep

user32.dll

Thread sleep

SetTimer

user32.dll

Create message-based timer

timeGetTime

winmm.dll

Get milliseconds elapsed since system startup

GetTickCount

kernel32.dll

Get milliseconds elapsed since system startup

GetTickCount64

kernel32.dll

Get milliseconds elapsed since system startup (64-bit)

QueryPerformanceCounter

kernel32.dll

High precision performance counter

GetSystemTimeAsFileTime

kernel32.dll

Get system time

GetSystemTimePreciseAsFileTime

kernel32.dll

Get high precision system time

⚠️ Notes
========

-   This tool is for learning and research purposes only
-   Some online games may have anti-cheat systems. Using this tool may result in your account being banned
-   Excessive speeding up may cause the game physics engine to malfunction or crash
-   Not recommended for use in competitive online games
-   Open source product does not include digital signature and may be falsely flagged by antivirus software

🔄 Feedback
===========

If you encounter any issues during use, feel free to provide feedback via:

-   FAQ - You can first check the wiki to locate the issue.
-   GitHub Issues - Submit issue reports

🎁 Buy me a coffee
==================

If you find the OpenSpeedy project helpful, you can buy me a coffee~ ☕️

Name

Description

365VPN

uses dedicated lines to connect worldwide, offering speeds of up to 10Gbps. Download now to start surfing for free🏄: https://ref.365tz87989.com/?r=RWQVZD

Patreon

https://patreon.com/game1024

Sponsors
========

This program uses free code signing provided by SignPath.io and a certificate by the SignPath Foundation

📜 License
==========

OpenSpeedy is licensed under the GNU v3 License.

🙏 Acknowledgements
===================

OpenSpeedy uses source code from the following projects. Thanks to the open-source community! If OpenSpeedy helps you, please give us a Star!

-   minhook: For API Hooking
-   Qt: GUI

Disclaimer: OpenSpeedy is intended for educational and research purposes only. Users assume all risks and responsibilities for using this software. The author is not responsible for any loss or legal liability resulting from the use of this software.
