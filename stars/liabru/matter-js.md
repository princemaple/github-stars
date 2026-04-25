---
project: matter-js
stars: 18159
description: a 2D rigid body physics engine for the web ▲● ■
url: https://github.com/liabru/matter-js
---

> _Matter.js_ is a JavaScript 2D rigid body physics engine for the web

brm.io/matter-js

Demos ・ Gallery ・ Features ・ Plugins ・ Install ・ Usage ・ Examples ・ Docs ・ Wiki ・ References ・ License

### Demos

-   Mixed Shapes
-   Solid Shapes
-   Concave SVG Paths
-   Concave Terrain
-   Concave Bodies
-   Compound Bodies
-   Newton's Cradle
-   Wrecking Ball
-   Slingshot Game
-   Rounded Corners
-   Views
-   Time Scaling
-   Body Manipulation
-   Composite Manipulation

-   Raycasting
-   Sprites
-   Pyramid
-   Car
-   Catapult
-   Reverse Gravity
-   Bridge
-   Avalanche
-   Basic Soft Bodies
-   Cloth
-   Events
-   Collision Filtering
-   Chains
-   Ball Pool

-   Stack
-   Circle Stack
-   Compound Stack
-   Restitution
-   Friction
-   Air Friction
-   Static Friction
-   Sleeping
-   Beach Balls
-   Stress 1
-   Stress 2
-   Sensors

  

### Gallery

See how others are using matter.js physics

-   Patrick Heng by Patrick Heng
-   USELESS by Nice and Serious
-   Secret 7 by Goodness
-   New Company by New Company
-   Game of The Year by Google
-   Pablo The Flamingo by Nathan Gordon
-   Les métamorphoses de Mr. Kalia by Lab212
-   Phaser by Photon Storm
-   Sorry I Have No Filter by Jessica Walsh
-   Fuse by Fuse
-   Glyphfinder by überdosis
-   Isolation by sabato studio
-   more...

### Features

-   Rigid bodies
-   Compound bodies
-   Composite bodies
-   Concave and convex hulls
-   Physical properties (mass, area, density etc.)
-   Restitution (elastic and inelastic collisions)
-   Collisions (broad-phase, mid-phase and narrow-phase)
-   Stable stacking and resting
-   Conservation of momentum
-   Friction and resistance
-   Events
-   Constraints
-   Gravity
-   Sleeping and static bodies
-   Plugins
-   Rounded corners (chamfering)
-   Views (translate, zoom)
-   Collision queries (raycasting, region tests)
-   Time scaling (slow-mo, speed-up)
-   Canvas renderer (supports vectors and textures)
-   MatterTools for creating, testing and debugging worlds
-   World state serialisation (requires resurrect.js)
-   Cross-browser and Node.js support (Chrome, Firefox, Safari, IE8+)
-   Mobile-compatible (touch, responsive)
-   An original JavaScript physics implementation (not a port)

### Install

You can install using package managers npm and Yarn using:

```
npm install matter-js
```

Alternatively you can download a stable release or try the latest experimental alpha build (master) and include the script in your web page:

```
<script src="matter.js" type="text/javascript"></script>
```

### Performance with other tools (e.g. Webpack, Vue etc.)

Bundlers and frameworks may reduce real-time performance when using their default configs, especially in development modes.

When using Webpack, the default sourcemap config can have a large impact, for a solution see issue.

When using Vue.js, watchers can have a large impact, for a solution see issue.

### Usage

Visit the Getting started wiki page for a minimal usage example which should work in both browsers and Node.js.  
Also see the Running and Rendering wiki pages, which show how to use your own game and rendering loops.

### Tutorials

See the list of tutorials.

### Examples

See the examples directory which contains the source for all demos.  
There are even more examples on codepen.

### Plugins

The engine can be extended through plugins, see these resources:

-   Using plugins
-   Creating plugins
-   List of plugins
-   matter-plugin-boilerplate

### Documentation

See the API Documentation and the wiki

### Building and Contributing

To build you must first install node.js, then run

```
npm install
```

This will install the required build dependencies, then run

```
npm run dev
```

to spawn a development server. For information on contributing see CONTRIBUTING.md.

### Changelog

To see what's new or changed in the latest version, see the changelog.

### References

See the wiki page on References.

### License

Matter.js is licensed under The MIT License (MIT)  
Copyright (c) 2014 Liam Brummitt

This license is also supplied with the release and source code.  
As stated in the license, absolutely no warranty is provided.
