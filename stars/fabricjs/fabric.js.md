---
project: fabric.js
stars: 31404
description: Javascript Canvas Library, SVG-to-Canvas (& canvas-to-SVG) Parser
url: https://github.com/fabricjs/fabric.js
---

Fabric.js
=========

A **simple and powerful Javascript HTML5 canvas library**.

-   **Website**
-   **Old V5 documentation**
-   **GOTCHAS**
-   **Contributing, Developing and More**

Special Thanks
--------------

Here is a section for recognition of companies or individuals that support fabricJS with a sponsorship

Atlas Cloud is a full-modal AI inference platform that gives developers a single AI API to access video generation, image generation, and LLM APIs. Instead of managing multiple vendor integrations, you connect once and get unified access to 300+ curated models across all modalities. Check out Atlas Cloud's new coding plan promotion for more budget-friendly API access：https://www.atlascloud.ai/console/coding-plan

Features
--------

-   Out of the box interactions such as scale, move, rotate, skew, group...
-   Built in shapes, controls, animations, image filters, gradients, patterns, brushes...
-   `JPG`, `PNG`, `JSON` and `SVG` i/o
-   Typed and modular
-   Unit tested
-   Security efforts

#### Supported Browsers/Environments

Context

Supported Version

Notes

Firefox

✔️

58

Safari

✔️

11

Opera

✔️

chromium based

Chrome

✔️

64

Edge

✔️

chromium based

Edge Legacy

❌

IE11

❌

Node.js

✔️

Node.js installation

Fabric.js does not use polyfills by default, or tries to keep it at minimum. the browser version we support is determined by the level of canvas api we want to use and some js syntax. While JS can be easily transpiled, canvas API can't.

Installation
------------

For new applications, install the environment-specific package:

# Browser applications
npm install @fabricjs/browser

# Node.js applications
npm install @fabricjs/node

The legacy `fabric` package remains supported for existing applications:

$ npm install fabric --save
# or use yarn
$ yarn add fabric
# or use pnpm
$ pnpm add fabric

Packages and migration
----------------------

Package

Role

`fabric`

Legacy compatibility facade. It re-exports `@fabricjs/browser`.

`@fabricjs/browser`

Preferred entrypoint for new browser applications.

`@fabricjs/node`

Preferred entrypoint for new Node.js applications. It owns the Node-specific dependencies.

`@fabricjs/core`

Shared, environment-neutral runtime used by the browser and Node packages. It is intended for advanced and shared dependencies.

Extension packages

Optional features imported individually, such as `@fabricjs/aligning-guidelines`.

Existing imports continue to work:

import { Canvas } from 'fabric';
import { StaticCanvas } from 'fabric/node';

New applications should prefer the explicit entrypoints:

import { Canvas } from '@fabricjs/browser';
import { StaticCanvas } from '@fabricjs/node';
import { AligningGuidelines } from '@fabricjs/aligning-guidelines';

The `fabric` and `fabric/node` facades share the same class identities as their corresponding workspace packages. Keep `fabric` and every `@fabricjs/*` package on matching versions; mixing mismatched versions can load separate runtimes.

`@fabricjs/core` has no Node-specific runtime dependencies, but it is not a DOM-free API. Advanced consumers using core APIs that touch DOM or canvas must provide a suitable environment implementation.

### Legacy distribution files

The ESM `fabric` and `fabric/node` entries are small compatibility facades over the workspace packages. The legacy standalone files remain available for existing usage:

-   `dist/index.js` and `dist/index.min.js` are full browser UMD builds from `@fabricjs/browser`, for `<script>` tags and `require('fabric')`.
-   `dist/index.node.cjs` is the legacy CommonJS compatibility build for `require('fabric/node')`.

New ESM applications should continue to import `@fabricjs/browser` or `@fabricjs/node` directly.

#### Browser

See browser modules for using es6 imports in the browser or use a dedicated bundler.

#### Node.js

We strongly recommend to run your applications only LTS versions of node.

Said so the minimum supported version of node is 20. We bump up the minimum version of node with a Major release only when the dependencies force us to do so.

Fabric.js depends on node-canvas for a canvas implementation (`HTMLCanvasElement` replacement) and jsdom for a `window` implementation on node. This means that you may encounter `node-canvas` limitations and bugs.

Follow these instructions to get `node-canvas` up and running.

Quick Start
-----------

// Preferred entrypoints for new applications
import { Canvas } from '@fabricjs/browser';
import { StaticCanvas } from '@fabricjs/node';

// Supported compatibility entrypoints
import { Canvas } from 'fabric';
import { StaticCanvas } from 'fabric/node';

// v5 compatibility
import { fabric } from 'fabric';

**Plain HTML**

<canvas id\="canvas" width\="300" height\="300"\></canvas\>

<script src\="https://cdn.jsdelivr.net/npm/fabric@6.4.3/dist/index.js"\></script\>
<script\>
  const canvas \= new fabric.Canvas('canvas');
  const rect \= new fabric.Rect({
    top: 100,
    left: 100,
    width: 60,
    height: 70,
    fill: 'red',
  });
  canvas.add(rect);
</script\>

**React.js**

import React, { useEffect, useRef } from 'react';
import \* as fabric from 'fabric'; // v6
import { fabric } from 'fabric'; // v5

export const FabricJSCanvas \= () \=> {
  const canvasEl \= useRef<HTMLCanvasElement\>(null);
  useEffect(() \=> {
    const options \= { ... };
    const canvas \= new fabric.Canvas(canvasEl.current, options);
    // make the fabric.Canvas instance available to your app
    updateCanvasContext(canvas);
    return () \=> {
      updateCanvasContext(null);
      canvas.dispose();
    }
  }, \[\]);

  return <canvas width\="300" height\="300" ref\={canvasEl}/>;
};

**Node.js**

import http from 'http';
import \* as fabric from 'fabric/node'; // v6
import { fabric } from 'fabric'; // v5

const port \= 8080;

http
  .createServer((req, res) \=> {
    const canvas \= new fabric.Canvas(null, { width: 100, height: 100 });
    const rect \= new fabric.Rect({ width: 20, height: 50, fill: '#ff0000' });
    const text \= new fabric.Text('fabric.js', { fill: 'blue', fontSize: 24 });
    canvas.add(rect, text);
    canvas.renderAll();
    if (req.url \=== '/download') {
      res.setHeader('Content-Type', 'image/png');
      res.setHeader('Content-Disposition', 'attachment; filename="fabric.png"');
      canvas.createPNGStream().pipe(res);
    } else if (req.url \=== '/view') {
      canvas.createPNGStream().pipe(res);
    } else {
      const imageData \= canvas.toDataURL();
      res.writeHead(200, '', { 'Content-Type': 'text/html' });
      res.write(\`<img src="${imageData}" />\`);
      res.end();
    }
  })
  .listen(port, (err) \=> {
    if (err) throw err;
    console.log(
      \`> Ready on http://localhost:${port}, http://localhost:${port}/view, http://localhost:${port}/download\`,
    );
  });

See our ready to use templates.

* * *

Other Solutions
---------------

Project

Description

Three.js

3D graphics

PixiJS

WebGL renderer

Konva

Similar features

html-to-image

HTML to image/canvas

More Resources
--------------

-   Demos on `fabricjs.com`
-   Fabric.js on `Twitter`
-   Fabric.js on `CodeTriage`
-   Fabric.js on `Stack Overflow`
-   Fabric.js on `jsfiddle`
-   Fabric.js on `Codepen.io`

Credits
-------

-   kangax
-   asturur on `Twitter`
-   ShaMan123
-   melchiar
-   Ernest Delgado for the original idea of manipulating images on canvas
-   Maxim "hakunin" Chernyak for ideas, and help with various parts of the library throughout its life
-   Sergey Nisnevich for help with geometry logic
-   Stefan Kienzle for help with bugs, features, documentation, GitHub issues
-   Shutterstock for the time and resources invested in using and improving Fabric.js
-   and all the other contributors
