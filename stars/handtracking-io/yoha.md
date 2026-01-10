---
project: yoha
stars: 2105
description: A practical hand tracking engine.
url: https://github.com/handtracking-io/yoha
---

  
Yoha  

==========

#### A practical hand tracking engine.

Note: Yoha is currently unmaintained.
-------------------------------------

Quick Links:
------------

-   Demo (Code)
-   Docs
-   Website
-   npm

Installation
------------

`npm install @handtracking.io/yoha`

Please note:

-   You need to serve the files from `node_modules/@handtracking.io/yoha` since the library needs to download the model files from here. (Webpack Example)
-   You need to serve your page with https for webcam access. (Webpack Example)
-   You _should_ use cross-origin isolation as it improves the engine's performance in certain scenarios. (Webpack Example)

Description
-----------

Yoha is a hand tracking engine that is built with the goal of being a versatile solution in practical scenarios where hand tracking is employed to add value to an application. While ultimately the goal is to be a general purpose hand tracking engine supporting any hand pose, the engine evolves around specific hand poses that users/developers find useful. These poses are detected by the engine which allows to build applications with meaningful interactions. See the demo for an example.

Yoha is currently in beta.

About the name: Yoha is short for ("**Yo**ur **Ha**nd Tracking").

Language Support
----------------

Yoha is currently available for the web via JavaScript. More languages will be added in the future. If you want to port Yoha to another language and need help feel free reach out.

Technical Details
-----------------

Yoha was built from scratch. It uses a custom neural network trained using a custom dataset. The backbone for the inference in the browser is currently TensorFlow.js

### Features:

-   Detection of 21 2D-landmark coordinates (single hand).
-   Hand presence detection.
-   Hand orientation (left/right hand) detection.
-   Inbuilt pose detection.

#### Supported Hand Poses:

-   Pinch (index finger and thumb touch)
-   Fist

Your desired pose is not on this list? Feel free to create an issue for it.

### Performance

Yoha was built with performance in mind. It is able to provide realtime user experience on a broad range of laptops and desktop devices. The performance on mobile devices is not great which hopefuly will change with the further development of inference frameworks like TensorFlow.js

Please note that native inference speed can not be compared with the web inference speed. Differently put, if you were to run Yoha natively it would be much faster than via the web browser.

Minimal Example
---------------

-   Source
-   Running locally:

```
git clone https://github.com/handtracking-io/yoha && \
cd yoha/example && \
yarn && \
yarn start
```

Drawing Demo
------------

-   Live Version
-   Source
-   Running locally:

```
git clone https://github.com/handtracking-io/yoha && \
cd yoha && \
./download_models.sh && \
yarn && \
yarn start
```
