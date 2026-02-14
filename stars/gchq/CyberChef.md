---
project: CyberChef
stars: 34042
description: The Cyber Swiss Army Knife - a web app for encryption, encoding, compression and data analysis
url: https://github.com/gchq/CyberChef
---

CyberChef
=========

#### _The Cyber Swiss Army Knife_

CyberChef is a simple, intuitive web app for carrying out all manner of "cyber" operations within a web browser. These operations include simple encoding like XOR and Base64, more complex encryption like AES, DES and Blowfish, creating binary and hexdumps, compression and decompression of data, calculating hashes and checksums, IPv6 and X.509 parsing, changing character encodings, and much more.

The tool is designed to enable both technical and non-technical analysts to manipulate data in complex ways without having to deal with complex tools or algorithms. It was conceived, designed, built and incrementally improved by an analyst in their 10% innovation time over several years.

Live demo
---------

CyberChef is still under active development. As a result, it shouldn't be considered a finished product. There is still testing and bug fixing to do, new features to be added and additional documentation to write. Please contribute!

Cryptographic operations in CyberChef should not be relied upon to provide security in any situation. No guarantee is offered for their correctness.

A live demo can be found here - have fun!

Running Locally with Docker
---------------------------

**Prerequisites**

-   Docker
    -   Docker Desktop must be open and running on your machine

#### Option 1: Build the Docker Image Yourself

1.  Build the docker image

docker build --tag cyberchef --ulimit nofile=10000 .

1.  Run the docker container

docker run -it -p 8080:80 cyberchef

1.  Navigate to `http://localhost:8080` in your browser

#### Option 2: Use the pre-built Docker Image

If you prefer to skip the build process, you can use the pre-built image

docker run -it -p 8080:80 ghcr.io/gchq/cyberchef:latest

Just like before, navigate to `http://localhost:8080` in your browser.

This image is built and published through our GitHub Workflows

How it works
------------

There are four main areas in CyberChef:

1.  The **input** box in the top right, where you can paste, type or drag the text or file you want to operate on.
2.  The **output** box in the bottom right, where the outcome of your processing will be displayed.
3.  The **operations** list on the far left, where you can find all the operations that CyberChef is capable of in categorised lists, or by searching.
4.  The **recipe** area in the middle, where you can drag the operations that you want to use and specify arguments and options.

You can use as many operations as you like in simple or complex ways. Some examples are as follows:

-   Decode a Base64-encoded string
-   Convert a date and time to a different time zone
-   Parse a Teredo IPv6 address
-   Convert data from a hexdump, then decompress
-   Decrypt and disassemble shellcode
-   Display multiple timestamps as full dates
-   Carry out different operations on data of different types
-   Use parts of the input as arguments to operations
-   Perform AES decryption, extracting the IV from the beginning of the cipher stream
-   Automagically detect several layers of nested encoding

Features
--------

-   Drag and drop
    -   Operations can be dragged in and out of the recipe list, or reorganised.
    -   Files up to 2GB can be dragged over the input box to load them directly into the browser.
-   Auto Bake
    -   Whenever you modify the input or the recipe, CyberChef will automatically "bake" for you and produce the output immediately.
    -   This can be turned off and operated manually if it is affecting performance (if the input is very large, for instance).
-   Automated encoding detection
    -   CyberChef uses a number of techniques to attempt to automatically detect which encodings your data is under. If it finds a suitable operation that make sense of your data, it displays the 'magic' icon in the Output field which you can click to decode your data.
-   Breakpoints
    -   You can set breakpoints on any operation in your recipe to pause execution before running it.
    -   You can also step through the recipe one operation at a time to see what the data looks like at each stage.
-   Save and load recipes
    -   If you come up with an awesome recipe that you know you’ll want to use again, just click "Save recipe" and add it to your local storage. It'll be waiting for you next time you visit CyberChef.
    -   You can also copy the URL, which includes your recipe and input, to easily share it with others.
-   Search
    -   If you know the name of the operation you want or a word associated with it, start typing it into the search field and any matching operations will immediately be shown.
-   Highlighting
    -   When you highlight text in the input or output, the offset and length values will be displayed and, if possible, the corresponding data will be highlighted in the output or input respectively (example: highlight the word 'question' in the input to see where it appears in the output).
-   Save to file and load from file
    -   You can save the output to a file at any time or load a file by dragging and dropping it into the input field. Files up to around 2GB are supported (depending on your browser), however, some operations may take a very long time to run over this much data.
-   CyberChef is entirely client-side
    -   It should be noted that none of your recipe configuration or input (either text or files) is ever sent to the CyberChef web server - all processing is carried out within your browser, on your own computer.
    -   Due to this feature, CyberChef can be downloaded and run locally. You can use the link in the top left corner of the app to download a full copy of CyberChef and drop it into a virtual machine, share it with other people, or host it in a closed network.

Deep linking
------------

By manipulating CyberChef's URL hash, you can change the initial settings with which the page opens. The format is `https://gchq.github.io/CyberChef/#recipe=Operation()&input=...`

Supported arguments are `recipe`, `input` (encoded in Base64), and `theme`.

Browser support
---------------

CyberChef is built to support

-   Google Chrome 50+
-   Mozilla Firefox 38+

Node.js support
---------------

CyberChef is built to fully support Node.js `v16`. For more information, see the "Node API" wiki page

Contributing
------------

Contributing a new operation to CyberChef is super easy! The quickstart script will walk you through the process. If you can write basic JavaScript, you can write a CyberChef operation.

An installation walkthrough, how-to guides for adding new operations and themes, descriptions of the repository structure, available data types and coding conventions can all be found in the "Contributing" wiki page.

-   Push your changes to your fork.
-   Submit a pull request. If you are doing this for the first time, you will be prompted to sign the GCHQ Contributor Licence Agreement via the CLA assistant on the pull request. This will also ask whether you are happy for GCHQ to contact you about a token of thanks for your contribution, or about job opportunities at GCHQ.

Licencing
---------

CyberChef is released under the Apache 2.0 Licence and is covered by Crown Copyright.
