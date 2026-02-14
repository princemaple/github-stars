---
project: angular-three
stars: 278
description: Angular Renderer for THREE.js
url: https://github.com/angular-threejs/angular-three
---

Angular Three workspace
=======================

Versioning
----------

Angular Three follows a modified semantic versioning scheme to balance stability with the fast-paced Three.js ecosystem:

Version

Meaning

Examples

**Patch** (x.x.X)

Bug fixes and new features. **No breaking changes ever.**

`4.0.0` → `4.0.1`

**Minor** (x.X.0)

Breaking changes for Three.js version bumps, or Angular minor updates that require breaking changes.

`4.0.x` → `4.1.0`

**Major** (X.0.0)

True breaking changes: API changes, Angular major bumps, or other peer dependency major bumps.

`4.x.x` → `5.0.0`

> **Why this approach?** Three.js releases frequently, and following true semver would exhaust major version numbers quickly. By using minor versions for Three.js breaking changes, we maintain a practical versioning scheme while clearly communicating compatibility boundaries.

Netlify Status
--------------

-   Angular Three:
-   Angular Three Demo:
-   Angular Three Soba:

Here, you'll find the source code for the entire `angular-three` ecosystem, the documentation, and the examples.

Documentation
-------------

The documentation is available at angularthree.org.

Examples
--------

The examples are available at demo.angularthree.org.

Packages
--------

Package

Description

angular-three

Core library - Angular renderer for Three.js

angular-three-soba

Helpers, abstractions, and ready-to-use components

angular-three-cannon

Cannon.js physics integration

angular-three-rapier

Rapier physics integration

angular-three-postprocessing

Post-processing effects

angular-three-theatre

Theatre.js animation integration

angular-three-tweakpane

Tweakpane debug controls

angular-three-plugin

Nx plugin with generators and utilities
