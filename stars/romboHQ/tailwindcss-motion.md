---
project: tailwindcss-motion
stars: 3293
description: tailwindcss-motion is a Tailwind CSS Plugin made at RomboHQ. It’s a simple, yet powerful, animation library with a simple syntax.
url: https://github.com/romboHQ/tailwindcss-motion
---

✨ tailwindcss-motion ✨
======================

tailwindcss-motion is a Tailwind CSS Plugin made at RomboHQ. It’s a simple, yet powerful, animation library with a simple syntax.

_Motion, without commotion._

⚒️ Installation
---------------

**1\. Install npm package**

npm i -D tailwindcss-motion

**2\. Add into your tailwind.config.js**

// tailwind.config.js

export default {
     content: \[...\],
     theme: {
        extend: {...},
     },
     plugins: \[require('tailwindcss-motion')\],
};

**or,** to use ESM:

import tailwindcssMotion from "tailwindcss-motion";

/\*\* @type {import('tailwindcss').Config} \*/
export default {
     content: \[...\],
     theme: {
          extend: {},
     },
     plugins: \[tailwindcssMotion\],
};

📝 TypeScript Support
---------------------

The plugin includes TypeScript definitions out of the box. Theme customizations and plugin configuration are fully typed:

import type { Config } from "tailwindcss";
import motion from "tailwindcss-motion";

const config: Config \= {
  theme: {
    extend: {
      motionScale: {
        "200": "200%",
      },
      motionTimingFunction: {
        custom: "cubic-bezier(0.4, 0, 0.2, 1)",
      },
    },
  },
  plugins: \[motion\],
};

How does it work?
-----------------

We provide a simple syntax to animate any element in your Tailwind project. Instead of defining custom keyframes, we provide utility classes to animate every dimension, inline.

For example, for a slide and fade effect — you simply need `motion-translate-x-in-25 motion-opacity-in-0` or, you can use one of our presets with `motion-preset-fade`

Documentation
-------------

For full documentation, visit docs.rombo.co/tailwind

🧩 Introducing the Chrome Extension
-----------------------------------

Take your animations to the next level with the Rombo Chrome Extension!

Create animations visually:

-   Use our intuitive animator directly in your browser.
-   Loop animations
-   Save presets: Keep your animations organized and reusable.
-   Export options: Output animations as Tailwind classes, pure CSS, or Framer Motion code.

Examples
--------

Landing page - https://play.tailwindcss.com/uAuVF8F1vC

Chat dialog - https://play.tailwindcss.com/gjGqEKswjQ

Low Battery Dynamic Island - https://play.tailwindcss.com/tvYFbHtNNQ

Apple Color Swatches - https://play.tailwindcss.com/cvQ3Nk3v8j

Rombo Loop - https://play.tailwindcss.com/MLdegkb9Wq

Emoji Animations - https://play.tailwindcss.com/86s55I4wmC

What's Rombo?
-------------

Rombo is an early-stage company, building tools to help companies build beautiful interactive interfaces. We're starting out with a toolkit for engineers, designers and creative marketers to animate natively inside common Workflows — like Tailwind, Figma, Webflow, Shopify & more to come!

More Resources
--------------

-   Bringing Motion to Tailwind CSS: Building an animation plugin at Rombo - Blog post about the creation of this library
-   Animator Builder - Create animations intuitively and export them to Tailwind classes
-   UnoCSS port - Port created by @whatnickcodes
