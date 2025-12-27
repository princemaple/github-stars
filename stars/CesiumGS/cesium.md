---
project: cesium
stars: 14647
description: An open-source JavaScript library for world-class 3D globes and maps :earth_americas:
url: https://github.com/CesiumGS/cesium
---

CesiumJS
========

CesiumJS is a JavaScript library for creating 3D globes and 2D maps in a web browser without a plugin. It uses WebGL for hardware-accelerated graphics, and is cross-platform, cross-browser, and tuned for dynamic-data visualization.

Built on open formats, CesiumJS is designed for robust interoperability and scaling for massive datasets.

* * *

**Examples** 🌏 **Docs** 🌎 **Website** 🌍 **Forum** 🌏 **User Stories**

* * *

🚀 Get started
--------------

Visit the Downloads page to download a pre-built copy of CesiumJS.

### npm & yarn

If you’re building your application using a module bundler such as Webpack, Parcel, or Rollup, you can install CesiumJS via the `cesium` npm package:

npm install cesium --save

Then, import CesiumJS in your app code. Import individual modules to benefit from tree shaking optimizations through most build tools:

import { Viewer } from "cesium";
import "cesium/Build/Cesium/Widgets/widgets.css";

const viewer \= new Viewer("cesiumContainer");

In addition to the `cesium` package, CesiumJS is also distributed as scoped npm packages for better dependency management:

-   `@cesium/engine` - CesiumJS's core, rendering, and data APIs
-   `@cesium/widgets` - A widgets library for use with CesiumJS

### What next?

See our Quickstart Guide for more information on getting a CesiumJS app up and running.

Instructions for serving local data are in the CesiumJS Offline Guide.

Interested in contributing? See CONTRIBUTING.md. ❤️

📗 License
----------

Apache 2.0. CesiumJS is free for both commercial and non-commercial use.

🌎 Where does the Global 3D Content come from?
----------------------------------------------

The Cesium platform follows an open-core business model with open source runtime engines such as CesiumJS and optional commercial subscription to Cesium ion.

CesiumJS can stream 3D content such as terrain, imagery, and 3D Tiles from the commercial Cesium ion platform alongside open standards from other offline or online services. We provide Cesium ion as the quickest option for all users to get up and running, but you are free to use any combination of content sources with CesiumJS that you please.

Bring your own data for tiling, hosting, and streaming from Cesium ion. Using Cesium ion helps support CesiumJS development.

✅ Features
----------

-   Stream in 3D Tiles and other standard formats from Cesium ion or another source
-   Visualize and analyze on a high-precision WGS84 globe
-   Share with users on desktop or mobile

See more in the CesiumJS Features Checklist.
