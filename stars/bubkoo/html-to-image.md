---
project: html-to-image
stars: 7274
description: ✂️ Generates an image from a DOM node using HTML5 canvas and SVG.
url: https://github.com/bubkoo/html-to-image
---

html-to-image
=============

**✂️ Generates an image from a DOM node using HTML5 canvas and SVG.**

Fork from dom-to-image with more maintainable code and some new features.

Install
-------

npm install --save html-to-image

Usage
-----

/\* ES6 \*/
import \* as htmlToImage from 'html-to-image';
import { toPng, toJpeg, toBlob, toPixelData, toSvg } from 'html-to-image';

/\* ES5 \*/
var htmlToImage \= require('html-to-image');

All the top level functions accept a DOM node and rendering options, and return a promise with the requested output:

-   toPng
-   toSvg
-   toJpeg
-   toBlob
-   toCanvas
-   toPixelData

### Reuse and customization (v2 branch)

The existing functions remain the shortest path for one image. Create a renderer when several captures share defaults, and create a capture when the same DOM snapshot needs several formats:

import { createRenderer } from 'html-to-image'

const renderer \= createRenderer({ pixelRatio: 2, skipFonts: false })
const capture \= await renderer.capture(document.querySelector('#receipt')!)
try {
  const png \= await capture.toPng()
  const jpeg \= await capture.toJpeg({ quality: 0.85 })
  const blob \= await capture.toBlob({ type: 'image/webp', quality: 0.8 })
  // All three outputs use the same frozen DOM snapshot and rasterization.
} finally {
  capture.dispose()
  renderer.dispose()
}

For a one-off change, `onClone` edits the detached copy before resource discovery. For reusable behavior, register a named plugin. A resource resolver returns a `Blob` to handle a URL, or `undefined` to continue to the next resolver and then normal `fetch`:

const renderer \= createRenderer({
  onClone: ({ root }) \=> {
    root.querySelectorAll('\[data-private\]').forEach((node) \=> node.remove())
  },
  plugins: \[{
    name: 'app-assets',
    resolveResource: async ({ url, kind }, { signal }) \=> {
      if (!url.startsWith('app:')) return undefined
      return fetch(\`/assets/${url.slice(4)}\`, { signal }).then((res) \=> res.blob())
    },
  }\],
})

For a change tied to each source element, use `onCloneNode(original, copy)`. It runs synchronously after that element's children, computed styles, pseudo elements and form state have been copied. Children run before parents. It runs before `onClone`, plugins, and resource embedding, so edit `copy`, not `original`. Filtered nodes and text nodes do not call it. A thrown error rejects the capture.

const png \= await htmlToImage.toPng(node, {
  onCloneNode(original, copy) {
    if (original.matches('\[data-private\]')) copy.textContent \= 'Hidden'
  },
})

`stylePropertiesForNode(source)` chooses computed CSS properties before they are copied. Its array applies to that element and its pseudo elements; `[]` copies none, and `undefined` copies the full computed style even when a global `includeStyleProperties` list exists. Inline styles already on the DOM clone remain. Include `content` if a selected pseudo element needs its generated text. The callback runs synchronously and must return an array or `undefined`.

Each capture has its own cancellation signal and resource cache. `capture.dispose()` releases the snapshot; `renderer.dispose()` cancels outstanding work and releases its captures. Per-call `signal` and `timeout` are supported. `exclude` accepts CSS selectors for subtrees. See v2 architecture for extension order, migration details, and current limits.

On WebKit, a large embedded image can be blank on the first rasterization. If affected, opt into repeated rasterization of the same snapshot:

const png \= await htmlToImage.toPng(node, { stabilizationAttempts: 3 });

This adds rendering time and is capped at 10 attempts. The default is one.

Go with the following examples.

#### toPng

Get a PNG image base64-encoded data URL and display it right away:

const node \= document.getElementById('my-node');

htmlToImage
  .toPng(node)
  .then((dataUrl) \=> {
    const img \= new Image();
    img.src \= dataUrl;
    document.body.appendChild(img);
  })
  .catch((err) \=> {
    console.error('oops, something went wrong!', err);
  });

Get a PNG image base64-encoded data URL and download it (using download):

htmlToImage
  .toPng(document.getElementById('my-node'))
  .then((dataUrl) \=> download(dataUrl, 'my-node.png'));

#### toSvg

Get an SVG data URL, but filter out all the `<i>` elements:

function filter (node) {
  return (node.tagName !== 'i');
}

htmlToImage
  .toSvg(document.getElementById('my-node'), { filter: filter })
  .then(function (dataUrl) {
    /\* do something \*/
  });

#### toJpeg

Save and download a compressed JPEG image:

htmlToImage
  .toJpeg(document.getElementById('my-node'), { quality: 0.95 })
  .then(function (dataUrl) {
    var link \= document.createElement('a');
    link.download \= 'my-image-name.jpeg';
    link.href \= dataUrl;
    link.click();
  });

#### toBlob

Get a PNG image blob and download it (using FileSaver):

htmlToImage
  .toBlob(document.getElementById('my-node'))
  .then(function (blob) {
    if (window.saveAs) {
      window.saveAs(blob, 'my-node.png');
    } else {
     FileSaver.saveAs(blob, 'my-node.png');
   }
  });

#### toCanvas

Get a HTMLCanvasElement, and display it right away:

htmlToImage
  .toCanvas(document.getElementById('my-node'))
  .then(function (canvas) {
    document.body.appendChild(canvas);
  });

#### toPixelData

Get the raw RGBA pixel data. `toPixelData` returns a `Uint8ClampedArray`; `toImageData` also provides the actual output width and height, which account for `pixelRatio` and canvas scaling:

const { width, height, data } \= await htmlToImage.toImageData(node);
for (let y \= 0; y < height; y++) {
  for (let x \= 0; x < width; x++) {
    const offset \= 4 \* (y \* width + x);
    const rgba \= data.slice(offset, offset + 4);
  }
}

#### React

import React, { useCallback, useRef } from 'react';
import { toPng } from 'html-to-image';

const App: React.FC \= () \=> {
  const ref \= useRef<HTMLDivElement\>(null)

  const onButtonClick \= useCallback(() \=> {
    if (ref.current \=== null) {
      return
    }

    toPng(ref.current, { cacheBust: true, })
      .then((dataUrl) \=> {
        const link \= document.createElement('a')
        link.download \= 'my-image-name.png'
        link.href \= dataUrl
        link.click()
      })
      .catch((err) \=> {
        console.log(err)
      })
  }, \[ref\])

  return (
    <\>
      <div ref\={ref}\>
      {/\* DOM nodes you want to convert to PNG \*/}
      </div\>
      <button onClick\={onButtonClick}\>Click me</button\>
    </\>
  )
}

Options
-------

### filter

(domNode: HTMLElement) \=> boolean

A function taking DOM node as argument. Should return true if passed node should be included in the output. Excluding node means excluding it's children as well.

You can add filter to every image function. For example,

const filter \= (node: HTMLElement) \=> {
  const exclusionClasses \= \['remove-me', 'secret-div'\];
  return !exclusionClasses.some((classname) \=> node.classList?.contains(classname));
}

htmlToImage.toJpeg(node, { quality: 0.95, filter: filter});

or

htmlToImage.toPng(node, {filter:filter})

Not called on the root node.

### backgroundColor

A string value for the background color, any valid CSS color value.

### width, height

Width and height in pixels to be applied to node before rendering.

### canvasWidth, canvasHeight

Allows to scale the canva's size including the elements inside to a given width and height (in pixels).

### style

An object whose properties to be copied to node's style before rendering. You might want to check this reference for JavaScript names of CSS properties.

### quality

A number between `0` and `1` indicating image quality (e.g. `0.92` => `92%`) of the JPEG image.

Defaults to `1.0` (`100%`)

### cacheBust

Set to true to append the current time as a query string to URL requests to enable cache busting.

Defaults to `false`

### includeQueryParams

Full URLs, including query parameters, identify resources by default. Set `false` only to opt into the legacy behavior that treats query variants as the same resource within one capture.

### imagePlaceholder

A data URL for a placeholder image that will be used when fetching an image fails.

Defaults to an empty string and will render empty areas for failed images.

### pixelRatio

The pixel ratio of the captured image. Default use the actual pixel ratio of the device. Set `1` to use as initial-scale `1` for the image.

### stabilizationAttempts

Rasterize the frozen SVG this many times and use the last result. This can help when Safari/WebKit produces a blank embedded image on an initial draw. Set an integer from `1` to `10`; the default is `1`. It does not re-read the source DOM. Extra attempts cost time and remain subject to `timeout`.

### preferredFontFormat

The format required for font embedding. This is a useful optimisation when a webfont provider specifies several different formats for fonts in the CSS, for example:

@font-face {
  name: 'proxima-nova';
  src: url("...") format("woff2"), url("...") format("woff"), url("...") format("opentype");
}

Instead of embedding each format, all formats other than the one specified will be discarded. If this option is not specified then all formats will be downloaded and embedded.

### fontEmbedCSS

When supplied, the library will skip the process of parsing and embedding webfont URLs in CSS, instead using this value. This is useful when combined with `getFontEmbedCSS()` to only perform the embedding process a single time across multiple calls to library functions.

const fontEmbedCSS \= await htmlToImage.getFontEmbedCSS(element1);
html2Image.toSVG(element1, { fontEmbedCSS });
html2Image.toSVG(element2, { fontEmbedCSS });

### skipAutoScale

When supplied, the library will skip the process of scaling extra large doms into the canvas object. You may experience loss of parts of the image if set to `true` and you are exporting a very large image.

Defaults to `false`

### type

A string indicating the image format. The default type is image/png; that type is also used if the given type isn't supported. When supplied, `toBlob` returns a blob matching the given image type and quality.

Defaults to `image/png`

### includeStyleProperties

An array of style property names. Can be used to manually specify which style properties are included when cloning nodes. This can be useful for performance-critical scenarios.

### stylePropertiesForNode

A synchronous callback that selects computed style property names for each source element and its pseudo elements. Returning `[]` copies no computed properties; returning `undefined` copies all of them, overriding `includeStyleProperties` for that element. Existing inline styles on the copy remain.

Browsers
--------

Only standard lib is currently used, but make sure your browser supports:

-   Promise
-   SVG `<foreignObject>` tag

The V2 branch runs source and built-package browser tests in Chromium, Firefox, and Playwright WebKit on every pull request. Playwright WebKit is not a real iPhone/iPad Safari device. See the test architecture and release readiness for the exact validation scope. Large DOM performance varies by browser and fixture; the measured V2 comparison is recorded here.

_Internet Explorer is not (and will not be) supported, as it does not support SVG `<foreignObject>` tag._

How it works
------------

There might some day exist (or maybe already exists?) a simple and standard way of exporting parts of the HTML to image (and then this script can only serve as an evidence of all the hoops I had to jump through in order to get such obvious thing done) but I haven't found one so far.

This library uses a feature of SVG that allows having arbitrary HTML content inside of the `<foreignObject>` tag. So, in order to render that DOM node for you, following steps are taken:

1.  Clone the original DOM node recursively
2.  Compute the style for the node and each sub-node and copy it to corresponding clone
    -   and don't forget to recreate pseudo-elements, as they are not cloned in any way, of course
3.  Embed web fonts
    -   find all the `@font-face` declarations that might represent web fonts
    -   parse file URLs, download corresponding files
    -   base64-encode and inline content as dataURLs
    -   concatenate all the processed CSS rules and put them into one `<style>` element, then attach it to the clone
4.  Embed images
    -   embed image URLs in `<img>` elements
    -   inline images used in `background` CSS property, in a fashion similar to fonts
5.  Serialize the cloned node to XML
6.  Wrap XML into the `<foreignObject>` tag, then into the SVG, then make it a data URL
7.  Optionally, to get PNG content or raw pixel data as a Uint8Array, create an Image element with the SVG as a source, and render it on an off-screen canvas, that you have also created, then read the content from the canvas
8.  Done!

Things to watch out for
-----------------------

-   If the DOM node you want to render includes a `<canvas>` element with something drawn on it, it should be handled fine, unless the canvas is tainted - in this case rendering will rather not succeed.
-   Rendering will failed on huge DOM due to the dataURI limit varies.

Contributing
------------

Please let us know how can we help. Do check out issues for bug reports or suggestions first.

To become a contributor, please follow our contributing guide.

License
-------

The scripts and documentation in this project are released under the MIT License
