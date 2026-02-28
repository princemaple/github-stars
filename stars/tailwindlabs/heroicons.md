---
project: heroicons
stars: 23373
description: A set of free MIT-licensed high-quality SVG icons for UI development.
url: https://github.com/tailwindlabs/heroicons
---

Beautiful hand-crafted SVG icons, by the makers of Tailwind CSS.  
Available as basic SVG icons and via first-party React and Vue libraries.

**Browse at Heroicons.com →**

Basic Usage
-----------

The quickest way to use these icons is to simply copy the source for the icon you need from heroicons.com and inline it directly into your HTML:

<svg
  class\="size-6 text-gray-500"
  fill\="none"
  viewBox\="0 0 24 24"
  stroke\="currentColor"
  stroke-width\="2"
\>
  <path
    stroke-linecap\="round"
    stroke-linejoin\="round"
    d\="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"
  />
</svg\>

Both icon styles are preconfigured to be stylable by setting the `color` CSS property, either manually or using utility classes like `text-gray-500` in a framework like Tailwind CSS.

React
-----

First, install `@heroicons/react` from npm:

npm install @heroicons/react

Now each icon can be imported individually as a React component:

import { BeakerIcon } from '@heroicons/react/24/solid'

function MyComponent() {
  return (
    <div\>
      <BeakerIcon className\="size-6 text-blue-500" />
      <p\>...</p\>
    </div\>
  )
}

The 24x24 outline icons can be imported from `@heroicons/react/24/outline`, the 24x24 solid icons can be imported from `@heroicons/react/24/solid`, the 20x20 solid icons can be imported from `@heroicons/react/20/solid`, and 16x16 solid icons can be imported from `@heroicons/react/16/solid`.

Icons use an upper camel case naming convention and are always suffixed with the word `Icon`.

Browse the full list of icon names on UNPKG →

Vue
---

First, install `@heroicons/vue` from npm:

npm install @heroicons/vue

Now each icon can be imported individually as a Vue component:

<template\>
  <div\>
    <BeakerIcon class\="size-6 text-blue-500" />
    <p\>...</p\>
  </div\>
</template\>

<script setup>
import { BeakerIcon } from '@heroicons/vue/24/solid'
</script\>

The 24x24 outline icons can be imported from `@heroicons/vue/24/outline`, the 24x24 solid icons can be imported from `@heroicons/vue/24/solid`, the 20x20 solid icons can be imported from `@heroicons/vue/20/solid`, and the 16x16 solid icons can be imported from `@heroicons/vue/16/solid`.

Icons use an upper camel case naming convention and are always suffixed with the word `Icon`.

Browse the full list of icon names on UNPKG →

Contributing
------------

While we absolutely appreciate anyone's willingness to try and improve the project, we're currently only interested in contributions that fix bugs, for example things like incorrect TypeScript types, or fixing an icon that's been exported with a fill instead of a stroke, etc.

**We're not accepting contributions for new icons or adding support for other frameworks like Svelte or SolidJS**. Instead we encourage you to release your own icons in your own library, and create your own packages for any other frameworks you'd like to see supported.

License
-------

This library is MIT licensed.
