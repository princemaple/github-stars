---
project: simple-icons
stars: 24057
description: SVG icons for popular brands
url: https://github.com/simple-icons/simple-icons
---

### Simple Icons

Over 3300 SVG icons for popular brands. See them all on one page at SimpleIcons.org. Contributions, corrections & requests can be made on GitHub.

  

Usage
-----

Important

We ask that all users read our legal disclaimer before using icons from Simple Icons.

### General Usage

Icons can be downloaded as SVGs directly from simpleicons.org - simply click the download button of the icon you want, and the download will start automatically.

### CDN Usage

Icons can be served from a CDN such as jsDelivr or unpkg. Simply use the `simple-icons` npm package and specify a version in the URL like the following:

<img height\="32" width\="32" src\="https://cdn.jsdelivr.net/npm/simple-icons@v16/icons/\[ICON SLUG\].svg" />
<img height\="32" width\="32" src\="https://unpkg.com/simple-icons@v16/icons/\[ICON SLUG\].svg" />

Where `[ICON SLUG]` is replaced by the slug of the icon you want to use, for example:

<img height\="32" width\="32" src\="https://cdn.jsdelivr.net/npm/simple-icons@v16/icons/simpleicons.svg" />
<img height\="32" width\="32" src\="https://unpkg.com/simple-icons@v16/icons/simpleicons.svg" />

These examples use the latest major version. This means you won't receive any updates following the next major release. You can use `@latest` instead to receive updates indefinitely. However, this will result in a `404` error if the icon is removed.

#### CDN with colors

We also provide a CDN service which allows you to use colors.

<img height\="32" width\="32" src\="https://cdn.simpleicons.org/\[ICON SLUG\]" />
<img height\="32" width\="32" src\="https://cdn.simpleicons.org/\[ICON SLUG\]/\[COLOR\]" />
<img height\="32" width\="32" src\="https://cdn.simpleicons.org/\[ICON SLUG\]/\[COLOR\]/\[DARK\_MODE\_COLOR\]" />

Where `[COLOR]` is optional, and can be replaced by the hex colors or CSS keywords of the icon you want to use. The color is defaulted to the HEX color of the icon shown in simpleicons.org website. `[DARK_MODE_COLOR]` is used for dark mode. The CSS prefers-color-scheme will be used when a value is specified. For example:

<img height\="32" width\="32" src\="https://cdn.simpleicons.org/simpleicons" />
<img height\="32" width\="32" src\="https://cdn.simpleicons.org/simpleicons/gray" />
<img height\="32" width\="32" src\="https://cdn.simpleicons.org/simpleicons/hotpink" />
<img height\="32" width\="32" src\="https://cdn.simpleicons.org/simpleicons/0cf" />
<img height\="32" width\="32" src\="https://cdn.simpleicons.org/simpleicons/0cf9" />
<img height\="32" width\="32" src\="https://cdn.simpleicons.org/simpleicons/00ccff" />
<img height\="32" width\="32" src\="https://cdn.simpleicons.org/simpleicons/00ccff99" />
<img height\="32" width\="32" src\="https://cdn.simpleicons.org/simpleicons/orange/pink" />
<img height\="32" width\="32" src\="https://cdn.simpleicons.org/simpleicons/\_/eee" />
<img height\="32" width\="32" src\="https://cdn.simpleicons.org/simpleicons/eee/\_" />

You can use a `viewbox=auto` parameter to get a auto-sized viewbox. This is useful if you want all icons rendered with consistent size:

<img height\="20" src\="https://cdn.simpleicons.org/github?viewbox=auto" />
<img height\="20" src\="https://cdn.simpleicons.org/simpleicons?viewbox=auto" />
<img height\="20" src\="https://cdn.simpleicons.org/awesomelists?viewbox=auto" />

### Node Usage

The icons are also available through our npm package. To install, simply run:

npm install simple-icons

All icons are imported from a single file, where `[ICON SLUG]` is replaced by a capitalized slug. We highly recommend using a bundler that can tree shake such as webpack to remove the unused icon code:

// Import a specific icon by its slug as:
// import { si\[ICON SLUG\] } from 'simple-icons'

// For example:
// use import/esm to allow tree shaking
import {siSimpleicons} from 'simple-icons';
// or with require/cjs
const {siSimpleicons} \= require('simple-icons');

It will return an icon object:

console.log(siSimpleicons);

/\*
{
    title: 'Simple Icons',
    slug: 'simpleicons',
    hex: '111111',
    source: 'https://simpleicons.org/',
    svg: '<svg role="img" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">...</svg>',
    path: 'M12 12v-1.5c-2.484 ...',
    guidelines: 'https://simpleicons.org/styleguide',
    license: {
        type: '...',
        url: 'https://example.com/'
    }
}
NOTE: the \`guidelines\` entry will be \`undefined\` if we do not yet have guidelines for the icon.
NOTE: the \`license\` entry will be \`undefined\` if we do not yet have license data for the icon.
\*/

If you need to iterate over all icons, use:

import \* as icons from 'simple-icons';

#### TypeScript Usage

Type definitions are bundled with the package.

import type {SimpleIcon} from 'simple-icons';

### PHP Usage

The icons are also available through our Packagist package. To install, simply run:

composer require simple-icons/simple-icons

The package can then be used as follows, where `[ICON SLUG]` is replaced by a slug:

<?php
// Import a specific icon by its slug as:
echo file\_get\_contents('path/to/package/icons/\[ICON SLUG\].svg');

// For example:
echo file\_get\_contents('path/to/package/icons/simpleicons.svg');

// <svg role="img" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">...</svg>
?>

### Font Usage

See simple-icons-font to learn how to use our font distribution.

Third-Party Extensions
----------------------

The below are known extensions to third-party tools.

Extension

Author

Blender add-on

@mondeja

Boxy SVG library

@Jarek

Drawio library

@mondeja

Figma plugin

@LitoMore

Jekyll plugin

@pirafrank

Kando icon theme

@Schneegans

Miro app

@LitoMore

Raycast extension

@LitoMore

Stream Deck icon pack

@mackenly

Typst package

@cscnk52

Webflow app

@diegoliv

Maintain an extension? Submit a PR to include it in the list above.

Third-Party Libraries
---------------------

The below are known third-party libraries for use in your own projects. We only keep items in the list that are at least up to date with our previous major version.

Library

Author

License

Simple Icons

Angular package

@gridatek

Astro package

@Aviortheking

Blazor Nuget package

@TimeWarpEngineering

Flutter package

@jlnrrg

Framer component

@LitoMore

Hugo module

@foo-dogsquared

Java library

@silentsoft

Kirby plugin

@runxel

LaTeX package

@ineshbose

Laravel package

@adrian-ub

Python wheel

@carstencodes

React package

@wootsbot

Ruby gem

@thepew

Rust crate

@cscnk52

Svelte package

@wootsbot

Vue 3 package

@wyatt-herkamp

Maintain a library? Submit a PR to include it in the list above.

Contribute
----------

Information describing how to contribute can be found in the file CONTRIBUTING.md

Contributors
------------
