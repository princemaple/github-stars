---
project: Winhance
stars: 8753
description: Application designed to optimize, customize and enhance your Windows experience.
url: https://github.com/memstechtips/Winhance
---

Winhance - Windows Enhancement Utility 🚀
=========================================

**Winhance** is a C# application designed to debloat, optimize and customize your Windows experience. From software management to system optimizations and customization, Winhance provides everything you need to enhance Windows 10 and 11 systems.

**Winhance** features most of the same enhancements as UnattendedWinstall without needing to do a clean install of Windows.

Note

Winhance is an independent, open-source project and is **not affiliated with, endorsed by, or associated with Microsoft** in any way. "Windows" is a registered trademark of Microsoft Corporation. Any similarities to Windows Settings or other Microsoft interfaces are a natural result of building a Windows enhancement tool using native Windows UI frameworks.

Requirements 💻
---------------

-   Windows 10/11
    -   _Tested on Windows 10 x64 22H2 and Windows 11 23H2, 24H2 and 25H2_

Installation 📥
---------------

### Quick Install via PowerShell

Paste this command into PowerShell to download and run the installer:

irm "https://get.winhance.net" | iex

### Download the Installer

The `Winhance.Installer.exe` includes both Installable and Portable versions during setup.

Note

This tool is currently in development. Any issues can be reported using the Issues tab.  
Also, I'm not a developer, I'm just enjoying learning more about scripting/programming and learning as I go.  
  
Please also understand that I prefer to develop and work on these projects independently.  
I do value other people's insights and appreciate any feedback, but don't take it personally if a pull request is not accepted.

Support the developer
---------------------

It really does make a big difference, and is very much appreciated. Thanks  

Current Features 🛠️
--------------------

### Software & Apps 💿

-   **Windows Apps & Features Section**
    -   Searchable interface with explanatory legend
    -   Organized sections for Windows Apps, Legacy Capabilities, and Optional Features
    -   One-click removal and installation of selected items
    -   Control scripts and scheduled tasks via Windows Apps Help menu
-   **External Apps Section**
    -   Install various useful applications via WinGet
        -   (WinGet COM API integration based on https://github.com/marticliment/WinGet-API-from-CSharp)
    -   Categories include Browsers, Multimedia utilities, Document viewers, and more

### Optimize 🚀

-   Searchable interface with quick nav control
-   Toggle switches and selection controls for each setting
-   Set UAC Notification Level
-   Privacy Settings
-   Gaming and Performance Optimizations
-   Windows Updates
-   Power Settings with Power Plan selection
-   Sound Settings
-   Notification Preferences

### Customize 🎨

-   Searchable interface with quick nav control
-   Toggle switches and selection controls for each setting
-   Windows Theme selector (Dark/Light Mode)
-   Taskbar Customization
-   Start Menu Customization
-   Explorer Customizations

### Advanced Tools 🛠️

-   Create Custom Windows ISO's with WIMUtil (Windows Installation Media Utility) including adding drivers from current OS
-   Create autounattend.xml files based on your Winhance selections

### Other Settings

-   Manage Your Winhance (and Windows) Settings with Wihance Configuration Files:
    -   Save settings currently applied in Winhance to a config file for easy importing on a new system or after a fresh Windows install.
-   Toggle Winhance's theme (Light/Dark Mode)

License
-------

Except where otherwise stated (see THIRD-PARTY-NOTICES.txt), the content of this repository is provided under the PolyForm Shield 1.0.0 license by Marco du Plessis.

**In plain language:** Winhance is free to use for everyone -- individuals, businesses, and IT professionals. You can use it to service and consult for clients. You just can't fork or rebrand it and redistribute it as a competing product. See the full LICENSE.txt for details.

Feedback and Community
----------------------

If you have feedback, suggestions, or need help with Winhance, please join the discussion on GitHub or our Discord community:
