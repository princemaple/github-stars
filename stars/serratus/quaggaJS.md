---
project: quaggaJS
stars: 5203
description: An advanced barcode-scanner written in JavaScript
url: https://github.com/serratus/quaggaJS
---

quaggaJS
========

-   Changelog (2017-06-07)
-   Browser Support
-   Installing
-   Getting Started
-   API
-   Configuration
-   Tips & Tricks
-   Sponsors

What is QuaggaJS?
-----------------

QuaggaJS is a barcode-scanner entirely written in JavaScript supporting real- time localization and decoding of various types of barcodes such as **EAN**, **CODE 128**, **CODE 39**, **EAN 8**, **UPC-A**, **UPC-C**, **I2of5**, **2of5**, **CODE 93** and **CODABAR**. The library is also capable of using `getUserMedia` to get direct access to the user's camera stream. Although the code relies on heavy image-processing even recent smartphones are capable of locating and decoding barcodes in real-time.

Try some examples and check out the blog post (How barcode-localization works in QuaggaJS) if you want to dive deeper into this topic.

Yet another barcode library?
----------------------------

This is not yet another port of the great zxing library, but more of an extension to it. This implementation features a barcode locator which is capable of finding a barcode-like pattern in an image resulting in an estimated bounding box including the rotation. Simply speaking, this reader is invariant to scale and rotation, whereas other libraries require the barcode to be aligned with the viewport.

Browser Support
---------------

Quagga makes use of many modern Web-APIs which are not implemented by all browsers yet. There are two modes in which Quagga operates: 1. analyzing static images and 2. using a camera to decode the images from a live-stream. The latter requires the presence of the MediaDevices API. You can track the compatibility of the used Web-APIs for each mode:

-   Static Images
-   Live Stream

### Static Images

The following APIs need to be implemented in your browser:

-   webworkers
-   canvas
-   typedarrays
-   bloburls
-   blobbuilder

### Live Stream

In addition to the APIs mentioned above:

-   MediaDevices

**Important:** Accessing `getUserMedia` requires a secure origin in most browsers, meaning that `http://` can only be used on `localhost`. All other hostnames need to be served via `https://`. You can find more information in the Chrome M47 WebRTC Release Notes.

### Feature-detection of getUserMedia

Every browser seems to differently implement the `mediaDevices.getUserMedia` API. Therefore it's highly recommended to include webrtc-adapter in your project.

Here's how you can test your browser's capabilities:

if (navigator.mediaDevices && typeof navigator.mediaDevices.getUserMedia \=== 'function') {
  // safely access \`navigator.mediaDevices.getUserMedia\`
}

The above condition evaluates to:

Browser

result

Edge

`true`

Chrome

`true`

Firefox

`true`

IE 11

`false`

Safari iOS

`true`

Installing
----------

QuaggaJS can be installed using **npm**, **bower**, or by including it with the **script** tag.

### NPM

\> npm install quagga

And then import it as dependency in your project:

import Quagga from 'quagga'; // ES6
const Quagga \= require('quagga').default; // Common JS (important: default)

Currently, the full functionality is only available through the browser. When using QuaggaJS within **node**, only file-based decoding is available. See the example for node\_examples.

### Bower

You can also install QuaggaJS through **bower**:

\> bower install quagga

### Script-Tag Anno 1998

You can simply include `dist/quagga.min.js` in your project and you are ready to go. The script exposes the library on the global namespace under `Quagga`.

Getting Started
---------------

For starters, have a look at the examples to get an idea where to go from here.

Building
--------

You can build the library yourself by simply cloning the repo and typing:

\> npm install
> npm run build

This npm script builds a non optimized version `quagga.js` and a minified version `quagga.min.js` and places both files in the `dist` folder. Additionally, a `quagga.map` source-map is placed alongside these files. This file is only valid for the non-uglified version `quagga.js` because the minified version is altered after compression and does not align with the map file any more.

### Node

The code in the `dist` folder is only targeted to the browser and won't work in node due to the dependency on the DOM. For the use in node, the `build` command also creates a `quagga.js` file in the `lib` folder.

API
---

You can check out the examples to get an idea of how to use QuaggaJS. Basically the library exposes the following API:

### Quagga.init(config, callback)

This method initializes the library for a given configuration `config` (see below) and invokes the `callback(err)` when Quagga has finished its bootstrapping phase. The initialization process also requests for camera access if real-time detection is configured. In case of an error, the `err` parameter is set and contains information about the cause. A potential cause may be the `inputStream.type` is set to `LiveStream`, but the browser does not support this API, or simply if the user denies the permission to use the camera.

If you do not specify a target, QuaggaJS would look for an element that matches the CSS selector `#interactive.viewport` (for backwards compatibility). `target` can be a string (CSS selector matching one of your DOM node) or a DOM node.

Quagga.init({
    inputStream : {
      name : "Live",
      type : "LiveStream",
      target: document.querySelector('#yourElement')    // Or '#yourElement' (optional)
    },
    decoder : {
      readers : \["code\_128\_reader"\]
    }
  }, function(err) {
      if (err) {
          console.log(err);
          return
      }
      console.log("Initialization finished. Ready to start");
      Quagga.start();
  });

### Quagga.start()

When the library is initialized, the `start()` method starts the video-stream and begins locating and decoding the images.

### Quagga.stop()

If the decoder is currently running, after calling `stop()` the decoder does not process any more images. Additionally, if a camera-stream was requested upon initialization, this operation also disconnects the camera.

### Quagga.onProcessed(callback)

This method registers a `callback(data)` function that is called for each frame after the processing is done. The `data` object contains detailed information about the success/failure of the operation. The output varies, depending whether the detection and/or decoding were successful or not.

### Quagga.onDetected(callback)

Registers a `callback(data)` function which is triggered whenever a barcode- pattern has been located and decoded successfully. The passed `data` object contains information about the decoding process including the detected code which can be obtained by calling `data.codeResult.code`.

### Quagga.decodeSingle(config, callback)

In contrast to the calls described above, this method does not rely on `getUserMedia` and operates on a single image instead. The provided callback is the same as in `onDetected` and contains the result `data` object.

### Quagga.offProcessed(handler)

In case the `onProcessed` event is no longer relevant, `offProcessed` removes the given `handler` from the event-queue.

### Quagga.offDetected(handler)

In case the `onDetected` event is no longer relevant, `offDetected` removes the given `handler` from the event-queue.

The result object
-----------------

The callbacks passed into `onProcessed`, `onDetected` and `decodeSingle` receive a `data` object upon execution. The `data` object contains the following information. Depending on the success, some fields may be `undefined` or just empty.

{
  "codeResult": {
    "code": "FANAVF1461710",  // the decoded code as a string
    "format": "code\_128", // or code\_39, codabar, ean\_13, ean\_8, upc\_a, upc\_e
    "start": 355,
    "end": 26,
    "codeset": 100,
    "startInfo": {
      "error": 1.0000000000000002,
      "code": 104,
      "start": 21,
      "end": 41
    },
    "decodedCodes": \[{
      "code": 104,
      "start": 21,
      "end": 41
    },
    // stripped for brevity
    {
      "error": 0.8888888888888893,
      "code": 106,
      "start": 328,
      "end": 350
    }\],
    "endInfo": {
      "error": 0.8888888888888893,
      "code": 106,
      "start": 328,
      "end": 350
    },
    "direction": \-1
  },
  "line": \[{
    "x": 25.97278706156836,
    "y": 360.5616435369468
  }, {
    "x": 401.9220519377024,
    "y": 70.87524989906444
  }\],
  "angle": \-0.6565217179979483,
  "pattern": \[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, /\* ... \*/ 1\],
  "box": \[
    \[77.4074243622672, 410.9288668804402\],
    \[0.050203235235130705, 310.53619724086366\],
    \[360.15706727788256, 33.05711026051813\],
    \[437.5142884049146, 133.44977990009465\]
  \],
  "boxes": \[
    \[
      \[77.4074243622672, 410.9288668804402\],
      \[0.050203235235130705, 310.53619724086366\],
      \[360.15706727788256, 33.05711026051813\],
      \[437.5142884049146, 133.44977990009465\]
    \],
    \[
      \[248.90769330706507, 415.2041489551161\],
      \[198.9532321622869, 352.62160512937635\],
      \[339.546160777576, 240.3979259789976\],
      \[389.5006219223542, 302.98046980473737\]
    \]
  \]
}

Configuration
-------------

The configuration that ships with QuaggaJS covers the default use-cases and can be fine-tuned for specific requirements.

The configuration is managed by the `config` object defining the following high-level properties:

{
  numOfWorkers: 4,
  locate: true,
  inputStream: {...},
  frequency: 10,
  decoder:{...},
  locator: {...},
  debug: false,
}

### numOfWorkers

QuaggaJS supports web-workers out of the box and runs with `4` workers in its default configuration. The number should align with the number of cores available in your targeted devices.

In case you don't know the number upfront, or if the variety of devices is too big, you can either use `navigator.hardwareConcurrency` (see here) where available or make use of core-estimator.

### locate

One of the main features of QuaggaJS is its ability to locate a barcode in a given image. The `locate` property controls whether this feature is turned on (default) or off.

Why would someone turn this feature off? Localizing a barcode is a computationally expensive operation and might not work properly on some devices. Another reason would be the lack of auto-focus producing blurry images which makes the localization feature very unstable.

However, even if none of the above apply, there is one more case where it might be useful to disable `locate`: If the orientation, and/or the approximate position of the barcode is known, or if you want to guide the user through a rectangular outline. This can increase performance and robustness at the same time.

### inputStream

The `inputStream` property defines the sources of images/videos within QuaggaJS.

{
  name: "Live",
  type: "LiveStream",
  constraints: {
    width: 640,
    height: 480,
    facingMode: "environment",
    deviceId: "7832475934759384534"
  },
  area: { // defines rectangle of the detection/localization area
    top: "0%",    // top offset
    right: "0%",  // right offset
    left: "0%",   // left offset
    bottom: "0%"  // bottom offset
  },
  singleChannel: false // true: only the red color-channel is read
}

First, the `type` property can be set to three different values: `ImageStream`, `VideoStream`, or `LiveStream` (default) and should be selected depending on the use-case. Most probably, the default value is sufficient.

Second, the `constraint` key defines the physical dimensions of the input image and additional properties, such as `facingMode` which sets the source of the user's camera in case of multiple attached devices. Additionally, if required, the `deviceId` can be set if the selection of the camera is given to the user. This can be easily achieved via MediaDevices.enumerateDevices()

Thirdly, the `area` prop restricts the decoding area of the image. The values are given in percentage, similar to the CSS style property when using `position: absolute`. This `area` is also useful in cases the `locate` property is set to `false`, defining the rectangle for the user.

The last key `singleChannel` is only relevant in cases someone wants to debug erroneous behavior of the decoder. If set to `true` the input image's red color-channel is read instead of calculating the gray-scale values of the source's RGB. This is useful in combination with the `ResultCollector` where the gray-scale representations of the wrongly identified images are saved.

### frequency

This top-level property controls the scan-frequency of the video-stream. It's optional and defines the maximum number of scans per second. This renders useful for cases where the scan-session is long-running and resources such as CPU power are of concern.

### decoder

QuaggaJS usually runs in a two-stage manner (`locate` is set to `true`) where, after the barcode is located, the decoding process starts. Decoding is the process of converting the bars into its true meaning. Most of the configuration options within the `decoder` are for debugging/visualization purposes only.

{
  readers: \[
    'code\_128\_reader'
  \],
  debug: {
      drawBoundingBox: false,
      showFrequency: false,
      drawScanline: false,
      showPattern: false
  }
  multiple: false
}

The most important property is `readers` which takes an array of types of barcodes which should be decoded during the session. Possible values are:

-   code\_128\_reader (default)
-   ean\_reader
-   ean\_8\_reader
-   code\_39\_reader
-   code\_39\_vin\_reader
-   codabar\_reader
-   upc\_reader
-   upc\_e\_reader
-   i2of5\_reader
-   2of5\_reader
-   code\_93\_reader

Why are not all types activated by default? Simply because one should explicitly define the set of barcodes for their use-case. More decoders means more possible clashes, or false-positives. One should take care of the order the readers are given, since some might return a value even though it is not the correct type (EAN-13 vs. UPC-A).

The `multiple` property tells the decoder if it should continue decoding after finding a valid barcode. If multiple is set to `true`, the results will be returned as an array of result objects. Each object in the array will have a `box`, and may have a `codeResult` depending on the success of decoding the individual box.

The remaining properties `drawBoundingBox`, `showFrequency`, `drawScanline` and `showPattern` are mostly of interest during debugging and visualization.

#### Enabling extended EAN

The default setting for `ean_reader` is not capable of reading extensions such as EAN-2 or EAN-5. In order to activate those supplements you have to provide them in the configuration as followed:

decoder: {
    readers: \[{
        format: "ean\_reader",
        config: {
            supplements: \[
                'ean\_5\_reader', 'ean\_2\_reader'
            \]
        }
    }\]
}

Beware that the order of the `supplements` matters in such that the reader stops decoding when the first supplement was found. So if you are interested in EAN-2 and EAN-5 extensions, use the order depicted above.

It's important to mention that, if supplements are supplied, regular EAN-13 codes cannot be read any more with the same reader. If you want to read EAN-13 with and without extensions you have to add another `ean_reader` reader to the configuration.

### locator

The `locator` config is only relevant if the `locate` flag is set to `true`. It controls the behavior of the localization-process and needs to be adjusted for each specific use-case. The default settings are simply a combination of values which worked best during development.

Only two properties are relevant for the use in Quagga (`halfSample` and `patchSize`) whereas the rest is only needed for development and debugging.

{
  halfSample: true,
  patchSize: "medium", // x-small, small, medium, large, x-large
  debug: {
    showCanvas: false,
    showPatches: false,
    showFoundPatches: false,
    showSkeleton: false,
    showLabels: false,
    showPatchLabels: false,
    showRemainingPatchLabels: false,
    boxFromPatches: {
      showTransformed: false,
      showTransformedBox: false,
      showBB: false
    }
  }
}

The `halfSample` flag tells the locator-process whether it should operate on an image scaled down (half width/height, quarter pixel-count ) or not. Turning `halfSample` on reduces the processing-time significantly and also helps finding a barcode pattern due to implicit smoothing. It should be turned off in cases where the barcode is really small and the full resolution is needed to find the position. It's recommended to keep it turned on and use a higher resolution video-image if needed.

The second property `patchSize` defines the density of the search-grid. The property accepts strings of the value `x-small`, `small`, `medium`, `large` and `x-large`. The `patchSize` is proportional to the size of the scanned barcodes. If you have really large barcodes which can be read close-up, then the use of `large` or `x-large` is recommended. In cases where the barcode is further away from the camera lens (lack of auto-focus, or small barcodes) then it's advised to set the size to `small` or even `x-small`. For the latter it's also recommended to crank up the resolution in order to find a barcode.

Examples
--------

The following example takes an image `src` as input and prints the result on the console. The decoder is configured to detect _Code128_ barcodes and enables the locating-mechanism for more robust results.

Quagga.decodeSingle({
    decoder: {
        readers: \["code\_128\_reader"\] // List of active readers
    },
    locate: true, // try to locate the barcode in the image
    src: '/test/fixtures/code\_128/image-001.jpg' // or 'data:image/jpg;base64,' + data
}, function(result){
    if(result.codeResult) {
        console.log("result", result.codeResult.code);
    } else {
        console.log("not detected");
    }
});

### Using node

The following example illustrates the use of QuaggaJS within a node environment. It's almost identical to the browser version with the difference that node does not support web-workers out of the box. Therefore the config property `numOfWorkers` must be explicitly set to `0`.

var Quagga \= require('quagga').default;

Quagga.decodeSingle({
    src: "image-abc-123.jpg",
    numOfWorkers: 0,  // Needs to be 0 when used within node
    inputStream: {
        size: 800  // restrict input-size to be 800px in width (long-side)
    },
    decoder: {
        readers: \["code\_128\_reader"\] // List of active readers
    },
}, function(result) {
    if(result.codeResult) {
        console.log("result", result.codeResult.code);
    } else {
        console.log("not detected");
    }
});

Tips & Tricks
-------------

A growing collection of tips & tricks to improve the various aspects of Quagga.

### Barcodes too small?

Barcodes too far away from the camera, or a lens too close to the object result in poor recognition rates and Quagga might respond with a lot of false-positives.

Starting in Chrome 59 you can now make use of `capabilities` and directly control the zoom of the camera. Head over to the web-cam demo and check out the **Zoom** feature.

You can read more about those `capabilities` in Let's light a torch and explore MediaStreamTrack's capabilities

### Video too dark?

Dark environments usually result in noisy images and therefore mess with the recognition logic.

Since Chrome 59 you can turn on/off the **Torch** of our device and vastly improve the quality of the images. Head over to the web-cam demo and check out the **Torch** feature.

To find out more about this feature read on.

Tests
-----

Unit Tests can be run with Karma and written using Mocha, Chai and SinonJS. Coverage reports are automatically generated in the coverage/ folder.

\> npm install
> npm run test

Image Debugging
---------------

In case you want to take a deeper dive into the inner workings of Quagga, get to know the _debugging_ capabilities of the current implementation. The various flags exposed through the `config` object give you the abilily to visualize almost every step in the processing. Because of the introduction of the web-workers, and their restriction not to have access to the DOM, the configuration must be explicitly set to `config.numOfWorkers = 0` in order to work.

ResultCollector
---------------

Quagga is not perfect by any means and may produce false positives from time to time. In order to find out which images produced those false positives, the built-in `ResultCollector` will support you and me helping squashing bugs in the implementation.

### Creating a `ResultCollector`

You can easily create a new `ResultCollector` by calling its `create` method with a configuration.

var resultCollector \= Quagga.ResultCollector.create({
    capture: true, // keep track of the image producing this result
    capacity: 20,  // maximum number of results to store
    blacklist: \[   // list containing codes which should not be recorded
        {code: "3574660239843", format: "ean\_13"}\],
    filter: function(codeResult) {
        // only store results which match this constraint
        // returns true/false
        // e.g.: return codeResult.format === "ean\_13";
        return true;
    }
});

### Using a `ResultCollector`

After creating a `ResultCollector` you have to attach it to Quagga by calling `Quagga.registerResultCollector(resultCollector)`.

### Reading results

After a test/recording session, you can now print the collected results which do not fit into a certain schema. Calling `getResults` on the `resultCollector` returns an `Array` containing objects with:

{
    codeResult: {}, // same as in onDetected event
    frame: "data:image/png;base64,iVBOR..." // dataURL of the gray-scaled image
}

The `frame` property is an internal representation of the image and therefore only available in gray-scale. The dataURL representation allows easy saving/rendering of the image.

### Comparing results

Now, having the frames available on disk, you can load each single image by calling `decodeSingle` with the same configuration as used during recording . In order to reproduce the exact same result, you have to make sure to turn on the `singleChannel` flag in the configuration when using `decodeSingle`.

Sponsors
--------

-   Maintenance Connection Canada (Asset Pro Solutions Inc.

Changelog
---------

### 2017-06-07

-   Improvements
    -   added `muted` and `playsinline` to `<video/>` to make it work for Safari 11 Beta (even iOS)
-   Fixes
    -   Fixed example/live\_w\_locator.js

### 2017-06-06

-   Features
    -   Support for Standard 2of5 barcodes (See #194)
    -   Support for Code 93 barcodes (See #194)
    -   Exposing `Quagga.CameraAccess.getActiveTrack()` to get access to the currently used `MediaStreamTrack`
        -   Example can be viewed here: example/live\_w\_locator.js and a demo

Take a look at the release-notes ( 0.12.0)

### 2017-01-08

-   Improvements
    -   Exposing `CameraAccess` module to get access to methods like `enumerateVideoDevices` and `getActiveStreamLabel` (see `example/live_w_locator`)
    -   Update to webpack 2.2 (API is still unstable)

### 2016-10-03

-   Fixes
    -   Fixed `facingMode` issue with Chrome >= 53 (see #128)

### 2016-08-15

-   Features
    -   Proper handling of EXIF orientation when using `Quagga.decodeSingle` (see #121)

### 2016-04-24

-   Features
    -   EAN-13 extended codes can now be decoded (See #71)

Take a look at the release-notes ( 0.11.0)

### 2016-04-19

-   Improvements
    -   Reducing false-positives for Code 128 barcodes ( addresses #104)

### 2016-03-31

Take a look at the release-notes ( 0.10.0)

### 2016-02-18

-   Internal Changes
    -   Restructuring into meaningful folders
    -   Removing debug-code in production build

### 2016-02-15

Take a look at the release-notes ( 0.9.0)

### 2015-11-22

-   Fixes
    -   Fixed inconsistencies for Code 128 decoding (See #76)

### 2015-11-15

-   Fixes
    -   Fixed inconsistency in Code 39 decoding
    -   added inline-source-map to quagga.js file

### 2015-10-13

Take a look at the release-notes (\[0.8.0\] (https://github.com/serratus/quaggaJS/releases/tag/v0.8.0))

-   Improvements
    -   Replaced RequireJS with webpack

### 2015-09-15

Take a look at the release-notes (\[0.7.0\] (https://github.com/serratus/quaggaJS/releases/tag/v0.7.0))

-   Features
    -   Added basic support for running QuaggaJS inside **node** (see \[example\] (#node-example))

### 2015-08-29

-   Improvements
    -   Added support for Internet Explorer (only Edge+ supports `getUserMedia`)

### 2015-08-13

-   Improvements
    -   Added `offProcessed` and `offDetected` methods for detaching event- listeners from the event-queue.

### 2015-07-29

-   Features
    -   Added basic support for ITF barcodes (`i2of5_reader`)

### 2015-07-08

-   Improvements
    -   Parameter tweaking to reduce false-positives significantly (for the entire EAN and UPC family)
    -   Fixing bug in parity check for UPC-E codes
    -   Fixing bug in alignment for EAN-8 codes

### 2015-07-06

-   Improvements
    -   Added `err` parameter to Quagga.init() callback function

### 2015-06-21

-   Features
    -   Added `singleChannel` configuration to `inputStream` (in \[config\] (#configobject))
    -   Added `ResultCollector` functionality (see \[ResultCollector\] (#resultcollector))

### 2015-06-13

-   Improvements
    -   Added `format` property to `codeResult` (in result)

### 2015-06-13

-   Improvements
    -   Added fixes for `Code39Reader` (trailing whitespace was missing)

### 2015-06-09

-   Features
    -   Introduced the `area` property
    -   Ability to define a rectangle where localization/decoding should be applied

### 2015-05-20

-   Improvements
    -   Making EAN and UPC readers even more restrictive
    -   Added example using requirejs

### 2015-05-18

-   Improvements
    -   Making EAN and UPC readers more restrictive
    -   Added integration-tests for all barcode-readers

### 2015-05-09

-   Improvements
    -   Odd image dimensions no longer cause problems

### 2015-04-30

-   Features
    -   Added support for UPC-A and UPC-E barcodes
    -   Added support for EAN-8 barcodes
-   Improvements
    -   Added extended configuration to the live-video example
    -   Releasing resources when calling `Quagga.stop()`

### 2015-04-25

-   Improvements
    -   Added extended configuration to the file-input example
    -   Configurable `patchSize` for better adjustment to small/medium/large barcodes

### 2015-04-16

-   Features
    -   Added support for Codabar barcodes

### 2015-03-16

-   Improvements
    -   now includes minified version (23.3KB gzipped)
    -   No need for configuration of script-name any more

### 2015-03-12

-   Improvements
    -   removed dependency on async.js

### 2015-03-04

-   Features
    -   Added support for Code 39 barcodes

### 2015-01-21

-   Features
    -   Added support for web-worker (using 4 workers as default, can be changed through `config.numOfWorkers`)
    -   Due to the way how web-workers are created, the name of the script file (`config.scriptName`) should be kept in sync with your actual filename
    -   Removed canvas-overlay for decoding (boxes & scanline) which can now be easily implemented using the existing API (see example)
-   API Changes In the course of implementing web-workers some breaking changes were introduced to the API.
    -   The `Quagga.init` function no longer receives the callback as part of the config but rather as a second argument: `Quagga.init(config, cb)`
    -   The callback to `Quagga.onDetected` now receives an object containing much more information in addition to the decoded code.(see data)
    -   Added `Quagga.onProcessed(callback)` which provides a way to get information for each image processed. The callback receives the same `data` object as `Quagga.onDetected` does. Depending on the success of the process the `data` object might not contain any `resultCode` and/or `box` properties.
