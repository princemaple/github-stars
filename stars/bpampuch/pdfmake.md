---
project: pdfmake
stars: 12151
description: Client/server side PDF printing in pure JavaScript
url: https://github.com/bpampuch/pdfmake
---

pdfmake
=======

PDF document generation library for server-side and client-side in pure JavaScript.

Check out the playground and examples.

#### This is unstable master branch for version 0.3.x, for stable use version 0.2.x see branch 0.2 or older version 0.1.x see branch 0.1.

### Features

-   line-wrapping,
-   text-alignments (left, right, centered, justified),
-   numbered and bulleted lists,
-   tables and columns
    -   auto/fixed/star-sized widths,
    -   col-spans and row-spans,
    -   headers automatically repeated in case of a page-break,
-   images and vector graphics,
-   convenient styling and style inheritance,
-   page headers and footers:
    -   static or dynamic content,
    -   access to current page number and page count,
-   background-layer,
-   page dimensions and orientations,
-   margins,
-   document sections,
-   custom page breaks,
-   font embedding,
-   support for complex, multi-level (nested) structures,
-   table of contents,
-   helper methods for opening/printing/downloading the generated PDF,
-   setting of PDF metadata (e.g. author, subject).

Documentation
-------------

**Documentation URL: https://pdfmake.github.io/docs/**

Source of documentation: https://github.com/pdfmake/docs **Improvements are welcome!**

Building from sources
---------------------

using npm:

```
git clone https://github.com/bpampuch/pdfmake.git
cd pdfmake
npm install
npm run build
```

using yarn:

```
git clone https://github.com/bpampuch/pdfmake.git
cd pdfmake
yarn
yarn run build
```

License
-------

MIT

Authors
-------

-   @bpampuch (founder)
-   @liborm85

pdfmake is based on a truly amazing library pdfkit (credits to @devongovett).

Thanks to all contributors.
