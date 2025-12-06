---
project: manim
stars: 35883
description: A community-maintained Python framework for creating mathematical animations. 
url: https://github.com/ManimCommunity/manim
---

  
  
  
  
_An animation engine for explanatory math videos_

* * *

Manim is an animation engine for explanatory math videos. It's used to create precise animations programmatically, as demonstrated in the videos of 3Blue1Brown.

Note

The community edition of Manim (ManimCE) is a version maintained and developed by the community. It was forked from 3b1b/manim, a tool originally created and open-sourced by Grant Sanderson, also creator of the 3Blue1Brown educational math videos. While Grant Sanderson continues to maintain his own repository, we recommend this version for its continued development, improved features, enhanced documentation, and more active community-driven maintenance. If you would like to study how Grant makes his videos, head over to his repository (3b1b/manim).

Table of Contents:
------------------

-   Installation
-   Usage
-   Documentation
-   Docker
-   Help with Manim
-   Contributing
-   License

Installation
------------

Caution

These instructions are for the community version _only_. Trying to use these instructions to install 3b1b/manim or instructions there to install this version will cause problems. Read this and decide which version you wish to install, then only follow the instructions for your desired version.

Manim requires a few dependencies that must be installed prior to using it. If you want to try it out first before installing it locally, you can do so in our online Jupyter environment.

For local installation, please visit the Documentation and follow the appropriate instructions for your operating system.

Usage
-----

Manim is an extremely versatile package. The following is an example `Scene` you can construct:

from manim import \*

class SquareToCircle(Scene):
    def construct(self):
        circle \= Circle()
        square \= Square()
        square.flip(RIGHT)
        square.rotate(\-3 \* TAU / 8)
        circle.set\_fill(PINK, opacity\=0.5)

        self.play(Create(square))
        self.play(Transform(square, circle))
        self.play(FadeOut(square))

In order to view the output of this scene, save the code in a file called `example.py`. Then, run the following in a terminal window:

manim -p -ql example.py SquareToCircle

You should see your native video player program pop up and play a simple scene in which a square is transformed into a circle. You may find some more simple examples within this GitHub repository. You can also visit the official gallery for more advanced examples.

Manim also ships with a `%%manim` IPython magic which allows to use it conveniently in JupyterLab (as well as classic Jupyter) notebooks. See the corresponding documentation for some guidance and try it out online.

Command line arguments
----------------------

The general usage of Manim is as follows:

The `-p` flag in the command above is for previewing, meaning the video file will automatically open when it is done rendering. The `-ql` flag is for a faster rendering at a lower quality.

Some other useful flags include:

-   `-s` to skip to the end and just show the final frame.
-   `-n <number>` to skip ahead to the `n`'th animation of a scene.
-   `-f` show the file in the file browser.

For a thorough list of command line arguments, visit the documentation.

Documentation
-------------

Documentation is in progress at ReadTheDocs.

Docker
------

The community also maintains a docker image (`manimcommunity/manim`), which can be found on DockerHub. Instructions on how to install and use it can be found in our documentation.

Help with Manim
---------------

If you need help installing or using Manim, feel free to reach out to our Discord Server or Reddit Community. If you would like to submit a bug report or feature request, please open an issue.

Contributing
------------

Contributions to Manim are always welcome. In particular, there is a dire need for tests and documentation. For contribution guidelines, please see the documentation.

However, please note that Manim is currently undergoing a major refactor. In general, contributions implementing new features will not be accepted in this period. The contribution guide may become outdated quickly; we highly recommend joining our Discord server to discuss any potential contributions and keep up to date with the latest developments.

Most developers on the project use `uv` for management. You'll want to have uv installed and available in your environment. Learn more about `uv` at its documentation and find out how to install manim with uv at the manim dev-installation guide in the manim documentation.

How to Cite Manim
-----------------

We acknowledge the importance of good software to support research, and we note that research becomes more valuable when it is communicated effectively. To demonstrate the value of Manim, we ask that you cite Manim in your work. Currently, the best way to cite Manim is to go to our repository page (if you aren't already) and click the "cite this repository" button on the right sidebar. This will generate a citation in your preferred format, and will also integrate well with citation managers.

Code of Conduct
---------------

Our full code of conduct, and how we enforce it, can be read on our website.

License
-------

The software is double-licensed under the MIT license, with copyright by 3blue1brown LLC (see LICENSE), and copyright by Manim Community Developers (see LICENSE.community).
