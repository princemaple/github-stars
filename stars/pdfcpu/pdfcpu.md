---
project: pdfcpu
stars: 8475
description: A PDF processor written in Go.
url: https://github.com/pdfcpu/pdfcpu
---

pdfcpu: a Go PDF processor and CLI
==================================

pdfcpu is a PDF processing library written in Go that supports encryption and offers both an API and a command-line interface (CLI). It is compatible with all PDF versions with basic support and ongoing improvement for PDF 2.0 (ISO-32000-2).

Motivation
----------

This is an effort to build a comprehensive PDF processing library from the ground up written in Go. Over time pdfcpu aims to support the standard range of PDF processing features and also any interesting use cases that may present themselves along the way.

           
  
           
  
 

Focus
-----

The primary emphasis is on providing robust assistance for batch processing and scripting through a comprehensive command-line interface. Simultaneously, pdfcpu aims to simplify the integration of PDF processing into your Go-based backend system by offering a versatile set of commands.

Command Set
-----------

-   annotations
-   attachments
-   booklet
-   bookmarks
-   boxes
-   certificates
-   change owner password
-   change user password
-   collect
-   config
-   create
-   crop
-   cut
-   decrypt
-   encrypt
-   extract
-   fonts
-   form
-   grid
-   images
-   import
-   info
-   keywords
-   merge
-   ndown
-   nup
-   optimize
-   pagelayout
-   pagemode
-   pages
-   permissions
-   portfolio
-   poster
-   properties
-   resize
-   rotate
-   signatures
-   split
-   stamp
-   trim
-   validate
-   viewerpref
-   watermark
-   zoom

Documentation
-------------

-   pdfcpu.io
-   API tests
-   API samples
-   CLI usage: `$ pdfcpu help cmd`

### GoDoc

-   pdfcpu package
-   pdfcpu API
-   pdfcpu CLI

Reminder
--------

-   Always make sure your work is based on the latest commit!  
    
-   pdfcpu is still _Alpha_ - bugfixes are committed on the fly and will be mentioned in the next release notes.  
    
-   Follow pdfcpu for news and release announcements.
-   For quick questions or discussions get in touch on the Gopher Slack in the #pdfcpu channel.

Demo Screencast
---------------

(using older version with a smaller command set)

Installation
------------

### Download

Get the latest binary here.

### Using Go Modules

```
$ git clone https://github.com/pdfcpu/pdfcpu
$ cd pdfcpu/cmd/pdfcpu
$ go install
$ pdfcpu version
```

or directly through Go install:

```
$ go install github.com/pdfcpu/pdfcpu/cmd/pdfcpu@latest
```

### Using Homebrew (macOS)

```
$ brew install pdfcpu
$ pdfcpu version
```

### Using DNF/YUM (Fedora)

```
$ sudo dnf install golang-github-pdfcpu
$ pdfcpu version
```

### Run in a Docker container

$ docker build -t pdfcpu .
# mount current host folder into container as /app to process files in the local host folder
$ docker run -it -v "$(pwd)":/app pdfcpu validate a.pdf

Contributing
------------

### What

-   Please create an issue if you find a bug or want to propose a change.
-   Feature requests - always welcome!
-   Bug fixes - always welcome!
-   PRs - let's discuss first or create an issue.
-   pdfcpu is stable but still _Alpha_ and occasionally undergoing heavy changes.

### How

-   The pdfcpu discussion board is open! Please engage in any form helpful for the community.
-   If you want to report a bug please attach the _very verbose_ (`pdfcpu cmd -vv ...`) output and ideally a test PDF that you can share.
-   Always make sure your contribution is based on the latest commit.
-   Please sign your commits.

### Reporting Crashes

Unfortunately crashes do happen :( For the majority of the cases this is due to a diverse pool of PDF Writers out there and millions of PDF files using different versions waiting to be processed by pdfcpu. Sometimes these PDFs were written more than 20(!) years ago. Often there is an issue with validation - sometimes a bug in the parser. Many times even using relaxed validation with pdfcpu does not work. In these cases we need to extend relaxed validation and for this we are relying on your help. By reporting crashes you are helping to improve the stability of pdfcpu. If you happen to crash on any pdfcpu operation be it on the command line or in your Go backend these are the steps to report this:

Regardless of the pdfcpu operation, please start using the pdfcpu command line to validate your file:

$ pdfcpu validate -v &\> crash.log

or to produce very verbose output

$ pdfcpu validate -vv &\> crash.log

will produce what's needed to investigate a crash. Then open an issue and post `crash.log` or its contents. Ideally post a test PDF you can share to reproduce this. You can also email to hhrutter@gmail.com or if you prefer Slack you can get in touch on the Gopher slack #pdfcpu channel.

If processing your PDF with pdfcpu crashes during validation and can be opened by Adobe Reader and Mac Preview chances are we can extend relaxed validation and provide a fix. If the file in question cannot be opened by both Adobe Reader and Mac Preview we cannot help you!

Contributors
------------

Thanks 💚 goes to these wonderful people:

  
**Horst Rutter**

  
**haldyr**

  
**Vyacheslav**

  
**Erik Unger**

  
**Richard Wilkes**

  
**minenok-tutu**

  
**Mateusz Burniak**

  
**Dmitry Harnitski**

  
**ryarnyah**

  
**Sam Giffney**

  
**Carlos Eduardo Witte**

  
**minusworld**

  
**Witold Konior**

  
**joonas.fi**

  
**Henrik Reinstädtler**

  
**VMorozov-wh**

  
**Benoit KUGLER**

  
**Adam Greenhall**

  
**moritamori**

  
**JanBaryla**

  
**TheDiscordian**

  
**Rafael Garcia Argente**

  
**truyet**

  
**Christian Nicola**

  
**Benjamin Krill**

  
**Peter Wyatt**

  
**Kroum Tzanev**

  
**Stefan Huber**

  
**Juan Iscar**

  
**Eng Zer Jun**

  
**Dmitry Ivanov**

  
**Rene Kaufmann**

  
**Christian Heusel**

  
**Chris**

  
**Lukasz Czaplinski**

  
**Joel Silva Schutz**

  
**semvis123**

  
**guangwu**

  
**Yoshiki Nakagawa**

  
**Steve van Loben Sels**

  
**Yaofu**

  
**vsenko**

  
**Alexis Hildebrandt**

  
**Sivukhin Nikita**

  
**Joachim Bauch**

  
**kalimit**

  
**Andreas Erhard**

  
**Matsumoto Toshi**

  
**Carl Wilson**

  
**LNAhri**

  
**vishal**

  
**Andreas Deininger**

  
**Robert Raines**

  
**Frank Anderson**

  
**Sven Lilienthal**

  
**Florian Kinder**

Code of Conduct
---------------

Please note that this project is released with a Contributor Code of Conduct. By participating in this project you agree to abide by its terms.

Disclaimer
----------

Usage of pdfcpu assumes you know about and respect all copyrights of any PDF content you may be processing. This applies to the PDF files as such, their content and in particular all embedded resources like font files or images. Credit goes to Renee French for creating our beloved Gopher.

License
-------

Apache-2.0
