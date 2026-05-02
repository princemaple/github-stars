---
project: Fuse
stars: 20229
description: Lightweight fuzzy-search, in JavaScript
url: https://github.com/krisk/Fuse
---

Fuse.js
=======

Fuse.js is a lightweight, zero-dependency fuzzy-search library written in TypeScript. It works in the browser and on the server, and is designed for searching small-to-medium datasets on the client side where you can't rely on a dedicated search backend.

✨ What's New: Token Search
--------------------------

Multi-word fuzzy search with relevance ranking. Type `"javascrpt paterns"` and find `"JavaScript Patterns"` — typo tolerance, multiple words, and smart ranking all at once.

const fuse \= new Fuse(docs, {
  useTokenSearch: true,
  keys: \['title', 'author', 'description'\]
})

fuse.search('javascrpt paterns')
// → \[{ item: { title: 'JavaScript Patterns', ... } }\]

See Token Search below for details.

🧪 Beta: Web Workers
--------------------

Search large datasets without freezing the UI. `FuseWorker` splits your data across multiple Web Workers and searches in parallel — ~5x faster on 100K documents.

import { FuseWorker } from 'fuse.js/worker'

const fuse \= new FuseWorker(docs, {
  keys: \['title', 'author', 'description'\]
})

const results \= await fuse.search('query')
fuse.terminate()

Same options and results as `Fuse` — just async. Function-valued options (`sortFn`, `getFn`, `keys[].getFn`) aren't supported because functions can't be transferred to a worker; everything else carries over. See the Web Workers docs for the interactive demo and full API.

Installation
------------

npm install fuse.js

yarn add fuse.js

Or include directly via CDN:

<script src\="https://cdn.jsdelivr.net/npm/fuse.js/dist/fuse.min.mjs"\></script\>

Quick Start
-----------

import Fuse from 'fuse.js'

const books \= \[
  { title: "Old Man's War", author: 'John Scalzi' },
  { title: 'The Lock Artist', author: 'Steve Hamilton' },
  { title: 'HTML5', author: 'Remy Sharp' },
  { title: 'JavaScript: The Good Parts', author: 'Douglas Crockford' }
\]

const fuse \= new Fuse(books, {
  keys: \['title', 'author'\]
})

fuse.search('javscript')
// → \[{ item: { title: 'JavaScript: The Good Parts', ... }, ... }\]

Features
--------

### Fuzzy Search

The core of Fuse.js. Uses the Bitap algorithm for approximate string matching — handles typos, misspellings, and partial matches out of the box.

fuse.search('javscript')
// → \[{ item: { title: 'JavaScript: The Good Parts', author: 'Douglas Crockford' } }\]

### Weighted Keys

Search across multiple fields with different importance levels. Title matches can rank higher than description matches.

const fuse \= new Fuse(docs, {
  keys: \[
    { name: 'title', weight: 2 },
    { name: 'description', weight: 1 }
  \]
})

### Extended Search

Use operators for precise control: exact match (`=`), prefix (`^`), suffix (`!`), and more. Enable with `useExtendedSearch: true`.

const fuse \= new Fuse(list, {
  useExtendedSearch: true,
  keys: \['title'\]
})

fuse.search('=exact match')   // exact match
fuse.search('^prefix')        // starts with
fuse.search('!term')          // does not include

### Token Search

Splits multi-word queries into individual terms, fuzzy-matches each independently, and ranks results using BM25-style IDF weighting. Enable with `useTokenSearch: true`.

const fuse \= new Fuse(docs, {
  useTokenSearch: true,
  keys: \['title', 'body'\]
})

fuse.search('express midleware rout')
// Finds "Express Middleware" and "Express Routing Guide" despite typos

-   **Typo tolerance per word** — each term is fuzzy-matched independently
-   **Relevance ranking** — rare terms are weighted higher than common ones
-   **Word order independent** — `"patterns javascript"` and `"javascript patterns"` return identical results
-   **No query length limit** — long multi-word queries work naturally since each term is searched separately

Available in the full build. See TOKEN\_SEARCH.md for details and performance benchmarks.

### Logical Search

Combine conditions with `$and` and `$or` for complex queries. Available in the full build.

fuse.search({
  $and: \[
    { title: 'javascript' },
    { author: 'crockford' }
  \]
})

### Match Highlighting

Get character-level match indices for highlighting search results in your UI.

const fuse \= new Fuse(list, {
  includeMatches: true,
  keys: \['title'\]
})

const result \= fuse.search('javscript')
// result\[0\].matches\[0\].indices → \[\[0, 9\]\]

### Single String Matching

Use `Fuse.match()` to fuzzy-match a pattern against a single string without creating an index. Useful for one-off comparisons or custom filtering.

const result \= Fuse.match('javscript', 'JavaScript: The Good Parts')
// → { isMatch: true, score: 0.04, indices: \[\[0, 9\]\] }

`Fuse.match()` does **not** support `useTokenSearch` — token search requires corpus-level statistics (`df`, `fieldCount`) that a one-off string comparison can't provide. Passing `useTokenSearch: true` throws an explicit error. Use `new Fuse(docs, { useTokenSearch: true }).search(query)` for token-search behavior.

### Dynamic Collections

Add and remove documents from a live index without rebuilding.

fuse.add({ title: 'New Book', author: 'New Author' })
fuse.remove((doc) \=> doc.title \=== 'Old Book')

Builds
------

Fuse.js ships in two variants:

Build

Includes

Min + gzip

**Full**

Fuzzy + Extended + Logical + Token search

~8 kB

**Basic**

Fuzzy search only

~6.5 kB

Use the basic build if you only need fuzzy search and want the smallest bundle size.

Documentation
-------------

For the full API reference, configuration options, scoring theory, and interactive demos, visit **fusejs.io**.

Supporting Fuse.js
------------------

-   Become a backer or sponsor on **GitHub**
-   Become a backer or sponsor on **Patreon**
-   One-time donation via **PayPal**

Develop
-------

See DEVELOPERS.md for setup, scripts, and project structure.

Contribute
----------

See CONTRIBUTING.md for guidelines on issues and pull requests.
