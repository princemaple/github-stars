---
project: Babylon.js
stars: 24886
description: Babylon.js is a powerful, beautiful, simple, and open game and rendering engine packed into a friendly JavaScript framework.
url: https://github.com/BabylonJS/Babylon.js
---

Babylon.js
==========

Getting started? Play directly with the Babylon.js API using our playground. It also contains a lot of samples to learn how to use it.

**Any questions?** Here is our official forum.

CDN
---

> ⚠️ WARNING: The CDN should not be used in production environments. The purpose of our CDN is to serve Babylon packages to users learning how to use the platform or running small experiments. Once you've built an application and are ready to share it with the world at large, you should serve all packages from your own CDN.

-   https://cdn.babylonjs.com/babylon.js
-   https://cdn.babylonjs.com/babylon.max.js

For the preview release, use the following URLs:

-   https://preview.babylonjs.com/babylon.js
-   https://preview.babylonjs.com/babylon.max.js

A list of additional references can be found here.

npm
---

BabylonJS and its modules are published on npm with full typing support. To install, use:

```
npm install babylonjs --save
```

> alternatively, you can now rely on our ES6 packages. Using the ES6 version will allow tree shaking among other bundling benefits.

This will allow you to import BabylonJS entirely using:

import \* as BABYLON from 'babylonjs';

or individual classes using:

import { Scene, Engine } from 'babylonjs';

If using TypeScript, don't forget to add 'babylonjs' to 'types' in `tsconfig.json`:

    ...
    "types": \[
        "babylonjs",
        "anotherAwesomeDependency"
    \],
    ...

To add a module, install the respective package. A list of extra packages and their installation instructions can be found on the babylonjs user on npm.

Usage
-----

See Getting Started:

// Get the canvas DOM element
var canvas \= document.getElementById('renderCanvas');
// Load the 3D engine
var engine \= new BABYLON.Engine(canvas, true, {preserveDrawingBuffer: true, stencil: true});
// CreateScene function that creates and return the scene
var createScene \= function(){
    // Create a basic BJS Scene object
    var scene \= new BABYLON.Scene(engine);
    // Create a FreeCamera, and set its position to {x: 0, y: 5, z: -10}
    var camera \= new BABYLON.FreeCamera('camera1', new BABYLON.Vector3(0, 5, \-10), scene);
    // Target the camera to scene origin
    camera.setTarget(BABYLON.Vector3.Zero());
    // Attach the camera to the canvas
    camera.attachControl(canvas, false);
    // Create a basic light, aiming 0, 1, 0 - meaning, to the sky
    var light \= new BABYLON.HemisphericLight('light1', new BABYLON.Vector3(0, 1, 0), scene);
    // Create a built-in "sphere" shape using the SphereBuilder
    var sphere \= BABYLON.MeshBuilder.CreateSphere('sphere1', {segments: 16, diameter: 2, sideOrientation: BABYLON.Mesh.FRONTSIDE}, scene);
    // Move the sphere upward 1/2 of its height
    sphere.position.y \= 1;
    // Create a built-in "ground" shape;
    var ground \= BABYLON.MeshBuilder.CreateGround("ground1", { width: 6, height: 6, subdivisions: 2, updatable: false }, scene);
    // Return the created scene
    return scene;
}
// call the createScene function
var scene \= createScene();
// run the render loop
engine.runRenderLoop(function(){
    scene.render();
});
// the canvas/window resize event handler
window.addEventListener('resize', function(){
    engine.resize();
});

Contributing
------------

If you want to contribute, please read our contribution guidelines first.

Documentation
-------------

-   Documentation
-   Demos

Useful links
------------

-   Official web site: www.babylonjs.com
-   Online playground to learn by experimentating
-   Online sandbox where you can test your .babylon and glTF scenes with a simple drag'n'drop
-   Online shader creation tool where you can learn how to create GLSL shaders
-   3DS Max exporter can be used to generate a .babylon file from 3DS Max
-   Maya exporter can be used to generate a .babylon file from Maya
-   Blender exporter can be used to generate a .babylon file from Blender 3d
-   Unity 5 (deprecated) exporter can be used to export your geometries from Unity 5 scene editor(animations are supported)
-   glTF Tools by KhronosGroup

Features
--------

To get a complete list of supported features, please visit our website.
