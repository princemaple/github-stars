---
project: PowerToys
stars: 128346
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
Go to the PowerToys GitHub releases, click Assets to reveal the downloads, and choose the installer that matches your architecture and install scope. For most devices, that's the x64 per-user installer.

Description

Filename

Per user - x64

PowerToysUserSetup-0.97.0-x64.exe

Per user - ARM64

PowerToysUserSetup-0.97.0-arm64.exe

Machine wide - x64

PowerToysSetup-0.97.0-x64.exe

Machine wide - ARM64

PowerToysSetup-0.97.0-arm64.exe

**Microsoft Store**  
You can easily install PowerToys from the Microsoft Store:

**WinGet**  
Download PowerToys from WinGet. Updating PowerToys via winget will respect the current PowerToys installation scope. To install PowerToys, run the following command from the command line / PowerShell:

_User scope installer \[default\]_

winget install Microsoft.PowerToys \-s winget

_Machine-wide scope installer_

winget install \--scope machine Microsoft.PowerToys \-s winget

**Other methods**  
There are community driven install methods such as Chocolatey and Scoop. If these are your preferred install solutions, you can find the install instructions there.

✨ What's new
------------

**Version 0.97 (January 2026)**

For an in-depth look at the latest changes, visit the Windows Command Line blog.

**✨ Highlights**

-   **Command Palette**: Major expansion with PowerToys extension (Windows 11 only), Remote Desktop built-in extension, theme customization, drag-and-drop support, fallback ranking controls, sections/separators for pages, pinyin Chinese matching, and many UX refinements.
-   **Settings**: Quick Access flyout is now a standalone process for significantly faster startup, theme-adaptive tray icon, AOT serialization, and multiple UI/accessibility fixes
-   **CursorWrap (New!)**: New mouse utility that lets your cursor wrap around screen edges, making multi-monitor navigation faster and more seamless.
-   **Advanced Paste**: Image input for AI, color detection in clipboard history, Foundry Local improvements, Azure AI icons, and multiple bug fixes
-   **CLI Support Expanded**: FancyZones, Image Resizer, and File Locksmith can now be controlled from the command line for layout management, batch image resizing, and file lock inspection.
-   **LightSwitch**: Added support for automatically following Windows Night Light mode.
-   **Release Experience & Quality**: Refreshed "What’s new" dialog, plus many performance improvements, stability fixes, and refinements across PowerToys.

Advanced Paste
--------------

-   Added hex color previews in clipboard history. Thanks @crramirez!
-   Added automatic placeholder endpoints when required fields are left empty.
-   Fixed a grammar issue in the AI settings description. Thanks @erik-anderson!
-   Fixed loading order so custom action hotkeys are read correctly.
-   Updated Advanced Paste descriptions to reflect support for online and local models.
-   Fixed clipboard history item selection so it doesn’t duplicate entries.
-   Prevented placeholder endpoints from being saved for providers that don’t need them.
-   Added image input support for AI transforms and improved clipboard change tracking.

Awake
-----

-   Fixed Awake CLI so help, errors, and logs appear correctly in the console. Thanks @daverayment!

Command Palette
---------------

-   Fixed background image loading in BlurImageControl. Thanks @jiripolasek!
-   Fixed SDK packaging paths and added a CI SDK build stage.
-   Aligned naming and spell-checking with .NET conventions. Thanks @jiripolasek!
-   Added drag-and-drop support for Command Palette items. Thanks @jiripolasek!
-   Added a PowerToys Command Palette extension to discover and launch PowerToys utilities.
-   Fixed grid view bindings and layout issues. Thanks @jiripolasek!
-   Fixed a line-break issue in RDC extension toast messages. Thanks @jiripolasek!
-   Made the Settings button text localizable. Thanks @jiripolasek!
-   Hid the RDC fallback on the home page and fixed MSTSC working directory handling. Thanks @jiripolasek!
-   Optimized result list merging for better performance. Thanks @daverayment!
-   Added Small/Medium/Large detail sizes in the extensions API. Thanks @DevLGuilherme!
-   Hid fallback commands on the home page when no query is entered. Thanks @jiripolasek!
-   Added back navigation support in the Settings window. Thanks @jiripolasek!
-   Added a Command Palette solution filter. Thanks @jiripolasek!
-   Updated Extension SDK documentation links to Microsoft Learn. Thanks @RubenFricke!
-   Added a custom search engine URL setting for Web Search. Thanks @jiripolasek!
-   Added pinyin matching for Chinese input. Thanks @frg2089!
-   Bumped Command Palette version to 0.8.
-   Removed subtitles from built-in top-level commands. Thanks @jiripolasek!
-   Refined separator styling in the details pane. Thanks @jiripolasek!
-   Added a built-in Remote Desktop extension.
-   Added a Peek command to the Indexer extension.
-   Improved default browser detection using the Windows Shell API. Thanks @jiripolasek!
-   Added Escape key behavior options. Thanks @jiripolasek!
-   Added theme and background customization options. Thanks @jiripolasek!
-   Improved WinGet package app matching. Thanks @jiripolasek!
-   Added an auto-return-home delay setting. Thanks @jiripolasek!
-   Added fallback ranking and global results settings.
-   Removed the selection indicator in the context menu list. Thanks @jiripolasek!
-   Added a developer ribbon with build and log info. Thanks @jiripolasek!
-   Updated the “Learn more” string for Command Palette. Thanks @pratnala!
-   Added arrow-key navigation for grid views. Thanks @samrueby!
-   Fixed version display when running unpackaged. Thanks @jiripolasek!
-   Added a native debugging launch profile. Thanks @jiripolasek!
-   Reduced redundant property change notifications in the SDK. Thanks @jiripolasek!
-   Improved section readability and accessibility. Thanks @jiripolasek!
-   Made gallery spacing uniform. Thanks @jiripolasek!
-   Added sections and separators for list and grid pages. Thanks @DevLGuilherme!

Crop & Lock
-----------

-   Added a screenshot mode that freezes a cropped region into its own window. Thanks @fm-sys!

Cursor Wrap
-----------

-   Improved Cursor Wrap behavior on multi-monitor setups by wrapping only at outer edges. Thanks @mikehall-ms!

FancyZones
----------

-   Fixed editor overlay positioning on mixed-DPI multi-monitor setups. Thanks @Memphizzz!
-   Added a FancyZones CLI for command-line layout management.

File Locksmith
--------------

-   Added a File Locksmith CLI for querying, waiting on, or killing file locks.

Find My Mouse
-------------

-   Improved spotlight edge rendering for clearer Find My Mouse visuals.
-   Added telemetry to track how Find My Mouse is triggered.

Image Resizer
-------------

-   Fixed Fill mode cropping when Shrink Only is enabled. Thanks @daverayment!
-   Added a dedicated Image Resizer CLI for scripted resizing.

Light Switch
------------

-   Added telemetry events for Light Switch usage and settings changes.
-   Added a Follow Night Light mode to sync theme changes with Night Light.
-   Clarified LightSwitchService and LightSwitchStateManager roles in docs.
-   Added a Quick Access dashboard button to toggle Light Switch quickly.
-   Ensured Light Switch honors GPO policy states with clear status messaging.

Mouse Without Borders
---------------------

-   Continued refactoring Mouse Without Borders by splitting the large Common class into focused components. Thanks @mikeclayton!
-   Completed the Common class refactor with Core and IPC helper extraction. Thanks @mikeclayton!

Peek
----

-   Hardened Peek previews with strict resource filtering and safer external link warnings.
-   Improved SVG preview compatibility by rendering via WebView2.

PowerRename
-----------

-   Added HEIF/AVIF EXIF metadata extraction and extension status guidance for related previews.
-   Fixed undefined behavior in file time handling. Thanks @safocl!
-   Optimized memory allocation for depth-based rename processing.
-   Fixed Unicode normalization and non‑breaking space matching. Thanks @daverayment!
-   Fixed date token replacements followed by capital letters. Thanks @daverayment!

PowerToys Run Plugins
---------------------

-   Fixed a plugin name typo and added Project Launcher to the third‑party list. Thanks @artickc!
-   Added the Open With Antigravity plugin to the third‑party list. Thanks @artickc!

PowerToys Run
-------------

-   Avoided unnecessary hotkey conflict checks when settings change.
-   Added QuickAI to the third-party PowerToys Run plugin list. Thanks @ruslanlap!

Quick Accent
------------

-   Added localized quotation marks to Quick Accent. Thanks @warquys!
-   Fixed duplicate and redundant characters in Quick Accent sets. Thanks @noraa-junker!
-   Fixed DPI positioning issues for Quick Accent on mixed-DPI setups. Thanks @noraa-junker!

Settings
--------

-   Added a new tray icon that adapts to theme changes. Thanks @HO-COOH!
-   Centralized module enable/disable logic for cleaner Settings UI updates.
-   Simplified Settings utilities by removing ISettingsUtils/ISettingsPath interfaces. Thanks @noraa-junker!
-   Improved Settings UI consistency and disabled-state visuals.
-   Added semantic headings to the Dashboard for better accessibility.
-   Introduced Quick Access as a standalone host with updated Settings integration.
-   Fixed Dashboard toggle flicker and sort menu checkmarks. Thanks @daverayment!
-   Added Native AOT-compatible settings serialization.
-   Standardized mouse tool description text. Thanks @daverayment!
-   Added a global SettingsUtils singleton to reduce repeated initialization.

Development
-----------

-   Fixed broken devdocs links to the coding style guide. Thanks @RubenFricke!
-   Migrated main and installer solutions to .slnx for improved build tooling.
-   Restored local installer builds after the WiX v5 upgrade with signing and versioning fixes.
-   Added incremental review tooling and structured AI prompts for PR/issue reviews.
-   Documented bot commands and cleaned up devdocs structure. Thanks @noraa-junker!
-   Updated WinAppSDK pipeline defaults to 1.8 and fixed restore handling.
-   Updated the COMMUNITY list to reflect current roles.
-   Maintained community member ordering and added a new entry.
-   Re-enabled centralized PackageReference for native projects with VS auto-restore.
-   Disabled MSBuild caching by default in CI to avoid build instability.
-   Updated the latest WinAppSDK daily pipeline for split-dependency restores.
-   Suppressed experimental build warnings and aligned WrapPanel stretch handling.
-   Reordered the spell-check expect list for consistent automation.
-   Migrated native projects to centralized PackageReference management.
-   Cleaned spell-check dictionary entries and capitalization.
-   Synced commit/PR prompts and wired VS Code to repo prompt files.
-   Added VS Code build tasks and improved build script path handling.
-   Updated Windows App SDK package versions in central package management.
-   Migrated cmdpal extension native project to PackageReference and fixed outputs.
-   Reverted PackageReference changes back to packages.config where needed.
-   Bypassed a release version check for a failing DLL to keep pipelines green.
-   Consolidated Copilot instructions and fixed prompt frontmatter.
-   Added signing entries for new Quick Access binaries and CLI version metadata.
-   Fixed install scope detection to avoid mixed per-user/per-machine installs.
-   Added a Module Loader tool to quickly test PowerToys modules without full builds. Thanks @mikehall-ms!
-   Added update telemetry to understand auto-update checks and downloads.
-   Updated the telemetry package for new compliance requirements. Thanks @carlos-zamora!
-   Documented missing telemetry events in DATA\_AND\_PRIVACY.
-   Fixed UI test pipeline restores for .slnx solutions.
-   Added UI automation coverage for Advanced Paste clipboard history flows.
-   Stabilized FancyZones UI tests with more reliable selectors and screen recordings.

🛣️ Roadmap
-----------

We are planning some nice new features and improvements for the next releases – PowerDisplay, Command Palette improvements and a brand-new Shortcut Guide experience! Stay tuned for v0.97!

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
