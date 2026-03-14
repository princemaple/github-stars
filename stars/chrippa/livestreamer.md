---
project: livestreamer
stars: 3876
description: Command-line utility that extracts streams from various services and pipes them into a video player of choice. No longer maintained, use streamlink or youtube-dl instead.
url: https://github.com/chrippa/livestreamer
---

Livestreamer
============

Overview
--------

Livestreamer is a command-line utility that pipes video streams from various services into a video player, such as VLC. The main purpose of Livestreamer is to allow the user to avoid buggy and CPU heavy flash plugins but still be able to enjoy various streamed content. There is also an API available for developers who want access to the video stream data.

-   Documentation: http://docs.livestreamer.io/
-   Issue tracker: https://github.com/chrippa/livestreamer/issues
-   PyPI: https://pypi.python.org/pypi/livestreamer
-   Discussions: https://groups.google.com/forum/#!forum/livestreamer
-   IRC: #livestreamer @ Freenode
-   Free software: Simplified BSD license

Features
--------

Livestreamer is built upon a plugin system which allows support for new services to be easily added. Currently most of the big streaming services are supported, such as:

-   Dailymotion
-   Livestream
-   Twitch
-   UStream
-   YouTube Live

... and many more. A full list of plugins currently included can be found on the Plugins page.

Quickstart
----------

The default behaviour of Livestreamer is to playback a stream in the default player (VLC).

\# pip install livestreamer
$ livestreamer twitch.tv/day9tv best
\[cli\]\[info\] Found matching plugin twitch for URL twitch.tv/day9tv
\[cli\]\[info\] Opening stream: source
\[cli\]\[info\] Starting player: vlc

For more in-depth usage and install instructions see the User guide.

Related software
----------------

Feel free to add any Livestreamer related things to the wiki.

Contributing
------------

If you wish to report a bug or contribute code, please take a look at CONTRIBUTING.rst first.
