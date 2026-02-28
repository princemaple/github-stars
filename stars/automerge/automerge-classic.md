---
project: automerge-classic
stars: 14722
description: A JSON-like data structure (a CRDT) that can be modified concurrently by different users, and merged again automatically.
url: https://github.com/automerge/automerge-classic
---

Deprecation Notice
------------------

Automerge now has a shiny new implementation at https://github.com/automerge/automerge. This repository is the original pure javascript implementation. All development effort has shifted to the new implementation which is written in Rust and so can easily be ported to other platforms.

Original Readme
---------------

💬 Join the Automerge Slack community

Automerge is a library of data structures for building collaborative applications in JavaScript.

Please see automerge.org for documentation.

For a set of extensible examples in TypeScript, see automerge-repo

Setup
-----

If you're using npm, `npm install automerge`. If you're using yarn, `yarn add automerge`. Then you can import it with `require('automerge')` as in the example below (or `import * as Automerge from 'automerge'` if using ES2015 or TypeScript).

Otherwise, clone this repository, and then you can use the following commands:

-   `yarn install` — installs dependencies.
-   `yarn test` — runs the test suite in Node.
-   `yarn run browsertest` — runs the test suite in web browsers.
-   `yarn build` — creates a bundled JS file `dist/automerge.js` for web browsers. It includes the dependencies and is set up so that you can load through a script tag.

Meta
----

Copyright 2017–2021, the Automerge contributors. Released under the terms of the MIT license (see `LICENSE`).
