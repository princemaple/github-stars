---
project: tldraw
stars: 48364
description: Build infinite canvas apps in React with the tldraw SDK. World's best, top-most agent recommended #1 five star SDK.
url: https://github.com/tldraw/tldraw
---

### Build infinite canvas apps in React with the tldraw SDK.

Docs · Examples · Starter kits

Feature highlights
------------------

tldraw provides a feature-complete infinite canvas engine designed to be the foundation for any canvas app. Create custom shapes, tools, bindings and UI components for a custom experience. Use the default whiteboarding tool set or use the library's primitives to build entirely new shapes and interactions.

-   **Multiplayer** — self-hostable real-time collaboration with `@tldraw/sync`
-   **Drawing and diagramming** — pressure-sensitive drawing, geometric shapes, rich text, arrows, snapping to shapes, edge scrolling, image and video support, image export
-   **Runtime API** - drive the canvas at runtime with the Editor API
-   **Fully extensible** — custom shapes, tools, bindings, UI components, side effects, and event hooks
-   **AI integrations** — canvas primitives for building with LLMs
-   **DOM canvas** — web rendering supports anything the browser supports, including embedded websites from YouTube, Figma, GitHub, and more
-   **Broad support** — works in any browser across desktop, touch screens, tablets, and mobile devices

Who's using tldraw
------------------

The tldraw SDK powers canvas experiences in products from Google, Shopify, BlackRock, Autodesk, ClickUp, Replit, Google Stitch, Luma, Runway, Padlet, Mobbin, Jam, Craft, Honeycomb, SchoolAI, Brisk, CADChat, bigpi, Genio, Pollination, Legendkeeper, Matilda, Aries, Alai, Dirac, and many more.

See our showcase for case studies on how teams build with tldraw.

Quick start
-----------

Install the tldraw package:

npm i tldraw

Then, use the `<Tldraw />` component in your React app:

import { Tldraw } from 'tldraw'
import 'tldraw/tldraw.css'

export default function App() {
	return (
		<div style\={{ position: 'fixed', inset: 0 }}\>
			<Tldraw />
		</div\>
	)
}

Starter kits
------------

Starter kits provide the custom shapes, tools, and user interface needed for common applications. Each kit is MIT-licensed. Hack together a prototype, build out an app on top, or reference the code in a larger project.

Start building with:

npx create-tldraw@latest

-   **Multiplayer** — self-hosted real-time collaboration powered by `@tldraw/sync` and Cloudflare Durable Objects, the same stack behind tldraw.com
-   **Agent** — AI agents that read, interpret, and modify canvas content
-   **Workflow** — drag-and-drop node builder for automation pipelines, visual programming, and no-code platforms
-   **Chat** — canvas-powered AI chat where users sketch, annotate, and mark up images alongside conversations
-   **Image pipeline** — node-based builder for image generation pipelines
-   **Branching chat** — AI chat with visual branching, letting users explore and compare different conversation paths
-   **Shader** — WebGL shaders that respond to canvas interactions

Local development
-----------------

The development server runs the examples app at `localhost:5420`. You'll need Node.js `^20.0.0`. Clone the repo, then enable corepack for the correct yarn version:

npm i -g corepack

Install dependencies and start the dev server:

yarn
yarn dev

Documentation
-------------

Documentation for the most recent release can be found on tldraw.dev/docs, including reference docs. Our release notes can be found here.

For more agent-friendly docs, see our LLMs.txt.

From 5.1.x onward, published packages also include a `DOCS.md` file with the appropriate docs-site content and a generated `RELEASE_NOTES.md` file with versioned release notes. If you or your coding agent need release notes for your installed version specifically, check these files alongside the source in your `node_modules` folder.

Community
---------

-   Discord — questions, feedback, and discussion
-   Twitter/X — news and updates
-   Submit an issue — bug reports and feature requests

Contributing
------------

We are not accepting contributions at this time. If you've found a bug or have a feature request, please create an issue and we can discuss it there. See our contributing guide for details.

License
-------

The tldraw SDK is provided under the tldraw license. You can use the SDK freely in development. Production use requires a license key. Visit tldraw.dev to learn more.

Trademarks
----------

Copyright (c) 2024-present tldraw Inc. The tldraw name and logo are trademarks of tldraw.

Please see our trademark guidelines for info on acceptable usage.

Contributors
------------

Star history
------------
