---
project: pdf.js
stars: 51309
description: PDF Reader in JavaScript
url: https://github.com/mozilla/pdf.js
---

PDF.js
======

PDF.js is a Portable Document Format (PDF) viewer that is built with HTML5.

PDF.js is community-driven and supported by Mozilla. Our goal is to create a general-purpose, web standards-based platform for parsing and rendering PDFs.

Contributing
------------

PDF.js is an open source project and always looking for more contributors. To get involved, visit:

-   Issue Reporting Guide
-   Code Contribution Guide
-   Frequently Asked Questions
-   Good Beginner Bugs
-   Projects

Feel free to stop by our Matrix room for questions or guidance.

Getting Started
---------------

### Online demo

Please note that the "Modern browsers" version assumes native support for the latest JavaScript features; please also see this wiki page.

-   Modern browsers: https://mozilla.github.io/pdf.js/web/viewer.html
    
-   Older browsers: https://mozilla.github.io/pdf.js/legacy/web/viewer.html
    

### Browser Extensions

#### Firefox

PDF.js is built into version 19+ of Firefox.

#### Chrome

-   The official extension for Chrome can be installed from the Chrome Web Store. _This extension is maintained by @Rob--W._
-   Build Your Own - Get the code as explained below and issue `npx gulp chromium`. Then open Chrome, go to `Tools > Extension` and load the (unpackaged) extension from the directory `build/chromium`.

Getting the Code
----------------

To get a local copy of the current code, clone it using git:

```
$ git clone https://github.com/mozilla/pdf.js.git
$ cd pdf.js
```

Next, install Node.js via the official package or via nvm. If everything worked out, install all dependencies for PDF.js:

```
$ npm install
```

Finally, you need to start a local web server as some browsers do not allow opening PDF files using a `file://` URL. Run:

```
$ npx gulp server
```

and then you can open:

-   http://localhost:8888/web/viewer.html

Please keep in mind that this assumes the latest version of Mozilla Firefox; refer to Building PDF.js for non-development usage of the PDF.js library.

It is also possible to view all test PDF files on the right side by opening:

-   http://localhost:8888/test/pdfs/?frame

Building PDF.js
---------------

In order to bundle all `src/` files into two production scripts and build the generic viewer, run:

```
$ npx gulp generic
```

If you need to support older browsers, run:

```
$ npx gulp generic-legacy
```

This will generate `pdf.js` and `pdf.worker.js` in the `build/generic/build/` directory (respectively `build/generic-legacy/build/`). Both scripts are needed but only `pdf.js` needs to be included since `pdf.worker.js` will be loaded by `pdf.js`. The PDF.js files are large and should be minified for production.

Using PDF.js in a web application
---------------------------------

To use PDF.js in a web application you can choose to use a pre-built version of the library or to build it from source. We supply pre-built versions for usage with NPM under the `pdfjs-dist` name. For more information and examples please refer to the wiki page on this subject.

Including via a CDN
-------------------

PDF.js is hosted on several free CDNs:

-   https://www.jsdelivr.com/package/npm/pdfjs-dist
-   https://cdnjs.com/libraries/pdf.js
-   https://unpkg.com/pdfjs-dist/

Learning
--------

You can play with the PDF.js API directly from your browser using the live demos below:

-   Interactive examples

More examples can be found in the examples folder. Some of them are using the pdfjs-dist package, which can be built and installed in this repo directory via `npx gulp dist-install` command.

For an introduction to the PDF.js code, check out the presentation by our contributor Julian Viereck:

-   https://www.youtube.com/watch?v=Iv15UY-4Fg8

More learning resources can be found at:

-   https://github.com/mozilla/pdf.js/wiki/Additional-Learning-Resources

The API documentation can be found at:

-   https://mozilla.github.io/pdf.js/api/

Questions
---------

Check out our FAQs and get answers to common questions:

-   https://github.com/mozilla/pdf.js/wiki/Frequently-Asked-Questions

Talk to us on Matrix:

-   https://chat.mozilla.org/#/room/#pdfjs:mozilla.org

File an issue:

-   https://github.com/mozilla/pdf.js/issues/new/choose
