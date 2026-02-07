---
project: teenyicons
stars: 1835
description: Tiny minimal 1px icons designed to fit in the smallest places.
url: https://github.com/teenyicons/teenyicons
---

Why Teenyicons?
---------------

Designed on a **15x15** grid, Teenyicons easily fit in very _small spaces_ 🤏 and maintain a _crisp look_ ✨

Preview: https://teenyicons.com/ (repo) or `npm home teenyicons`

Install
-------

npm i teenyicons
yarn add teenyicons

Usage
-----

### Inline

Copy the SVGs you wish to use from `outline` and `solid` directories inside `node_modules/teenyicons` and inline them in your HTML. Use CSS's `color` to change the SVG's color.

<svg class\="w-4 h-4 text-white" viewBox\="0 0 15 15" fill\="none" xmlns\="http://www.w3.org/2000/svg"\>
  <path d\="M0 1.5h1.5a6 6 0 110 12H0m7-12h4.5a3 3 0 110 6m0 0H9m2.5 0h-2m2 0a3 3 0 110 6H7" stroke\="currentColor"/>
</svg\>

### Sprites

You can find 3 different sprites:

-   All SVGs. (Around 510 KB.)
-   Outline only. (Around 270 KB.)
-   Solid only. (Around 240 KB.)

To use one of them, inline the sprite in your HTML or put it in some `/path/to/sprite.svg` and include an icon as such:

<svg class\="tiny-cyan-icon"\>
  <!-- Inlined sprite. Possible variants are outline and solid. \-->
  <use xlink:href\="#variant--icon-id"/>
</svg\>

<svg width\="15" height\="15" style\="color: slateblue"\>
  <!-- Outline sprite \-->
  <use xlink:href\="teenyicons-outline-sprite.svg#outline--360"/>
</svg\>

<svg class\="h-5 w-5 text-gray-800"\>
  <!-- Solid sprite \-->
  <use xlink:href\="teenyicons-solid-sprite.svg#solid--globe-africa"/>
</svg\>

Roadmap
-------

-   Tests for SVG dimensions.
-   Frameworks component libraries (Vue, React, etc.)
-   Figma plugin.

Request an icon
---------------

Icon requests are very welcome. Open an issue.

License
-------

Teenyicons is released under the MIT License.
