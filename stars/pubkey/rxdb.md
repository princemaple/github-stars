---
project: rxdb
stars: 22912
description: A fast, local first, reactive Database for JavaScript Applications https://rxdb.info/
url: https://github.com/pubkey/rxdb
---

  

  
  

### A fast, local-first, reactive Database for JavaScript Applications

       

     

  

  What is RxDB?
---------------

RxDB (short for **R**eactive **D**ata**b**ase) is a local-first, NoSQL-database for JavaScript Applications like Websites, hybrid Apps, Electron-Apps, Progressive Web Apps, Deno and Node.js. Reactive means that you can not only query the current state, but **subscribe** to all state changes like the result of a query or even a single field of a document. This is great for UI-based **realtime** applications in a way that makes it easy to develop and also has great performance benefits but can also be used to create fast backends in Node.js.  
RxDB provides an easy to implement protocol for realtime **replication** with your existing infrastructure or one of the plugins for HTTP, GraphQL, CouchDB, Websocket, WebRTC, Supabase, Firestore, NATS.  
RxDB is based on a storage interface that enables you to swap out the underlying storage engine. This increases **code reuse** because you can use the same database code for different JavaScript environments by just switching out the storage settings.

Use the quickstart, read the documentation or explore the example projects.

  Used by **many**
------------------

RxDB is a proven technology used by thousands of developers worldwide. With its flexibility, RxDB is used in a diverse range of apps and services.

  
(add yours)

  Multiplayer realtime applications
-----------------------------------

  Replicate with your **existing infrastructure**
-------------------------------------------------

RxDB provides an easy to implement, **battle-tested** Sync Engine for realtime replication with your existing infrastructure.  
You do not have to use a specific cloud or backend database. The protocol works by implementing three simple HTTP endpoints. There are also production-ready plugins to easily replicate with GraphQL, CouchDB, Websocket, WebRTC (P2P),Supabase, Firestore or NATS.

  **Flexible** storage layer
----------------------------

RxDB is based on a storage interface that enables you to swap out the underlying storage engine. This increases **code reuse** because the same database code can be used in different JavaScript environments by just switching out the storage settings.

You can use RxDB on top of LocalStorage, IndexedDB, OPFS, LokiJS, Dexie.js, in-memory, SQLite, in a WebWorker thread and even on top of FoundationDB and DenoKV.

No matter what kind of runtime you have, as long as it runs JavaScript, it can run RxDB:

#### Browsers Node.js React Native Capacitor NativeScript Flutter or as an Electron Database

All the features that you need
------------------------------

Since its beginning in 2018, RxDB has gained a huge set of features and plugins which makes it a flexible full solution regardless of which type of application you are building. Every feature that you need now or might need in the future is already there.

Logging  
Attachments  
ORM  
Conflict Handling  
Middleware  
Signals

State  
Backup  
Replication  
Server  
Storages  
Local Documents

Schema Validation  
Compression  
Migration  
Encryption  
CRDT  
Population

  Quick start
-------------

#### Install

npm install rxdb rxjs --save

#### Store data

import { 
  createRxDatabase
} from 'rxdb/plugins/core';

/\*\*
 \* For browsers, we use the localstorage based storage.
 \* In other JavaScript runtimes, we can use different storages:
 \* @link https://rxdb.info/rx-storage.html
 \*/
import { getRxStorageLocalstorage } from 'rxdb/plugins/storage-localstorage';

// create a database
const db \= await createRxDatabase({
    name: 'heroesdb', // the name of the database
    storage: getRxStorageLocalstorage()
});

// add collections
await db.addCollections({
  heroes: {
    schema: mySchema
  }
});

// insert a document
await db.heroes.insert({
  name: 'Bob',
  healthpoints: 100
});

#### Query data once

const aliveHeroes \= await db.heroes.find({
  selector: {
    healthpoints: {
      $gt: 0
    }
  }
}).exec(); // the exec() returns the result once

#### Observe a Query

await db.heroes.find({
  selector: {
    healthpoints: {
      $gt: 0
    }
  }
})
.$ // the $ returns an observable that emits each time the result set of the query changes
.subscribe(aliveHeroes \=> console.dir(aliveHeroes));

  Get started
-------------

Get started now by reading the docs or exploring the example-projects.

  Support and Contribute
------------------------

-   **Leave a Star ☝️**
-   Check out how you can contribute to this project.
-   Read this when you have found a bug
-   Buy access to the premium plugins
-   Join us at discord to get help
-   Follow us at LinkedIn

#### More content

Angular Database, Frontend Database, localStorage, React Database, Browser Database, React Native Database, PWA Database, In-memory NoSQL database, JSON database, Angular IndexedDB, React IndexedDB, Optimistic UI, local database, React Native Encryption, Vue Database, jQuery Database, Vue IndexedDB, Firestore Alternative, Firebase Realtime Database Alternative, Ionic Storage
