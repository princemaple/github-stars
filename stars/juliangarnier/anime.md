---
project: anime
stars: 67738
description: JavaScript animation engine
url: https://github.com/juliangarnier/anime
---

Anime.js
========

**_Anime.js_ is a fast, multipurpose and lightweight JavaScript animation library with a simple, yet powerful API.  
It works with CSS properties, SVG, DOM attributes and JavaScript Objects.**

Sponsors
--------

Anime.js is 100% free and is only made possible with the help of our sponsors. Help the project become sustainable by sponsoring us on GitHub Sponsors.

### Platinum sponsors

### Silver sponsors

Get featured here by becoming a GitHub Sponsor.

Usage
-----

Anime.js V4 works by importing ES modules like so:

import {
  animate,
  stagger,
} from 'animejs';

animate('.square', {
  x: 320,
  rotate: { from: \-180 },
  duration: 1250,
  delay: stagger(65, { from: 'center' }),
  ease: 'inOutQuint',
  loop: true,
  alternate: true
});

V4 Documentation
----------------

The full documentation is available here.

V3 Migration guide
------------------

You can find the v3 to v4 migration guide here.

NPM development scripts
-----------------------

First, run `npm i` to install all the necessary packages. Then, execute the following scripts with `npm run <script>`.

script

action

`dev`

Watches for changes in `src/**/*.js`, bundles the ESM version to `lib/` and creates type declarations in `types/`

`dev:test`

Runs `dev` and `test:browser` concurrently

`build`

Bundles ESM / UMD / CJS / IIFE versions to `lib/` and creates type declarations in `types/`

`test:browser`

Starts a local server and runs all browser-related tests

`test:node`

Starts Node-related tests

`open:examples`

Starts a local server to browse the examples locally

© Julian Garnier | MIT License
