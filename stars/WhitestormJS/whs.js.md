---
project: whs.js
stars: 6340
description: :rocket: 🌪 Super-fast 3D framework for Web Applications 🥇 & Games 🎮. Based on Three.js
url: https://github.com/WhitestormJS/whs.js
---

-   Documentation
-   Examples
-   Contributions/Trello
-   Donate / OpenCollective

Community chat. Join us!

### Table of content

-   Basic setup
    -   npm
-   Featured projects
-   Features
-   Donate
-   Why?

##### New releases

> `whs` is currently at v2 major version. We had plans for v3 yet but development isn't active. So v2 will probably remain the main stable version until further notice.

> We try to publish **minor update releases** for bug fixes, we will review PRs.

#### NPM

# Install npm version
$ npm install whs

> For `whs@2.2.x` (Three.js r92) use @beta tag

# Install npm version
$ npm install whs@beta

### Basic setup

Download the minified library or link the one from CDN

<script src\="js/three.min.js"\></script\>
<script src\="js/whs.min.js"\></script\>

The code below makes a `WHS.App` instance which handles all your modules and components for better work with `WebGL`. This one creates a _scene_, _camera_ and _renderer_ - we add the following modules to the App.

const app \= new WHS.App(\[
  new WHS.ElementModule(), // Apply to DOM.
  new WHS.SceneModule(), // Create a new THREE.Scene and set it to app.

  new WHS.DefineModule('camera', new WHS.PerspectiveCamera({ // Apply a camera.
    position: new THREE.Vector3(0, 0, 50)
  })),

  new WHS.RenderingModule({bgColor: 0x162129}), // Apply THREE.WebGLRenderer
  new WHS.ResizeModule() // Make it resizable.
\]);

app.start(); // Run app.

### Featured projects

### Features

-   💎 **Simple in usage**
-   🚀 Speeds up 3D scene prototyping
-   🔌 **Component based scene graph**
-   💣 Simple integration of any **high performance physics** even with `Worker` (Multithreading)
-   💫 Automatization of rendering
-   🆕 **ES2015+ based**
-   🔷 Extension system (modules)
-   📦 Webpack friendly
-   ✔️ **Integrated Three.js rendering engine**
-   💞 Work with whs.js and Three.js at the same time

### External Modules

Name

Status

Description

physics-module-ammonext

Physics module based on Ammo.js

### Donate

#### Backers

Support us with a monthly donation and help us continue framework development🎉 and adding new features💡🎁.
