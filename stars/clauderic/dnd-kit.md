---
project: dnd-kit
stars: 17052
description: The modern toolkit for building drag and drop interfaces
url: https://github.com/clauderic/dnd-kit
---

A modern, lightweight, performant, accessible and extensible drag and drop toolkit for the web

Features
--------

-   **Framework agnostic core:** The architecture is built in layers — a framework-agnostic core (`@dnd-kit/abstract`), a DOM implementation (`@dnd-kit/dom`), and thin adapters for your framework of choice.
-   **Supports a wide range of use cases:** lists, grids, multiple containers, nested contexts, variable sized items, virtualized lists, 2D games, and more.
-   **Built-in support for multiple input methods:** Pointer, mouse, touch and keyboard sensors.
-   **Fully customizable & extensible:** Customize every detail — animations, transitions, behaviours, styles. Build your own sensors, collision detection algorithms, customize key bindings and more.
-   **Accessibility:** Keyboard support, sensible default ARIA attributes, customizable screen reader instructions and live regions built-in.
-   **Performance:** Built with performance in mind to support silky smooth animations.
-   **Sortable:** Need to build a sortable interface? Check out `@dnd-kit/dom/sortable`, a thin layer built on top of the core.

Getting started
---------------

Choose your preferred framework to get started:

  

  
  

**Vanilla**

Build drag and drop interfaces using plain JavaScript  

  
  

**React**

Build drag and drop interfaces using React components and hooks  
  

  
  

**Vue**

Build drag and drop interfaces using Vue composables and components  
  

  
  

**Svelte**

Build drag and drop interfaces using Svelte primitives and components  
  

  
  

**Solid**

Build drag and drop interfaces using SolidJS hooks and components  
  

Documentation
-------------

Visit **dndkit.com** for full documentation, API reference, guides, and interactive examples.

Packages
--------

Package

Version

Description

`@dnd-kit/abstract`

Abstract core

`@dnd-kit/collision`

Collision detection

`@dnd-kit/dom`

Framework-agnostic DOM layer

`@dnd-kit/geometry`

Geometry utilities

`@dnd-kit/helpers`

Helper functions

`@dnd-kit/react`

React adapter

`@dnd-kit/solid`

SolidJS adapter

`@dnd-kit/state`

Reactive state management

`@dnd-kit/svelte`

Svelte adapter

`@dnd-kit/vue`

Vue adapter

Contributing
------------

This is a monorepo managed with Turborepo and bun.

# Install dependencies
bun install

# Build all packages
bun run build

# Run dev mode
bun run dev

License
-------

MIT
