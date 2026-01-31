---
project: barcode-detector
stars: 189
description: A Barcode Detection API ponyfill/polyfill that uses ZXing-C++ WebAssembly under the hood.
url: https://github.com/Sec-ant/barcode-detector
---

barcode-detector
================

A Barcode Detection API ponyfill/polyfill that uses ZXing-C++ WebAssembly under the hood.

Supported barcode formats:

Linear Barcode Formats

Matrix Barcode Formats

Special Barcode Formats

`codabar`

`aztec`

   `linear_codes`1

`code_39`

`data_matrix`

   `matrix_codes`2

`code_93`

   `maxi_code`3

   `any`4

`code_128`

`pdf417`

`databar`

`qr_code`

`databar_limited`

`micro_qr_code`

`databar_expanded`

`rm_qr_code`

`dx_film_edge`

`ean_8`

`ean_13`

`itf`

`upc_a`

`upc_e`

Install
-------

To install, run the following command:

npm i barcode-detector

Usage
-----

### Ponyfill

import { BarcodeDetector } from "barcode-detector/ponyfill";

To avoid potential namespace collisions, you can also rename the export:

import { BarcodeDetector as BarcodeDetectorPonyfill } from "barcode-detector/ponyfill";

A ponyfill is a module required to be explicitly imported without introducing side effects. Use this subpath if you want to avoid polluting the global object with the `BarcodeDetector` class, or if you intend to use the implementation provided by this package instead of the native one.

### Polyfill

import "barcode-detector/polyfill";

This subpath is used to polyfill the native `BarcodeDetector` class. It will automatically register the `BarcodeDetector` class in the global object **_if it's not already present_**.

Important

The polyfill will opt in only if no `BarcodeDetector` is present in `globalThis`. It basically works like this:

import { BarcodeDetector } from "barcode-detector/ponyfill";
globalThis.BarcodeDetector ??= BarcodeDetector;

Note that it **_doesn't_** check if the implementation is provided natively or by another polyfill. It also **_doesn't_** try to augment the existing implementation with all the barcode formats supported by this package. If you want all the features provided by this package, but you already have a native or another polyfilled `BarcodeDetector`, you should use the ponyfill approach. You can register it to the `globalThis` object manually if you want to.

### Ponyfill + Polyfill

import { BarcodeDetector } from "barcode-detector";

This approach combines the ponyfill and polyfill approaches.

Note

The `ponyfill` subpath was named `pure` and the `polyfill` subpath was named `side-effects` in early versions. They are no longer recommended for use and are considered deprecated. Please use the new subpaths as described above.

### `<script type="module">`

For modern browsers that support ES modules, this package can be imported via the `<script type="module">` tags:

1.  Include the polyfill:
    
    <!-- register -->
    <script
      type\="module"
      src\="https://fastly.jsdelivr.net/npm/barcode-detector@3/dist/es/polyfill.min.js"
    \></script\>
    
    <!-- use -->
    <script type\="module"\>
      const barcodeDetector \= new BarcodeDetector();
    </script\>
    
2.  Script scoped access:
    
    <script type\="module"\>
      import { BarcodeDetector } from "https://fastly.jsdelivr.net/npm/barcode-detector@3/dist/es/ponyfill.min.js";
      const barcodeDetector \= new BarcodeDetector();
    </script\>
    
3.  With import maps:
    
    <!-- import map -->
    <script type\="importmap"\>
      {
        "imports": {
          "barcode-detector/ponyfill": "https://fastly.jsdelivr.net/npm/barcode-detector@3/dist/es/ponyfill.min.js"
        }
      }
    </script\>
    
    <!-- script scoped access -->
    <script type\="module"\>
      import { BarcodeDetector } from "barcode-detector/ponyfill";
      const barcodeDetector \= new BarcodeDetector();
    </script\>
    

### IIFE

For legacy browsers or userscripts that lack support for `<script type="module">` tags, IIFE is the preferred choice. Upon executing the IIFE script, a variable named `BarcodeDetectionAPI` will be registered in the global `window` by `var` declaration.

<!-- 
  IIFE ponyfill.js registers:
  window.BarcodeDetectionAPI.BarcodeDetector
  window.BarcodeDetectionAPI.prepareZXingModule
  -->
<script src\="https://fastly.jsdelivr.net/npm/barcode-detector@3/dist/iife/ponyfill.min.js"\></script\>

<!-- 
  IIFE polyfill.js registers:
  window.BarcodeDetector
  window.BarcodeDetectionAPI.prepareZXingModule
  -->
<script src\="https://fastly.jsdelivr.net/npm/barcode-detector@3/dist/iife/polyfill.min.js"\></script\>

<!-- 
  IIFE index.js registers:
  window.BarcodeDetector
  window.BarcodeDetectionAPI.BarcodeDetector
  window.BarcodeDetectionAPI.prepareZXingModule
  -->
<script src\="https://fastly.jsdelivr.net/npm/barcode-detector@3/dist/iife/index.min.js"\></script\>

`prepareZXingModule`
--------------------

The core barcode reading functionality of this package is powered by `zxing-wasm`. Therefore, a `.wasm` binary file is fetched at runtime. By default, the `.wasm` serving path is initialized with a jsDelivr CDN URL. However, there're cases where this is not desired, such as the allowed serving path is white-listed by the Content Security Policy (CSP), or offline usage is required.

To customize the `.wasm` serving path, this package reexports `prepareZXingModule` along with `ZXING_WASM_VERSION`, `ZXING_WASM_SHA256` and `ZXING_CPP_COMMIT` from `zxing-wasm`. For more details on how to use them, please check Configuring `.wasm` Serving and Controlling `.wasm` Instantiation Timing and Caching sections in the `zxing-wasm` repository.

An example usage to override the `.wasm` serving path with an `unpkg.com` CDN url is as follows:

import {
  BarcodeDetector,
  ZXING\_WASM\_VERSION,
  prepareZXingModule,
} from "barcode-detector/ponyfill";

// Override the locateFile function
prepareZXingModule({
  overrides: {
    locateFile: (path, prefix) \=> {
      if (path.endsWith(".wasm")) {
        return \`https://unpkg.com/zxing-wasm@${ZXING\_WASM\_VERSION}/dist/reader/${path}\`;
      }
      return prefix + path;
    },
  },
});

// Now you can create a BarcodeDetector instance
const barcodeDetector \= new BarcodeDetector({
  formats: \["qr\_code"\],
});

Note

The `setZXingModuleOverrides` method is deprecated in favor of `prepareZXingModule`.

API
---

Please check the spec, MDN doc and Chromium implementation for more information.

An example usage is as follows:

import { BarcodeDetector } from "barcode-detector/ponyfill";

// check supported formats
const supportedFormats \= await BarcodeDetector.getSupportedFormats();

const barcodeDetector: BarcodeDetector \= new BarcodeDetector({
  // make sure the formats are supported
  formats: \["qr\_code"\],
});

const imageFile \= await fetch(
  "https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=Hello%20world!",
).then((resp) \=> resp.blob());

barcodeDetector.detect(imageFile).then(console.log);

License
-------

The source code in this repository is licensed under the MIT license.

Footnotes
---------

1.  `linear_codes` is a shorthand for all linear barcode formats. ↩
    
2.  `matrix_codes` is a shorthand for all matrix barcode formats. ↩
    
3.  Detection support for `MaxiCode` requires a pure monochrome image that contains an unrotated and unskewed symbol, along with a sufficient white border surrounding it. ↩
    
4.  `any` is a shorthand for `linear_codes` and `matrix_codes`, i.e., all barcode formats. Note that you don't need to specify `any` in the `formats` option, as not providing the option also indicates detecting all barcode formats. ↩
