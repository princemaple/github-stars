---
project: embed-pdf-viewer
stars: 4583
description: A PDF viewer that seamlessly integrates with any JavaScript project
url: https://github.com/embedpdf/embed-pdf-viewer
---

EmbedPDF
========

Open-source PDF viewer for JavaScript
=====================================

EmbedPDF is a PDF viewer you add to any web app, in plain HTML, React, Vue, Svelte or Angular. People read, annotate, fill in, sign and redact PDFs right in the browser, on a PDF engine built on PDFium that runs as WebAssembly. Apache-2.0 licensed.

-   **Docs:** www.embedpdf.com/docs
-   **Live demo:** www.embedpdf.com/demo

Three ways to use it
--------------------

What it is

Start here

**Viewer**

A complete viewer, toolbar and panels included: one tag, made yours with plain config

Quick start

**Headless components**

The same plugins without the UI, to build your own viewer in React, Vue, Svelte or Angular

Headless

**Engine**

Open, read, change and render PDFs from your own code, in the browser or in Node

Engine

Quick start
-----------

In plain HTML, from a CDN:

<embedpdf-viewer src\="https://www.embedpdf.com/pdfs/welcome.pdf" style\="height: 100vh"\></embedpdf-viewer\>

<script
  type\="module"
  src\="https://cdn.jsdelivr.net/npm/@embedpdf/viewer@3/dist/embedpdf.js"
\></script\>

In React:

npm install @embedpdf/viewer-react

import { PDFViewer } from '@embedpdf/viewer-react';

export function App() {
  return <PDFViewer src\="https://www.embedpdf.com/pdfs/welcome.pdf" style\={{ height: '100vh' }} />;
}

Vue, Svelte and Angular work the same way, with `@embedpdf/viewer-vue`, `@embedpdf/viewer-svelte` and `@embedpdf/viewer-angular`. The Quick start then shows how to use your colors, leave features out and add your own buttons.

Features
--------

Every feature is on from the start, and each one can be turned off:

-   **Annotations:** highlight, underline and strike out text; draw; notes, text boxes and callouts; shapes; stamps; comments with replies.
-   **Forms and signatures:** fill in forms and build them; draw, type or upload a signature, sign fields, and check signatures.
-   **Redaction:** mark text and areas, then remove them from the file for good.
-   **Measurement:** distances, perimeters and areas at the drawing's scale.
-   **Pages:** rotate, move, insert, duplicate and delete pages, each step undoable.
-   **Reading:** search, text selection, thumbnails, the outline, attachments, snapshots, printing, downloading, and several documents in tabs.
-   **Any language:** Hebrew and Arabic work with no setup, right to left, and other scripts with a font of your own.

Each feature is a plugin. The headless packages let you take only the ones you need.

EmbedPDF and CloudPDF
---------------------

EmbedPDF is made by CloudPDF. Both are the same viewer, added to your app as a package. What differs is the engine behind it:

EmbedPDF

CloudPDF

**The engine**

Local: runs in the browser, as WebAssembly

Cloud: runs on a CloudPDF server

**The PDF**

Opened on the user's computer

Stays on the server; the viewer gets the pages it shows

**The packages**

`@embedpdf/viewer`, `@embedpdf/viewer-react`, …

`@cloudpdf/viewer`, `@cloudpdf/viewer-react`, …

**License**

Open source

Open source, except the server (see License)

Keeping the file on a server is what CloudPDF adds:

-   **Access control.** Your backend gives each user a short-lived token for one document, saying what they may do: view, annotate, fill in, sign or download. The server checks every call against it. Someone who may only view never receives the file, only its pages.
-   **Collaboration.** Annotations and comments are saved on the server as people make them, and everyone with the document open sees each other's changes live, with who made them.
-   **Sharing.** Public links that can expire, ask for a passphrase or work only on your sites, with one shared copy for everyone or a copy of their own for each visitor.
-   **Large files.** The first page shows at once, without downloading the whole PDF.

CloudPDF runs hosted, or on your own servers with its Docker image or Helm chart. See the CloudPDF docs.

Sponsors
--------

We are grateful for the support of our sponsors!

### Silver Sponsors

  

### Bronze Sponsors

           

Contributing
------------

We love contributions! To get started, read our contributing guide and jump into the GitHub discussions.

License
-------

### EmbedPDF: open source

EmbedPDF is completely open source, under the Apache License 2.0: the viewer, the engine and every plugin, every `@embedpdf/*` package. Use it, change it and ship it in any app, commercial or not. (The handwriting fonts in `@embedpdf/default-signature-fonts` keep their own open license, the SIL Open Font License.)

### CloudPDF: open source, except the server

Everything you build with CloudPDF is open source under the Apache License 2.0 too: the viewer (`@cloudpdf/viewer` and its framework packages), the engine (`@cloudpdf/engine`) and the SDK (`@cloudpdf/sdk`).

The one exception is the server itself, `cloudpdf/server`. It is the product CloudPDF sells, so it is **Fair Source**, under the Fair Core License (FCL-1.0-ALv2):

-   **You can read, copy and change its source** for the purposes the FCL permits.
-   **Running it needs a CloudPDF license:** a license key for a connected server, or a signed certificate for an air-gapped one.
-   **The license check stays in place.** You may not move, change, disable or get around it, turn on protected features without a valid license, or remove protected features.
-   **No competing use**, as the FCL defines it: a product or service that substitutes for CloudPDF or offers the same or substantially similar functionality.
-   **Each release becomes Apache 2.0** two years after it is published.

LICENSING.md has the full map, including the websites' content and trademarks.

Third-party licenses
--------------------

The engine is powered by EmbedPDF Runtime, our fork of PDFium, which is licensed under the Apache License, Version 2.0. PDFium is a Google project; EmbedPDF is not affiliated with or endorsed by Google.
