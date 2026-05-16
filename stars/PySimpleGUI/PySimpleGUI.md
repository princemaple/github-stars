---
project: PySimpleGUI
stars: 13803
description: Python GUIs for Humans! PySimpleGUI is the top-rated Python application development environment. Launched in 2018. NEW for 2026 - the LGPL3 Version 6.  Transforms tkinter, Qt, WxPython, and Remi into a simple, intuitive, and fun experience for both hobbyists and expert users.  
url: https://github.com/PySimpleGUI/PySimpleGUI
---

Open Source Once Again...
=========================

Hey, it's Mike....

We gave commercialization a try. It was an incredible experience, but it didn’t generate the resources needed to sustain PySimpleGUI at the level we had hoped. In February 2025, we announced that PySimpleSoft would be shutting down, with support continuing through the end of 2025.

That process is now complete. The next question was what to do with the code, documentation, and repositories. I always planned to keep the repos available for reference—so the decision came down to the software itself.

PySimpleGUI 6
=============

I’ve released the PySimpleGUI 5 code as open source. After removing licensing and security components, it’s now available under the LGPL3 license on GitHub and PyPI.

Installing from PyPI
--------------------

To install the latest version (v6):

`python -m pip install PySimpleGUI`

If you need the older version (4.60.5.1):

`python -m pip install PySimpleGUI==4.60.5.1`

Installing from Github
----------------------

The GitHub repo has the most up-to-date code. You can install directly without cloning:

`python -m pip install --upgrade https://github.com/PySimpleGUI/PySimpleGUI/zipball/master`

Or clone/download the repo and install locally:

`python -m pip install .`

Longer Term Outlook
-------------------

I’m still wrapping up the transition from version 5 to 6, including the docs. After that, I’m honestly not sure what the long-term future looks like—but if the past 8 years are any indication, I’m not great at predicting it.

For now, I’m here and happy to help.

Thank you
---------

PySimpleGUI has been a once-in-a-lifetime experience. It’s been amazing to see what people have built and to be a small part of it. Thanks to everyone who supported the project over the years.

* * *

What is PySimpleGUI?
====================

PySimpleGUI is a wrapper for tkinter (and other GUI libraries) that transforms the GUI SDK into a simpler, more compact architecture while still providing detailed customization. No prior GUI programming experience needed.

This is an entire interactive application.

import PySimpleGUI as sg

\# Define the window's contents
layout \= \[\[sg.Text("What's your name?")\],
          \[sg.Input(key\='-INPUT-')\],
          \[sg.Text(size\=(40,1), key\='-OUTPUT-')\],
          \[sg.Button('Ok'), sg.Button('Quit')\]\]

\# Create the window
window \= sg.Window('Window Title', layout)

\# Display and interact with the Window using an Event Loop
while True:
    event, values \= window.read()
    \# See if user wants to quit or window was closed
    if event \== sg.WINDOW\_CLOSED or event \== 'Quit':
        break
    \# Output a message to the window
    window\['-OUTPUT-'\].update('Hello ' + values\['-INPUT-'\] + "! Thanks for trying PySimpleGUI")

\# Finish up by removing from the screen
window.close()

This is the window that's created.

Here's the same window after some user interaction.

Documentation - want to learn more?
-----------------------------------

You'll find **extensive** documentation at:

https://Docs.PySimpleGUI.com

Contributing
------------

PySimpleGUI has always been developed more like a proprietary product than an open source project. Pull requests aren't accepted.

* * *

Recently added features and activities
======================================

Documentation
-------------

-   The move of the documentation from ReadTheDocs to GitHub pages is complete. Users should notice no difference.
-   Removal of Version 5 specifics is done for the mostpart. There may be a few spots that need cleanup
-   Work has started to include PSG 6 details. The SDK Call Reference needs upating before the next PyPO release, preferably sooner so that the code on GitHub is in there prior to PyPO release.

Features & Fixes
----------------

-   6.0.2 - Fixed bug in Window.settings\_save
-   6.0.3 - Added ability to "print" an image inline in a Multiline element

-   6.0.5 - The ability to upgrade to the latest Maint Release is once again built into PSG. You can use the Home Window or the command line command`psgupgrade`. You can see the release notes and install a new version.

-   PSGWeb - PySimpleGUI running in a browser window
    -   Works with most demo programs
    -   To try it, go to any PySimpleGUI application on GitHub, add `psgweb.us` onto the front of the url, press enter
    -   https://github.com/PySimpleGUI/PySimpleGUI/blob/master/DemoPrograms/Demo\_All\_Elements.py becomes https://psgweb.us/github.com/PySimpleGUI/PySimpleGUI/blob/master/DemoPrograms/Demo\_All\_Elements.py
    -   There are no plans to release or expand this prototype. It was created as part of the larger PSG 5 effort, but not released.

Here's that Demo Program running in browser:

* * *

AI....
------

Seems most projects have something to say about AI usage now. This is my **opinion** and how I've decided to use AI. It's what's right for me. It might not be right for you or anyone else.

I use LLMs to search and summarize documentation, lookup errors, do research, get knowledge. I don't use LLMs to write code. My reason is very simple.

### **I like to write code.**

I fell in love with programming 50 years ago. Writing software is my happy place. Why would I give that to a computer to do instead of getting the enjoyment I get from doing it? AI can generate lots of things. The feeling I get writing software is not one of the things AI can generate.

I'm not in a hurry. If I wanted code written for me, I would have opened the project up to pull requests years ago, but I didn't because I wanted to write the code. It's fun!

### PySimpleGUI in the AI era

A common question in software today is whether a library is still relevant. I think for PySimpleGUI the answer is yes. People discover and install PySimpleGUI every day. GUI applications are often built incrementally. As features are added, layouts change, buttons move, and the code needs to evolve. That’s much easier when the code is understandable, whether it was written by a person or an AI.

I use PySimpleGUI regularly, and I can’t imagine building a Windows app without it. I’ve recently been working on a 6502 breadboard computer. I built a bus analyzer using a couple of Raspberry Pi Picos and a PySimpleGUI app to control everything from Windows. Coding up a windows application to be the front-end to my tools is very easy for me to do using PySimpleGUI.

That’s reason enough for me to keep working to clean up the ecosystem and keep it running well.

License & Copyright
-------------------

Copyright 2018-2026 PySimpleGUI. All rights reserved.

Licensed under LGPL3.
