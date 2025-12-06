---
project: uid
stars: 666
description: A tiny (130B to 205B) and fast utility to generate random IDs of fixed length
url: https://github.com/lukeed/uid
---

uid
===

> A tiny (130B to 205B) and fast utility to randomize unique IDs of fixed length

_**Fast object IDs.** Available for Node.js and the browser._  
Generate **randomized** output strings of fixed length using lowercase alphanumeric characters (`a-z0-9`). To produce IDs in UUID.V4 format, please see `@lukeed/uuid`.

This module offers multiple modes for your needs:

-   `uid`  
    _The default is "non-secure", which uses `Math.random` to produce UUIDs._
-   `uid/secure`  
    _The "secure" mode produces cryptographically secure (CSPRNG) UUIDs using the current environment's `crypto` module._
-   `uid/single`  
    _The "single" mode does not maintain an internal cache, which makes it ideal for short-lived environments._

Additionally, this module is preconfigured for native ESM support in Node.js with fallback to CommonJS. It will also work with any Rollup and webpack configuration, regardless of the "mode" selected.

Install
-------

```
$ npm install --save uid
```

Modes
-----

There are three "versions" of `uid` available:

#### `uid`

> **Size (gzip):** 174 bytes  
> **Availability:** CommonJS, ES Module, UMD

Relies on `Math.random`, which means that, while faster, this mode **is not** cryptographically secure.  
Works in Node.js and all browsers.  
Alphabet: _**Hexadecimal**_

#### `uid/secure`

> **Size (gzip):** 205 bytes  
> **Availability:** CommonJS, ES Module, UMD

Relies on the environment's `crypto` module in order to produce cryptographically secure (CSPRNG) values.  
Works in all versions of Node.js. Works in all browsers with `crypto.getRandomValues()` support.  
Alphabet: _**Hexadecimal**_

#### `uid/single`

> **Size (gzip):** 131 bytes  
> **Availability:** CommonJS, ES Module, UMD

Relies on `Math.random`, which means that this mode **is not** cryptographically secure.  
Does **not** maintain an internal buffer, which makes this mode ideal for single-use and/or short-lived environments.  
Works in Node.js and all browsers.  
Alphabet: _**Alphanumeric**_

Usage
-----

import { uid } from 'uid';
// or: import { uid } from 'uid/secure';
// or: import { uid } from 'uid/single';

// length = 11 (default)
uid(); //=> 'c92054d1dd6'
uid(); //=> 'ac84bbb3728'

// customize length
uid(16); //=> '8234dbf9a7dcec3b'
uid(25); //=> '4bbb3728b7a00a12209ec5ff5'
uid(32); //=> 'dcbc3e65506a7e6f15d30a357e884432'

API
---

### uid(length?)

Returns: `String`

Creates a new random identifer of fixed length.

#### length

Type: `Number`  
Default: `11`

Then length of the output string.

> **Important:** Your risk of collisions decreases with longer strings!

Benchmarks
----------

You can run the benchmark(s) yourself via the `/bench` directory.

All items listed pass a validation step for length and uniqueness.  
Items marked with a `†` are cryptographically secure (via CSPRNG).

> Running on Node.js v12.18.4

```
Benchmark (length = 11):
  hashids/fixed        x   387,306 ops/sec ±1.03% (92 runs sampled)
  nanoid/non-secure    x  5,338,433 ops/sec ±0.20% (95 runs sampled)
† nanoid               x  2,705,158 ops/sec ±0.31% (95 runs sampled)
† uid/secure           x  9,648,755 ops/sec ±0.18% (96 runs sampled)
  uid/single           x  4,843,529 ops/sec ±0.19% (96 runs sampled)
  uid                  x 21,276,788 ops/sec ±0.37% (94 runs sampled)

Benchmark (length = 16):
  hashids/fixed        x    409,228 ops/sec ±0.36% (98 runs sampled)
  nanoid/non-secure    x  3,643,896 ops/sec ±1.27% (96 runs sampled)
† nanoid               x  2,273,555 ops/sec ±0.15% (95 runs sampled)
† uid/secure           x  9,167,545 ops/sec ±0.32% (95 runs sampled)
  uid/single           x  3,624,579 ops/sec ±0.29% (95 runs sampled)
  uid                  x 24,770,463 ops/sec ±0.41% (97 runs sampled)

Benchmark (length = 25):
  cuid                 x    177,241 ops/sec ±1.38% (91 runs sampled)
  hashids/fixed        x    396,013 ops/sec ±0.21% (98 runs sampled)
  nanoid/non-secure    x  2,477,463 ops/sec ±0.37% (96 runs sampled)
† nanoid               x  1,794,062 ops/sec ±0.18% (97 runs sampled)
† uid/secure           x  3,778,663 ops/sec ±0.16% (95 runs sampled)
  uid/single           x  2,428,167 ops/sec ±0.27% (96 runs sampled)
  uid                  x 24,580,091 ops/sec ±0.31% (96 runs sampled)

Benchmark (length = 36):
  uuid/v1              x  1,738,574 ops/sec ±0.36% (97 runs sampled)
  uuid/v4              x  1,276,888 ops/sec ±0.26% (94 runs sampled)
  hashids/fixed        x    374,294 ops/sec ±0.14% (98 runs sampled)
  nanoid/non-secure    x  1,816,630 ops/sec ±0.31% (97 runs sampled)
† nanoid               x  1,364,928 ops/sec ±0.18% (95 runs sampled)
† @lukeed/uuid/secure  x  5,144,752 ops/sec ±0.28% (93 runs sampled)
  @lukeed/uuid         x  5,950,932 ops/sec ±0.53% (95 runs sampled)
† uid/secure           x  5,163,209 ops/sec ±0.32% (96 runs sampled)
  uid/single           x  1,755,748 ops/sec ±0.24% (99 runs sampled)
  uid                  x 20,166,119 ops/sec ±0.66% (94 runs sampled)
```

> Running on Chrome 85.0.4183.121

```
Benchmark (length = 11):
  hashids/fixed        x    369,393 ops/sec ±1.04% (67 runs sampled)
  nanoid/non-secure    x  4,741,795 ops/sec ±0.67% (68 runs sampled)
† nanoid               x    176,138 ops/sec ±7.17% (57 runs sampled)
† uid/secure           x  2,061,703 ops/sec ±3.95% (65 runs sampled)
  uid/single           x  4,547,527 ops/sec ±0.29% (67 runs sampled)
  uid                  x 21,073,518 ops/sec ±0.60% (67 runs sampled)

Benchmark (length = 16):
  hashids/fixed        x    362,882 ops/sec ±0.25% (67 runs sampled)
  nanoid/non-secure    x  3,245,036 ops/sec ±1.05% (67 runs sampled)
† nanoid               x    165,535 ops/sec ±5.21% (59 runs sampled)
† uid/secure           x  1,676,705 ops/sec ±0.25% (68 runs sampled)
  uid/single           x  3,322,695 ops/sec ±0.49% (67 runs sampled)
  uid                  x 24,074,441 ops/sec ±0.35% (67 runs sampled)

Benchmark (length = 25):
  cuid                 x     99,011 ops/sec ±6.09% (57 runs sampled)
  hashids/fixed        x    349,187 ops/sec ±0.21% (68 runs sampled)
  nanoid/non-secure    x  2,245,251 ops/sec ±1.21% (61 runs sampled)
† nanoid               x    143,529 ops/sec ±4.53% (62 runs sampled)
† uid/secure           x    936,133 ops/sec ±2.14% (67 runs sampled)
  uid/single           x  2,276,265 ops/sec ±1.17% (66 runs sampled)
  uid                  x 23,409,912 ops/sec ±1.81% (67 runs sampled)

Benchmark (length = 36):
  uuid/v1              x  1,695,352 ops/sec ±0.26% (67 runs sampled)
  uuid/v4              x    294,032 ops/sec ±1.75% (63 runs sampled)
  hashids/fixed        x    340,402 ops/sec ±0.37% (50 runs sampled)
  nanoid/non-secure    x  1,611,905 ops/sec ±0.45% (66 runs sampled)
† nanoid               x    118,006 ops/sec ±6.31% (52 runs sampled)
† @lukeed/uuid/secure  x    859,592 ops/sec ±0.54% (67 runs sampled)
  @lukeed/uuid         x  6,041,873 ops/sec ±0.33% (66 runs sampled)
† uid/secure           x    776,658 ops/sec ±0.31% (56 runs sampled)
  uid/single           x  1,646,199 ops/sec ±1.17% (66 runs sampled)
  uid                  x 22,779,817 ops/sec ±0.66% (67 runs sampled)
```

Performance
-----------

The reason `uid` and `uid/secure` are so much faster than its alternatives is two-fold:

1.  It composes an output with hexadecimal pairs (from a cached dictionary) instead of single characters.
2.  It allocates a larger Buffer/ArrayBuffer up front (expensive) and slices off chunks as needed (cheap).

The `uid/secure` module maintains an internal ArrayBuffer of 4096 bytes, which supplies **256** `uid()` invocations. However, the default module (`uid`) preallocates **512** invocations using less memory upfront. Both implementations will regenerate its internal allocation as needed.

Larger buffers would result in higher performance over time, but I found these to be a good balance of performance and memory space.

> **Note:** If you want to don't want to preallocate memory, and do not need a CSPRNG, check out the `uid/single` mode.

Related
-------

-   hexoid - A slightly larger (190B) but extremely fast variant of this module with a different API
-   @lukeed/uuid - A tiny (230B), fast, and cryptographically secure UUID (V4) generator for Node and the browser

Credits
-------

Thank you Matthew Mueller for gifting the `uid` name on npm.  
This module was previously known as `foid` (fast object IDs).

License
-------

MIT © Luke Edwards
