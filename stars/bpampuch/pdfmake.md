---
project: pdfmake
stars: 12359
description: Client/server side PDF printing in pure JavaScript
url: https://github.com/bpampuch/pdfmake
---

pdfmake
=======

PDF document generation library for Node.js and browsers, written in pure JavaScript.

Check out the playground and examples.

Features
--------

-   line wrapping
-   text alignment (left, right, centered, justified)
-   numbered and bulleted lists
-   tables and columns:
    -   auto/fixed/star-sized widths
    -   column spans and row spans
    -   headers automatically repeated after a page break
    -   snaking columns (newspaper-style layout where content flows from column to column)
-   images, SVG and vector graphics
-   QR codes
-   convenient styling and style inheritance
-   page headers and footers:
    -   static or dynamic content
    -   access to current page number and page count
-   background layer
-   watermarks
-   page dimensions and orientations
-   margins
-   document sections
-   custom page breaks
-   font embedding
-   support for complex, multi-level (nested) structures
-   table of contents
-   document outlines (bookmarks)
-   external links and internal navigation
-   file attachments
-   encryption, password protection and document permissions
-   PDF/A support
-   helper methods for opening/printing/downloading the generated PDF
-   PDF metadata (e.g. author, subject)

Installation
------------

Install with npm:

npm install pdfmake

Quick start
-----------

### Node.js

Save the following as `example.js`:

const pdfmake \= require('pdfmake');
const Roboto \= require('pdfmake/fonts/Roboto');

pdfmake.addFonts(Roboto);

const docDefinition \= {
	content: \['Hello from pdfmake!'\]
};

pdfmake.createPdf(docDefinition).write('document.pdf').catch(console.error);

Run `node example.js` to create `document.pdf` in the current directory.

### Browser

Save the following as `index.html` next to your `node_modules` directory and open it in a browser.

<!doctype html\>
<meta charset\="utf-8"\>
<script src\="node\_modules/pdfmake/build/pdfmake.min.js"\></script\>
<script src\="node\_modules/pdfmake/build/vfs\_fonts.js"\></script\>

<button onclick\="pdfMake.createPdf(docDefinition).download('document.pdf').catch(console.error)"\>Download PDF</button\>
<script\>
	const docDefinition \= {
		content: \['Hello from pdfmake!'\]
	};
</script\>

Documentation
-------------

See the documentation for usage and API details.

Documentation improvements are welcome in the documentation repository.

Building from source
--------------------

git clone https://github.com/bpampuch/pdfmake.git
cd pdfmake
npm install
npm run build

License
-------

MIT

Authors
-------

-   @bpampuch (founder)
-   @liborm85

pdfmake is based on PDFKit.

Thanks to all contributors.
