---
project: zx
stars: 44936
description: A tool for writing better scripts
url: https://github.com/google/zx
---

zx
==

#!/usr/bin/env zx

await $\`cat package.json | grep name\`

const branch \= await $\`git branch --show-current\`
await $\`dep deploy --branch=${branch}\`

await Promise.all(\[
  $\`sleep 1; echo 1\`,
  $\`sleep 2; echo 2\`,
  $\`sleep 3; echo 3\`,
\])

const name \= 'foo bar'
await $\`mkdir /tmp/${name}\`

Bash is great, but when it comes to writing more complex scripts, many people prefer a more convenient programming language. JavaScript is a perfect choice, but the Node.js standard library requires additional hassle before using. No compromise, take the best of both. The `zx` package provides useful cross-platform wrappers around `child_process`, escapes arguments and gives sensible defaults.

Install
-------

npm install zx

All setup options: zx/setup. See also **zx@lite**.

Usage
-----

-   Documentation at google.github.io/zx/
-   Code examples

Compatibility
-------------

-   Linux, macOS, or Windows
-   JavaScript Runtime:
    -   Node.js >= 12.17.0
    -   Bun >= 1.0.0
    -   Deno 1.x, 2.x
    -   GraalVM Node.js
-   Some kind of bash or PowerShell
-   Both CJS or ESM modules in JS or TS

See also
--------

-   srf — a tiny, dependency-free static file server for Node.js
-   fx — a JSON cli tool and terminal JSON viewer

License
-------

Apache-2.0

Disclaimer: _This is not an officially supported Google product._
