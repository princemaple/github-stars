---
project: brotli-webpack-plugin
stars: 214
description: Prepare Brotli-compressed versions of assets to serve them with Content-Encoding: br
url: https://github.com/mynameiswhm/brotli-webpack-plugin
---

brotli plugin for webpack
=========================

This plugin compresses assets with Brotli compression algorithm using zlib, iltorb or brotli.js libraries for serving it with ngx\_brotli or such.

Installation
------------

```
npm install --save-dev brotli-webpack-plugin
```

Usage
-----

var BrotliPlugin \= require('brotli-webpack-plugin');
module.exports \= {
	plugins: \[
		new BrotliPlugin({
			asset: '\[path\].br\[query\]',
			test: /\\.(js|css|html|svg)$/,
			threshold: 10240,
			minRatio: 0.8
		})
	\]
}

Arguments:

-   `asset`: The target asset name. Defaults to `'[path].br[query]'`.
    -   `[file]` is replaced with the original asset file name.
    -   `[fileWithoutExt]` is replaced with the file name minus its extension, e.g. the `style` of `style.css`.
    -   `[ext]` is replaced with the file name extension, e.g. the `css` of `style.css`.
    -   `[path]` is replaced with the path of the original asset.
    -   `[query]` is replaced with the query.
-   `test`: All assets matching this RegExp are processed. Defaults to every asset.
-   `threshold`: Only assets bigger than this size (in bytes) are processed. Defaults to `0`.
-   `minRatio`: Only assets that compress better that this ratio are processed. Defaults to `0.8`.
-   `deleteOriginalAssets`: remove original files that were compressed with brotli. Default: false

Optional arguments for Brotli (see iltorb doc for details):

-   `mode`: Default: 0,
-   `quality`: Default: 11,
-   `lgwin`: Default: 22,
-   `lgblock`: Default: 0,
-   `size_hint`: Default: 0,
-   `disable_literal_context_modeling`: Default: false

License
-------

Heavily copy-pasted from webpack/compression-webpack-plugin by Tobias Koppers.

Licensed under MIT.
