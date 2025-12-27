---
project: goby
stars: 3513
description: Goby - Yet another programming language written in Go
url: https://github.com/goby-lang/goby
---

**Goby** is an object-oriented interpreter language deeply inspired by **Ruby** as well as its core implementation by 100% pure **Go**. Moreover, it has standard libraries to provide several features such as the Plugin system. Note that we do not intend to reproduce whole of the honorable works of Ruby syntax/implementation/libraries.

The expected use case for Goby would be backend development. With this goal, it equips (but not limited to) the following features:

-   thread/channel mechanism powered by Go's goroutine
-   Builtin database library (currently only support PostgreSQL adapter)
-   JSON support
-   Plugin system that can load existing Go packages dynamically (Only for Linux and MacOS right now)
-   Accessing Go objects from Goby directly

> Note: Goby had formerly been known as "Rooby", which was renamed in May 2017.

Table of contents
-----------------

-   Demo screen and sample Goby app
-   Structure
-   3D Visualization
-   Features
-   Installation
-   Usage
-   Sample codes
-   Documentation
-   Joining to Goby
-   Maintainers
-   Supporters
-   References

Demo screen and sample Goby app
-------------------------------

Click to see the demo below (powered by asciinema and GIPHY).

**New!** Check-out our sample app built with Goby. Source code is also available here.

Structure
---------

3D Visualization
----------------

A 3D visualization of Goby codebase, powered by GoCity

Major Features
--------------

-   Plugin system
    -   Allows using Go libraries (packages) dynamically
    -   Allows calling Go's methods from Goby directly (only on Linux for now)
-   Builtin multi-threaded server and DB library
-   REPL (run `goby -i`)

Here's a complete list of all the features.

Installation
------------

Confirmed Goby runs on Mac OS and Linux for now. Try Goby on Windows and let us know the result.

### A. Via Homebrew (binary installation for Mac OS)

**Note: Please check the latest release before installing Goby via Homebrew**

```
brew tap goby-lang/goby
brew install goby
```

In the case, `$GOBY_ROOT` is automatically configured.

### B. From Source

Try this if you'd like to contribute Goby! Skip 1 if you already have Golang in your environment.

1.  Prepare Golang environment
    -   Install Golang >= 1.14
    -   Make sure `$GOPATH` in your shell's config file( like .bashrc) is correct
    -   Add your `$GOPATH/bin` to `$PATH`
    -   Add `export GO111MODULE=on` to your shell profile
2.  Run `go get github.com/goby-lang/goby`
3.  Set the Goby project's exact root path `$GOBY_ROOT` manually, which should be:

```
$GOPATH/src/github.com/goby-lang/goby
```

### C. Installation on a Linux system

In order to install Go, Goby and PostgreSQL on a Linux system, see the wiki page.

### Verifying Goby installation

1.  Run `goby -v` to see the version.
2.  Run `goby -i` to launch igb REPL.
3.  Type `require "uri"` in igb.

FYI: You can just run `brew test goby` to check Homebrew installation.

**If you have any issue installing Goby, please let us know via GitHub issues**

### Using Docker

Goby has official docker image as well. You can try the Plugin System using docker.

Syntax highlighting
-------------------

The Goby syntax is currently a subset of the Ruby one, with an exception (`get_block`), therefore, it's possible to attain syntax highlighting on any platform/editor by simply switching it to Ruby for the currently opened file.

### Sublime Text 3

Sublime Text 3 users can use the `Only Goby` package, by typing the following in a terminal:

git clone git@github.com:saveriomiroddi/only-goby-for-sublime-text "$HOME/.config/sublime-text-3/Packages/only-goby-for-sublime-text"

this will automatically apply the Goby syntax highlighting to the `.gb` files.

### Vim

Vim users can use the `vim-goby-syntax-highlighting` definition, by typing the following in a terminal:

mkdir -p "$HOME/.vim/syntax"
wget -O "$HOME/.vim/syntax/goby.vim" https://raw.githubusercontent.com/saveriomiroddi/vim-goby-syntax-highlighting/master/goby.vim
echo 'au BufNewFile,BufRead \*.gb    setf goby' \>> "$HOME/.vim/filetype.vim"

this will automatically apply the Goby syntax highlighting to the `.gb` files.

### SpaceVim

SpaceVim users can load the `lang#goby` layer by adding following configuration:

\[\[layers\]\]
  name = "lang#goby"

Sample codes
------------

-   Built a stack data structure using Goby
-   Running a "Hello World" app with built in server library
-   Sending request using http library
-   Running load test on blocking server (This shows `Goby`'s simple server is very performant and can handle requests concurrently)
-   One thousand threads

More sample Goby codes can be found in sample directory.

Joining to Goby
---------------

**Join us on Slack!**

See the guideline.

Maintainers
-----------

-   @st0012
-   @hachi8833
-   @saveriomiroddi

Designer
--------

-   steward379

Supporters
----------

### Sponsors

### Powered by

-   JetBrains Goland IDE

**Supporting Goby by sending your first PR! See contribution guideline**

References
----------

The followings are the essential resources to create Goby; I highly recommend you to check them first if you'd be interested in building your own languages:

-   Write An Interpreter In Go
-   Nand2Tetris II
-   Ruby under a microscope
-   YARV's instruction table
