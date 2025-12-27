---
project: pixijs
stars: 46303
description: The HTML5 Creation Engine: Create beautiful digital content with the fastest, most flexible 2D WebGL renderer.
url: https://github.com/pixijs/pixijs
---

  

Guides | Tutorials | Examples | API Docs | Discord | Bluesky | 𝕏

PixiJS ⚡️
=========

> Next-Generation, Fastest HTML5 Creation Engine for the Web

-   🚀 WebGL & WebGPU Renderers
-   ⚡️ Unmatched Performance & Speed
-   🎨 Easy to use, yet powerful API
-   📦 Asset Loader
-   ✋ Full Mouse & Multi-touch Support
-   ✍️ Flexible Text Rendering
-   📐 Versatile Primitive and SVG Drawing
-   🖼️ Dynamic Textures
-   🎭 Masking
-   🪄 Powerful Filters
-   🌈 Advanced Blend Modes

PixiJS is the fastest, most lightweight 2D library available for the web, working across all devices and allowing you to create rich, interactive graphics and cross-platform applications using WebGL and WebGPU.

### Setup

It's easy to get started with PixiJS! Just use our PixiJS Create CLI and get set up in just one command:

```
npm create pixi.js@latest
```

or to add it to an existing project:

```
npm install pixi.js
```

### Usage

import { Application, Assets, Sprite } from 'pixi.js';

(async () \=>
{
    // Create a new application
    const app \= new Application();

    // Initialize the application
    await app.init({ background: '#1099bb', resizeTo: window });

    // Append the application canvas to the document body
    document.body.appendChild(app.canvas);

    // Load the bunny texture
    const texture \= await Assets.load('https://pixijs.com/assets/bunny.png');

    // Create a bunny Sprite
    const bunny \= new Sprite(texture);

    // Center the sprite's anchor point
    bunny.anchor.set(0.5);

    // Move the sprite to the center of the screen
    bunny.x \= app.screen.width / 2;
    bunny.y \= app.screen.height / 2;

    app.stage.addChild(bunny);

    // Listen for animate update
    app.ticker.add((time) \=>
    {
        // Just for fun, let's rotate mr rabbit a little.
        // \* Delta is 1 if running at 100% performance \*
        // \* Creates frame-independent transformation \*
        bunny.rotation += 0.1 \* time.deltaTime;
    });
})();

### Contribute

Want to be part of the PixiJS project? Great! All are welcome! We will get there quicker together :) Whether you find a bug, have a great feature request, or you fancy owning a task from the road map above, feel free to get in touch.

Make sure to read the Contributing Guide before submitting changes.

### License

This content is released under the MIT License.

### Change Log

Releases

### Support

We're passionate about making PixiJS the best graphics library possible. Our dedication comes from our love for the project and community. If you'd like to support our efforts, please consider contributing to our open collective.
