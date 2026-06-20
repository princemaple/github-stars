---
project: pdfcpu
stars: 8680
description: PDF tooling for Go and the command line.
url: https://github.com/pdfcpu/pdfcpu
---

pdfcpu: PDF tooling for Go and the command line
===============================================

pdfcpu provides a Go API and command-line tools for working with PDF files.

It supports PDFs across versions. PDF 2.0 (ISO-32000-2) validation support is basic and continuously improving.

* * *

Installation
------------

### CLI

👉 CLI Installation instructions

### Go API

👉 API Installation instructions

* * *

Usage
-----

### CLI

Validate a PDF:

```
pdfcpu validate input.pdf
```

Merge two PDFs:

```
pdfcpu merge merged.pdf in1.pdf in2.pdf
```

### Go API

See API documentation for usage examples.

* * *

Features
--------

-   Validate, optimize, split, trim, and merge PDFs
-   Extract and manipulate images, fonts, and metadata
-   Encrypt and decrypt PDFs
-   Resize and rotate pages
-   Add and remove stamps and watermarks
-   Validate signature integrity, report signature evidence, and remove signatures
-   Manage attachments and more...

In Action
---------

Common operations and examples:

           
  
           
  
 

* * *

Command Set
-----------

Complete list of supported commands:

annotations

attachments

booklet

bookmarks

boxes

certificates

change owner password

change user password

collect

config

create

crop

cut

decrypt

encrypt

extract

fonts

form

grid

images

import

info

keywords

merge

ndown

nup

optimize

pagelayout

pagemode

pages

permissions

portfolio

poster

properties

resize

rotate

signatures

split

stamp

trim

validate

viewerpref

watermark

zoom

* * *

Motivation
----------

pdfcpu aims to provide comprehensive PDF processing capabilities implemented in Go.

It focuses on correctness, robustness and independence from external dependencies.

* * *

Focus
-----

-   comprehensive PDF processing functionality
-   minimal external dependencies
-   predictable and stable behavior

* * *

Documentation
-------------

-   Project documentation: https://pdfcpu.io
-   Changelog: https://pdfcpu.io/changelog

### CLI

-   Command help: `pdfcpu [command] --help`

### Go API

-   Package documentation: https://pkg.go.dev/github.com/pdfcpu/pdfcpu
    
-   API documentation: https://pkg.go.dev/github.com/pdfcpu/pdfcpu/pkg/api
    
-   Examples:
    
    -   https://github.com/pdfcpu/pdfcpu/tree/master/pkg/api/test
    -   https://github.com/pdfcpu/pdfcpu/tree/master/pkg/samples

* * *

Contributing
------------

Contributions are welcome.

-   Report bugs or propose changes via issues
-   Discuss ideas on the discussion board
-   For PRs, please open an issue or discussion first

### Guidelines

-   Base your work on the latest commit
-   Include verbose output (`pdfcpu cmd -vv ...`) and a sample PDF when reporting issues
-   Please sign your commits

### Reporting crashes

Crashes may occur due to the wide variety of PDF producers and formats in use, including older or non-compliant files. In many cases this is related to validation issues or edge cases in the parser.

Even with relaxed validation, some files cannot be processed. These cases are essential for improving pdfcpu by extending validation and handling additional real-world PDFs.

If you encounter a crash, please report it.

Start by validating the file using the CLI:

pdfcpu validate -vv <file.pdf\>

Include in your report:

-   the command used
-   verbose output (`-vv`)
-   a sanitized sample PDF

If validation crashes for a PDF that opens in Adobe Reader or macOS Preview, it is likely we can extend relaxed validation and provide a fix.

If the file cannot be opened by both Adobe Reader and macOS Preview, we cannot support it.

Please include a sample PDF to reproduce the issue whenever possible.

* * *

Contributors
------------

Thanks 💚 to all contributors:

  
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

  
**mdmcconnell**

  
**Bradley Erickson**

  
**doronbehar**

  
**joeyave**

  
**Zhenbang Wei**

  
**HarishTeens**

* * *

Code of Conduct
---------------

This project is released with a Contributor Code of Conduct. By participating, you agree to abide by its terms.

* * *

Disclaimer
----------

Use of pdfcpu assumes compliance with all applicable copyrights for any processed PDF content, including embedded resources such as fonts and images.

Gopher artwork by Renee French

* * *

License
-------

Apache License 2.0

* * *
