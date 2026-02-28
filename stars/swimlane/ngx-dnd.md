---
project: ngx-dnd
stars: 572
description: 🕶  Drag, Drop and Sorting Library for Angular2 and beyond!
url: https://github.com/swimlane/ngx-dnd
---

ngx-dnd
=======

🕶 Drag, Drop and Sorting Library for Angular6 and beyond!

_Note: The drag-and-drop directives in angular/cdk are great. Use that if you don't need nested DnD containers. We are investigating using angular/cdk directives internally_

Features
--------

-   Drag and Drop
-   Sorting
-   Events (drag, drop, over, out)
-   Nesting
-   Touch support
-   Templating

Install
-------

To use ngx-dnd in your project install it via npm:

-   `npm i @swimlane/ngx-dnd @swimlane/dragula @types/dragula --save`
-   Add `NgxDnDModule.forRoot()` to your application module.
-   If using directives you will need to BYO styles or include `@swimlane/ngx-dnd/release/index.css`.
-   You may need to add the following to your `polyfills.ts` file:

if (typeof window\['global'\] \=== 'undefined') {
  window\['global'\] \= window;
}

Quick intro and examples
------------------------

### Directives

`ngx-dnd` provides a base set of directives to enable drag-and-drop. By default all children of a `ngxDroppable` element may be dragged and dropped. Add the `ngxDraggable` to restrict drag-and-drop to the parent container. In general prefer using the base directives to the help components introduced later.

<div class\="ngx-dnd-container" ngxDroppable\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 1</div\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 2</div\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 3</div\>
</div\>

Give multiple containers the same `dropZone` name to allow drag-and-drop between these containers.

<div class\="ngx-dnd-container" ngxDroppable\="example"\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 1a</div\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 2a</div\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 3a</div\>
</div\>
<div class\="ngx-dnd-container" ngxDroppable\="example"\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 1b</div\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 2b</div\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 3b</div\>
</div\>

`ngxDraggable` items can be restricted to specific containers:

<div class\="ngx-dnd-container" ngxDroppable\>
  <div class\="ngx-dnd-item" \[ngxDraggable\]\="\['example-target'\]"\>Item 1a</div\>
  <div class\="ngx-dnd-item" \[ngxDraggable\]\="\['example-target'\]"\>Item 2a</div\>
  <div class\="ngx-dnd-item" \[ngxDraggable\]\="\['example-target'\]"\>Item 3a</div\>
</div\>
<div class\="ngx-dnd-container" ngxDroppable\="example-target"\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 1b</div\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 2b</div\>
  <div class\="ngx-dnd-item" ngxDraggable\>Item 3b</div\>
</div\>

### Components

`ngx-dnd` provides a set of helper components that encapsulates the directives mentioned and adds capability for data driven structures. In general you should prefer directives to components.

orderableLists \= \[
  \['Item 1a', 'Item 2a', 'Item 3a'\],
  \['Item 1b', 'Item 2b', 'Item 3b'\]
\];

<ngx-dnd-container \[model\]\="orderableLists"\> </ngx-dnd-container\>

This component is effectively equivalent to:

<div class\="ngx-dnd-container" ngxDroppable \[model\]\="orderableLists"\>
  <div class\="ngx-dnd-item" ngxDraggable \[model\]\="item" \*ngFor\="let item of orderableLists"\>{{item}}</div\>
</div\>

Including nested containers:

<ngx-dnd-container \[model\]\="nestedLists"\> </ngx-dnd-container\>

nestedLists \= \[
  {
    label: 'Item 1',
    children: \[\]
  },
  {
    label: 'Item 2',
    children: \[
      {
        label: 'Item 2a',
        children: \[\]
      },
      {
        label: 'Item 2b',
        children: \[\]
      },
      {
        label: 'Item 2c',
        children: \[\]
      }
    \]
  },
  {
    label: 'Item 3',
    children: \[
      {
        label: 'Item 3a',
        children: \[\]
      },
      {
        label: 'Item 3b',
        children: \[\]
      },
      {
        label: 'Item 3c',
        children: \[\]
      }
    \]
  }
\];

See https://swimlane.github.io/ngx-dnd/ for more lives examples. Demo code is at https://github.com/swimlane/ngx-dnd/tree/master/src/.

Development
-----------

-   `git clone git@github.com:swimlane/ngx-dnd.git`
-   `cd ngx-dnd`
-   `ng build @swimlane/ngx-dnd`
-   `ng serve`
-   Browse to http://localhost:4200

### Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

### Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

### Running unit tests

Run `ng test` to execute the unit tests via Karma.

### Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via Protractor.

### Further help

To get more help on the Angular CLI use `ng help` or go check out the Angular CLI README.

CHANGELOG
---------

This project uses heff/chg, a simple changelog/release history manager. When contributing to this project please add change notes (manually or using the heff/chg cli) to the `## HEAD (Unreleased)` section.

Release
-------

-   Checkout master (`git checkout master`)
-   Pull master (`git pull`)
-   Clean and test (Optional)
    -   Run `rm -rf node_modules`
    -   Run `npm i`
    -   Run tests (`npm run test:ci`)
-   Examine CHANGELOG.md to determine next version (X.Y.Z)
-   Run `git checkout -b release/X.Y.Z`
-   Update version using `npm version [<newversion> | major | minor | patch]`
    -   This will update `package.json` versions and `changelog.md`.
-   Run `git push origin HEAD --tags`
-   Run `npm run publish:lib`
-   Run `npm run deploy`
-   Submit PR

Credits
-------

`ngx-dnd` is a Swimlane open-source project; we believe in giving back to the open-source community by sharing some of the projects we build for our application. Swimlane is an automated cyber security operations and incident response platform that enables cyber security teams to leverage threat intelligence, speed up incident response and automate security operations.
