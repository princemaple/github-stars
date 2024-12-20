---
project: PowerToys
stars: 112222
description: Windows system utilities to maximize productivity
url: https://github.com/microsoft/PowerToys
---

Microsoft PowerToys
===================

How to use PowerToys | Downloads & Release notes | Contributing to PowerToys | What's Happening | Roadmap

About
-----

Microsoft PowerToys is a set of utilities for power users to tune and streamline their Windows experience for greater productivity. For more info on PowerToys overviews and how to use the utilities, or any other tools and resources for Windows development environments, head over to learn.microsoft.com!

Current utilities:

Advanced Paste

Always on Top

PowerToys Awake

Command Not Found

Color Picker

Crop And Lock

Environment Variables

FancyZones

File Explorer Add-ons

File Locksmith

Hosts File Editor

Image Resizer

Keyboard Manager

Mouse utilities

Mouse Without Borders

New+

Peek

Paste as Plain Text

PowerRename

PowerToys Run

Quick Accent

Registry Preview

Screen Ruler

Shortcut Guide

Text Extractor

Video Conference Mute

Workspaces

🎁⭐ PowerToys Advent calendar ⭐🎁
---------------------------------

We will be highlighting a cool utility each day for 24 days in December! To follow along, check out these threads:

-   https://bsky.app/profile/kaylacinnamon.bsky.social/post/3lcb7iljxck2o
-   https://x.com/cinnamon\_msft/status/1863284610773246257

Installing and running Microsoft PowerToys
------------------------------------------

### Requirements

-   Windows 11 or Windows 10 version 2004 (code name 20H1 / build number 19041) or newer.
-   x64 or ARM64 processor
-   Our installer will install the following items:
    -   Microsoft Edge WebView2 Runtime bootstrapper. This will install the latest version.

### Via GitHub with EXE \[Recommended\]

Go to the Microsoft PowerToys GitHub releases page and click on `Assets` at the bottom to show the files available in the release. Please use the appropriate PowerToys installer that matches your machine's architecture and install scope. For most, it is `x64` and per-user.

Description

Filename

sha256 hash

Per user - x64

PowerToysUserSetup-0.86.0-x64.exe

CFB9608B28B8FF12C9A7C9814A6EF981636EB5AB261DC278C28EC93FD959CCE2

Per user - ARM64

PowerToysUserSetup-0.86.0-arm64.exe

861CEDBFDCDA993D1D1056E3280319D5EA45D142CA3C737AB1FB4FABD651A5F5

Machine wide - x64

PowerToysSetup-0.86.0-x64.exe

857DE9DC5938D9602F82DFD6183DB5E6823B875A412AEC59B4BE93617E27E9CD

Machine wide - ARM64

PowerToysSetup-0.86.0-arm64.exe

6F37192534C195A02A80AAE1E449DF61C894C50763096A06195581801943FA31

This is our preferred method.

### Via Microsoft Store

Install from the Microsoft Store's PowerToys page. You must be using the new Microsoft Store which is available for both Windows 11 and Windows 10.

### Via WinGet

Download PowerToys from WinGet. Updating PowerToys via winget will respect current PowerToys installation scope. To install PowerToys, run the following command from the command line / PowerShell:

#### User scope installer \[default\]

winget install Microsoft.PowerToys \-s winget

#### Machine-wide scope installer

winget install \--scope machine Microsoft.PowerToys \-s winget

### Other install methods

There are community driven install methods such as Chocolatey and Scoop. If these are your preferred install solutions, you can find the install instructions there.

Third-Party Run Plugins
-----------------------

There is a collection of third-party plugins created by the community that aren't distributed with PowerToys.

Contributing
------------

This project welcomes contributions of all types. Besides coding features / bug fixes, other ways to assist include spec writing, design, documentation, and finding bugs. We are excited to work with the power user community to build a set of tools for helping you get the most out of Windows.

We ask that **before you start work on a feature that you would like to contribute**, please read our Contributor's Guide. We would be happy to work with you to figure out the best approach, provide guidance and mentorship throughout feature development, and help avoid any wasted or duplicate effort.

Most contributions require you to agree to a Contributor License Agreement (CLA) declaring that you grant us the rights to use your contribution and that you have permission to do so.

For guidance on developing for PowerToys, please read the developer docs for a detailed breakdown. This includes how to setup your computer to compile.

What's Happening
----------------

### PowerToys Roadmap

Our prioritized roadmap of features and utilities that the core team is focusing on.

### 0.86 - October 2024 Update

In this release, we focused on new features, stability, and improvements.

**Highlights**

-   Advanced Paste has new abilities: Image to text, and paste to file (text / png / html).
-   In settings, we've adjusted the left navigation to group the utilities. As the number of utilities shipped with PowerToys keeps growing, we felt this was a needed adjustment. Thanks everyone for your feedback!
-   Workspaces received many bug fixes, including the proper launching of many instances of the same application in the same workspace. Note, we are still actively looking at how to properly handle PWA detection.
-   We've added a diagnostic data (telemetry) opt-in option in the Settings General tab. As it is off-by-default, we encourage users to turn it on as that helps direct our development efforts and their journeys. More information about the data we collect can be found in the PowerToys Data and Privacy documentation and what each event does.

### General

-   Added a setting for diagnostic data (telemetry) opt-in (off by default, however, see above for why we encourage you to opt-in!) and user controls to view data.
-   Improved exception logging by adding the type of Exception and InnerException. Thanks @davidegiacometti!

### Advanced Paste

-   Added new built-in actions: Image to text, and paste txt, png or html as a file.

### Mouse Jump

-   Refactored the common classes into a separate project. Thanks @mikeclayton!
-   Brought back the telemetry events that were deleted across previous refactoring efforts.

### Mouse Without Borders

-   Refactored the Logger common classes. Thanks @mikeclayton!

### New+

-   Fixed the telemetry event for when the modules is enabled or disabled. (This was a hotfix for 0.85)
-   Fixed bug when creating folders or files that contain Unicode characters. Thanks @cgaarden!
-   Fixed bug when the name of a new folder collided with an already existing folder. Thanks @cgaarden!
-   Updated the New+ icons to the fluent style.

### Peek

-   Folder preview enumeration of size and number of files is now more responsive and faster. Thanks @daverayment!

### PowerToys Run

-   Handled a culture not found error when checking for right-to-left languages.
-   Fixed the WebSearch plugin results title being trimmed in the UI. Thanks @octastylos-pseudodipteros!
-   The Unit Converter plugin will now show more significant digits. Thanks @PesBandi!
-   Improved error handling when copying to the clipboard results in an error. Thanks @PesBandi!

### Quick Accent

-   Added support for the Serbian Cyrillic character set. Thanks @Sirozha1337!

### Registry Preview

-   Adopted the Monaco Editor as the UI text editor. Thanks @davidegiacometti!

### Settings

-   Fixed a crash when trying to access a non-existing templates folder from the New+ page. (This was a hotfix for 0.85)
-   Added a navigation tree to group utilities in the left navigation menu.
-   Sorted the list of languages in the language selection combo box in the General tab. Thanks @davidegiacometti!
-   Fixed the state of the info bar about templates not being backed up to not close and react to the module's enabled state in the New+ page. Thanks @htcfreek!
-   Fixed a crash caused by a dangling thread.
-   Clicking a notification about there being an update available should now correctly open the Settings application in the General tab.
-   Fixed a UI freeze when trying to access the Diagnostic Data Viewer files. Thanks @davidegiacometti!

### Workspaces

-   Fixed launching the incorrect workspace when launching many workspaces quickly through shortcuts. (This was a hotfix for 0.85)
-   Fixed launching many instances of the same application in a workspace.
-   Fixed a crash when a previously captured monitor ID no longer existed.
-   Fixed an issue causing the wrong coordinates to be saved for minimized applications.
-   Fixed an issue causing a crash when stress testing workspace launching.
-   Fixed application launching when UAC is off and every application always runs elevated.

### Documentation

-   Added HackMD plugin mention to thirdPartyRunPlugins.md. Thanks @8LWXpg!
-   Added SSH plugin mention to thirdPartyRunPlugins.md. Thanks @8LWXpg!
-   Added the Data and Privacy documentation to the repo.

### Development

-   Fixed the CI precheck action to take into account the recent changes in CI actions.
-   Added the new Microsoft org issue types to the issue templates. Thanks @Aaron-Junker!
-   Updated System.Text.Json to 8.0.5 and System.Runtime.Caching to 8.0.1 and related dependencies to the latest to address security reports. Thanks @snickler!
-   Updated WinAppSDK to 1.6.1 and CsWinRT to 2.1.5. Thanks @snickler!
-   Upgraded the WpfUI dependency to 3.0.5.
-   Updated MessagePack to 2.5.187 and StreamJsonRpc to 2.19.27 to address security reports.
-   Removed some of the hacks that are no longer needed that tried to force same dependency versions in .csproj files.
-   Removed the Markdown file exclusions from the conditions that trigger a full CI test.
-   CI fails again when there are XAML style errors in a PR.
-   Fixed CI actions that were not failing when one of the powershell scripts they tried to run was failing.
-   Fixed analyzer violations to allow fully building PowerToys on Visual Studio 17.12. Thanks @snickler!

#### What is being planned for version 0.87

For v0.87, we'll work on the items below:

-   Stability / bug fixes
-   New module: File Actions Menu
-   Integrate Sysinternals ZoomIt

PowerToys Community
-------------------

The PowerToys team is extremely grateful to have the support of an amazing active community. The work you do is incredibly important. PowerToys wouldn’t be nearly what it is today without your help filing bugs, updating documentation, guiding the design, or writing features. We want to say thank you and take time to recognize your work. Month by month, you directly help make PowerToys a better piece of software.

Code of Conduct
---------------

This project has adopted the Microsoft Open Source Code of Conduct.

Privacy Statement
-----------------

The application logs basic diagnostic data (telemetry). For more information on privacy and what we collect, see our PowerToys Data and Privacy documentation.
