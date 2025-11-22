---
project: covalent
stars: 2237
description: Covalent - A Design System for Teradata
url: https://github.com/Teradata/covalent
---

Covalent Design System
======================

Covalent is Teradata's design system used to create consistent, branded experiences. This repository provides tools and components to support developers building applications for Teradata products. We currently support Angular and offer a comprehensive library of web components.

**Vision: To build an atomic, reusable component platform for Teradata to consume, while collaborating in an open source model.**

Setup
-----

-   Ensure you have Node 22.16.0+
-   Install Node packages `npm ci`
-   Run local build `npm run start`

* * *

-   Web Components
-   Web Components theming
-   Web Components developer Guide
-   Contributing guidelines
-   Releasing
-   Changelog

* * *

Angular Support
---------------

-   Getting Started
-   StackBlitz Template
-   Plunker Template

Certain versions of Covalent are designed to work with specific versions of Angular. Below is a matrix that outlines these compatibility details:

Covalent

Angular

2.X

8.X

3.X

9.X / 10.X / 11.x

4.X

12.X / 13.X

5.X

14.X

6.X

15.X

7.X

16.X

8.X

17.X

9.X

18.X

10.X

19.X

11.X

20.X

...existing code...

* * *

Angular Support
---------------

...existing code...

| 11.X | 20.X |

* * *

* * *

Browser Support
---------------

Covalent is built on a CSS Flexbox layout and all layouts and components heavily rely on that support, so the current browsers are supported in order of recommendation:

#### Current version - 1 for the following:

Chrome

Firefox

Safari

Edge

Mobile Chrome

Mobile Safari

**Supported**

✓

✓

✓

✓

~

~

~ Indicates limited testing & lower priority

Using this workspace with VS code and NX
----------------------------------------

-   Covalent uses Nx for monorepo builds and task running.
-   For a better experience, install the Nx Console extension for VS Code.
-   **Nx Console** lets you:
    -   Run builds, tests, lint, and affected commands with a click.
    -   Generate libraries, components, and schematics interactively.
    -   Explore project/dependency graphs visually.
    -   Edit workspace configs quickly.
-   **Get started:**
    1.  Open the repo in VS Code.
    2.  Install Nx Console from the Extensions Marketplace.
    3.  Use the Nx Console sidebar or search Nx commands in the Command Palette (`Cmd+Shift+P`).

Running Chromatic
-----------------

npx chromatic --project-token=${CHROMATIC\_PROJECT\_TOKEN}
