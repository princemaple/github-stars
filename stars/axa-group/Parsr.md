---
project: Parsr
stars: 6167
description: Transforms PDF, Documents and Images into Enriched Structured Data
url: https://github.com/axa-group/Parsr
---

  

_Turn your documents into data!_
--------------------------------

Français | Portuguese | Spanish | 中文

-   **Parsr**, is a minimal-footprint document (**image, pdf, docx, eml**) cleaning, parsing and extraction toolchain which generates readily available, organized and usable data in **JSON, Markdown (MD), CSV/Pandas DF** or **TXT** formats.
    
-   It provides analysts, data scientists and developers with clean structured and label-enriched information set for ready-to-use applications ranging from data entry and document analysts automation, archival, and many others.
    
-   Currently, Parsr can perform: document cleaning, _hierarchy regeneration_ (words, lines, paragraphs), detection of _headings, tables, lists, table of contents, page numbers, headers/footers, links_, and others. Check out all the features.
    

Table of Contents
=================

-   Table of Contents
-   Getting Started
    -   Installation
    -   Usage
-   Documentation
-   Contribute
-   Third Party Licenses
-   License

Getting Started
===============

Installation
------------

_\-- The advanced installation guide is available here --_

The quickest way to install and run the Parsr API is through the docker image:

docker pull axarev/parsr

If you also wish to install the GUI for sending documents and visualising results:

docker pull axarev/parsr-ui-localhost

Note: Parsr can also be installed bare-metal (not via Docker containers), the procedure for which is documented in the installation guide.

Usage
-----

_\-- The advanced usage guide is available here --_

To run the API, issue:

docker run -p 3001:3001 axarev/parsr

which will launch it on http://localhost:3001.  
Consult the documentation on the usage of the API.

1.  To access the **python** client to Parsr API, issue:
    
    pip install parsr-client
    
    To sample the **Jupyter Notebook**, using the python client, head over to the jupyter demo.
    

1.  To use the GUI tool (the API needs to already be running), issue:
    
    docker run -t -p 8080:80 axarev/parsr-ui-localhost:latest
    
    Then, access it through http://localhost:8080.

Refer to the Configuration documentation to interpret the configurable options in the GUI viewer.

The API based usage and the command line usage are documented in the advanced usage guide.

Documentation
=============

All documentation files can be found here.

Contribute
==========

Please refer to the contribution guidelines.

Third Party Licenses
====================

Third Party Libraries licenses for its dependencies:

1.  **QPDF**: Apache http://qpdf.sourceforge.net
2.  **ImageMagick**: Apache 2.0 https://imagemagick.org/script/license.php
3.  **Pdfminer.six**: MIT https://github.com/pdfminer/pdfminer.six/blob/master/LICENSE
4.  **PDF.js**: Apache 2.0 https://github.com/mozilla/pdf.js
5.  **Tesseract**: Apache 2.0 https://github.com/tesseract-ocr/tesseract
6.  **Camelot**: MIT https://github.com/camelot-dev/camelot
7.  **MuPDF** (Optional dependency): AGPL https://mupdf.com/license.html
8.  **Pandoc** (Optional dependency): GPL https://github.com/jgm/pandoc

License
=======

Copyright 2020 AXA Group Operations S.A.  
Licensed under the Apache 2.0 license (see the LICENSE file).
