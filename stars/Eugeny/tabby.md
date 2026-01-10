---
project: tabby
stars: 68088
description: A terminal for a more modern age
url: https://github.com/Eugeny/tabby
---

     

* * *

> 👋 Managing remote environments? Check out Warpgate, my smart SSH/HTTP/MySQL bastion server, it works great with Tabby, you'll love it.

* * *

### Downloads:

-   Latest release
-   Repositories: Debian/Ubuntu-based, RPM-based
-   Latest nightly build

  

This README is also available in: 🇪🇸 Spanish · 🇷🇺 Русский · 🇰🇷 한국어 · 🇨🇳 简体中文 · 🇮🇹 Italiano · 🇩🇪 Deutsch · 🇯🇵 日本語 · 🆔 Bahasa Indonesia · 🇧🇷 Português · 🇵🇱 Polski

* * *

**Tabby** (formerly **Terminus**) is a highly configurable terminal emulator, SSH and serial client for Windows 10, macOS and Linux

-   Integrated SSH and Telnet client and connection manager
-   Integrated serial terminal
-   Theming and color schemes
-   Fully configurable shortcuts and multi-chord shortcuts
-   Split panes
-   Remembers your tabs
-   PowerShell (and PS Core), WSL, Git-Bash, Cygwin, MSYS2, Cmder and CMD support
-   Direct file transfer from/to SSH sessions via Zmodem
-   Full Unicode support including double-width characters
-   Doesn't choke on fast-flowing outputs
-   Proper shell experience on Windows including tab completion (via Clink)
-   Integrated encrypted container for SSH secrets and configuration
-   SSH, SFTP and Telnet client available as a web app (also self-hosted).

Contents
========

-   What Tabby is and isn't
-   Terminal features
-   SSH Client
-   Serial Terminal
-   Portable
-   Plugins
-   Themes
-   Contributing

What Tabby is and isn't
=======================

-   **Tabby is** an alternative to Windows' standard terminal (conhost), PowerShell ISE, PuTTY, macOS Terminal.app and iTerm
    
-   **Tabby is not** a new shell or a MinGW or Cygwin replacement. Neither is it lightweight - if RAM usage is of importance, consider Conemu or Alacritty
    

Terminal features
=================

-   A VT220 terminal + various extensions
-   Multiple nested split panes
-   Tabs on any side of the window
-   Optional dockable window with a global spawn hotkey ("Quake console")
-   Progress detection
-   Notification on process completion
-   Bracketed paste, multiline paste warnings
-   Font ligatures
-   Custom shell profiles
-   Optional RMB paste and copy-on select (PuTTY style)

SSH Client
==========

-   SSH2 client with a connection manager
-   X11 and port forwarding
-   Automatic jump host management
-   Agent forwarding (incl. Pageant and Windows native OpenSSH Agent)
-   Login scripts

Serial Terminal
===============

-   Saved connections
-   Readline input support
-   Optional hex byte-by-byte input and hexdump output
-   Newline conversion
-   Automatic reconnection

Portable
========

Tabby will run as a portable app on Windows, if you create a `data` folder in the same location where `Tabby.exe` lives.

Plugins
=======

Plugins and themes can be installed directly from the Settings view inside Tabby.

-   docker - connect to Docker containers
-   title-control - allows modifying the title of the terminal tabs by providing a prefix, suffix, and/or strings to be removed
-   quick-cmds - quickly send commands to one or all terminal tabs
-   save-output - record terminal output into a file
-   sync-config - sync the config to Gist or Gitee
-   clippy - an example plugin which annoys you all the time
-   workspace-manager - allows creating custom workspace profiles based on the given config
-   search-in-browser - opens default system browser with a text selected from the Tabby's tab
-   sftp-tab - open sftp tab for ssh connection like SecureCRT
-   background - change Tabby background image and more...
-   highlight - Tabby terminal keyword highlight plugin
-   web-auth-handler - In-app web authentication popups (Built primarily for warpgate in-browser auth)
-   mcp-server - Powerful Model Context Protocol server integration for Tabby that seamlessly connects with AI assistants through MCP clients like Cursor and Windsurf, enhancing your terminal workflow with intelligent AI capabilities.

Themes
======

-   hype - a Hyper inspired theme
-   relaxed - the Relaxed theme for Tabby
-   gruvbox
-   windows10
-   altair
-   catppuccin - Soothing pastel theme for Tabby
-   noctis - color themes inspired by Noctis VS Code theme

Sponsors
========

**packagecloud** has provided free Debian/RPM repository hosting

**keygen** has provided free release & auto-update hosting

**IQ Hive** is providing financial support for the project development

Contributing
============

Pull requests and plugins are welcome!

See HACKING.md and API docs for information of how the project is laid out, and a very brief plugin development tutorial.

* * *

Thanks goes to these wonderful people (emoji key):

  
**Russell Myers**  
💻

  
**Austin Warren**  
💻

  
**Felicia Hummel**  
💻

  
**Mike MacCana**  
⚠️ 🎨

  
**Yacine Kanzari**  
💻

  
**BBJip**  
💻

  
**Futagirl**  
🎨

  
**Levin Rickert**  
💻

  
**OJ Kwon**  
💻

  
**domain**  
🔌 💻

  
**James Brumond**  
🔌

  
**Daniel Imms**  
💻 🔌 ⚠️

  
**Florian Bachmann**  
💻

  
**Michael Kühnel**  
💻 🎨

  
**Tilmann Meyer**  
💻

  
**PM Extra**  
🐛

  
**Jonathan**  
💻

  
**Hans Koch**  
💻

  
**Dak Smyth**  
💻

  
**Wang Zhi**  
💻

  
**jack1142**  
💻

  
**Howie Douglas**  
💻

  
**Chris Kaczor**  
💻

  
**Johannes Kadak**  
💻

  
**LeSeulArtichaut**  
💻

  
**Cyril Taylor**  
💻

  
**nstefanou**  
💻 🔌

  
**orin220444**  
💻

  
**Gobius Dolhain**  
💻

  
**Gwilherm Folliot**  
💻

  
**Dmitry Pronin**  
💻

  
**Jonathan Beverley**  
💻

  
**Zenghai Liang**  
💻

  
**Mateusz Tracz**  
💻

  
**pinpin**  
💻

  
**Takuro Onoda**  
💻

  
**frauhottelmann**  
💻

  
**Piotr Patalong**  
🎨

  
**Clark Wang**  
💻

  
**iamchating**  
💻

  
**starxg**  
🔌

  
**Alisue**  
🎨

  
**Dominic Yin**  
💻

  
**Brandon Rothweiler**  
🎨

  
**Logic Machine**  
📖

  
**cypherbits**  
📖

  
**Matthew Davidson**  
💻

  
**Alexander Wiedemann**  
💻

  
**장보연**  
📖

  
**zZ**  
💻

  
**Aaron Davison**  
💻

  
**Przemyslaw Kozik**  
🎨

  
**Alfredo Arellano de la Fuente**  
💻

  
**MH Kim**  
💻

  
**Marmota**  
🎨

  
**Ares Andrew**  
📖

  
**George Korsnick**  
💵

  
**Artem Smirnov**  
💵

  
**Tim Kopplow**  
💵

  
**mrthock**  
💵

  
**Lukas Rottach**  
💵

  
**boonkerz**  
💻 🌍

  
**Milo Ivir**  
🌍

  
**JasonCubic**  
🎨

  
**MaxWaldorf**  
🚇

  
**Michael Wizner**  
💻

  
**Martin**  
💻

  
**Piersandro Guerrera**  
📖 🌍

  
**0x973**  
💻

  
**Allenator**  
📖

  
**Matheus Castello**  
💻

  
**Jai A P**  
📦

  
**Richard Yu**  
💻

  
**artu-ole**  
💻

  
**Timofey Gribanov**  
📖 🌍

  
**Christian Bingman**  
💻

  
**zhipeng**  
💻

  
**woodmeal**  
💻

  
**MagicLike**  
📖

  
**Hisam Fahri**  
💻

  
**Liangcheng Juves**  
💻

  
**Atte Timonen**  
💻

  
**João Pinto**  
📖

  
**Alan**  
💻

  
**Atsushi Morimoto**  
💵

  
**Arles**  
💵

  
**six2dez**  
💵

  
**Candice**  
💵

  
**Rowen Willabus**  
💵

  
**HengY1Coding✨**  
💵

  
**Francis Gelderloos**  
💵

  
**astromasoud**  
💵

  
**Anders G. Jørgensen**  
💵

  
**Dave Richardson**  
💵

  
**Thomas Peter Berntsen**  
💵

  
**Ikko Ashimine**  
📖

  
**giejqf**  
💻

  
**Thomas LACAZE**  
💻

  
**Po Chen**  
💵

  
**Victor Chandra**  
📖

  
**Dan Nissenbaum**  
💵

  
**RogueThorn**  
💵

  
**Spenser Black**  
💻

  
**Alex**  
💵

  
**HengY1Coding✨**  
💵

  
**David Carrero**  
📖

  
**Andrii Zhovtiak**  
💻

  
**Mason Ma**  
💵

  
**Timo**  
💵

  
**Evin Watson**  
📖

  
**Hendra Juli**  
📖

  
**Wellinton Kricowski**  
💵 📖

  
**Allan**  
🎨

  
**Benjamin Brandmeier**  
💻

  
**patric1025**  
🌍

  
**hermitpopcorn**  
💻

  
**Joshua Tzucker**  
💵

  
**luxifr**  
💵

  
**Anne Summers**  
💵

  
**Clem**  
💻

  
**Elizabeth Martín Campos**  
💻

  
**Tomáš Hruška**  
💻

  
**Osman Karaketir**  
💻

  
**Crypto Gnome**  
💵

  
**Richard Bukovansky**  
💵

  
**catlas**  
💵

  
**Thomas Kapocsi**  
📖

  
**Dylan Hackworth**  
💵

  
**Sangboak Lee**  
💻

  
**qyecst**  
💻

  
**Han**  
💻

  
**wljince007**  
💻

  
**fero**  
💻

  
**Sibren**  
💻

  
**Nathaniel Walser**  
💻

  
**Aaron Huggins**  
🎨

  
**KDex**  
💻

  
**ChangHwan Kim**  
💻

  
**Ash Neilson**  
💻

  
**Chen Fansong**  
💻

  
**Mxmilu**  
💻

  
**Charles Buffington**  
💻

  
**Yu Qin**  
💻

  
**fireblue**  
💻

  
**marko1616**  
💻

  
**SelfHosted**  
💵

  
**Hiroaki Ogasawara**  
💻

  
**geodic**  
💻

  
**P Foundation**  
💵

  
**et304383**  
💻

This project follows the all-contributors specification. Contributions of any kind are welcome!
