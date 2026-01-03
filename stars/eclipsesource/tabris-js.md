---
project: tabris-js
stars: 1414
description: Create native mobile apps in JavaScript or TypeScript.
url: https://github.com/eclipsesource/tabris-js
---

Tabris.js
=========

Tabris.js is a framework for developing mobile apps with native UIs in JavaScript. iOS and Android apps can be built entirely from one code base, which frees you from the task of managing code for multiple platforms.

import {Button, contentView, TextView} from 'tabris';

// in JS

new Button({top: 16, centerX: true, text: 'Use native UI'})
  .onSelect(() \=> $(TextView).only().text \= 'Powered by Tabris.js')
  .appendTo(contentView);
new TextView({top: 'prev() 16', centerX: true})
  .appendTo(contentView);

// or in JSX

contentView.append(
  <$\>
    <Button top\={16} centerX text\='Use native UI'
            onSelect\={() \=> $(TextView).only().text \= 'Powered by Tabris.js'}/>
    <TextView top\='prev() 16' centerX/>
  </$\>
);

Native widgets
--------------

The code of the application is loaded dynamically - nothing is precompiled. JavaScript is executed Just-in-Time and passed via a native bridge to the device. Tabris.js accesses native controls and does not depend on webviews to render the app's UI. As a result, the performance of the apps cannot be distinguished from apps developed directly in native code of the platforms.

Getting started
---------------

To start developing Tabris.js applications, visit tabrisjs.com and check out the "Getting Started" guide in the documentation. Be sure to also consult the code snippets in the Tabris.js Developer App (download from the app store for Android and iOS).

Extensible
----------

Tabris.js can be extended with Cordova plugins to add support for additional native features. A cordova plugin is also able to directly interface with the native widgets (as can be seen e.g. in the tabris-plugin-maps).

Additionally npm modules can be used to further enrich the available JS APIs.

Tabris.js also adds support for many key web technologies including:

-   _Canvas_
-   _XMLHttpRequest / fetch()_
-   _WebSockets_
-   _localStorage_

Build tabris npm module
-----------------------

Follow these steps if you want to build the tabris module yourself.

Install the Grunt build tool using npm:

npm install -g grunt-cli

In the tabris-js root directory fetch the dependencies and build:

npm install
grunt

License
-------

Published under the terms of the BSD 3-Clause License.
