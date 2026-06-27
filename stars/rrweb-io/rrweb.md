---
project: rrweb
stars: 19782
description: record and replay the web
url: https://github.com/rrweb-io/rrweb
---

Try rrweb

rrweb
=====

**(new!) rrweb cloud - hosted rrweb backend is now available**

中文文档

rrweb refers to 'record and replay the web', which is a tool for recording and replaying users' interactions on the web.

Guide
-----

**📚 Read the rrweb guide here. 📚**

**🍳 Recipes 🍳**

**📺 Presentation:** Hacking the browser to digital twin your users 📺

Project Structure
-----------------

rrweb is composed of the following principal parts:

-   **rrweb-snapshot**, including both snapshot and rebuilding features. The snapshot is used to convert the DOM and its state into a serializable data structure with a unique identifier; the rebuilding feature is to rebuild the snapshot into corresponding DOM. This package can be used on it's own to provide a static HTML based 'screenshot' of the current web page state, with all Javascript deactivated.
-   **record**, builds on an initial snapshot to record all HTML state changes (mutations) and user interactions as the user browses the web page. Multiple page loads can be chained together into a single recording.
-   **replay**, rebuilds the inital snapshot and replays the list or stream of subsequent events to show a 'session replay'
-   **rrweb-player**, a player UI on top of the replay package to provide GUI-based functions like pause, fast-forward, drag and drop to play at any time.

Roadmap
-------

-   ✅ storage engine: do deduplication on a large number of rrweb sessions
-   Token efficient AI session replay format (in progress)
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

For the latest setup, testing, and pull request workflow, see Contributing to rrweb.

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

  
**Juice10**  
open for rrweb consulting

  
**eoghanmurray**  
  

  
**Yun Feng**  
  

Who's using rrweb?
------------------
