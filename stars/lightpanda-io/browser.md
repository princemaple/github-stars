---
project: browser
stars: 10398
description: Lightpanda: the headless browser designed for AI and automation
url: https://github.com/lightpanda-io/browser
---

Lightpanda Browser
==================

lightpanda.io

Lightpanda is the open-source browser made for headless usage:

-   Javascript execution
-   Support of Web APIs (partial, WIP)
-   Compatible with Playwright1, Puppeteer, chromedp through CDP

Fast web automation for AI agents, LLM training, scraping and testing:

-   Ultra-low memory footprint (9x less than Chrome)
-   Exceptionally fast execution (11x faster than Chrome)
-   Instant startup

 

_Puppeteer requesting 100 pages from a local website on a AWS EC2 m5.large instance. See benchmark details._

Quick start
-----------

### Install

**Install from the nightly builds**

You can download the last binary from the nightly builds for Linux x86\_64 and MacOS aarch64.

_For Linux_

curl -L -o lightpanda https://github.com/lightpanda-io/browser/releases/download/nightly/lightpanda-x86\_64-linux && \\
chmod a+x ./lightpanda

_For MacOS_

curl -L -o lightpanda https://github.com/lightpanda-io/browser/releases/download/nightly/lightpanda-aarch64-macos && \\
chmod a+x ./lightpanda

_For Windows + WSL2_

The Lightpanda browser is compatible to run on windows inside WSL. Follow the Linux instruction for installation from a WSL terminal. It is recommended to install clients like Puppeteer on the Windows host.

**Install from Docker**

Lightpanda provides official Docker images for both Linux amd64 and arm64 architectures. The following command fetches the Docker image and starts a new container exposing Lightpanda's CDP server on port `9222`.

docker run -d --name lightpanda -p 9222:9222 lightpanda/browser:nightly

### Dump a URL

./lightpanda fetch --dump https://lightpanda.io

info(browser): GET https://lightpanda.io/ http.Status.ok
info(browser): fetch script https://api.website.lightpanda.io/js/script.js: http.Status.ok
info(browser): eval remote https://api.website.lightpanda.io/js/script.js: TypeError: Cannot read properties of undefined (reading 'pushState')
<!DOCTYPE html>

### Start a CDP server

./lightpanda serve --host 127.0.0.1 --port 9222

info(websocket): starting blocking worker to listen on 127.0.0.1:9222
info(server): accepting new conn...

Once the CDP server started, you can run a Puppeteer script by configuring the `browserWSEndpoint`.

'use strict'

import puppeteer from 'puppeteer-core';

// use browserWSEndpoint to pass the Lightpanda's CDP server address.
const browser \= await puppeteer.connect({
  browserWSEndpoint: "ws://127.0.0.1:9222",
});

// The rest of your script remains the same.
const context \= await browser.createBrowserContext();
const page \= await context.newPage();

// Dump all the links from the page.
await page.goto('https://wikipedia.com/');

const links \= await page.evaluate(() \=> {
  return Array.from(document.querySelectorAll('a')).map(row \=> {
    return row.getAttribute('href');
  });
});

console.log(links);

await page.close();
await context.close();
await browser.disconnect();

### Telemetry

By default, Lightpanda collects and sends usage telemetry. This can be disabled by setting an environment variable `LIGHTPANDA_DISABLE_TELEMETRY=true`. You can read Lightpanda's privacy policy at: https://lightpanda.io/privacy-policy.

Status
------

Lightpanda is in Beta and currently a work in progress. Stability and coverage are improving and many websites now work. You may still encounter errors or crashes. Please open an issue with specifics if so.

Here are the key features we have implemented:

-   HTTP loader (based on Libcurl)
-   HTML parser and DOM tree (based on Netsurf libs)
-   Javascript support (v8)
-   DOM APIs
-   Ajax
    -   XHR API
    -   Fetch API (polyfill)
-   DOM dump
-   CDP/websockets server
-   Click
-   Input form
-   Cookies
-   Custom HTTP headers
-   Proxy support
-   Network interception

NOTE: There are hundreds of Web APIs. Developing a browser (even just for headless mode) is a huge task. Coverage will increase over time.

You can also follow the progress of our Javascript support in our dedicated zig-js-runtime project.

Build from sources
------------------

### Prerequisites

Lightpanda is written with Zig `0.15.2`. You have to install it with the right version in order to build the project.

Lightpanda also depends on zig-js-runtime (with v8), Libcurl, Netsurf libs and Mimalloc.

To be able to build the v8 engine for zig-js-runtime, you have to install some libs:

For Debian/Ubuntu based Linux:

```
sudo apt install xz-utils \
    python3 ca-certificates git \
    pkg-config libglib2.0-dev \
    gperf libexpat1-dev unzip rsync \
    cmake clang
```

For systems with Nix, you can use the devShell:

```
nix develop
```

For MacOS, you need Xcode and the following pacakges from homebrew:

```
brew install cmake pkgconf
```

### Install and build dependencies

#### All in one build

You can run `make install` to install deps all in one (or `make install-dev` if you need the development versions).

Be aware that the build task is very long and cpu consuming, as you will build from sources all dependencies, including the v8 Javascript engine.

#### Step by step build dependency

The project uses git submodules for dependencies.

To init or update the submodules in the `vendor/` directory:

```
make install-submodule
```

**iconv**

libiconv is an internationalization library used by Netsurf.

```
make install-libiconv
```

**Netsurf libs**

Netsurf libs are used for HTML parsing and DOM tree generation.

```
make install-netsurf
```

For dev env, use `make install-netsurf-dev`.

**Mimalloc**

Mimalloc is used as a C memory allocator.

```
make install-mimalloc
```

For dev env, use `make install-mimalloc-dev`.

Note: when Mimalloc is built in dev mode, you can dump memory stats with the env var `MIMALLOC_SHOW_STATS=1`. See https://microsoft.github.io/mimalloc/environment.html.

**v8**

First, get the tools necessary for building V8, as well as the V8 source code:

```
make get-v8
```

Next, build v8. This build task is very long and cpu consuming, as you will build v8 from sources.

```
make build-v8
```

For dev env, use `make build-v8-dev`.

Test
----

### Unit Tests

You can test Lightpanda by running `make test`.

### End to end tests

To run end to end tests, you need to clone the demo repository into `../demo` dir.

You have to install the demo's node requirements

You also need to install Go > v1.24.

```
make end2end
```

### Web Platform Tests

Lightpanda is tested against the standardized Web Platform Tests.

The relevant tests cases are committed in a dedicated repository which is fetched by the `make install-submodule` command.

All the tests cases executed are located in the `tests/wpt` sub-directory.

For reference, you can easily execute a WPT test case with your browser via wpt.live.

#### Run WPT test suite

To run all the tests:

```
make wpt
```

Or one specific test:

```
make wpt Node-childNodes.html
```

#### Add a new WPT test case

We add new relevant tests cases files when we implemented changes in Lightpanda.

To add a new test, copy the file you want from the WPT repo into the `tests/wpt` directory.

⚠️ Please keep the original directory tree structure of `tests/wpt`.

Contributing
------------

Lightpanda accepts pull requests through GitHub.

You have to sign our CLA during the pull request process otherwise we're not able to accept your contributions.

Why?
----

### Javascript execution is mandatory for the modern web

In the good old days, scraping a webpage was as easy as making an HTTP request, cURL-like. It’s not possible anymore, because Javascript is everywhere, like it or not:

-   Ajax, Single Page App, infinite loading, “click to display”, instant search, etc.
-   JS web frameworks: React, Vue, Angular & others

### Chrome is not the right tool

If we need Javascript, why not use a real web browser? Take a huge desktop application, hack it, and run it on the server. Hundreds or thousands of instances of Chrome if you use it at scale. Are you sure it’s such a good idea?

-   Heavy on RAM and CPU, expensive to run
-   Hard to package, deploy and maintain at scale
-   Bloated, lots of features are not useful in headless usage

### Lightpanda is built for performance

If we want both Javascript and performance in a true headless browser, we need to start from scratch. Not another iteration of Chromium, really from a blank page. Crazy right? But that’s what we did:

-   Not based on Chromium, Blink or WebKit
-   Low-level system programming language (Zig) with optimisations in mind
-   Opinionated: without graphical rendering

Footnotes
---------

1.  **Playwright support disclaimer:** Due to the nature of Playwright, a script that works with the current version of the browser may not function correctly with a future version. Playwright uses an intermediate JavaScript layer that selects an execution strategy based on the browser's available features. If Lightpanda adds a new Web API, Playwright may choose to execute different code for the same script. This new code path could attempt to use features that are not yet implemented. Lightpanda makes an effort to add compatibility tests, but we can't cover all scenarios. If you encounter an issue, please create a GitHub issue and include the last known working version of the script. ↩
