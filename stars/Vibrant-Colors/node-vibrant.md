---
project: node-vibrant
stars: 2374
description: 🎨 Extract prominent colors from an image
url: https://github.com/Vibrant-Colors/node-vibrant
---

node-vibrant
============

Extract prominent colors from an image.

-   Identical API for node.js, browser, and worker environments

Install
-------

$ npm install node-vibrant

Usage
-----

// Node
import { Vibrant } from "node-vibrant/node";
// Browser
import { Vibrant } from "node-vibrant/browser";
// Web Worker
import { Vibrant } from "node-vibrant/worker";

// Using builder
Vibrant.from("path/to/image")
	.getPalette()
	.then((palette) \=> console.log(palette));

// Using constructor
let v \= new Vibrant("path/to/image", opts);
v.getPalette().then((palette) \=> console.log(palette));

### Worker Usage

Quantization is the most time-consuming stage in `node-vibrant`. Luckily, the quantization can be run in the WebWorker to avoid freezing the UI thread.

Here's how to use this feature:

import { Vibrant, WorkerPipeline } from "node-vibrant/worker";
import PipelineWorker from "node-vibrant/worker.worker?worker";

Vibrant.use(new WorkerPipeline(PipelineWorker as never));

This requires your bundler to handle `?worker` transforms similar to how Vite does

Documentation
-------------

Docs can be seen currently in the `docs` folder. It includes reference docs and step-by-step guides.

We also have a few `examples` that you can reference for your needs.

PRs welcomed to expand either of these!

Notes
-----

### Result Consistency

The results are consistent within each user's browser instance regardless of the visible region or display size of an image, unlike the original `vibrant.js` implementation.

However, due to the nature of the HTML5 canvas element, image rendering is platform/machine-dependent. The resulting swatches may vary between browsers, Node.js versions, and between machines. See Canvas Fingerprinting.

The test specs use CIE delta E 1994 color difference to measure inconsistencies across platforms. It compares the generated color on Node.js, Chrome, Firefox, and IE11. At `quality` == 1 (no downsampling) with no filters and the results are rather consistent. Color diffs between browsers are mostly not perceptible by the human eye. Downsampling _will_ cause perceptible inconsistent results across browsers due to differences in canvas implementations.
