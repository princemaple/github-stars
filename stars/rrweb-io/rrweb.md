---
project: rrweb
stars: 19664
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

  
**Yuyz0112**  
  

  
**Yun Feng**  
  

  
**eoghanmurray**  
  

  
**Juice10**  
open for rrweb consulting

Who's using rrweb?
------------------
