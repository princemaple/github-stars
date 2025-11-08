---
project: qart.js
stars: 3190
description: Generate artistic QR code. 🎨
url: https://github.com/kciter/qart.js
---

qart.js
=======

  
Merges Pictures and QR Codes for Artistic QR Codes.  

Glance At
---------

https://kciter.github.io/qart.js/

Installation
------------

### NPM

```
$ npm install qartjs
```

or clone this repository and copy `qart.min.js` to your project.

### CDN

<script src\="https://cdnjs.cloudflare.com/ajax/libs/qartjs/1.0.2/qart.min.js"\></script\>

Usage
-----

### In the browser

<script src\="../dist/qart.min.js"\></script\>
<script\>
  // directly appending canvas to the document
  new QArt({
    value: value,
    imagePath: './example.png',
    filter: filter,
    size: 195
	}).make(document.getElementById('qart'));

	// using callback
	new QArt({
      value: value,
      imagePath: './example.png',
      filter: filter,
      size: 195
  	}).make(function (canvas) {
  	  document.getElementById('qart').appendChild(canvas)
  	});
</script\>

### With ES6

import QArt from 'qartjs';
const qart \= new QArt({
  value: value,
  imagePath: './example.png',
  filter: filter,
  size: 195
});

// directly appending canvas to the document
qart.make(document.getElementById('qart'))

// using callback
qart.make((canvas) \=> {
  document.getElementById('qart').appendChild(canvas);
});

### With React

This is a simple implementation of QArt as React Component. react-qart

### With Angular.JS

There is a directive available for using qart.js in Angular.js: angular-qart

### With Vue 2.x

There is a directive available for using qart.js in Vue.js 2.x : vue-qart

Options
-------

Field

Type

Description

Default

value

String

The data of the QR code.

_Required_

imagePath

String

The path of the combined image.

_Required_

filter

String

Define an image filter. `threshold` or `color`

threshold

size

Integer

Define an image size in pixels.

195

version

Integer

QRCode version (1 <= version <= 40)

10

background

CSSColor

Implement background if exist

undefinded

fillType

scale\_to\_fit/fill

Place image type(fill or scale to fit)

scale\_to\_fit

Dependency
----------

-   qrcode

Inspire
-------

-   CuteR

TODO
----

-   Server-Side Rendering.
-   CLI Command.

Donate
------

If you like this open source, you can sponsor it. 😄

LICENSE
-------

GPLv3
