---
project: llama-ocr
stars: 2425
description: Document to Markdown OCR library with Llama 3.2 vision
url: https://github.com/Nutlope/llama-ocr
---

Llama OCR
=========

An npm library to run OCR for free with Llama 3.2 Vision.

* * *

Installation
------------

`npm i llama-ocr`

Usage
-----

import { ocr } from "llama-ocr";

const markdown \= await ocr({
  filePath: "./trader-joes-receipt.jpg", // path to your image (soon PDF!)
  apiKey: process.env.TOGETHER\_API\_KEY, // Together AI API key
});

Hosted Demo
-----------

We have a hosted demo at LlamaOCR.com where you can try it out!

How it works
------------

This library uses the free Llama 3.2 endpoint from Together AI to parse images and return markdown. Paid endpoints for Llama 3.2 11B and Llama 3.2 90B are also available for faster performance and higher rate limits.

You can control this with the `model` option which is set to `Llama-3.2-90B-Vision` by default but can also accept `free` or `Llama-3.2-11B-Vision`.

Roadmap
-------

-   Add support for local images OCR
-   Add support for remote images OCR
-   Add support for single page PDFs
-   Add support for multi-page PDFs OCR (take screenshots of PDF & feed to vision model)
-   Add support for JSON output in addition to markdown

Credit
------

This project was inspired by Zerox. Go check them out!
