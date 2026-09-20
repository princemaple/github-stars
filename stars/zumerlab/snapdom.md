---
project: snapdom
stars: 8136
description: High-performance engine for capturing, modifying, and converting DOM elements into any format.
url: https://github.com/zumerlab/snapdom
---

English | 简体中文

SnapDOM
=======

SnapDOM is a browser capture engine for web interfaces. It captures rendered DOM state as a reusable result, with styles, fonts and images included.

Export images and canvas with the core. Use plugins for self-contained HTML, page context, maps for visual agents, PDF and recordings. Captures can also feed WebGL textures, visual regression tests and UI transitions. Everything runs in the page, using standard Web APIs, with no core dependencies.

Documentation and demos · Technical features · Official plugins · 简体中文

This checkout documents **v3.x.x**. The migration guide below compares it with **v2.x.x**. The v2 source and v2 documentation remain available.

What you can build
------------------

Use

Output

Provided by

Share a card, chart, invoice or dashboard

SVG, PNG, JPG, WebP, canvas or Blob

Core

Reuse a capture in a texture, overlay or transition

Canvas plus capture geometry

Core

Save a page fragment for later display

HTML with captured styles and fonts

`html-export` plugin

Give an agent or a log a view of page content

Text/JSON context, or an image with an element map

`context-export` / `agent-map` plugins

Download a document or record changing content

Image-based PDF, animated GIF or browser-encoded video

`pdf-image` / `gif-export` / `video-export` plugins

Image, HTML and context exports use the captured state. GIF and video plugins record the live element over time.

Quick start
-----------

import { snapdom } from '@zumer/snapdom';

const card \= document.querySelector('#card');
const image \= await snapdom.toPng(card);
document.body.appendChild(image);

Capture once when you need several outputs:

const result \= await snapdom(card);

const image \= await result.toPng();
const canvas \= await result.toCanvas();
const blob \= await result.toBlob({ format: 'png' });
await result.download({ format: 'jpg', filename: 'card' });

The result keeps that capture even if the source element later changes. Call `snapdom(card)` again to capture its new state.

Installation
------------

Install the core and, when you need them, the official plugins; use matching major versions:

npm i @zumer/snapdom@latest @zumer/snapdom-plugins@latest

Or load it in a browser:

<script src\="https://unpkg.com/@zumer/snapdom@latest/dist/snapdom.js"\></script\>
<script\>
  snapdom.toPng(document.querySelector('#card')).then(image \=> {
    document.body.appendChild(image);
  });
</script\>

As an ES module from a CDN:

import { snapdom } from 'https://esm.sh/@zumer/snapdom@latest';
import { htmlExport } from 'https://esm.sh/@zumer/snapdom-plugins@latest/html-export';

`https://unpkg.com/@zumer/snapdom@latest/dist/snapdom.mjs` serves the same module. These examples load the latest published core and plugins.

To run the docs site against a local build of this checkout instead:

npm install
npm run compile
npm run site

The local site runs the local build. The public site's demos load the published package.

### Build outputs

File

Use

`dist/snapdom.mjs`

ES module for imports and bundlers

`dist/snapdom.js`

Script tag exposing `window.snapdom`

`types/snapdom.d.ts`

TypeScript declarations

There is no CommonJS build. `@zumer/snapdom/plugins` and the package root share the same runtime and plugin registry.

Usage
-----

### Choose an output

Result method

Returns

`toPng()`, `toJpg()`, `toWebp()`

An `HTMLImageElement`

`toSvg()`

An SVG-backed `HTMLImageElement`

`toCanvas()`

An `HTMLCanvasElement`

`toBlob()`

An SVG `Blob` unless a format was explicitly set on the capture or export

`toRaw()` / `url`

The capture's SVG data URL

`download()`

Downloads the chosen format

`to(name, options?)`

Runs a core or plugin exporter by name

One-step shortcuts such as `snapdom.toPng(element, options)` capture and export in one call. Results also have `toJpeg()` as an alias for `toJpg()`. `toImg()` remains available; prefer `toSvg()` for an SVG image.

### Set size and content

const result \= await snapdom(card, {
  width: 800,
  dpr: 1,
  backgroundColor: '#ffffff',
  exclude: '.capture-ignore',
  excludeMode: 'remove'
});

`width` and `height` define output size. If only one is set, the aspect ratio is preserved. `scale` applies when neither is set, and `dpr` multiplies the pixel dimensions.

Common option

Default

Purpose

`scale` / `dpr`

`1` / device pixel ratio

Output resolution

`width` / `height`

Unset

Output dimensions

`embedFonts`

`'auto'`

Embed the web fonts the capture uses

`backgroundColor`

Transparent; white for JPG/WebP

Output background

`exclude`

None

Selectors or predicates; `true` means exclude

`excludeMode`

`'hide'`

Keep an invisible spacer, or use `'remove'`

`filter`

None

Predicate; `true` keeps a node and `false` filters it out

`filterMode`

`'hide'`

Independent layout mode for nodes rejected by `filter`

`clip`

Unset

Capture the viewport or a page-coordinate rectangle

`captureSelection`

`false`

Include the user's text selection

`canvas`

Unset

Reuse an existing canvas

`invalidate`

`false`

Refresh after changes such as programmatic CSSOM edits

`fast`

`true`

`false` keeps the page responsive during long captures

All options include shadows, transforms, fonts, CORS, fallbacks and layout reconciliation.

### Export HTML or structured context

Official plugins are published separately as `@zumer/snapdom-plugins` and must match the core major version; they declare a peer dependency on a v3 core. Their sources live in `packages/plugins/` in this checkout.

import { htmlExport, contextExport } from '@zumer/snapdom-plugins';

const result \= await snapdom(card, {
  plugins: \[htmlExport(), contextExport({ format: 'json' })\]
});

const html \= await result.toHtml();
const context \= await result.toContext();

The same plugin system supports overlays, redaction and custom exporters. Local plugins override global plugins by name. See the official plugin reference and plugin specification.

### Capture HTML strings

const result \= await snapdom.fromString('<article>Hello</article>');
const image \= await result.toPng();

`fromString()` mounts the markup offscreen and removes it after capture. The string is parsed and activated like markup you wrote yourself: inline handlers such as `<img onerror>` run in the caller's origin, and can keep running after the mount is removed. Sanitize untrusted HTML first, with DOMPurify or equivalent.

### Feed a WebGL texture

const canvas \= document.createElement('canvas');
const texture \= new THREE.CanvasTexture(canvas);
texture.colorSpace \= THREE.SRGBColorSpace;

async function refresh(element) {
  await snapdom.toCanvas(element, { canvas, scale: 1, dpr: 1 });
  texture.needsUpdate \= true;
}

`result.meta` contains the capture geometry needed to place an exported image over the source interface. The labs show textures, mirrors and transitions.

What's new in v3
----------------

-   Eligible unchanged captures reuse the first result. Safe local changes rebuild only affected subtrees; other changes use a full capture.
-   Web fonts embed automatically when used. System-font captures skip that work.
-   The style pass avoids redundant reads, and per-capture state is isolated for concurrent captures.
-   Safari image decoding and drawing retain their browser-specific handling.
-   `snapdom.preCapture()` can prepare captures on user intent. It learns a control when a capture starts during its press/click event, then prepares that capture on later hover or focus.

snapdom.preCapture();
button.onclick \= () \=> snapdom.toPng(card);

Image compression and resource caching remain automatic. They do not make rasterization or image encoding free. See performance measurements and the cache guide.

SnapDOM has two rendering engines: **SVG**, the default, and **html-in-canvas**, which paints the same captured clone through the browser's native canvas API. Select the second with `engine: 'html-in-canvas'`.

The second engine is experimental: it still needs a compatible browser with its canvas drawing flag enabled, plus a build compiled with `SNAPDOM_CANVAS_ENGINE=1`. The default build includes SVG only. Unsupported captures fall back to SVG. A successful native capture produces a bitmap, so its URL and `toRaw()` return PNG, not serialized SVG. See ARCHITECTURE.md for details.

Migrating from v2
-----------------

The main capture pattern remains `snapdom(element, options)`. This guide compares v3 with **v2.x.x**; review these changes before upgrading:

In v2

In v3

What to change

Web fonts were opt-in

`embedFonts: 'auto'`

Usually nothing; use `false` only if you want to omit them

Raster width/height could be multiplied by `scale`

Width/height win over scale

Pass the final size: `width: 400` instead of `width: 200, scale: 2`

`burst` opted into repeat memoization

Eligible captures memoize automatically; `burst` is no longer documented or supported

Remove `burst` (the engine still reads it for internal use, do not rely on it) and use `invalidate: true` for one fresh capture after unobservable changes such as `sheet.insertRule()`

`preCache` prepared resources

Removed; `preCapture()` learns capture intent

Remove `preCache`; `preCapture()` is not a drop-in rename

`fast: false` cloned through idle callbacks

`fast: false` pauses about every frame, at nearly the same total time

Keep `fast: false`

`filter` / `filterMode` and `exclude` / `excludeMode` could be used together

Both controls and their independent modes remain supported; `exclude` also accepts predicates

Keep existing rules and modes; use the additional predicate form only when useful

`cache: 'auto'` or `'full'`

Both map to `'soft'`

Usually omit it; `'disabled'` / `false` is for debugging

`compress` controlled embedded image downsampling

Image optimization is automatic; `compress` is no longer documented or supported

Remove `compress`; the engine still reads it for internal use, do not rely on it

`resolvePicturePlaceholders` / `pictureResolver` configured lazy-image preparation

Responsive/lazy image resolution happens on the clone; these options are no longer documented or supported

Remove the options and handle custom loading/timeouts in your app before capture; the engine still reads `resolvePicturePlaceholders` for internal use, do not rely on it

Some visible input values were redacted

Core masks passwords only

Add `redactInputs()` for other fields

`afterExport` returns became the next hook's payload, not the caller's result

Returns are ignored; hooks receive the same export payload

Stop chaining through return values; use `defineExports` to produce a different output

Plugins v2.x.x exposed `@zumer/snapdom-plugins/html-in-canvas`

That subpath is removed

Use the experimental core `engine: 'html-in-canvas'` with a compatible custom build; the default build uses SVG

TypeScript exported `PluginExportFacade`

The named type is removed; `ctx.exports` still provides core exporters

Infer it in `defineExports`, or use `NonNullable<CaptureContext['exports']>`

### Use filter and exclude together

`filter` and `exclude` are independent controls, as in v2. `filter(node)` returns true to keep a node and false to filter it out; `filterMode` controls how a filtered node affects layout. `exclude` specifies additional omissions using selectors or predicates; an exclusion predicate returns true to omit the node. `excludeMode` controls those omissions. You can keep both controls and different modes in the same capture:

// Works in v2 and v3: hide private fields, remove the toolbar.
await snapdom(card, {
  filter: node \=> !node.matches('\[data-private\]'),
  filterMode: 'hide',
  exclude: \['.toolbar'\],
  excludeMode: 'remove'
});

`'hide'` keeps an invisible spacer; `'remove'` drops the node and allows reflow. Both omit its content. V3 additionally lets `exclude` mix selectors and predicates, such as `exclude: ['.toolbar', node => node.dataset.export === 'omit']`; any matching rule excludes the node. This is optional and does not replace `filter` or merge the two modes. The separate CSS-effect plugin named `filter` is also available.

Both modes default to `'hide'`. Per node, `data-capture="exclude"` is checked first, then `exclude`, then `filter`. The first omission decides the mode and stops evaluation for that node: if it matches `exclude`, `excludeMode` wins even when `filter` would reject it with a different mode. `filter` uses the v2 truthiness rule: any falsy return filters the node out.

### Callbacks that read changing application state

Captures with function-valued `filter`, `exclude`, `excludeStyleProps` or `fallbackURL` run fresh so applicable callbacks can read current application state on each new capture. They do not reuse an unchanged capture or an earlier callback's style/fallback decision. You do not need `invalidate` just because a callback's closure changed. That freshness has a cost: a function-valued `filter`, `exclude`, `excludeStyleProps` or `fallbackURL` turns off memoization and differential recapture for the capture, so a polling loop with a predicate pays a full capture on every tick. When the rule can be written as a selector, pass the selector and keep the reuse:

let privateMode \= false;
const options \= {
  exclude: node \=> privateMode && node.matches('\[data-private\]'),
  excludeMode: 'remove'
};
const before \= await snapdom(card, options);
privateMode \= true;
const after \= await snapdom(card, options); // evaluates the current policy

`before` still contains its original captured state; exporting it again does not apply a new policy. Use a new capture such as `after`. Keep exclusion and style predicates synchronous and boolean-returning. `invalidate: true` remains necessary after unobservable changes such as direct CSSOM edits.

Capture-affecting plugins suspend memoization unless they declare `pure: true`. Declare it only for deterministic hooks; timestamps and callbacks reading external state must run again. See the v3 plugin contract.

Limitations
-----------

-   SnapDOM needs a browser DOM. A server-side Node.js process needs a browser environment to run it.
-   Cross-origin images, fonts and stylesheets need readable resources or an appropriate proxy. `crossorigin` does not grant access unless the server also allows it. Cross-origin iframes use placeholders.
-   SVG output includes HTML inside `<foreignObject>`. It is suitable for browsers; support varies in other SVG viewers and document tools.
-   Output depends on browser rendering and canvas limits. Safari may fall back to PNG when WebP encoding is unavailable.
-   Canvas, video and other changing surfaces are captured fresh. JavaScript CSSOM edits are not observable automatically; use `invalidate: true` after them.
-   Core captures visible input values. Semantic plugins redact sensitive field values in their text/map output, but their attached image needs `redactInputs` or `exclude` if you want those pixels hidden too.

Technical features and browser behavior covers the details.

Performance benchmarks
----------------------

Recorded measurements separate first captures, repeat captures and image-heavy scenes. The live comparison runs in your browser and identifies the package version it loads.

For a useful comparison, use the same scene, output format, scale and DPR. Compare the images as well as the times.

Documentation
-------------

-   Archived v2 documentation and v2 source
-   API and options
-   Framework guides and how-to examples
-   Official plugins, plugin specification and contributing plugins
-   Architecture and technical features

Development
-----------

From this checkout:

npm install
npx playwright install
npm run compile
npm run lint
npm run test:types
npm run test:bundle
BROWSER=all npx vitest run \_\_tests\_\_ --browser.headless
npm run test:pack

`npm run site` serves the docs with the local build. `npm test` checks lint without changing files; use `npm run lint:fix` to apply fixes. See ARCHITECTURE.md for implementation notes.

Contributors
------------

Sponsors
--------

Special thanks to @megaphonecolin, @sdraper69, @reynaldichernando, @gamma-app, @jrjohnson, and @ryanander for supporting this project!

If you'd like to support this project too, you can become a sponsor.

Show your support
-----------------

If SnapDOM saved you time, a star on GitHub helps other developers find it.

Shipping something built with SnapDOM? Add the badge to your README:

\[!\[Built with SnapDOM\](https://img.shields.io/badge/built%20with-SnapDOM-blue)\](https://snapdom.dev)

### Projects using SnapDOM

Projects using SnapDOM include:

-   LobeHub — platform for operating AI agents
-   Hugging Face Chat UI — HuggingChat interface with artifact preview captures
-   Sealos — AI-native cloud operating system
-   Tencent tmagic-editor — low-code page editor
-   Playroom — JSX design tool by SEEK
-   GPT-Vis — AI-friendly data viz by Ant Group's AntV
-   Rabby Wallet — browser wallet for EVM chains
-   uMap — OpenStreetMap map builder
-   ListenBrainz — music tracker by MetaBrainz
-   Mind Elixir — mind-map core; recommends SnapDOM for image export
-   Kong UI Components — Kong's dashboard renderer exports PDFs with SnapDOM
-   SnapDIFF — in-browser visual regression testing _(by Zumerlab)_

See the full gallery at **snapdom.dev/made-with**. Shipping SnapDOM? Open a PR to add your project — real, verifiable projects only.

License
-------

MIT © Zumerlab
