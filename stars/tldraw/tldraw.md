---
project: tldraw
stars: 45205
description: very good whiteboard infinite canvas SDK
url: https://github.com/tldraw/tldraw
---

tldraw
======

Welcome to the public monorepo for tldraw. tldraw is a library for creating infinite canvas experiences in React. It's the software behind the digital whiteboard tldraw.com.

-   Read the docs and learn more at tldraw.dev.
-   Learn about our license.

> Click here to learn about our license and pricing.

Installation
------------

npm i tldraw

Usage
-----

import { Tldraw } from 'tldraw'
import 'tldraw/tldraw.css'

export default function App() {
	return (
		<div style\={{ position: 'fixed', inset: 0 }}\>
			<Tldraw />
		</div\>
	)
}

Learn more at tldraw.dev.

Local development
-----------------

The local development server will run our examples app. The basic example will show any changes you've made to the codebase.

To run the local development server, first clone this repo.

Enable corepack to make sure you have the right version of `yarn`:

npm i -g corepack

Install dependencies:

yarn

Start the local development server:

yarn dev

Open the example project at `localhost:5420`.

License
-------

The tldraw SDK is provided under the tldraw license.

You can use the tldraw SDK in commercial or non-commercial projects so long as you preserve the "Made with tldraw" watermark on the canvas. To remove the watermark, you can purchase a business license. Visit tldraw.dev to learn more.

Trademarks
----------

Copyright (c) 2024-present tldraw Inc. The tldraw name and logo are trademarks of tldraw. Please see our trademark guidelines for info on acceptable usage.

Distributions
-------------

You can find tldraw on npm here.

Contribution
------------

Please see our contributing guide. Found a bug? Please submit an issue.

Community
---------

Have questions, comments or feedback? Join our discord. For the latest news and release notes, visit tldraw.dev.

Contributors
------------

Star History
------------

Contact
-------

Find us on Twitter/X at @tldraw. You can contact us by email at hello@tldraw.com.
