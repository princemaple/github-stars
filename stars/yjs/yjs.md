---
project: yjs
stars: 20599
description: Shared data types for building collaborative software
url: https://github.com/yjs/yjs
---

> A CRDT framework with a powerful abstraction of shared data

Yjs is a CRDT implementation that exposes its internal data structure as _shared types_. Shared types are common data types like `Map` or `Array` with superpowers: changes are automatically distributed to other peers and merged without merge conflicts.

Yjs is **network agnostic** (p2p!), supports many existing **rich text editors**, **offline editing**, **version snapshots**, **undo/redo** and **shared cursors**. It scales well with an unlimited number of users and is well suited for even large documents.

-   Demos: https://github.com/yjs/yjs-demos
-   Discuss: https://discuss.yjs.dev
-   Chat: Gitter | Discord
-   Benchmark Yjs vs. Automerge: https://github.com/dmonad/crdt-benchmarks
-   Podcast **"Yjs Deep Dive into real time collaborative editing solutions":**
-   Podcast **"Google Docs-style editing in Gutenberg with the YJS framework":**

👷‍♀️ If you are looking for professional support, please consider supporting this project via a "support contract" on GitHub Sponsors. I will attend your issues quicker and we can discuss questions and problems in regular video conferences. Otherwise you can find help on our community discussion board.

Sponsorship
-----------

Please contribute to the project financially - especially if your company relies on Yjs.

Professional Support
--------------------

-   Support Contract with the Maintainer - By contributing financially to the open-source Yjs project, you can receive professional support directly from the author. This includes the opportunity for weekly video calls to discuss your specific challenges.
-   Synergy Codes - Specializing in consulting and developing real-time collaborative editing solutions for visual apps, Synergy Codes focuses on interactive diagrams, complex graphs, charts, and various data visualization types. Their expertise empowers developers to build engaging and interactive visual experiences leveraging the power of Yjs. See their work in action at Visual Collaboration Showcase.

Who is using Yjs
----------------

-   AFFiNE A local-first, privacy-first, open source knowledge base. 🌟
-   Huly - Open Source All-in-One Project Management Platform 🌟
-   Cargo Site builder for designers and artists 🌟
-   Gitbook Knowledge management for technical teams 🌟
-   Evernote Note-taking app 🌟
-   Lessonspace Enterprise platform for virtual classrooms and online training 🌟
-   Ellipsus - Collaborative writing app for storytelling etc. Supports versioning, change attribution, and "blame". A solution for the whole publishing process (also selling) ⭐
-   Dynaboard Build web apps collaboratively. ⭐
-   Relm A collaborative gameworld for teamwork and community. ⭐
-   Room.sh A meeting application with integrated collaborative drawing, editing, and coding tools. ⭐
-   Nimbus Note A note-taking app designed by Nimbus Web. ⭐
-   Pluxbox RadioManager A web-based app to collaboratively organize radio broadcasts. ⭐
-   modyfi - Modyfi is the design platform built for multidisciplinary designers. Design, generate, animate, and more — without switching between apps. ⭐
-   Sana A learning platform with collaborative text editing powered by Yjs.
-   Serenity Notes End-to-end encrypted collaborative notes app.
-   PRSM Collaborative mind-mapping and system visualisation. _(source)_
-   Alldone A next-gen project management and collaboration platform.
-   Living Spec A modern way for product teams to collaborate.
-   Slidebeamer Presentation app.
-   BlockSurvey End-to-end encryption for your forms/surveys.
-   Skiff Private, decentralized workspace.
-   JupyterLab Collaborative computational Notebooks
-   JupyterCad Extension to JupyterLab that enables collaborative editing of 3d FreeCAD Models.
-   JupyterGIS Collaborative GIS (Geographic Information System) editor in Jupyter
-   Hyperquery A collaborative data workspace for sharing analyses, documentation, spreadsheets, and dashboards.
-   Nosgestesclimat The french carbon footprint calculator has a group P2P mode based on yjs
-   oorja.io Online meeting spaces extensible with collaborative apps, end-to-end encrypted.
-   LegendKeeper Collaborative campaign planner and worldbuilding app for tabletop RPGs.
-   IllumiDesk Build courses and content with A.I.
-   btw Open-source Medium alternative
-   AWS SageMaker Tools for building Machine Learning Models
-   linear Streamline issues, projects, and product roadmaps.
-   Arkiter - Live interview software
-   Appflowy - They use Yrs
-   Multi.app - Multiplayer app sharing: Point, draw and edit in shared apps as if they're on your computer. They are using Yrs.
-   AppMaster A No-Code platform for creating production-ready applications with source code generation.
-   Synthesia - Collaborative Video Editor
-   thinkdeli - A fast and simple notes app powered by AI
-   ourboard - A collaborative whiteboard application
-   Ellie.ai - Data Product Design and Collaboration
-   GoPeer - Collaborative tutoring
-   screen.garden - Collaborative backend for PKM apps.
-   NextCloud - Content Collaboration Platform
-   keystatic - git-based CMS
-   QDAcity - Collaborative qualitative data analysis platform
-   Kanbert - Project management software
-   Eclipse Theia - A cloud & desktop IDE that runs in the browser.
-   ScienHub - Collaborative LaTeX editor in the browser.
-   Open Collaboration Tools - Collaborative editing for your IDE or custom editor
-   Typst - Compose, edit, and automate technical documents
-   Kedyou - Digital workspaces for tutoring
-   Lightpage - Personal living notebook
-   reearth-flow - Collaboratively calculate and convert various data
-   ProtonMail | Proton Docs - E2E encrypted collaborative documents in Proton Drive.
-   Theneo - AI-powered API docs with live team collaboration.

Table of Contents
-----------------

-   Overview
    -   Bindings
    -   Providers
    -   Tooling
    -   Ports
-   Getting Started
-   API
    -   Shared Types
    -   Y.Doc
    -   Document Updates
    -   Relative Positions
    -   Y.UndoManager
-   Yjs CRDT Algorithm
-   License and Author

Overview
--------

This repository contains a collection of shared types that can be observed for changes and manipulated concurrently. Network functionality and two-way-bindings are implemented in separate modules.

### Bindings

Name

Cursors

Binding

Demo

ProseMirror                                                  

✔

y-prosemirror

demo

Quill

✔

y-quill

demo

CodeMirror

✔

y-codemirror

demo

Monaco

✔

y-monaco

demo

Ace

✔

y-ace

Slate

✔

slate-yjs

demo

BlockSuite

✔

(native)

demo

Lexical

✔

(native)

demo

BlockNote

✔

y-prosemirror

demo

Tiptap

✔

y-prosemirror

demo

Milkdown

✔

y-prosemirror

demo

Superdoc

✔

(native)

demo

valtio

valtio-yjs

demo

immer

immer-yjs

demo

React

react-yjs

demo

React / Vue / Svelte / MobX

SyncedStore

demo

mobx-keystone

mobx-keystone-yjs

demo

PSPDFKit

yjs-pspdfkit

demo

Rows n'Columns

✔

@rowsncolumns/y-spreadsheet

### Utilities

Tools that extend the core functionality of Yjs.

y-utility

Library with `YMultiDocUndoManager` (undo/redo across Yjs docs) and `YKeyValue` (optimized key-value store).

yjs-orderedtree 🌳

Class for ordered trees via Y.Map. Handles `insert`, `delete`, and `move` operations for folder-like hierarchies.

### Providers

Setting up the communication between clients, managing awareness information, and storing shared data for offline usage is quite a hassle. **Providers** manage all that for you and are the perfect starting point for your collaborative app.

> This list of providers is incomplete. Please open PRs to add your providers to this list!

#### Connection Providers

y-websocket

A module that contains a simple websocket backend and a websocket client that connects to that backend. **y-redis**, **y-sweet**, **ypy-websocket**, **yrs-warp** and **Hocuspocus** (see below) are alternative backends to y-websocket.

y-webrtc

Propagates document updates peer-to-peer using WebRTC. The peers exchange signaling data over signaling servers. Publicly available signaling servers are available. Communication over the signaling servers can be encrypted by providing a shared secret, keeping the connection information and the shared document private.

@liveblocks/yjs 🌟

Liveblocks Yjs provides a fully hosted WebSocket infrastructure and persisted data store for Yjs documents. No configuration or maintenance is required. It also features Yjs webhook events, REST API to read and update Yjs documents, and a browser DevTools extension.

y-sweet ⭐

A standalone yjs server with persistence to S3 or filesystem. They offer a cloud service as well.

Hocuspocus ⭐

A standalone extensible yjs server with sqlite persistence, webhooks, auth and more.

@superviz/yjs

SuperViz Yjs Provider comes with a secure, scalable real-time infrastructure for Yjs documents, fully compatible with a set of real-time collaboration components offered by SuperViz. This solution ensures synchronization, offline editing, and real-time updates, enabling multiple users to collaborate effectively within shared workspaces.

PartyKit

Cloud service for building multiplayer apps.

@pluv/crdt-yjs

Use pluv.io as a full-featured backend for Yjs. pluv.io can either be be used on its fully-managed WebSocket infrastructure, or self-hosted on Cloudflare Workers and Node.js runtimes. Offers a typesafe API with authentication, webhooks, rooms, and more.

y-libp2p

Uses libp2p to propagate updates via GossipSub. Also includes a peer-sync mechanism to catch up on missed updates.

y-dat

\[WIP\] Write document updates efficiently to the dat network using multifeed. Each client has an append-only log of CRDT local updates (hypercore). Multifeed manages and sync hypercores and y-dat listens to changes and applies them to the Yjs document.

Matrix-CRDT

Use Matrix as an off-the-shelf backend for Yjs by using the MatrixProvider. Use Matrix as transport and storage of Yjs updates, so you can focus building your client app and Matrix can provide powerful features like Authentication, Authorization, Federation, hosting (self-hosting or SaaS) and even End-to-End Encryption (E2EE).

yrb-actioncable

An ActionCable companion for Yjs clients. There is a fitting redis extension as well.

ypy-websocket

Websocket backend, written in Python.

Tinybase

The reactive data store for local-first apps. They support multiple CRDTs and different network technologies.

y-webxdc

Provider for sharing data in webxdc chat apps.

secsync

An architecture to relay end-to-end encrypted CRDTs over a central service.

y-electric

Sync Yjs over ElectricSQL.

yjs-cf-ws-provider

Cloudflare provider for Yjs based on durable objects.

nostr-crdt

Sync Yjs over nostr.

#### Persistence Providers

y-indexeddb

Efficiently persists document updates to the browsers indexeddb database. The document is immediately available and only diffs need to be synced through the network provider.

y-mongodb-provider

Adds persistent storage to a server with MongoDB. Can be used with the y-websocket provider.

y-fire

A database and connection provider for Yjs based on Firestore.

y-op-sqlite

Persist YJS updates in your React Native app using op-sqlite , the fastest SQLite library for React Native.

y-postgresql

Provides persistent storage for a web server using PostgreSQL and is easily compatible with y-websocket.

k\_yrs\_go

Golang database server for YJS CRDT using Postgres + Redis

y-op-sqlite

Yjs persistence provider for op-sqlite

### Tooling

-   y-sweet debugger
-   liveblocks devtools
-   Yjs inspector

### Ports

There are several Yjs-compatible ports to other programming languages.

-   y-octo - Rust implementation by AFFiNE
-   y-crdt - Rust implementation with multiple language bindings to other languages
    -   yrs - Rust interface
    -   ypy - Python binding
    -   yrb - Ruby binding
    -   yswift - Swift binding
    -   yffi - C-FFI
    -   ywasm - WASM binding
    -   y\_ex - Elixir bindings
-   ycs - .Net compatible C# implementation.

Getting Started
---------------

Install Yjs and a provider with your favorite package manager:

npm i yjs y-websocket

Start the y-websocket server:

PORT=1234 node ./node\_modules/y-websocket/bin/server.cjs

### Example: Observe types

import \* as Y from 'yjs';

const doc \= new Y.Doc();
const yarray \= doc.getArray('my-array')
yarray.observe(event \=> {
  console.log('yarray was modified')
})
// every time a local or remote client modifies yarray, the observer is called
yarray.insert(0, \['val'\]) // => "yarray was modified"

### Example: Nest types

Remember, shared types are just plain old data types. The only limitation is that a shared type must exist only once in the shared document.

const ymap \= doc.getMap('map')
const foodArray \= new Y.Array()
foodArray.insert(0, \['apple', 'banana'\])
ymap.set('food', foodArray)
ymap.get('food') \=== foodArray // => true
ymap.set('fruit', foodArray) // => Error! foodArray is already defined

Now you understand how types are defined on a shared document. Next you can jump to the demo repository or continue reading the API docs.

### Example: Using and combining providers

Any of the Yjs providers can be combined with each other. So you can sync data over different network technologies.

In most cases you want to use a network provider (like y-websocket or y-webrtc) in combination with a persistence provider (y-indexeddb in the browser). Persistence allows you to load the document faster and to persist data that is created while offline.

For the sake of this demo we combine two different network providers with a persistence provider.

import \* as Y from 'yjs'
import { WebrtcProvider } from 'y-webrtc'
import { WebsocketProvider } from 'y-websocket'
import { IndexeddbPersistence } from 'y-indexeddb'

const ydoc \= new Y.Doc()

// this allows you to instantly get the (cached) documents data
const indexeddbProvider \= new IndexeddbPersistence('count-demo', ydoc)
indexeddbProvider.whenSynced.then(() \=> {
  console.log('loaded data from indexed db')
})

// Sync clients with the y-webrtc provider.
const webrtcProvider \= new WebrtcProvider('count-demo', ydoc)

// Sync clients with the y-websocket provider
const websocketProvider \= new WebsocketProvider(
  'wss://demos.yjs.dev', 'count-demo', ydoc
)

// array of numbers which produce a sum
const yarray \= ydoc.getArray('count')

// observe changes of the sum
yarray.observe(event \=> {
  // print updates when the data changes
  console.log('new sum: ' + yarray.toArray().reduce((a,b) \=> a + b))
})

// add 1 to the sum
yarray.push(\[1\]) // => "new sum: 1"

API
---

import \* as Y from 'yjs'

### Shared Types

**Y.Array**  

A shareable Array-like type that supports efficient insert/delete of elements at any position. Internally it uses a linked list of Arrays that is split when necessary.

const yarray = new Y.Array()

**`Y.Array.from(Array<object|boolean|Array|string|number|null|Uint8Array|Y.Type>): Y.Array`**

An alternative factory function to create a Y.Array based on existing content.

**`parent:Y.AbstractType|null`**

**`insert(index:number, content:Array<object|boolean|Array|string|number|null|Uint8Array|Y.Type>)`**

Insert content at index. Note that content is an array of elements. I.e. `array.insert(0, [1])` splices the list and inserts 1 at position 0.

**`push(Array<Object|boolean|Array|string|number|null|Uint8Array|Y.Type>)`**

**`unshift(Array<Object|boolean|Array|string|number|null|Uint8Array|Y.Type>)`**

**`delete(index:number, length:number)`**

**`get(index:number)`**

**`slice(start:number, end:number):Array<Object|boolean|Array|string|number|null|Uint8Array|Y.Type>`**

Retrieve a range of content

**`length:number`**

**`forEach(function(value:object|boolean|Array|string|number|null|Uint8Array|Y.Type, index:number, array: Y.Array))`**

**`map(function(T, number, YArray):M):Array<M>`**

**`clone(): Y.Array`**

Clone all values into a fresh Y.Array instance. The returned type can be included into the Yjs document.

**`toArray():Array<object|boolean|Array|string|number|null|Uint8Array|Y.Type>`**

Copies the content of this YArray to a new Array.

**`toJSON():Array<Object|boolean|Array|string|number|null>`**

Copies the content of this YArray to a new Array. It transforms all child types to JSON using their `toJSON` method.

**`[Symbol.Iterator]`**

Returns an YArray Iterator that contains the values for each index in the array.

for (let value of yarray) { .. }

**`observe(function(YArrayEvent, Transaction):void)`**

Adds an event listener to this type that will be called synchronously every time this type is modified. In the case this type is modified in the event listener, the event listener will be called again after the current event listener returns.

**`unobserve(function(YArrayEvent, Transaction):void)`**

Removes an `observe` event listener from this type.

**`observeDeep(function(Array<YEvent>, Transaction):void)`**

Adds an event listener to this type that will be called synchronously every time this type or any of its children is modified. In the case this type is modified in the event listener, the event listener will be called again after the current event listener returns. The event listener receives all Events created by itself or any of its children.

**`unobserveDeep(function(Array<YEvent>, Transaction):void)`**

Removes an `observeDeep` event listener from this type.

**Y.Map**  

A shareable Map type.

```
const ymap = new Y.Map()
```

**`parent:Y.AbstractType|null`**

**`size: number`**

Total number of key/value pairs.

**`get(key:string):object|boolean|string|number|null|Uint8Array|Y.Type`**

**`set(key:string, value:object|boolean|string|number|null|Uint8Array|Y.Type)`**

**`delete(key:string)`**

**`has(key:string):boolean`**

**`clear()`**

Removes all elements from this YMap.

**`clone():Y.Map`**

Clone this type into a fresh Yjs type.

**`toJSON():Object<string, Object|boolean|Array|string|number|null|Uint8Array>`**

Copies the `[key,value]` pairs of this YMap to a new Object.It transforms all child types to JSON using their `toJSON` method.

**`forEach(function(value:object|boolean|Array|string|number|null|Uint8Array|Y.Type, key:string, map: Y.Map))`**

Execute the provided function once for every key-value pair.

**`[Symbol.Iterator]`**

Returns an Iterator of `[key, value]` pairs.

for (let \[key, value\] of ymap) { .. }

**`entries()`**

Returns an Iterator of `[key, value]` pairs.

**`values()`**

Returns an Iterator of all values.

**`keys()`**

Returns an Iterator of all keys.

**`observe(function(YMapEvent, Transaction):void)`**

Adds an event listener to this type that will be called synchronously every time this type is modified. In the case this type is modified in the event listener, the event listener will be called again after the current event listener returns.

**`unobserve(function(YMapEvent, Transaction):void)`**

Removes an `observe` event listener from this type.

**`observeDeep(function(Array<YEvent>, Transaction):void)`**

Adds an event listener to this type that will be called synchronously every time this type or any of its children is modified. In the case this type is modified in the event listener, the event listener will be called again after the current event listener returns. The event listener receives all Events created by itself or any of its children.

**`unobserveDeep(function(Array<YEvent>, Transaction):void)`**

Removes an `observeDeep` event listener from this type.

**Y.Text**  

A shareable type that is optimized for shared editing on text. It allows to assign properties to ranges in the text. This makes it possible to implement rich-text bindings to this type.

This type can also be transformed to the delta format. Similarly the YTextEvents compute changes as deltas.

const ytext = new Y.Text()

**`parent:Y.AbstractType|null`**

**`insert(index:number, content:string, [formattingAttributes:Object<string,string>])`**

Insert a string at index and assign formatting attributes to it.

ytext.insert(0, 'bold text', { bold: true })

**`delete(index:number, length:number)`**

**`format(index:number, length:number, formattingAttributes:Object<string,string>)`**

Assign formatting attributes to a range in the text

**`applyDelta(delta: Delta, opts:Object<string,any>)`**

See Quill Delta Can set options for preventing remove ending newLines, default is true.

ytext.applyDelta(delta, { sanitize: false })

**`length:number`**

**`toString():string`**

Transforms this type, without formatting options, into a string.

**`toJSON():string`**

See `toString`

**`toDelta():Delta`**

Transforms this type to a Quill Delta

**`observe(function(YTextEvent, Transaction):void)`**

Adds an event listener to this type that will be called synchronously every time this type is modified. In the case this type is modified in the event listener, the event listener will be called again after the current event listener returns.

**`unobserve(function(YTextEvent, Transaction):void)`**

Removes an `observe` event listener from this type.

**`observeDeep(function(Array<YEvent>, Transaction):void)`**

Adds an event listener to this type that will be called synchronously every time this type or any of its children is modified. In the case this type is modified in the event listener, the event listener will be called again after the current event listener returns. The event listener receives all Events created by itself or any of its children.

**`unobserveDeep(function(Array<YEvent>, Transaction):void)`**

Removes an `observeDeep` event listener from this type.

**Y.XmlFragment**  

A container that holds an Array of Y.XmlElements.

```
const yxml = new Y.XmlFragment()
```

**`parent:Y.AbstractType|null`**

**`firstChild:Y.XmlElement|Y.XmlText|null`**

**`insert(index:number, content:Array<Y.XmlElement|Y.XmlText>)`**

**`delete(index:number, length:number)`**

**`get(index:number)`**

**`slice(start:number, end:number):Array<Y.XmlElement|Y.XmlText>`**

Retrieve a range of content

**`length:number`**

**`clone():Y.XmlFragment`**

Clone this type into a fresh Yjs type.

**`toArray():Array<Y.XmlElement|Y.XmlText>`**

Copies the children to a new Array.

**`toString():string`**

Get the XML serialization of all descendants.

**`toJSON():string`**

See `toString`.

**`createTreeWalker(filter: function(AbstractType<any>):boolean):Iterable`**

Create an Iterable that walks through the children.

**`observe(function(YXmlEvent, Transaction):void)`**

Adds an event listener to this type that will be called synchronously every time this type is modified. In the case this type is modified in the event listener, the event listener will be called again after the current event listener returns.

**`unobserve(function(YXmlEvent, Transaction):void)`**

Removes an `observe` event listener from this type.

**`observeDeep(function(Array<YEvent>, Transaction):void)`**

Adds an event listener to this type that will be called synchronously every time this type or any of its children is modified. In the case this type is modified in the event listener, the event listener will be called again after the current event listener returns. The event listener receives all Events created by itself or any of its children.

**`unobserveDeep(function(Array<YEvent>, Transaction):void)`**

Removes an `observeDeep` event listener from this type.

**Y.XmlElement**  

A shareable type that represents an XML Element. It has a `nodeName`, attributes, and a list of children. But it makes no effort to validate its content and be actually XML compliant.

```
const yxml = new Y.XmlElement()
```

**`parent:Y.AbstractType|null`**

**`firstChild:Y.XmlElement|Y.XmlText|null`**

**`nextSibling:Y.XmlElement|Y.XmlText|null`**

**`prevSibling:Y.XmlElement|Y.XmlText|null`**

**`insert(index:number, content:Array<Y.XmlElement|Y.XmlText>)`**

**`delete(index:number, length:number)`**

**`get(index:number)`**

**`length:number`**

**`setAttribute(attributeName:string, attributeValue:string)`**

**`removeAttribute(attributeName:string)`**

**`getAttribute(attributeName:string):string`**

**`getAttributes():Object<string,string>`**

**`get(i:number):Y.XmlElement|Y.XmlText`**

Retrieve the i-th element.

**`slice(start:number, end:number):Array<Y.XmlElement|Y.XmlText>`**

Retrieve a range of content

**`clone():Y.XmlElement`**

Clone this type into a fresh Yjs type.

**`toArray():Array<Y.XmlElement|Y.XmlText>`**

Copies the children to a new Array.

**`toString():string`**

Get the XML serialization of all descendants.

**`toJSON():string`**

See `toString`.

**`observe(function(YXmlEvent, Transaction):void)`**

Adds an event listener to this type that will be called synchronously every time this type is modified. In the case this type is modified in the event listener, the event listener will be called again after the current event listener returns.

**`unobserve(function(YXmlEvent, Transaction):void)`**

Removes an `observe` event listener from this type.

**`observeDeep(function(Array<YEvent>, Transaction):void)`**

Adds an event listener to this type that will be called synchronously every time this type or any of its children is modified. In the case this type is modified in the event listener, the event listener will be called again after the current event listener returns. The event listener receives all Events created by itself or any of its children.

**`unobserveDeep(function(Array<YEvent>, Transaction):void)`**

Removes an `observeDeep` event listener from this type.

### Y.Doc

const doc \= new Y.Doc()

**`clientID`**

A unique id that identifies this client. (readonly)

**`gc`**

Whether garbage collection is enabled on this doc instance. Set \`doc.gc = false\` in order to disable gc and be able to restore old content. See https://github.com/yjs/yjs#yjs-crdt-algorithm for more information about gc in Yjs.

**`transact(function(Transaction):void [, origin:any])`**

Every change on the shared document happens in a transaction. Observer calls and the `update` event are called after each transaction. You should _bundle_ changes into a single transaction to reduce the amount of event calls. I.e. `doc.transact(() => { yarray.insert(..); ymap.set(..) })` triggers a single change event.  
You can specify an optional `origin` parameter that is stored on `transaction.origin` and `on('update', (update, origin) => ..)`.

**`toJSON():any`**

Deprecated: It is recommended to call toJSON directly on the shared types. Converts the entire document into a js object, recursively traversing each yjs type. Doesn't log types that have not been defined (using `ydoc.getType(..)`).

**`get(string, Y.[TypeClass]):[Type]`**

Define a shared type.

**`getArray(string):Y.Array`**

Define a shared Y.Array type. Is equivalent to `y.get(string, Y.Array)`.

**`getMap(string):Y.Map`**

Define a shared Y.Map type. Is equivalent to `y.get(string, Y.Map)`.

**`getText(string):Y.Text`**

Define a shared Y.Text type. Is equivalent to `y.get(string, Y.Text)`.

**`getXmlElement(string, string):Y.XmlElement`**

Define a shared Y.XmlElement type. Is equivalent to `y.get(string, Y.XmlElement)`.

**`getXmlFragment(string):Y.XmlFragment`**

Define a shared Y.XmlFragment type. Is equivalent to `y.get(string, Y.XmlFragment)`.

**`on(string, function)`**

Register an event listener on the shared type

**`off(string, function)`**

Unregister an event listener from the shared type

#### Y.Doc Events

**`on('update', function(updateMessage:Uint8Array, origin:any, Y.Doc):void)`**

Listen to document updates. Document updates must be transmitted to all other peers. You can apply document updates in any order and multiple times. Use \`updateV2\` to receive V2 events.

**`on('beforeTransaction', function(Y.Transaction, Y.Doc):void)`**

Emitted before each transaction.

**`on('afterTransaction', function(Y.Transaction, Y.Doc):void)`**

Emitted after each transaction.

**`on('beforeAllTransactions', function(Y.Doc):void)`**

Transactions can be nested (e.g. when an event within a transaction calls another transaction). Emitted before the first transaction.

**`on('afterAllTransactions', function(Y.Doc, Array<Y.Transaction>):void)`**

Emitted after the last transaction is cleaned up.

### Document Updates

Changes on the shared document are encoded into _document updates_. Document updates are _commutative_ and _idempotent_. This means that they can be applied in any order and multiple times.

#### Example: Listen to update events and apply them on remote client

const doc1 \= new Y.Doc()
const doc2 \= new Y.Doc()

doc1.on('update', update \=> {
  Y.applyUpdate(doc2, update)
})

doc2.on('update', update \=> {
  Y.applyUpdate(doc1, update)
})

// All changes are also applied to the other document
doc1.getArray('myarray').insert(0, \['Hello doc2, you got this?'\])
doc2.getArray('myarray').get(0) // => 'Hello doc2, you got this?'

Yjs internally maintains a state vector that denotes the next expected clock from each client. In a different interpretation it holds the number of structs created by each client. When two clients sync, you can either exchange the complete document structure or only the differences by sending the state vector to compute the differences.

#### Example: Sync two clients by exchanging the complete document structure

const state1 \= Y.encodeStateAsUpdate(ydoc1)
const state2 \= Y.encodeStateAsUpdate(ydoc2)
Y.applyUpdate(ydoc1, state2)
Y.applyUpdate(ydoc2, state1)

#### Example: Sync two clients by computing the differences

This example shows how to sync two clients with the minimal amount of exchanged data by computing only the differences using the state vector of the remote client. Syncing clients using the state vector requires another roundtrip, but can save a lot of bandwidth.

const stateVector1 \= Y.encodeStateVector(ydoc1)
const stateVector2 \= Y.encodeStateVector(ydoc2)
const diff1 \= Y.encodeStateAsUpdate(ydoc1, stateVector2)
const diff2 \= Y.encodeStateAsUpdate(ydoc2, stateVector1)
Y.applyUpdate(ydoc1, diff2)
Y.applyUpdate(ydoc2, diff1)

#### Example: Syncing clients without loading the Y.Doc

It is possible to sync clients and compute delta updates without loading the Yjs document to memory. Yjs exposes an API to compute the differences directly on the binary document updates.

// encode the current state as a binary buffer
let currentState1 \= Y.encodeStateAsUpdate(ydoc1)
let currentState2 \= Y.encodeStateAsUpdate(ydoc2)
// now we can continue syncing clients using state vectors without using the Y.Doc
ydoc1.destroy()
ydoc2.destroy()

const stateVector1 \= Y.encodeStateVectorFromUpdate(currentState1)
const stateVector2 \= Y.encodeStateVectorFromUpdate(currentState2)
const diff1 \= Y.diffUpdate(currentState1, stateVector2)
const diff2 \= Y.diffUpdate(currentState2, stateVector1)

// sync clients
currentState1 \= Y.mergeUpdates(\[currentState1, diff2\])
currentState2 \= Y.mergeUpdates(\[currentState2, diff1\])

#### Obfuscating Updates

If one of your users runs into a weird bug (e.g. the rich-text editor throws error messages), then you don't have to request the full document from your user. Instead, they can obfuscate the document (i.e. replace the content with meaningless generated content) before sending it to you. Note that someone might still deduce the type of content by looking at the general structure of the document. But this is much better than requesting the original document.

Obfuscated updates contain all the CRDT-related data that is required for merging. So it is safe to merge obfuscated updates.

const ydoc \= new Y.Doc()
// perform some changes..
ydoc.getText().insert(0, 'hello world')
const update \= Y.encodeStateAsUpdate(ydoc)
// the below update contains scrambled data
const obfuscatedUpdate \= Y.obfuscateUpdate(update)
const ydoc2 \= new Y.Doc()
Y.applyUpdate(ydoc2, obfuscatedUpdate)
ydoc2.getText().toString() // => "00000000000"

#### Using V2 update format

Yjs implements two update formats. By default you are using the V1 update format. You can opt-in into the V2 update format which provides much better compression. It is not yet used by all providers. However, you can already use it if you are building your own provider. All below functions are available with the suffix "V2". E.g. `Y.applyUpdate` ⇒ `Y.applyUpdateV2`. Also when listening to updates you need to specifically need listen for V2 events e.g. `yDoc.on('updateV2', …)`. We also support conversion functions between both formats: `Y.convertUpdateFormatV1ToV2` & `Y.convertUpdateFormatV2ToV1`.

#### Update API

**`Y.applyUpdate(Y.Doc, update:Uint8Array, [transactionOrigin:any])`**

Apply a document update on the shared document. Optionally you can specify `transactionOrigin` that will be stored on `transaction.origin` and `ydoc.on('update', (update, origin) => ..)`.

**`Y.encodeStateAsUpdate(Y.Doc, [encodedTargetStateVector:Uint8Array]):Uint8Array`**

Encode the document state as a single update message that can be applied on the remote document. Optionally specify the target state vector to only write the differences to the update message.

**`Y.encodeStateVector(Y.Doc):Uint8Array`**

Computes the state vector and encodes it into an Uint8Array.

**`Y.mergeUpdates(Array<Uint8Array>)`**

Merge several document updates into a single document update while removing duplicate information. The merged document update is always smaller than the separate updates because of the compressed encoding.

**`Y.encodeStateVectorFromUpdate(Uint8Array): Uint8Array`**

Computes the state vector from a document update and encodes it into an Uint8Array.

**`Y.diffUpdate(update: Uint8Array, stateVector: Uint8Array): Uint8Array`**

Encode the missing differences to another update message. This function works similarly to `Y.encodeStateAsUpdate(ydoc, stateVector)` but works on updates instead.

**`convertUpdateFormatV1ToV2`**

Convert V1 update format to the V2 update format.

**`convertUpdateFormatV2ToV1`**

Convert V2 update format to the V1 update format.

### Relative Positions

When working with collaborative documents, we often need to work with positions. Positions may represent cursor locations, selection ranges, or even assign a comment to a range of text. Normal index-positions (expressed as integers) are not convenient to use because the index-range is invalidated as soon as a remote change manipulates the document. Relative positions give you a powerful API to express positions.

A relative position is fixated to an element in the shared document and is not affected by remote changes. I.e. given the document `"a|c"`, the relative position is attached to `c`. When a remote user modifies the document by inserting a character before the cursor, the cursor will stay attached to the character `c`. `insert(1, 'x')("a|c") = "ax|c"`. When the relative position is set to the end of the document, it will stay attached to the end of the document.

#### Example: Transform to RelativePosition and back

const relPos \= Y.createRelativePositionFromTypeIndex(ytext, 2)
const pos \= Y.createAbsolutePositionFromRelativePosition(relPos, doc)
pos.type \=== ytext // => true
pos.index \=== 2 // => true

#### Example: Send relative position to remote client (json)

const relPos \= Y.createRelativePositionFromTypeIndex(ytext, 2)
const encodedRelPos \= JSON.stringify(relPos)
// send encodedRelPos to remote client..
const parsedRelPos \= JSON.parse(encodedRelPos)
const pos \= Y.createAbsolutePositionFromRelativePosition(parsedRelPos, remoteDoc)
pos.type \=== remoteytext // => true
pos.index \=== 2 // => true

#### Example: Send relative position to remote client (Uint8Array)

const relPos \= Y.createRelativePositionFromTypeIndex(ytext, 2)
const encodedRelPos \= Y.encodeRelativePosition(relPos)
// send encodedRelPos to remote client..
const parsedRelPos \= Y.decodeRelativePosition(encodedRelPos)
const pos \= Y.createAbsolutePositionFromRelativePosition(parsedRelPos, remoteDoc)
pos.type \=== remoteytext // => true
pos.index \=== 2 // => true

**`Y.createRelativePositionFromTypeIndex(type:Uint8Array|Y.Type, index: number [, assoc=0])`**

Create a relative position fixated to the i-th element in any sequence-like shared type (if `assoc >= 0`). By default, the position associates with the character that comes after the specified index position. If `assoc < 0`, then the relative position associates with the character before the specified index position.

**`Y.createAbsolutePositionFromRelativePosition(RelativePosition, Y.Doc): { type: Y.AbstractType, index: number, assoc: number } | null`**

Create an absolute position from a relative position. If the relative position cannot be referenced, or the type is deleted, then the result is null.

**`Y.encodeRelativePosition(RelativePosition):Uint8Array`**

Encode a relative position to an Uint8Array. Binary data is the preferred encoding format for document updates. If you prefer JSON encoding, you can simply JSON.stringify / JSON.parse the relative position instead.

**`Y.decodeRelativePosition(Uint8Array):RelativePosition`**

Decode a binary-encoded relative position to a RelativePosition object.

### Y.UndoManager

Yjs ships with an Undo/Redo manager for selective undo/redo of changes on a Yjs type. The changes can be optionally scoped to transaction origins.

const ytext \= doc.getText('text')
const undoManager \= new Y.UndoManager(ytext)

ytext.insert(0, 'abc')
undoManager.undo()
ytext.toString() // => ''
undoManager.redo()
ytext.toString() // => 'abc'

**`constructor(scope:Y.AbstractType|Array<Y.AbstractType> [, {captureTimeout:number,trackedOrigins:Set<any>,deleteFilter:function(item):boolean}])`**

Accepts either single type as scope or an array of types.

**`undo()`**

**`redo()`**

**`stopCapturing()`**

**`on('stack-item-added', { stackItem: { meta: Map<any,any> }, type: 'undo' | 'redo' })`**

Register an event that is called when a `StackItem` is added to the undo- or the redo-stack.

**`on('stack-item-updated', { stackItem: { meta: Map<any,any> }, type: 'undo' | 'redo' })`**

Register an event that is called when an existing `StackItem` is updated. This happens when two changes happen within a "captureInterval".

**`on('stack-item-popped', { stackItem: { meta: Map<any,any> }, type: 'undo' | 'redo' })`**

Register an event that is called when a `StackItem` is popped from the undo- or the redo-stack.

**`on('stack-cleared', { undoStackCleared: boolean, redoStackCleared: boolean })`**

Register an event that is called when the undo- and/or the redo-stack is cleared.

#### Example: Stop Capturing

UndoManager merges Undo-StackItems if they are created within time-gap smaller than `options.captureTimeout`. Call `um.stopCapturing()` so that the next StackItem won't be merged.

// without stopCapturing
ytext.insert(0, 'a')
ytext.insert(1, 'b')
undoManager.undo()
ytext.toString() // => '' (note that 'ab' was removed)
// with stopCapturing
ytext.insert(0, 'a')
undoManager.stopCapturing()
ytext.insert(0, 'b')
undoManager.undo()
ytext.toString() // => 'a' (note that only 'b' was removed)

#### Example: Specify tracked origins

Every change on the shared document has an origin. If no origin was specified, it defaults to `null`. By specifying `trackedOrigins` you can selectively specify which changes should be tracked by `UndoManager`. The UndoManager instance is always added to `trackedOrigins`.

class CustomBinding {}

const ytext \= doc.getText('text')
const undoManager \= new Y.UndoManager(ytext, {
  trackedOrigins: new Set(\[42, CustomBinding\])
})

ytext.insert(0, 'abc')
undoManager.undo()
ytext.toString() // => 'abc' (does not track because origin \`null\` and not part
                 //           of \`trackedTransactionOrigins\`)
ytext.delete(0, 3) // revert change

doc.transact(() \=> {
  ytext.insert(0, 'abc')
}, 42)
undoManager.undo()
ytext.toString() // => '' (tracked because origin is an instance of \`trackedTransactionorigins\`)

doc.transact(() \=> {
  ytext.insert(0, 'abc')
}, 41)
undoManager.undo()
ytext.toString() // => 'abc' (not tracked because 41 is not an instance of
                 //        \`trackedTransactionorigins\`)
ytext.delete(0, 3) // revert change

doc.transact(() \=> {
  ytext.insert(0, 'abc')
}, new CustomBinding())
undoManager.undo()
ytext.toString() // => '' (tracked because origin is a \`CustomBinding\` and
                 //        \`CustomBinding\` is in \`trackedTransactionorigins\`)

#### Example: Add additional information to the StackItems

When undoing or redoing a previous action, it is often expected to restore additional meta information like the cursor location or the view on the document. You can assign meta-information to Undo-/Redo-StackItems.

const ytext \= doc.getText('text')
const undoManager \= new Y.UndoManager(ytext, {
  trackedOrigins: new Set(\[42, CustomBinding\])
})

undoManager.on('stack-item-added', event \=> {
  // save the current cursor location on the stack-item
  event.stackItem.meta.set('cursor-location', getRelativeCursorLocation())
})

undoManager.on('stack-item-popped', event \=> {
  // restore the current cursor location on the stack-item
  restoreCursorLocation(event.stackItem.meta.get('cursor-location'))
})

Yjs CRDT Algorithm
------------------

_Conflict-free replicated data types_ (CRDT) for collaborative editing are an alternative approach to _operational transformation_ (OT). A very simple differentiation between the two approaches is that OT attempts to transform index positions to ensure convergence (all clients end up with the same content), while CRDTs use mathematical models that usually do not involve index transformations, like linked lists. OT is currently the de-facto standard for shared editing on text. OT approaches that support shared editing without a central source of truth (a central server) require too much bookkeeping to be viable in practice. CRDTs are better suited for distributed systems, provide additional guarantees that the document can be synced with remote clients, and do not require a central source of truth.

Yjs implements a modified version of the algorithm described in this paper. This article explains a simple optimization on the CRDT model and gives more insight about the performance characteristics in Yjs. More information about the specific implementation is available in INTERNALS.md and in this walkthrough of the Yjs codebase.

CRDTs that are suitable for shared text editing suffer from the fact that they only grow in size. There are CRDTs that do not grow in size, but they do not have the characteristics that are beneficial for shared text editing (like intention preservation). Yjs implements many improvements to the original algorithm that diminish the trade-off that the document only grows in size. We can't garbage collect deleted structs (tombstones) while ensuring a unique order of the structs. But we can 1. merge preceding structs into a single struct to reduce the amount of meta information, 2. we can delete content from the struct if it is deleted, and 3. we can garbage collect tombstones if we don't care about the order of the structs anymore (e.g. if the parent was deleted).

**Examples:**

1.  If a user inserts elements in sequence, the struct will be merged into a single struct. E.g. `text.insert(0, 'a'), text.insert(1, 'b');` is first represented as two structs (`[{id: {client, clock: 0}, content: 'a'}, {id: {client, clock: 1}, content: 'b'}`) and then merged into a single struct: `[{id: {client, clock: 0}, content: 'ab'}]`.
2.  When a struct that contains content (e.g. `ItemString`) is deleted, the struct will be replaced with an `ItemDeleted` that does not contain content anymore.
3.  When a type is deleted, all child elements are transformed to `GC` structs. A `GC` struct only denotes the existence of a struct and that it is deleted. `GC` structs can always be merged with other `GC` structs if the id's are adjacent.

Especially when working on structured content (e.g. shared editing on ProseMirror), these improvements yield very good results when benchmarking random document edits. In practice they show even better results, because users usually edit text in sequence, resulting in structs that can easily be merged. The benchmarks show that even in the worst case scenario that a user edits text from right to left, Yjs achieves good performance even for huge documents.

### State Vector

Yjs has the ability to exchange only the differences when syncing two clients. We use lamport timestamps to identify structs and to track in which order a client created them. Each struct has an `struct.id = { client: number, clock: number}` that uniquely identifies a struct. We define the next expected `clock` by each client as the _state vector_. This data structure is similar to the version vectors data structure. But we use state vectors only to describe the state of the local document, so we can compute the missing struct of the remote client. We do not use it to track causality.

### Formal Proof

lean-yjs provides a formal verification of the YATA CRDT algorithm that Yjs implements, using the Lean theorem prover to mathematically prove correctness properties. While the CRDT algorithm itself is correct (currently proven for preservation and commutativity), the project reveals that the pseudocode in the original YATA paper contains errors.

License and Author
------------------

Yjs and all related projects are **MIT licensed**.

Yjs is based on my research as a student at the RWTH i5. Now I am working on Yjs in my spare time.

Fund this project by donating on GitHub Sponsors or hiring me as a contractor for your collaborative app.
