---
project: theBeamBook
stars: 4057
description: A description of the Erlang Runtime System ERTS and the virtual Machine BEAM.
url: https://github.com/happi/theBeamBook
---

The BEAM Book
=============

The first-edition manuscript is in book.asciidoc, with examples in code/. Read it online or download the PDF.

Second-edition examples and companion notes are also available.

Build the first edition
-----------------------

Install Ruby, Bundler, Erlang, Java, Graphviz and rsync, then run:

bundle install
make pdf-a4 html

Outputs are `beam-book-a4.pdf` and `site/index.html`. Use `make pdf-publish` for the print PDF and `make epub` for EPUB.

Licence
-------

The first edition and code examples use CC BY 4.0. The second-edition companion carries its own copyright and licence notices. Existing third-party notices apply to their respective files.
