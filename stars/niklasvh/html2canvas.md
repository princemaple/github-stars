---
project: html2canvas
stars: 31384
description: Screenshots with JavaScript
url: https://github.com/niklasvh/html2canvas
---

html2canvas
===========

Homepage | Downloads | Questions

#### JavaScript HTML renderer

The script allows you to take "screenshots" of webpages or parts of it, directly on the users browser. The screenshot is based on the DOM and as such may not be 100% accurate to the real representation as it does not make an actual screenshot, but builds the screenshot based on the information available on the page.

### How does it work?

The script renders the current page as a canvas image, by reading the DOM and the different styles applied to the elements.

It does **not require any rendering from the server**, as the whole image is created on the **client's browser**. However, as it is heavily dependent on the browser, this library is _not suitable_ to be used in nodejs. It doesn't magically circumvent any browser content policy restrictions either, so rendering cross-origin content will require a proxy to get the content to the same origin.

The script is still in a **very experimental state**, so I don't recommend using it in a production environment nor start building applications with it yet, as there will be still major changes made.

### Browser compatibility

The library should work fine on the following browsers (with `Promise` polyfill):

-   Firefox 3.5+
-   Google Chrome
-   Opera 12+
-   IE9+
-   Safari 6+

As each CSS property needs to be manually built to be supported, there are a number of properties that are not yet supported.

### Usage

The html2canvas library utilizes `Promise`s and expects them to be available in the global context. If you wish to support older browsers that do not natively support `Promise`s, please include a polyfill such as es6-promise before including `html2canvas`.

To render an `element` with html2canvas, simply call: `html2canvas(element[, options]);`

The function returns a Promise containing the `<canvas>` element. Simply add a promise fulfillment handler to the promise using `then`:

```
html2canvas(document.body).then(function(canvas) {
    document.body.appendChild(canvas);
});
```

### Building

You can download ready builds here.

Clone git repository:

```
$ git clone git://github.com/niklasvh/html2canvas.git
```

Install dependencies:

```
$ npm install
```

Build browser bundle

```
$ npm run build
```

### Examples

For more information and examples, please visit the homepage or try the test console.

### Contributing

If you wish to contribute to the project, please send the pull requests to the develop branch. Before submitting any changes, try and test that the changes work with all the support browsers. If some CSS property isn't supported or is incomplete, please create appropriate tests for it as well before submitting any code changes.
