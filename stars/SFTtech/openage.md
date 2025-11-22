---
project: openage
stars: 13908
description: Clone of the Age of Empires II engine 🚀 
url: https://github.com/SFTtech/openage
---

**openage**: a volunteer project to create a free engine clone of the _Genie Engine_ used by _Age of Empires_, _Age of Empires II (HD)_ and _Star Wars: Galactic Battlegrounds_, comparable to projects like OpenMW, OpenRA, OpenSAGE, OpenTTD and OpenRCT2.

openage uses the original game assets (such as sounds and graphics), but (for obvious reasons) doesn't ship them. To play, you require _any of the original games (AoE1, AoE2)_ or their _Definitive Edition_ releases.

Contact
-------

Contact

Where?

Issue Tracker

GitHub SFTtech/openage

Development Blog

blog.openage.dev

Subreddit

/r/openage

Discussions

GitHub Discussions

Matrix Chat

`#sfttech:matrix.org`

Money Sink

Technical foundation
--------------------

Technology

Component

**C++20**

Engine core

**Python3**

Scripting, media conversion, in-game console, code generation

**Cython**

Python/C++ Glue code

**Qt6**

Graphical user interface

**CMake**

Build system

**OpenGL**

Rendering, shaders

**Opus**

Audio codec

**nyan**

Content Configuration and Modding

**Humans**

Mixing together all of the above

Goals
-----

-   Fully authentic look and feel
    -   This can only be approximated since the behavior of the original game is mostly undocumented, and guessing/experimenting can only get you this close
    -   We will not implement useless artificial limitations (max 30 selectable units...)
-   An easily-moddable content format: **nyan** yet another notation
-   An integrated Python console and API, comparable to blender
-   AI scripting in Python, you can use machine learning
    -   here is some additional literature
-   Re-creating free game assets
-   Multiplayer (obviously)
-   Matchmaking and ranking with a haskell masterserver
-   Optionally, improvements over the original game
-   Awesome infrastructure such as our own Kevin CI service

But beware, for sanity reasons:

-   No network compatibility with the original game. You really wanna have the same problems again?
-   No binary compatibility with the original game. A one-way script to convert maps/savegames/missions to openage is planned though.

Current State of the Project
----------------------------

**Important notice**: At the moment, "gameplay" is basically non-functional. We're implementing the internal game simulation (how units even do anything) with simplicity and extensibility in mind, so we had to get rid of the temporary (but kind of working) previous version. With these changes, we can (finally) actually make use of our converted asset packs and our nyan API! We're working day and night to make gameplay return\*. If you're interested, we wrote detailed explanations on our blog: Part 1, Part 2, Monthly Devlog.

_\* may not actually be every day and night_

Operating System

Build status

Debian Sid

Ubuntu 24.04 LTS

macOS

Windows Server 2019

Windows Server 2022

Installation Packages
---------------------

There are many missing parts for an actually working game. So if you "just wanna play", you'll be disappointed, unfortunately.

We strongly recommend building the program from source to get the latest, greatest, and shiniest project state :)

-   For **Linux** check at repology if your distribution has any packages available. Otherwise, you need to build from source. We don't release `*.deb`, `*.rpm`, Flatpak, snap or AppImage packages yet.
    
-   For **Windows** check our release page for the latest installer. Otherwise, you need to build from the source.
    
-   For **macOS** we currently don't have any packages, you need to build from source.
    

If you need help, maybe our troubleshooting guide helps you.

Quickstart
----------

-   **How do I get this to run on my box?**
    
    1.  Clone the repo.
    2.  Install dependencies. See doc/building.md to get instructions for your favorite platform.
    3.  Build the project:
    
    ```
    ./configure --download-nyan
    make
    ```
    

**Alternative approach:** You can build and run the project using Docker. See Running with docker for more details.

-   **I compiled everything. Now how do I run it?**
    
    -   Execute `cd bin && ./run main`.
    -   The convert script will transform original assets into openage formats, which are a lot saner and more moddable.
    -   Use your brain and react to the things you'll see.
-   **Waaaaaah! It...**
    
    -   segfaults
    -   prints error messages I don't want to read
    -   ate my dog

All of those are features, not bugs.

To turn them off, use `./bin/run --dont-segfault --no-errors --dont-eat-dog`.

If this still does not help, try our troubleshooting guide, the contact section or the bug tracker.

Contributing
============

You might ask yourself now "Sounds cool, but how do I participate and get famous contribute useful features?".

Fortunately for you, there is a lot to do and we are very grateful for your help.

Where do I start?
-----------------

-   **Check the issues** labelled with `good first issue`. These are tasks that you can start right away and don't require much previous knowledge.
-   **Ask us** in the chat. Someone there could need help with something.
-   You can also **take the initiative** and fix a bug you found, create an issue for discussion or implement a feature that we never thought of, but always wanted.

Ok, I found something. What now?
--------------------------------

-   **Tell us**, if you haven't already. Chances are that we have additional information and directions.
-   **Read the docs**. They will answer most "administrative" questions like what code style is used and how the engine core parts are connected.
-   **Read the code** and get familiar with the engine component you want to work with.
-   Do not hesitate to **ask us for help** if you do not understand something.

How do I contribute my features/changes?
----------------------------------------

-   Read the **contributing guide**.
-   You can upload work-in-progress (WIP) versions or drafts of your contribution to get feedback or support.
-   Tell us (again) when you want us to review your work.

I want to help, but I'm not a programmer...
-------------------------------------------

Then openage might be a good reason to become one! We have many issues and tasks for beginners. You just have to ask and we'll find something. Alternatively, lurking is also allowed.

* * *

Cheers, happy hecking!

Development Process
-------------------

What does openage development look like in practice?

-   extensive synchronization!
-   doc/development.md.

How can I help?

-   doc/contributing.md.

All documentation is also in this repo:

-   Code documentation is embedded in the sources for Doxygen (see doc readme).
-   Have a look at the doc directory. This folder tends to get outdated when code changes.

License
-------

**GNU GPLv3** or later; see copying.md and legal/GPLv3.

I know that probably nobody is ever gonna look at the `copying.md` file, but if you want to contribute code to openage, please take the time to skim through it and add yourself to the authors list.
