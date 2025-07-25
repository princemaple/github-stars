---
project: material-components-web
stars: 17117
description: Modular and customizable Material Design UI components for the web
url: https://github.com/material-components/material-components-web
---

Note:

This project is no longer actively maintained. While automated updates may still occur, the team will not be prioritizing new features or bug fixes, and those updates will be turned off in the future.

For Angular users, our friends at Angular Material moved away from this library, and they expect that this may actually allow for faster iteration - see their blog post for more information.

Material Components for the web
===============================

Material Components for the web helps developers execute Material Design. Developed by a core team of engineers and UX designers at Google, these components enable a reliable development workflow to build beautiful and functional web projects.

Material Web strives to seamlessly incorporate into a wider range of usage contexts, from simple static websites to complex, JavaScript-heavy applications to hybrid client/server rendering systems. In short, whether you're already heavily invested in another framework or not, it should be easy to incorporate Material Components into your site in a lightweight, idiomatic fashion.

Material Components for the web is the successor to Material Design Lite. In addition to implementing the Material Design guidelines, it provides more flexible theming customization, not only in terms of color, but also typography, shape, states, and more. It is also specifically architected for adaptability to various major web frameworks.

> NOTE: Material Components Web tends to release breaking changes on a monthly basis, but follows semver so you can control when you incorporate them. We typically follow a 2-week release schedule which includes one major release per month with breaking changes, and intermediate patch releases with bug fixes.

Important links
---------------

-   Getting Started Guide
-   Demos (external site)
-   Material on other frameworks
-   Examples using Material Web
-   Contributing
-   Material Design Guidelines (external site)
-   Supported browsers
-   All Components
-   Changelog

Quick start
-----------

### Using via CDN

<!-- Required styles for Material Web -->
<link rel\="stylesheet" href\="https://unpkg.com/material-components-web@latest/dist/material-components-web.min.css"\>

<!-- Render textfield component -->
<label class\="mdc-text-field mdc-text-field--filled"\>
  <span class\="mdc-text-field\_\_ripple"\></span\>
  <span class\="mdc-floating-label" id\="my-label"\>Label</span\>
  <input type\="text" class\="mdc-text-field\_\_input" aria-labelledby\="my-label"\>
  <span class\="mdc-line-ripple"\></span\>
</label\>

<!-- Required Material Web JavaScript library -->
<script src\="https://unpkg.com/material-components-web@latest/dist/material-components-web.min.js"\></script\>
<!-- Instantiate single textfield component rendered in the document -->
<script\>
  mdc.textField.MDCTextField.attachTo(document.querySelector<HTMLElement\>('.mdc-text-field'));
</script\>

> Please see quick start demo on codepen for full example.

### Using NPM

> This guide assumes you have webpack configured to compile Sass into CSS. To configure webpack, please see the full getting started guide. You can also see the final code and result in the Material Starter Kit.

Install textfield node module to your project.

```
npm install @material/textfield
```

#### HTML

Sample usage of text field component. Please see Textfield component page for more options.

<label class\="mdc-text-field mdc-text-field--filled"\>
  <span class\="mdc-text-field\_\_ripple"\></span\>
  <input type\="text" class\="mdc-text-field\_\_input" aria-labelledby\="my-label"\>
  <span class\="mdc-floating-label" id\="my-label"\>Label</span\>
  <span class\="mdc-line-ripple"\></span\>
</label\>

#### CSS

Load styles required for text field component.

@use "@material/floating-label/mdc-floating-label";
@use "@material/line-ripple/mdc-line-ripple";
@use "@material/notched-outline/mdc-notched-outline";
@use "@material/textfield";

@include textfield.core-styles;

#### JavaScript

Import `MDCTextField` module to instantiate text field component.

import {MDCTextField} from '@material/textfield';
const textField \= new MDCTextField(document.querySelector<HTMLElement\>('.mdc-text-field'));

This'll initialize text field component on a single `.mdc-text-field` element.

> Please see quick start demo on glitch for full example.

Need help?
----------

We're constantly trying to improve our components. If Github Issues don't fit your needs, then please visit us on our Discord Channel.
