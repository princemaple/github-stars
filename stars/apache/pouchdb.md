---
project: pouchdb
stars: 17517
description: :kangaroo: - PouchDB is a pocket-sized database.
url: https://github.com/apache/pouchdb
---

PouchDB – The Database that Syncs!
==================================

PouchDB is an open-source JavaScript database inspired by Apache CouchDB that is designed to run well within the browser.

PouchDB was created to help web developers build applications that work as well offline as they do online.

Using PouchDB
-------------

To get started using PouchDB, check out the web site and API documentation.

Getting Help
------------

The PouchDB community is active in `#pouchdb` on the CouchDB Slack, in the Google Groups mailing list, and on StackOverflow. Or you can mastodon @pouchdb!

If you think you've found a bug in PouchDB, please write a reproducible test case and file a Github issue.

Prerelease builds
-----------------

If you like to live on the bleeding edge, you can build PouchDB from source using these steps:

```
git clone https://github.com/pouchdb/pouchdb.git
cd pouchdb
npm install
```

After running these steps, the browser build can be found in `packages/node_modules/pouchdb/dist/pouchdb.js`.

Changelog
---------

PouchDB follows semantic versioning. To see a changelog with all PouchDB releases, check out the Github releases page.

For a concise list of breaking changes, there's the wiki list of breaking changes.

Keep in mind that PouchDB is auto-migrating, so a database created in 1.0.0 will still work if you open it in 4.0.0+. Any release containing a migration is clearly marked in the release notes.

Contributing
------------

We're always looking for new contributors! If you'd like to try your hand at writing code, writing documentation, designing the website, writing a blog post, or answering questions on StackOverflow, then we'd love to have your input.

If you have a pull request that you'd like to submit, please read the contributing guide for info on style, commit message format, and other (slightly!) nitpicky things like that. PouchDB is heavily tested, so you'll also want to check out the testing guide.
