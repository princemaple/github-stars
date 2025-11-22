---
project: tabler-icons
stars: 19795
description: A set of over 5800 free MIT-licensed high-quality SVG icons for you to use in your web projects.
url: https://github.com/tabler/tabler-icons
---

Tabler Icons
============

A set of 5963 free MIT-licensed high-quality SVG icons for you to use in your web projects. Each icon is designed on a 24x24 grid and a 2px stroke.

**Browse at tabler.io/icons →**

Sponsors
--------

**If you want to support our project and help me grow it, you can become a sponsor on GitHub or just donate on PayPal :)**

Testing
-------

Browser testing via:

Preview
-------

### Outline version (4964 icons)

### Filled version (999 icons)

Installation
------------

```
npm install @tabler/icons --save
```

or just download from GitHub.

Usage
-----

All icons are built with SVG, so you can place them as `<img>`, `background-image` and inline in HTML code.

### HTML image

If you load an icon as an image, you can modify its size using CSS.

<img src\="path/to/icon.svg" alt\="icon title" />

### Inline HTML

You can paste the content of the icon file into your HTML code to display it on the page.

<a href\=""\>
  <svg
    xmlns\="http://www.w3.org/2000/svg"
    class\="icon icon-tabler icon-tabler-disabled"
    width\="24"
    height\="24"
    viewBox\="0 0 24 24"
    stroke-width\="1.25"
    stroke\="currentColor"
    fill\="none"
    stroke-linecap\="round"
    stroke-linejoin\="round"
  \>
    ...
  </svg\>
  Click me
</a\>

Thanks to that, you can change the size, color and the `stroke-width` of the icons with CSS code.

.icon-tabler {
  color: red;
  width: 32px;
  height: 32px;
  stroke-width: 1.25;
}

### SVG sprite

Add an icon to be displayed on your page with the following markup (`activity` in the above example can be replaced with any valid icon name):

<svg width\="24" height\="24"\>
  <use xlink:href\="path/to/tabler-sprite.svg#tabler-activity" />
</svg\>

### React

React components available through `@tabler/icons-react` package.

import { IconAward } from '@tabler/icons-react';

const MyComponent \= () \=> {
  return <IconAward
    size\={36} // set custom \`width\` and \`height\`
    color\="red" // set \`stroke\` color
    stroke\={3}  // set \`stroke-width\`
    strokeLinejoin\="miter" // override other SVG props
  />
}

`@tabler/icons-react` exports its own type declarations for usage with React and Typescript.

For more details, see the documentation.

### Vue

Vue components available through `@tabler/icons-vue` package.

<template\>
  <!-- basic usage \-->
  <IconHome />

  <!-- set \`stroke\` color \-->
  <IconHome color\="red"/>
  <IconHome stroke\="red"/>

  <!-- set custom \`width\` and \`height\` \-->
  <IconHome size\="36"/>

  <!-- set \`stroke-width\` \-->
  <IconHome strokeWidth\="2"/>
  <IconHome stroke-width\="2"/>
</template\>

<script\>
// Returns Vue component
import { IconHome } from '@tabler/icons-vue';
export default {
  components: { IconHome }
};
</script\>

or with `<script setup>`

<script setup>
// Import Vue component
import { IconHome } from '@tabler/icons-vue';
</script\>

<template\>
  <IconHome color\="red" size\="36" strokeWidth\="2"/>
</template\>

For more details, see the documentation.

### Angular

Angular components available through `angular-tabler-icons` package. Install the package, then create icons module:

import { NgModule } from '@angular/core';

import { TablerIconsModule } from 'angular-tabler-icons';
import { IconCamera, IconHeart, IconBrandGithub } from 'angular-tabler-icons/icons';

// Select some icons (use an object, not an array)
const icons \= {
  IconCamera,
  IconHeart,
  IconBrandGithub
};

@NgModule({
  imports: \[
    TablerIconsModule.pick(icons)
  \],
  exports: \[
    TablerIconsModule
  \]
})
export class IconsModule { }

After importing the _IconsModule_ in your feature or shared module, use the icons as follows:

<i-tabler name\="camera"\></i-tabler\>
<i-tabler name\="heart" style\="color: red;"\></i-tabler\>
<i-tabler name\="brand-github" class\="someclass"\></i-tabler\>

`angular-tabler-icons` exports its own type declarations for usage with Typescript.

For more usage documentation refer to the official documentation.

### Svelte

Svelte components available through `@tabler/icons-svelte` package.

<script lang\="ts"\>
  import { IconHeart } from '@tabler/icons-svelte';
</script\>

<main\>
  <IconHeart size\={48} stroke\={1} />
  <IconHeart size\="32" stroke\="1.5" /\>
  <IconHeart color\="crimson" class\="p-1" size\="96" stroke\="2" />
</main\>

CDN
---

All files included in `@tabler/icons` npm package are available over a CDN.

#### React icons

<script src\="https://cdn.jsdelivr.net/npm/@tabler/icons@latest/icons-react/dist/index.umd.min.js"\></script\>

#### Iconfont

<link rel\="stylesheet" href\="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css"\>

To load a specific version replace `latest` with the desired version number.

<script src\="https://cdn.jsdelivr.net/npm/@tabler/icons@1.74.0/icons-react/dist/index.umd.min.js"\></script\>

###### HTML

<i class\="ti ti-brand-tabler"\></i\>

###### CSS

content: 'ec8f';

### Compiling fonts

To compile fonts first install fontforge.

When compiling the font it will look for a json file `compile-options.json` in root folder (same folder as the `package.json`) In this file you can define extra options:

The default settings if you have not defined the file will be:

{
  "includeIcons": \[\],
  "fontForge": "fontforge",
  "strokeWidth": null
}

The fontforge executable needs to be in the path or you can set the path to the downloaded fontforge executable in the configuration file. If you installed in on a mac in your application directory it will be `/Applications/FontForge.app/Contents/MacOS/FontForge`. You can set this value in the `compile-options.json` file.

{
  "fontForge": "/Applications/FontForge.app/Contents/MacOS/FontForge"
}

To compile the fonts run:

npm run build-iconfont

By default the stroke width is 2. You can change the stroke width in the `compile-options.json`

{
  "strokeWidth": 1.5,
}

To reduce the font file size you can choose to compile a sub set of icons. When you leave the array empty it will compile all the fonts. To compile only two icons you can set for example the following option in the `compile-options.json`:

{
  "includeIcons": \["alert-octagon", "alert-triangle"\]
}

Optional property `includeCategories` - an array or string of icon categories to include, category names are case-insensitive.

{
  "includeCategories": \["Devices", "System"\]
}

or

{
  "includeCategories": "Devices System"
}

Optional property `excludeIcons` - an array of icon names using to exclude some category icons:

{
  "includeCategories": \["system"\],
  "excludeIcons": \["adjustments"\]
}

Complex solution:

{
  "includeIcons": \["alert-octagon", "alert-triangle"\],
  "includeCategories": \["devices", "system"\],
  "excludeIcons": \["adjustments"\]
}

### Jetpack Compose

For Android or Desktop you can use `compose-icons` to use icons in your projects. (see docs)

Multiple strokes
----------------

All icons in this repository have been created with the value of the `stroke-width` property, so if you change the value, you can get different icon variants that will fit in well with your design.

License
-------

Tabler Icons is licensed under the MIT License.

Sponsor Tabler
--------------
