---
project: tether
stars: 8502
description:  A positioning engine to make overlays, tooltips and dropdowns better
url: https://github.com/shipshapecode/tether
---

Tether
======

**Tether is maintained by Ship Shape. Contact us for web app consulting, development, and training for your project**.

🐙 Project status 🐙
--------------------

We at Ship Shape have recently taken over Tether's maintenance and hope to modernize and revitalize it. Stay tuned for updates!

Install
-------

**npm**

npm install tether

For the latest beta:

npm install tether@next

**download**

Or download from the releases.

Introduction
------------

Tether is a small, focused JavaScript library for defining and managing the position of user interface (UI) elements in relation to one another on a web page. It is a tool for web developers building features that require certain UI elements to be precisely positioned based on the location of another UI element.

There are often situations in UI development where elements need to be attached to other elements, but placing them right next to each other in the DOM tree can be problematic based on the context. For example, what happens if the element we’re attaching other elements to is fixed to the center of the screen? Or what if the element is inside a scrollable container? How can we prevent the attached element from being clipped as it disappears from view while a user is scrolling? Tether can solve all of these problems and more.

Some common UI elements that have been built with Tether are tooltips, select menus, and dropdown menus. Tether is flexible and can be used to solve all kinds of interesting problems; it ensures UI elements stay where they need to be, based on the various user interactions (click, scroll, etc) and layout contexts (fixed positioning, inside scrollable containers, etc).

Please have a look at the documentation for a more detailed explanation of why you might need Tether for your next project.

What to Use Tether for and When to Use It
-----------------------------------------

Tether is a small, focused JavaScript library. For those who might be new to JavaScript, a library is simply a JavaScript file (or files) that contain useful JavaScript code to help achieve tasks easier and faster. Since Tether is a JavaScript user interface (**UI**) library, it contains code to help you to manage the way your website or web app appears.

Tether’s goal to is to help you position your elements side-by-side when needed.

Let’s say you’ve started working on your dream project—a fancy web app that’s sure to become the next big thing! An important feature of your new app is to allow users to comment on shared photos. However, due to limited vertical space and the overall layout of your new app, you’d like to display the comments **next** to the image, similar to how Instagram does it.

Your HTML code might look something like this:

<div class\="container"\>
  <img src\="awesome-picture.jpg" alt\="Awesome Picture" class\="picture"\>
  <div class\="comments"\>
    ...
  </div\>
</div\>

Now, you could achieve this with some CSS using its `position` property, but going this route can be problematic since many of `position`’s values take elements **out** of the natural DOM flow. For example, if you have an element at the bottom of your HTML document, using `position: absolute` or `position: fixed` might could move it all the way to the top of your website in the browser.

Not only that, but you also have to make manual adjustments to ensure **other** elements aren’t negatively affected by the positioned elements. Not to mention, you probably want your comment box to be **responsive**, and look good across different device sizes. Coding a solution for this manually is a challenge all on its own.

**Enter Tether!**

After installing Tether and including it in your project, you can begin using it!

1.  In your JavaScript file, create a new instance (or constructor function) of the `Tether` object:
    
    new Tether({});
    
2.  Within the curly braces (`{}`) you can configure the library’s options. Tether’s extensive list of options can be found in the Tether documentation.
    
    new Tether({
      element: '.comments',
      target: '.picture',
      attachment: 'top right',
      targetAttachment: 'top left'
    });
    

Now you have a perfectly placed comment section to go with your awesome picture! It’ll even stay attached to the element when a user resizes their browser window.

There are tons of other useful features of Tether as well, instead of “comment boxes” you could also build:

-   Tooltips for useful hints and tricks,
-   Dropdown menus,
-   Autocomplete popups for forms,
-   and more!

Usage
-----

You only need to include `tether.min.js` in your page:

```
<script src="path/to/dist/js/tether.min.js"></script>
```

Or use a CDN:

```
<script src="https://cdn.jsdelivr.net/npm/tether@2.0.0-beta.5/dist/js/tether.min.js"></script>
```

The css files are not required to get tether running.

For more details jump straight in to the detailed Usage page.

Demo & API Documentation

Contributing
------------

We encourage contributions of all kinds. If you would like to contribute in some way, please review our guidelines for contributing.

License
-------

Copyright © 2019-2022 Ship Shape Consulting LLC - MIT License Copyright © 2014-2018 HubSpot - MIT License
