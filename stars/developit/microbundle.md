---
project: microbundle
stars: 8148
description: 📦 Zero-configuration bundler for tiny modules.
url: https://github.com/developit/microbundle
---

Microbundle
===========

The **zero-configuration** bundler for _tiny modules_, powered by Rollup.

* * *

**Guide →** Setup ✯ Formats ✯ Modern Mode ✯ Usage & Configuration ✯ All Options

* * *

✨ Features
----------

-   **One dependency** to bundle your library using only a `package.json`
-   Support for ESnext & async/await _(via Babel & async-to-promises)_
-   Produces tiny, optimized code for all inputs
-   Supports multiple entry modules _(`cli.js` + `index.js`, etc)_
-   Creates multiple output formats for each entry _(CJS, UMD & ESM)_
-   0 configuration TypeScript support
-   Built-in Terser compression & gzipped bundle size tracking

🔧 Installation & Setup
-----------------------

1️⃣ **Install** by running: `npm i -D microbundle`

2️⃣ **Set up** your `package.json`:

{
  "name": "foo",                      // your package name
  "type": "module",
  "source": "src/foo.js",             // your source code
  "exports": {
    "require": "./dist/foo.cjs",      // used for require() in Node 12+
    "default": "./dist/foo.modern.js" // where to generate the modern bundle (see below)
  },
  "main": "./dist/foo.cjs",           // where to generate the CommonJS bundle
  "module": "./dist/foo.module.js",   // where to generate the ESM bundle
  "unpkg": "./dist/foo.umd.js",       // where to generate the UMD bundle (also aliased as "umd:main")
  "scripts": {
    "build": "microbundle",           // compiles "source" to "main"/"module"/"unpkg"
    "dev": "microbundle watch"        // re-build when source files change
  }
}

3️⃣ **Try it out** by running `npm run build`.

💽 Output Formats
-----------------

Microbundle produces `esm`, `cjs`, `umd` bundles with your code compiled to syntax that works pretty much everywhere. While it's possible to customize the browser or Node versions you wish to support using a browserslist configuration, the default setting is optimal and strongly recommended.

🤖 Modern Mode
--------------

In addition to the above formats, Microbundle also outputs a `modern` bundle specially designed to work in _all modern browsers_. This bundle preserves most modern JS features when compiling your code, but ensures the result runs in 95% of web browsers without needing to be transpiled. Specifically, it uses Babel's "bugfixes" mode (previously known as preset-modules) to target the set of browsers that support `<script type="module">` - that allows syntax like async/await, tagged templates, arrow functions, destructured and rest parameters, etc. The result is generally smaller and faster to execute than the plain `esm` bundle.

Take the following source code for example:

// Our source, "src/make-dom.js":
export default async function makeDom(tag, props, children) {
	let el \= document.createElement(tag);
	el.append(...(await children));
	return Object.assign(el, props);
}

Compiling the above using Microbundle produces the following `modern` and `esm` bundles:

`make-dom.modern.js` (117b)

`make-dom.module.js` (194b)

export default async function (e, t, a) {
	let n \= document.createElement(e);
	n.append(...(await a));
	return Object.assign(n, t);
}

export default function (e, t, r) {
	try {
		var n \= document.createElement(e);
		return Promise.resolve(r).then(function (e) {
			return n.append.apply(n, e), Object.assign(n, t);
		});
	} catch (e) {
		return Promise.reject(e);
	}
}

**This is enabled by default.** All you have to do is add an `"exports"` field to your `package.json`:

{
	"main": "./dist/foo.umd.js", // legacy UMD output (for Node & CDN use)
	"module": "./dist/foo.module.mjs", // legacy ES Modules output (for bundlers)
	"exports": "./dist/foo.modern.mjs", // modern ES2017 output
	"scripts": {
		"build": "microbundle src/foo.js"
	}
}

The `"exports"` field can also be an object for packages with multiple entry modules:

{
	"name": "foo",
	"exports": {
		".": "./dist/foo.modern.mjs", // import "foo" (the default)
		"./lite": "./dist/lite.modern.mjs", // import "foo/lite"
		"./full": "./dist/full.modern.mjs" // import "foo/full"
	},
	"scripts": {
		"build": "microbundle src/\*.js" // build foo.js, lite.js and full.js
	}
}

📦 Usage & Configuration
------------------------

Microbundle includes two commands - `build` (the default) and `watch`. Neither require any options, but you can tailor things to suit your needs a bit if you like.

-   **`microbundle`** – bundles your code once and exits. (alias: `microbundle build`)
-   **`microbundle watch`** – bundles your code, then re-bundles when files change.

> ℹ️ Microbundle automatically determines which dependencies to inline into bundles based on your `package.json`.
> 
> Read more about How Microbundle decides which dependencies to bundle, including some example configurations.

### Specifying filenames in package.json

Unless overridden via the command line, microbundle uses the `source` property in your `package.json` to determine which of your JavaScript files to start bundling from (your "entry module"). The filenames and paths for generated bundles in each format are defined by the `main`, `umd:main`, `module` and `exports` properties in your `package.json`.

{
  "source": "src/index.js",             // input
  "main": "dist/foo.js",                // CommonJS output bundle
  "umd:main": "dist/foo.umd.js",        // UMD output bundle
  "module": "dist/foo.mjs",             // ES Modules output bundle
  "exports": {
    "types": "./dist/foo.d.ts",         // TypeScript typings for NodeNext modules
    "require": "./dist/foo.js",         // CommonJS output bundle
    "default": "./dist/foo.modern.mjs", // Modern ES Modules output bundle
  },
  "types": "dist/foo.d.ts"              // TypeScript typings
}

When deciding which bundle to use, Node.js 12+ and webpack 5+ will prefer the `exports` property, while older Node.js releases use the `main` property, and other bundlers prefer the `module` field. For more information about the meaning of the different properties, refer to the Node.js documentation.

For UMD builds, microbundle will use a camelCase version of the `name` field in your `package.json` as export name. Alternatively, this can be explicitly set by adding an `"amdName"` key in your `package.json`, or passing the `--name` command line argument.

### Usage with `{"type":"module"}` in `package.json`

Node.js 12.16+ adds a new "ES Module package", which can be enabled by adding `{"type":"module"}` to your package.json. This property changes the default source type of `.js` files to be ES Modules instead of CommonJS. When using `{"type":"module"}`, the file extension for CommonJS bundles generated by Microbundle must be changed to `.cjs`:

{
  "type": "module",
  "module": "dist/foo.js",  // ES Module bundle
  "main": "dist/foo.cjs",   // CommonJS bundle
}

### Additional Configuration Options

Config also can be overridded by the `publishConfig` property in your `package.json`.

{
  "main": "src/index.ts",          // this would be used in the dev environment (e.g. Jest)
  "publishConfig": {
    "source": "src/index.js",      // input
    "main": "dist/my-library.js",  // output
  },
  "scripts": {
    "build": "microbundle"
  }
}

### Building a single bundle with fixed output name

By default Microbundle outputs multiple bundles, one bundle per format. A single bundle with a fixed output name can be built like this:

microbundle -i lib/main.js -o dist/bundle.js --no-pkg-main -f umd

### Using with TypeScript

Just point the input to a `.ts` file through either the cli or the `source` key in your `package.json` and you’re done.

Microbundle will generally respect your TypeScript config defined in a `tsconfig.json` file with notable exceptions being the "target" and "module" settings. To ensure your TypeScript configuration matches the configuration that Microbundle uses internally it's strongly recommended that you set `"module": "ESNext"` and `"target": "ESNext"` in your `tsconfig.json`.

To ensure Microbundle does not process extraneous files, by default it only includes your entry point. If you want to include other files for compilation, such as ambient declarations, make sure to add either "files" or "include" into your `tsconfig.json`.

If you're using TypeScript with CSS Modules, you will want to set `"include": ["node_modules/microbundle/index.d.ts"]` in your `tsconfig.json` to tell TypeScript how to handle your CSS Module imports.

To ensure that your module's `.d.ts` type info is visible to other TypeScript projects that use `moduleResolution: 'NodeNext'`, add a `types` key to your `package.json`'s corresponding `exports` mapping.

### CSS and CSS Modules

Importing CSS files is supported via `import "./foo.css"`. By default, generated CSS output is written to disk. The `--css inline` command line option will inline generated CSS into your bundles as a string, returning the CSS string from the import:

// with the default external CSS:
import './foo.css'; // generates a minified .css file in the output directory

// with \`microbundle --css inline\`:
import css from './foo.css';
console.log(css); // the generated minified stylesheet

**CSS Modules:** CSS files with names ending in `.module.css` are treated as a CSS Modules. To instead treat imported `.css` files as modules, run Microbundle with `--css-modules true`. To disable CSS Modules for your project, pass `--no-css-modules` or `--css-modules false`.

The default scope name for CSS Modules is`_[name]__[local]__[hash:base64:5]` in watch mode, and `_[hash:base64:5]` for production builds. This can be customized by passing the command line argument `--css-modules "[name]_[hash:base64:7]"`, using these fields and naming conventions.

flag

import

is css module?

null

import './my-file.css';

❌

null

import './my-file.module.css';

✅

false

import './my-file.css';

❌

false

import './my-file.module.css';

❌

true

import './my-file.css';

✅

true

import './my-file.module.css';

✅

### Building Module Workers

Microbundle is able to detect and bundle Module Workers when generating bundles in the `esm` and `modern` formats. To use this feature, instantiate your Web Worker as follows:

worker \= new Worker(new URL('./worker.js', import.meta.url), { type: 'module' });
// or simply:
worker \= new Worker('./worker.js', { type: 'module' });

... then add the `--workers` flag to your build command:

microbundle --workers

For more information see @surma/rollup-plugin-off-main-thread.

### Visualize Bundle Makeup

Use the `--visualize` flag to generate a `stats.html` file at build time, showing the makeup of your bundle. Uses rollup-plugin-visualizer.

### Mangling Properties

To achieve the smallest possible bundle size, libraries often wish to rename internal object properties or class members to smaller names - transforming `this._internalIdValue` to `this._i`. Microbundle doesn't do this by default, however it can be enabled by creating a `mangle.json` file (or a `"mangle"` property in your package.json). Within that file, you can specify a regular expression pattern to control which properties should be mangled. For example: to mangle all property names beginning an underscore:

{
	"mangle": {
		"regex": "^\_"
	}
}

It's also possible to configure repeatable short names for each mangled property, so that every build of your library has the same output. **See the wiki for a complete guide to property mangling in Microbundle.**

### Defining build-time constants

The `--define` option can be used to inject or replace build-time constants when bundling. In addition to injecting string or number constants, prefixing the define name with `@` allows injecting JavaScript expressions.

Build command

Source code

Output

`microbundle --define VERSION=2`

`console.log(VERSION)`

`console.log(2)`

`microbundle --define API_KEY='abc123'`

`console.log(API_KEY)`

`console.log("abc123")`

`microbundle --define @assign=Object.assign`

`assign(a, b)`

`Object.assign(a, b)`

### All CLI Options

```
Usage
	$ microbundle <command> [options]

Available Commands
	build    Build once and exit
	watch    Rebuilds on any change

For more info, run any command with the `--help` flag
	$ microbundle build --help
	$ microbundle watch --help

Options
	-v, --version      Displays current version
	-i, --entry        Entry module(s)
	-o, --output       Directory to place build files into
	-f, --format       Only build specified formats (any of modern,esm,cjs,umd or iife) (default modern,esm,cjs,umd)
	-w, --watch        Rebuilds on any change  (default false)
	--pkg-main         Outputs files analog to package.json main entries  (default true)
	--target           Specify your target environment (node or web)  (default web)
	--external         Specify external dependencies, or 'none' (default peerDependencies and dependencies in package.json)
	--globals          Specify globals dependencies, or 'none'
	--define           Replace constants with hard-coded values (use @key=exp to replace an expression)
	--alias            Map imports to different modules
	--compress         Compress output using Terser (default true when --target is web, false when --target is node)
	--strict           Enforce undefined global context and add "use strict"
	--name             Specify name exposed in UMD and IIFE builds
	--cwd              Use an alternative working directory  (default .)
	--sourcemap        Generate source map  (default true)
	--raw              Show raw byte size  (default false)
	--jsx              A custom JSX pragma like React.createElement (default h)
	--jsxFragment      A custom JSX fragment pragma like React.Fragment (default Fragment)
	--jsxImportSource  Declares the module specifier to be used for importing jsx factory functions
	--tsconfig         Specify the path to a custom tsconfig.json
	--generateTypes    Whether or not to generate types, if `types` or `typings` is set in `package.json` then it will default to be `true`
	--css              Where to output CSS: "inline" or "external" (default "external")
	--css-modules      Configures .css to be treated as modules (default null)
	--workers          Bundle module workers - see https://github.com/surma/rollup-plugin-off-main-thread#auto-bundling  (default false)
	--visualize        Generate bundle makeup visualization (stats.html)
	-h, --help         Displays this message

Examples
	$ microbundle build --globals react=React,jquery=$
	$ microbundle build --define API_KEY=1234
	$ microbundle build --alias react=preact/compat
	$ microbundle watch --no-sourcemap # don't generate sourcemaps
	$ microbundle build --tsconfig tsconfig.build.json
```

🛣 Roadmap
----------

Here's what's coming up for Microbundle:

-   Multiple separate inputs->outputs
-   TypeScript support
-   Flowtype support

🔨 Built with Microbundle
-------------------------

-   Preact Fast 3kB React alternative with the same modern API. Components & Virtual DOM.
-   Stockroom Offload your store management to a worker easily.
-   Microenvi Bundle, serve, and hot reload with one command.
-   Theme UI Build consistent, themeable React apps based on constraint-based design principles.
-   react-recomponent Reason-style reducer components for React using ES6 classes.
-   react-hooks-lib A set of reusable react hooks.
-   mdx-deck-live-code A library for mdx-deck to do live React and JS coding directly in slides.
-   react-router-ext An Extended react-router-dom with simple usage.
-   routex.js A dynamic routing library for Next.js.
-   hooked-form A lightweight form-management library for React.
-   goober Less than 1KB css-in-js alternative with a familiar API.
-   react-model The next generation state management library for React.
-   Teaful Tiny, easy and powerful (P)React state management.
-   @studio-freight/lenis Tiny, Performant, Vanilla JS, Smooth Scroll library.
-   @studio-freight/tempus One rAF to rule them all.
-   @studio-freight/hamo Collection of React hooks.
-   glTF Transform Library for working with .gltf and .glb 3D models.
-   eta Lightweight, powerful, pluggable embedded JS template engine
-   swup Page transition library for server-rendered websites.

🥂 License
----------

MIT
