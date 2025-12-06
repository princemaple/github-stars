---
project: PowerToys
stars: 126272
description: Microsoft PowerToys is a collection of utilities that help you customize Windows and streamline everyday tasks
url: https://github.com/microsoft/PowerToys
---

Microsoft PowerToys
===================

Microsoft PowerToys is a collection of utilities that help you customize Windows and streamline everyday tasks.

### Installation · Documentation · Blog · Release notes

  
  

🔨 Utilities
------------

PowerToys includes over 25 utilities to help you customize and optimize your Windows experience:

Advanced Paste

Always on Top

Awake

Color Picker

Command Not Found

Command Palette

Crop And Lock

Environment Variables

FancyZones

File Explorer Add-ons

File Locksmith

Hosts File Editor

Image Resizer

Keyboard Manager

Light Switch

Mouse Utilities

Mouse Without Borders

New+

Peek

PowerRename

PowerToys Run

Quick Accent

Registry Preview

Screen Ruler

Shortcut Guide

Text Extractor

Workspaces

ZoomIt

📋 Installation
---------------

For detailed installation instructions and system requirements, visit the installation docs.

But to get started quickly, choose one of the installation methods below:  
  

**Download .exe from GitHub**  
Go to the \[PowerToys GitHub releases\]\[github-release-link\], click Assets to reveal the downloads, and choose the installer that matches your architecture and install scope. For most devices, that's the x64 per-user installer.

Description

Filename

Per user - x64

PowerToysUserSetup-0.96.1-x64.exe

Per user - ARM64

PowerToysUserSetup-0.96.1-arm64.exe

Machine wide - x64

PowerToysSetup-0.96.1-x64.exe

Machine wide - ARM64

PowerToysSetup-0.96.1-arm64.exe

**Microsoft Store**  
You can easily install PowerToys from the Microsoft Store:

**WinGet**  
Download PowerToys from \[WinGet\]\[winget-link\]. Updating PowerToys via winget will respect the current PowerToys installation scope. To install PowerToys, run the following command from the command line / PowerShell:

_User scope installer \[default\]_

winget install Microsoft.PowerToys \-s winget

_Machine-wide scope installer_

winget install \--scope machine Microsoft.PowerToys \-s winget

**Other methods**  
There are \[community driven install methods\](./doc/unofficialInstallMethods.md) such as Chocolatey and Scoop. If these are your preferred install solutions, you can find the install instructions there.

✨ What's new
------------

**Version 0.96 (November 2025)**

For an in-depth look at the latest changes, visit the Windows Command Line blog.

**✨ Highlights**

-   Advanced Paste now supports multiple online and on-device AI model providers: Azure OpenAI, OpenAI, Google Gemini, Mistral, Foundry Local and Ollama.
-   Command Palette received extensive improvements including file search filters, better clipboard history metadata, context-menu styling, and dozens of bug fixes and enhancements.
-   PowerRename can now extract and use photo metadata (EXIF, XMP) in renaming patterns like `%Camera`, `%Lens`, and `%ExposureTime`.

### Advanced Paste

-   Advanced Paste now lets you connect to multiple AI providers instead of being limited to a single OpenAI provider. See Advanced Paste documentation for usage.

### Awake

-   The Awake countdown timer now stays accurate over long periods. Thanks @daverayment!
-   Fixed Awake context menu positioning. The fix removed the conversion of the mouse cursor from screen to client-window coordinates, instead using the raw screen coordinates returned by GetCursorPos; the context menu now appears at the correct screen position. Thanks @lzandman!

### Command Palette

-   The search field in context menus now matches the look of the Command Palette, with a smoke backdrop and improved padding.
-   Fallback items such as math calculations or the Run command now appear in results more quickly. Thanks @jiripolasek!
-   Ensured the command bar updates correctly after navigating to another page and commands are displayed correctly. Thanks @jiripolasek!
-   The Command Palette settings page has been reorganized. Activation-key options are grouped under an expander and extension settings are framed for improved readability.
-   When you modify a command, its alias, hotkey, and tags now update in the top-level list, keeping the displayed information in sync. Thanks @jiripolasek!
-   Press `Ctrl + ,` to open Command Palette settings from anywhere. Thanks @jiripolasek!
-   You can use `Page Up` and `Page Down` to navigate the list while focus is in the search box. Thanks @samrueby!
-   Fixed an issue where the search box could disappear when navigating pages. Thanks @jiripolasek!
-   Ensured search text is selected when _Go home when activated_ and _Highlight search on activate_ are both enabled. Thanks @jiripolasek!
-   Fixed an issue where Command Palette window occasionally appeared on the taskbar under certain Windows settings. Thanks @jiripolasek!
-   Ensured that labels and icons of list items and menu items update when they change. Thanks @jiripolasek!
-   Fixed visibility of list filters when navigating to a content page. Thanks @DevLGuilherme!
-   Added search to the extension list and a link to extensions on the Microsoft Store. Thanks @jiripolasek!
-   Added options to open the Command Palette window at its last position or re-center it.
-   The Command Palette now remembers its window size after restarting.
-   Added a global error handler that logs fatal errors and provides feedback when unexpected failures force Command Palette to close. Thanks @jiripolasek!
-   Fixed forms and extension settings not showing on some machines due to a missing VC++ runtime.
-   Restored ranking of fallback commands for built-in extensions (Sleep, Shutdown, Windows settings, Web search, etc.). Thanks @jiripolasek.
-   Improved and unified labels and texts across the application!
-   Maintainance: Resolved numerous build warnings in Command Palette projects; no user-visible impact. Thanks @jiripolasek!
-   Maintainance: Fixed a logging issue so exception messages are properly recorded instead of placeholder text, improving troubleshooting. Thanks @jiripolasek!

### Command Palette Extensions

-   Bookmarks: Added hints about bookmark placeholders to the Add/Edit Bookmark form. — Thanks @jiripolasek!
-   Bookmarks: Improved migration of bookmarks from older versions and fixed an issue where aliases or keyboard shortcuts could be lost after restart. Thanks @jiripolasek!
-   Clipboard history: Items shown in Command Palette’s clipboard history now include helpful metadata. For example, image items show dimensions, text files show names and sizes, web links include page titles, and text entries display word counts. Thanks @jiripolasek!
-   File search: Added filter buttons to show _all items_, _files only_, or _folders only_. Selecting a filter adds `kind:folders` or `kind:not folders` to narrow results.
-   System commands: Replaced the `:red_circle:` placeholder with an actual red-circle emoji so the correct icon appears in the UI. Thanks @samrueby!
-   WinGet: Search performance feels more responsive because typed input is now processed via a task queue rather than complex cancellation tokens!
-   Window Walker: UWP apps no longer show a "not responding" label when suspended. Thanks @jiripolasek!
-   Window Walker: Now displays the actual icon of each window rather than using the process icon, improving recognition of PWAs and Python GUIs. Thanks @Lee-WonJun!
-   Windows Terminal profiles: Fixed a rare crash in the Windows Terminal extension when the `LOCALAPPDATA` environment variable was missing. The path is now retrieved via a reliable API. Thanks @jiripolasek!

### Find My Mouse

-   Activating Find My Mouse no longer makes the cursor change to the busy (hourglass) icon or steals focus from your active application.

### Hosts File Editor

-   Added customizable backup settings allowing users to configure backup frequency, location, and auto-deletion policies. Thanks @davidegiacometti!

### Image Resizer

-   Fixed settings consistency during batch resize operations by capturing settings once before processing. Thanks @daverayment!

### Light Switch

-   Introduced new UI to allow users to manually enter their latitude and longitude in Sunrise to Sunset mode.
-   Refactored service with cleaner state management for stability.
-   Removed logs from every tick, only logging key events to largely reduce log size.

### Mouse Pointer Crosshairs

-   Enabled switching between Mouse Pointer Crosshairs and Gliding Cursor modes. Thanks @mikehall-ms!

### Mouse Without Borders

-   Added horizontal scrolling support. Thanks @MasonBergstrom!

### Peek

-   Fixed media files remaining locked after preview window closes. Thanks @daverayment!
-   Added a command-line interface for file previewing. See the Peek documentation for usage. Thanks @prochan2!

### PowerRename

-   PowerRename no longer crashes due to a missing resources file.
-   Added photo metadata extraction support using EXIF and XMP for pattern-based renaming with camera info, GPS coordinates, and date taken. See PowerRename Documentation.

### PowerToys Run

-   Added retry logic with exponential backoff to handle DWM composition errors during theme changes. Thanks @jiripolasek!
-   Updated OneNote icons to reflect new Microsoft 365 design. Thanks @trevorNgo!

### Quick Accent

-   Added diameter symbol (⌀) for Shift+O in Special Characters mode, thanks to @anselumjuju!

### Zoomit

-   Smoothed out zoom-animation in ZoomIt by coalescing mouse-move and timer events, thanks to @foxmsft!
-   Enabled GIF support for ZoomIt, thanks to @MarioHewardt!
-   Fixed spelling mistakes, and refactored some literal strings to string constants, thanks to @lzandman!
-   Fixed inaccurate "actual size" screenshots in ZoomIt and resolves a GDI handle leak, improving capture fidelity and long-session stability. thanks to @daverayment!

### Settings

-   Fixed title bar overlapping issue at smaller window sizes.
-   Refined shortcut control visual design with improved consistency and spacing.
-   Added dashboard utilities sorting by name or status.
-   Made update notification InfoBar in flyout clickable for direct navigation to update page.
-   Expanded installation instructions by default in README.
-   Improved accessibility for shortcut conflict button with static resource-based automation properties.
-   Added ScrollViewer to Command Palette page in PowerToys Settings. Thanks @jiripolasek!
-   Fixed module list glitches and Sort Status checkmark issue. Thanks @daverayment!

### Development

-   Fixed accessibility by associating controls with labels for screen readers.
-   Added accessible name to Shortcut Conflicts button for screen readers.
-   Excluded TitleBars from tab navigation across multiple utilities. Thanks @jiripolasek!
-   Migrated build infrastructure from Windows Server 2019 to Server 2022 with improved failure logging and predictable NuGet package paths.
-   Configured build agents to use larger P: drive for release builds to address disk space constraints.
-   Enhanced DSC v3 support by organizing resource manifests in a dedicated subfolder with PATH configuration.
-   Reduced installer bundle size by 6-7MB through centralized Hybrid CRT configuration across all C++ projects.
-   Updated .NET packages to version 9.0.10 for security fixes. Thanks @snickler!
-   Fixed spell check dictionary entries for consistency.
-   Restored accidentally deleted NuGet configuration file for Command Palette extensions.
-   Fixed package identity build by updating AppxManifest entry points to use PowerShell Core.
-   Optimized CI pipeline by replacing file copy operations with hard links and moves, reducing build time and disk usage by 10-15GB.
-   Updated Copilot guidance and PR prompt workflow.
-   Included high-volume bugs in issue template header. Thanks @daverayment!
-   Fixed incorrect HRESULT logging for inner exceptions. Thanks @jiripolasek!
-   Introduced shared sparse package identity for PowerToys Win32 components to enable access to Windows platform APIs.
-   Consolidated installer builds to produce both machine and user installers simultaneously, reducing build time and complexity.
-   Migrated exclusively to WiX v5 installer infrastructure, removing legacy WiX v3 support.
-   Temporarily removed PowerToys installer path from PATH environment variable to prevent application crashes.
-   Added complete OCR UI test coverage with automated tests for activation, settings, language selection, and text extraction.
-   Fixed test input for drive path normalization in bookmark resolver unit tests.
-   Fixed Peek UI tests by restoring Ctrl+Space activation shortcut for test scenarios.
-   Hided apps in PowerToys.SpareApps package from Start Menu. Thanks @jiripolasek!

🛣️ Roadmap
-----------

We are planning some nice new features and improvements for the next releases – a revamped Keyboard Manager UI, custom endpoint and local model support for Advanced Paste, Command Palette improvements and a brand-new Shortcut Guide experience! Stay tuned for v0.96!

❤️ PowerToys Community
----------------------

The PowerToys team is extremely grateful to have the support of an amazing active community. The work you do is incredibly important. PowerToys wouldn't be nearly what it is today without your help filing bugs, updating documentation, guiding the design, or writing features. We want to say thank you and take time to recognize your work. Your contributions and feedback improve PowerToys month after month!

Contributing
------------

This project welcomes contributions of all types. Besides coding features / bug fixes, other ways to assist include spec writing, design, documentation, and finding bugs. We are excited to work with the power user community to build a set of tools for helping you get the most out of Windows. We ask that **before you start work on a feature that you would like to contribute**, please read our Contributor's Guide. We would be happy to work with you to figure out the best approach, provide guidance and mentorship throughout feature development, and help avoid any wasted or duplicate effort. Most contributions require you to agree to a Contributor License Agreement (CLA) declaring that you grant us the rights to use your contribution and that you have permission to do so. For guidance on developing for PowerToys, please read the developer docs for a detailed breakdown. This includes how to setup your computer to compile.

Code of Conduct
---------------

This project has adopted the Microsoft Open Source Code of Conduct.

Privacy Statement
-----------------

The application logs basic diagnostic data (telemetry). For more privacy information and what we collect, see our PowerToys Data and Privacy documentation.
