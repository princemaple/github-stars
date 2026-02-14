---
project: rrweb
stars: 19204
description: record and replay the web
url: https://github.com/rrweb-io/rrweb
---

Try rrweb

rrweb
=====

**The rrweb documentary (in Chinese, with English subtitles)**

中文文档

> I have joined Github Sponsors and highly appreciate your sponsorship.

rrweb refers to 'record and replay the web', which is a tool for recording and replaying users' interactions on the web.

Guide
-----

**📚 Read the rrweb guide here. 📚**

**🍳 Recipes 🍳**

**📺 Presentation:** Hacking the browser to digital twin your users 📺

Project Structure
-----------------

rrweb is mainly composed of 3 parts:

-   **rrweb-snapshot**, including both snapshot and rebuilding features. The snapshot is used to convert the DOM and its state into a serializable data structure with a unique identifier; the rebuilding feature is to rebuild the snapshot into corresponding DOM.
-   **rrweb**, including two functions, record and replay. The record function is used to record all the mutations in the DOM; the replay is to replay the recorded mutations one by one according to the corresponding timestamp.
-   **rrweb-player**, is a player UI for rrweb, providing GUI-based functions like pause, fast-forward, drag and drop to play at any time.

Roadmap
-------

-   storage engine: do deduplication on a large number of rrweb sessions
-   compact mutation data in common patterns
-   provide plugins via the new plugin API, including:
    -   XHR plugin
    -   fetch plugin
    -   GraphQL plugin
    -   ...

Internal Design
---------------

-   serialization
-   incremental snapshot
-   replay
-   sandbox

Contribute Guide
----------------

Since we want the record and replay sides to share a strongly typed data structure, rrweb is developed with typescript which provides stronger type support.

Typescript handbook

1.  Fork this repository.
2.  Run `yarn install` in the root to install required dependencies for all sub-packages (note: `npm install` is _not_ recommended).
3.  Run `yarn build:all` to build all packages and get a stable base, then `yarn dev` in the root to get auto-building for all the sub-packages whenever you modify anything.
4.  Navigate to one of the sub-packages (in the `packages` folder) where you'd like to make a change.
5.  Patch the code and run `yarn test` to run the tests, make sure they pass before you commit anything. Add test cases in order to avoid future regression.
6.  If tests are failing, but the change in output is desirable, run `yarn test:update` and carefully commit the changes in test output.
7.  Push the code and create a pull request.

Protip: You can run `yarn test` in the root folder to run all the tests.

In addition to adding integration tests and unit tests, rrweb also provides a REPL testing tool.

Using the REPL tool

Sponsors
--------

Become a sponsor and get your logo on our README on Github with a link to your site.

### Gold Sponsors 🥇

### Silver Sponsors 🥈

### Bronze Sponsors 🥉

### Backers

Core Team Members
-----------------

  
**Yuyz0112**  
  

  
**Yun Feng**  
  

  
**eoghanmurray**  
  

  
**Juice10**  
open for rrweb consulting

Who's using rrweb?
------------------
