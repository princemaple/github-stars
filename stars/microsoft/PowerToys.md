---
project: PowerToys
stars: 125725
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

PowerToysUserSetup-0.95.1-x64.exe

Per user - ARM64

PowerToysUserSetup-0.95.1-arm64.exe

Machine wide - x64

PowerToysSetup-0.95.1-x64.exe

Machine wide - ARM64

PowerToysSetup-0.95.1-arm64.exe

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

**Version 0.95 (October 2025)**

For an in-depth look at the latest changes, visit the Windows Command Line blog.

**✨ Highlights**

-   **NEW:** The **Light Switch** utility in PowerToys allows you to automatically switch between light and dark themes in Windows based on the time of day.
-   Command Palette delivered major search performance gains (new fuzzy matcher and smarter fallbacks) improving relevance and speed.
-   Peek can now be activated using just the Spacebar!
-   Find My Mouse added transparent spotlight with independent backdrop opacity, boosting focus and accessibility.
-   Settings now lets you delete shortcuts entirely and ignore conflicts.
-   Mouse Pointer Crosshairs gained orientation options (vertical / horizontal / both) for customizable accessibility. Thanks @mikehall-ms!
-   PowerRename fixed enumeration counter skipping ensuring reliable batch renames. Thanks @daverayment!
-   ZoomIt restored legacy draw and snipping behaviors, and fixed recording issues, improving reliability. Thanks @chakrik73!

### Command Palette

-   Applied conditional margin for icon-only tags to tighten layout. Thanks @samrueby
-   Improved the reliability of accessing Command Palette settings through PowerToys Settings and executing other x-cmdpal:// protocol commands. Thanks @jiripolasek
-   Enabled AOT by default for improved performance while simplifying publish configs.
-   Replaced service state color dots with play/pause/stop icons for enhanced accessibility. Thanks @samrueby
-   Fixed filter dropdown sync and crash by binding SelectedValue and raising UI-thread notifications. Thanks @jiripolasek
-   Ensured long links wrap correctly in details view.
-   Removed animation and enforced minimum width on filter dropdown for clarity. Thanks @jiripolasek
-   Restored focus to More button after ESC closes context menu, improving keyboard flow. Thanks @chatasweetie
-   Marked main and toast windows as tool windows to keep them out of Alt+Tab while preserving style. Thanks @jiripolasek
-   Fixed AOT template and theming issues for filter separators. Thanks @jiripolasek
-   Introduced grid layouts (small, medium, gallery) for richer page presentation.
-   Materialized result lists to avoid rescoring overhead.
-   Disabled problematic selection TextToSuggest behind environment flag.
-   Major search performance improvements (new fuzzy matcher, smarter fallbacks, fewer exceptions).
-   Added context menu "Show Details" command when details pane is hidden.
-   Reduced window flicker by avoiding unnecessary cloaking. Thanks @jiripolasek
-   Restored EmptyContent rendering for blank states. Thanks @DevLGuilherme
-   Saved new state even if prior app state file was corrupt (better resilience). Thanks @jiripolasek
-   Migrated settings window to WinUI TitleBar control. Thanks @jiripolasek
-   Prevented crash on duplicate keybindings and simplified matching. Thanks @jiripolasek
-   Hotkeys now always respect the “Ignore shortcut in fullscreen” setting. Thanks @jiripolasek
-   Hid search box on content pages, improving focus and accessibility, and added Home title. Thanks @jiripolasek
-   Blocked Ctrl+I from inserting stray tabs in search box.
-   Logged HRESULT codes in error logs for deeper diagnostics. Thanks @jiripolasek
-   Advanced font and emoji icon classification and alignment improvements. Thanks @jiripolasek
-   Ensured that fallback command icons are visible on the extension settings page. Thanks @jiripolasek
-   Fixed breadcrumb margin misalignment (visual polish). Thanks @jiripolasek
-   Truncated overly long command labels with ellipsis to prevent overflow.
-   Added a setting to configure the page transition animation.
-   Collection of small improvements and nits for Run Commands.
-   Improved bookmarks performance and experience. Thanks @jiripolasek
-   Added Ctrl+O shortcut in Clipboard History to open links directly.
-   Resolved conflict with external software that blocked Command Palette from hiding.
-   Updated context menu items to reflect name and icon changes, and ensured application icons are displayed correctly. Thanks @jiripolasek
-   Added Alt+Home shortcut to return immediately to the Command Palette home page. Thanks @jiripolasek
-   Fixed a crash when displaying code blocks in markdown on detail or content pages. Thanks @jiripolasek
-   Fixed an issue where the search bar icon and title were not updated when rapidly switching pages. Thanks @jiripolasek
-   Improved the appearance of the search box in the context menu.

### Command Palette Extensions

-   Replaced localized WebSearch setting keys with stable literals and numeric history count. Thanks @jiripolasek!
-   Enabled advanced markdown tables and emphasis extensions. Thanks @jiripolasek!
-   Added setting to choose Clipboard History primary action (Paste vs Copy). Thanks @jiripolasek
-   Added actionable empty-state hints for File Search (search PC / open indexing settings). Thanks @jiripolasek!
-   Ensured all WinGet extension assets copy reliably to output. Thanks @jiripolasek!
-   Improved Run command line parsing for paths with spaces; sped up related tests.
-   Updated WebSearch extension icon set for enhanced clarity and contrast. Thanks @jiripolasek!
-   Added Terminal profile sort order setting including MRU tracking. Thanks @jiripolasek!
-   Added Uninstall Application command (UWP direct, Win32 via Settings). Thanks @mKpwnz!
-   Deferred WinGet details loading and added timing logs.
-   Removed LINQ from All Apps extension for performance.
-   Added standardized key chord system + shortcuts to File Search commands. Thanks @jiripolasek!
-   Added Terminal channel filter & remembered selection option. Thanks @jiripolasek!
-   Enabled loading local/data/app images in markdown with sizing hints. Thanks @jiripolasek!
-   Added external extension reload via x-cmdpal://reload (configurable). Thanks @jiripolasek!
-   Instant WebSearch history updates with in-memory store & events. Thanks @jiripolasek!
-   Added keep-after-paste option and safe delete with confirmation for Clipboard History. Thanks @jiripolasek!

### Environment Variables

-   Replaced custom window chrome with WinUI TitleBar for cleaner, maintainable Environment Variables UI.

### File Locksmith

-   Adopted WinUI TitleBar to simplify window chrome while preserving appearance.

### Find My Mouse

-   Added transparent spotlight support with separate backdrop opacity; migrated to Windows App SDK composition APIs.

### Hosts File Editor

-   Migrated to native WinUI TitleBar for cleaner, maintainable window chrome.

### Light Switch

-   Introduced as a brand-new PowerToy module.
-   Automatically switches between light and dark themes.
-   Supports time-based scheduling or location-based sunrise/sunset switching.
-   Supports using a keyboard shortcut to force a change.
-   Supports filtering changes for Apps and/or System Theme.

### Mouse Pointer Crosshairs

-   Added Esc key to cancel active gliding cursor sequence. Thanks @mikehall-ms!
-   Added orientation option (vertical / horizontal / both) for crosshairs customization. Thanks @mikehall-ms!

### Mouse Without Borders

-   Continued Common class refactor (part 5/7) by extracting clipboard and init/cleanup logic into focused classes. Thanks @mikeclayton!
    
-   Fix connection failures caused by conflicting MachineId across machines. Thanks @noraa-junker for troubleshooting!
    

### Peek

-   Added the option to activate Peek with just the Spacebar.

### PowerRename

-   Fixed enumeration counter skipping when regex replacement equals original filename (counters now advance reliably). Thanks @daverayment!

### Quick Accent

-   Expanded Welsh layout with acute, grave, and dieresis variants for vowels (consistent ordering). Thanks @PesBandi!

### Registry Preview

-   Migrated to native TitleBar and AppWindow APIs for cleaner window chrome.

### Screen Ruler

-   Fixed ARM64 crash by aligning cursor position structure to 8-byte boundary.

### Settings

-   Added ability to ignore specific hotkey conflicts to reduce noise.
-   Stopped creating backup directory during dry-run status checks (cleaner first-run).
-   Standardized casing and localization for ZoomIt and modules header.
-   Improved search results page accessibility and conditional module grouping.

### ZoomIt

-   Updated resource file to reflect standalone v9.01 and current copyright year. Thanks @foxmsft!
-   Restored legacy draw/snipping behaviors and fixed recording race conditions. Thanks @chakrik73!
-   Added smooth image option for improved zoom quality using GDI+ for static zoom and Magnifier API for live zoom. Thanks @markrussinovich!

### Documentation

-   New Microsoft Learn documentation for the Light Switch module.
-   New dev docs for the Light Switch module.

### Development (Area-Build & Area-Tests)

-   Allowed debug launches to continue when modules fail to load, speeding developer iteration.
-   Fixed spell checker dictionary entry (advapi) to eliminate false error.
-   Added VS Code development guide and launch configs to streamline cross-editor workflows.
-   Upgraded Windows App SDK and related dependencies to 1.8 for newer platform features.
-   Rewrote YAML comment to resolve new spell checker forbidden pattern. Thanks @jiripolasek!
-   Corrected solution structure by returning misplaced Common project, reducing build confusion.
-   Modernized build scripts with shared helpers and VS environment autodetection for simpler CLI builds.
-   Standardized build scripts and platform detection to improve reliability and reuse.
-   Added missing Command Palette version bump to align module release cadence.
-   Added EXECUTEDEFAULT term to dictionary to prevent regression build failures. Thanks @jiripolasek!
-   Introduced nightly pre-warm pipeline and configurable MSBuild cache mode to improve CI performance.
-   Resolved CI forbidden pattern spelling complaint to keep pipelines green.
-   Added AI contributor instruction set to clarify code area expectations.
-   Added accessibility IDs to settings and FancyZones toggles, stabilizing UI tests.
-   Added automatic log collection on UI test failures to speed root cause analysis.
-   Stabilized Mouse Utils tests by switching to AccessibilityId selectors.
-   Added Screen Ruler UI test coverage to validate core measurement workflows.

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
