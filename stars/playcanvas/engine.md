---
project: engine
stars: 14240
description: Powerful web graphics runtime built on WebGL, WebGPU, WebXR and glTF
url: https://github.com/playcanvas/engine
---

PlayCanvas Engine
=================

| User Manual | API Reference | Examples | Blog | Forum |

PlayCanvas is an open-source game engine. It uses HTML5 and WebGL to run games and other interactive 3D content in any mobile or desktop browser.

English 中文 日本語 한글

Project Showcase
----------------

Many games and apps have been published using the PlayCanvas engine. Here is a small selection:

  
  

You can see more games on the PlayCanvas website.

Users
-----

PlayCanvas is used by leading companies in video games, advertising and visualization such as:  
**Animech, Arm, BMW, Disney, Facebook, Famobi, Funday Factory, IGT, King, Miniclip, Leapfrog, Mojiworks, Mozilla, Nickelodeon, Nordeus, NOWWA, PikPok, PlaySide Studios, Polaris, Product Madness, Samsung, Snap, Spry Fox, Zeptolab, Zynga**

Features
--------

PlayCanvas is a fully-featured game engine.

-   🧊 **Graphics** - Advanced 2D + 3D graphics engine built on WebGL2 & WebGPU
-   🏃 **Animation** - Powerful state-based animations for characters and arbitrary scene properties
-   ⚛️ **Physics** - Full integration with 3D rigid-body physics engine ammo.js
-   🎮 **Input** - Mouse, keyboard, touch, gamepad and VR controller APIs
-   🔊 **Sound** - 3D positional sounds built on the Web Audio API
-   📦 **Assets** - Asynchronous streaming system built on glTF 2.0, Draco and Basis compression
-   📜 **Scripts** - Write game behaviors in Typescript or JavaScript

Usage
-----

Here's a super-simple Hello World example - a spinning cube!

import \* as pc from 'playcanvas';

const canvas \= document.createElement('canvas');
document.body.appendChild(canvas);

const app \= new pc.Application(canvas);

// fill the available space at full resolution
app.setCanvasFillMode(pc.FILLMODE\_FILL\_WINDOW);
app.setCanvasResolution(pc.RESOLUTION\_AUTO);

// ensure canvas is resized when window changes size
window.addEventListener('resize', () \=> app.resizeCanvas());

// create box entity
const box \= new pc.Entity('cube');
box.addComponent('model', {
  type: 'box'
});
app.root.addChild(box);

// create camera entity
const camera \= new pc.Entity('camera');
camera.addComponent('camera', {
  clearColor: new pc.Color(0.1, 0.2, 0.3)
});
app.root.addChild(camera);
camera.setPosition(0, 0, 3);

// create directional light entity
const light \= new pc.Entity('light');
light.addComponent('light');
app.root.addChild(light);
light.setEulerAngles(45, 0, 0);

// rotate the box according to the delta time since the last frame
app.on('update', dt \=> box.rotate(10 \* dt, 20 \* dt, 30 \* dt));

app.start();

Want to play with the code yourself? Edit it on CodePen.

A full guide to setting up a local development environment based on the PlayCanvas Engine can be found here.

How to build
------------

Ensure you have Node.js 18+ installed. Then, install all of the required Node.js dependencies:

npm install

Now you can run various build options:

Command

Description

Outputs To

`npm run build`

Build all engine flavors and type declarations

`build`

`npm run docs`

Build engine API reference docs

`docs`

PlayCanvas Editor
-----------------

The PlayCanvas Engine is an open-source engine that you can use to create HTML5 apps/games. In addition to the engine, we also make the PlayCanvas Editor:

For Editor-related bugs and issues, please refer to the Editor's repo.
