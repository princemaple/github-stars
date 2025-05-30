---
project: theBeamBook
stars: 3206
description: A description of the Erlang Runtime System ERTS and the virtual Machine BEAM.
url: https://github.com/happi/theBeamBook
---

The BEAM Book
=============

This is an attempt to document the internals of the Erlang runtime system and the Erlang virtual machine known as the BEAM.

You can read or download the book as a PDF from the latest stable release or online as a webpage.

The book is written in AsciiDoc and most of it can be read directly from source on GitHub in your browser. To read the book online just open the file book.asciidoc.

You can also read it as an Github IO page.

Contributing
------------

The plan is to make this book project into a collaboration effort so that we can get a complete documentation of the Erlang runtime system as soon as possible. Please feel free to contribute since this work is far from done.

You can contribute by raising an issue, comment on open issues or create a branch with a fix or an addition.

Note that the book is released under a Creative Commons license (see below) and anything you contribute will also be included under that license.

The chapters in the book can be in one of four states:

1.  Placeholder, basically only the title and perhaps an outline of the chapter is done. If you are interested in writing the chapter or parts of the chapter grab the corresponding issue and start writing.
2.  First draft, most of the text is in place but more editing is needed. Feel free to comment, focusing on missing content, hard to read passages, the order of sections within the chapter, diagrams or pictures needed, and plain errors.
3.  Final draft, spelling and other errors probably still need fixing.
4.  Done (for OTP version X), if things changes in later versions of Erlang OTP the chapter will need an update.

(Not all chapters are yet marked in this way.)

### Style guide

There are several ways to use AsciiDoc and some constructs work better in some environments or for some targets.

The priority of the AsciiDoc code in this project is that it renders nicely for the following targets in the following order:

1.  The PDF target
2.  The HTML target
3.  View directly on GitHub

We will try to come up with specific guides for which AsciiDoc constructs to use and add them here as we discover what works and what doesn't work.

#### Comments in AsciiDoc

Each chapter should begin with a comment about the status of the chapter. This should be one of 'Placeholder', 'First Draft', 'Final Draft', or 'Done (for Erlang X.X)'. There can also be a link to an issue describing what is needed to bring the chapter to the next level.

A comment in the code starts with '//'.

#### Linking to OTP/Erlang source code

When referring to the source code of Erlang/OTP please add a link to a tagged version (not to master) of the code on GitHub, as in:

* * *

 link:https://github.com/erlang/otp/blob/OTP-19.1/erts/emulator/beam/erl\_time.h\[erl\_time.h\]

* * *

#### Directory structure and build

Try to keep the root directory clean.

Put each chapter in a separate .asciidoc file in the chapters directory. Use underscores "\_" to separate words in chapter names but try to use just one-word file names for the chapters.

Put code used in a chapter in code/CHAPTERNAME\_chapter/src, and add an include of the code in ap-code\_listings.asciidoc.

Put images in the images directory.

#### How to tag chapters, sections, figures

The following is not yet done consistently so please feel free to contribute by fixing tags in the current version.

Chapter tags should start with 'CH-'. Words in a tag are separated by underscores '\_'.

Part tags should start with 'P-'.

Section tags should start with 'SEC-'.

Figure tags should start with 'FIG-'.

Appendix tags should start with 'AP-'.

Code listing tags (in the appendix) should start with 'LISTING-'.

### Process

If you find something you do not understand or which is incorrect please raise an issue in the issue tracker.

If you find spelling or formatting errors feel free to fix them and just make a pull request.

For larger rewrites check the status of the chapter and check the issues to see if someone is likely to be working on that chapter right now. If someone else is working on the chapter try to contact that person before doing a major rewrite. Otherwise either just go ahead and do the rewrite and do a pull request or start by opening an issue declaring what you intend to do.

Building the PDF locally from source
------------------------------------

The project contains a Makefile which will let you build your own PDF from the source, provided that you have all the needed tools installed. Just running the command

make

will build the file `beam-book.pdf` in the top directory as well as the HTML version under the `site` directory.

We assume that you already have an Erlang installation of your choice for running examples etc. Apart from that, see below for what you need in order to build the book.

### Docker

You can build the project locally via Docker without having to install any addtional software, by first building the docker image. Assuming you have Docker installed, run:

make docker-build

And then you can build the book by running

make docker

(Note: On Linux, the resulting files will be created with User ID 1000, regardless of what your current user ID is outside Docker. This is due to how Docker integrates with the file system.)

#### Devcontainers in the IDE

If you use VSCode or any other editor that has support for Devcontainers, this repository contains a configuration that can be used out of the box. By opening the project in the dev container, you get a shell inside the container with all the tools pre-installed and with access to the project files so that all you need to do is run `make`.

For a tutorial on devcontainers, see Introduction to Dev Containers, Decvontainer setup, and Devcontainers, UIDs and file permissions.

If you prefer to build natively rather than use Docker, see the following sections depending on your system.

### Linux

The following should work on a Debian based system, such as Ubuntu:

1.  `apt install git rsync wget curl make`
2.  `apt install ruby ruby-dev default-jre`
3.  `apt install asciidoctor graphviz`
4.  `gem install asciidoctor-pdf asciidoctor-diagram rouge`
5.  `make`

### Mac OSX

#### Using Homebrew

1.  `brew install asciidoctor graphviz wget ditaa`
2.  `gem install asciidoctor-pdf asciidoctor-diagram rouge`
3.  `make`

#### Manual installation

1.  Install asciidoc
2.  Install asciidoctor-pdf
3.  Install asciidoctor-diagram
4.  Install ditaa
5.  Install graphviz
6.  Install rouge
7.  Install wget
8.  `make`

License
-------

_The Erlang Runtime System_ by Erik Stenman is licensed under a Creative Commons Attribution 4.0 International License. Based on a work at https://github.com/happi/theBeamBook. A complete copy of the license can be found here.

A short and personal history of the book
========================================

I, Erik Stenman (Happi), started writing this book back in 2013. At first I was thinking of self publishing the book on my blog, but since English isn't my native language I felt I needed help by a good editor.

I managed to get a deal with O'Reilly and started converting my outline to their build process. My original plan was for a very long and thorough book, which the editor felt would get few readers. I started cutting my content and tried to write more of a tutorial than a manual. Unfortunately progress was slow and pre-sales was even slower and the publisher cancelled the book in 2015.

I managed to get a new deal with Pragmatic and started converting my content to their build system and rewriting the book according to the more pragmatic style of the new publisher, cutting down the content even further. The series editor also wanted me to fit the book into the Elixir series and I tried to add more Elixir examples. I did not really manage to make it into an Elixir book and also my progress was still slow, which led to another cancellation of the book early 2017.

Now I had three repositories with three different book building systems with three different outlines of the book. In the end I more or less went back to the original longer book outline and the original AsciiDoc build system. I started a new repository in a private GitHub account and started pulling in content from the three different versions.

Then on April 7 2017 I opened the repository to the public to share it with some students. I didn't think anyone else would notice and I was not planning to release the book for real yet since the repo currently just contains bits and pieces from the different versions of the book.

There was more interest than I had expected though and fortunately also several who where willing to contribute. From now on the book is a collaborative effort to document the Erlang runtime system ERTS and the Erlang virtual machine BEAM, and it is released with a Creative Commons license (see above).

Watch this space for further news and to see the whole book take shape.

\-- Erik Stenman aka Happi
