---
project: isomorphic-git
stars: 8066
description: A pure JavaScript implementation of git for node and browsers!
url: https://github.com/isomorphic-git/isomorphic-git
---

isomorphic-git
==============

`isomorphic-git` is a pure JavaScript reimplementation of git that works in both Node.js and browser JavaScript environments. It can read and write to git repositories, fetch from and push to git remotes (such as GitHub), all without any native C++ module dependencies.

Goals
-----

Isomorphic-git aims for 100% interoperability with the canonical git implementation. This means it does all its operations by modifying files in a ".git" directory just like the git you are used to. The included `isogit` CLI can operate on git repositories on your desktop or server.

This library aims to be a complete solution with no assembly required. The API has been designed with modern tools like Rollup and Webpack in mind. By providing functionality as individual functions, code bundlers can produce smaller bundles by including only the functions your application uses.

The project includes type definitions so you can enjoy static type-checking and intelligent code completion in editors like VS Code and CodeSandbox.

Project status
--------------

The original author of the project (Billie Hilton) left the project, but the project is still maintained by two volunteers:

-   @jcubic (most active)
-   @mojavelinux

But they don't write much code, mainly do code review and try to answer to issues and on Gitter, they just don't want the project to die. So you can say that this project is community driven (as jcubic always reply to issues). Which means that if you want a feature to be implemented you need to do this yourself or find someone that is willing to write the code for you. The project have some money on OpenCollective and we can spend it on some development, if you find someone that is willing to code in exchange to some bucks (it may be you), but we don't have a lot so don't expect to have full sallary.

If you want to help this project you're more than welcome to do so.

Supported Environments
----------------------

The following environments are tested in CI and will continue to be supported until the next breaking version:

  
Node 10

  
Chrome 79

  
Edge 79

  
Firefox 72

  
Safari 13

  
Android 10

  
iOS 13

Upgrading from version 0.x to version 1.x?
------------------------------------------

See the full Release Notes on GitHub and the release Blog Post.

Install
-------

You can install it from npm:

```
npm install --save isomorphic-git
```

Getting Started
---------------

The "isomorphic" in `isomorphic-git` means that the same code runs in either the server or the browser. That's tricky to do since git uses the file system and makes HTTP requests. Browsers don't have an `fs` module. And node and browsers have different APIs for making HTTP requests!

So rather than relying on the `fs` and `http` modules, `isomorphic-git` lets you bring your own file system and HTTP client.

If you're using `isomorphic-git` in node, you use the native `fs` module and the provided node HTTP client.

// node.js example
const path \= require('path')
const git \= require('isomorphic-git')
const http \= require('isomorphic-git/http/node')
const fs \= require('fs')

const dir \= path.join(process.cwd(), 'test-clone')
git.clone({ fs, http, dir, url: 'https://github.com/isomorphic-git/lightning-fs' }).then(console.log)

If you're using `isomorphic-git` in the browser, you'll need something that emulates the `fs` API. The easiest to setup and most performant library is LightningFS which is written and maintained by the same author and is part of the `isomorphic-git` suite. If LightningFS doesn't meet your requirements, isomorphic-git should also work with ZenFS and Filer. Instead of `isomorphic-git/http/node` this time import `isomorphic-git/http/web`:

<script src\="https://unpkg.com/@isomorphic-git/lightning-fs"\></script\>
<script src\="https://unpkg.com/isomorphic-git"\></script\>
<script type\="module"\>
import http from 'https://unpkg.com/isomorphic-git@beta/http/web/index.js'
const fs \= new LightningFS('fs')

const dir \= '/test-clone'
git.clone({ fs, http, dir, url: 'https://github.com/isomorphic-git/lightning-fs', corsProxy: 'https://cors.isomorphic-git.org' }).then(console.log)
</script\>

If you're using ES module syntax, you can use either the default import for convenience, or named imports to benefit from tree-shaking if you are using a bundler:

import git from 'isomorphic-git'
// or
import \* as git from 'isomorphic-git'
// or
import {plugins, clone, commit, push} from 'isomorphic-git'

View the full Getting Started guide on the docs website.

Then check out the Useful Snippets page, which includes even more sample code written by the community!

### CORS support

Unfortunately, due to the same-origin policy by default `isomorphic-git` can only clone from the same origin as the webpage it is running on. This is terribly inconvenient, as it means for all practical purposes cloning and pushing repos must be done through a proxy.

For this purpose, @isomorphic-git/cors-proxy exists; which you can clone it or `npm install` it. Alternatively, use CloudFlare workers, which can be setup without leaving the browser (instructions).

For testing or small projects, you can also use https://cors.isomorphic-git.org - a free proxy sponsored by Clever Cloud.

We hope to get CORS headers added to all the major Git hosting platforms eventually, and will list the progress made here:

Service

Supports CORS requests

Gogs (self-hosted)

✔

Gitea (self-hosted)

✔

Azure DevOps

✔ (Usage Note: requires authentication)

Gitlab

❌ Our PR was rejected, but the issue is still open!

Bitbucket

❌

Github

❌

It is literally just two lines of code to add the CORS headers!! Easy stuff. Surely it will happen.

### `isogit` CLI

Isomorphic-git comes with a simple CLI tool, named `isogit` because `isomorphic-git` is a lot to type. It is really just a thin shell that translates command line arguments into the equivalent JS API commands. So you should be able to run _any_ current or future isomorphic-git commands using the CLI.

It always starts with an the assumption that the current working directory is a git root. E.g. `{ dir: '.' }`.

It uses `minimisted` to parse command line options and will print out the equivalent JS command and pretty-print the output JSON.

The CLI is more of a lark for quickly testing `isomorphic-git` and isn't really meant as a `git` CLI replacement.

Supported Git commands
----------------------

This project follows semantic versioning, so we may continue to make changes to the API but they will always be backwards compatible unless there is a major version bump.

### commands

-   abortMerge
-   add
-   addNote
-   addRemote
-   annotatedTag
-   branch
-   checkout
-   clone
-   commit
-   currentBranch
-   deleteBranch
-   deleteRef
-   deleteRemote
-   deleteTag
-   expandOid
-   expandRef
-   fastForward
-   fetch
-   findMergeBase
-   findRoot
-   getConfig
-   getConfigAll
-   getRemoteInfo
-   getRemoteInfo2
-   hashBlob
-   indexPack
-   init
-   isDescendent
-   isIgnored
-   listBranches
-   listFiles
-   listNotes
-   listRefs
-   listRemotes
-   listServerRefs
-   listTags
-   log
-   merge
-   packObjects
-   pull
-   push
-   readBlob
-   readCommit
-   readNote
-   readObject
-   readTag
-   readTree
-   remove
-   removeNote
-   renameBranch
-   resetIndex
-   resolveRef
-   setConfig
-   stash
-   status
-   statusMatrix
-   tag
-   updateIndex
-   version
-   walk
-   writeBlob
-   writeCommit
-   writeObject
-   writeRef
-   writeTag
-   writeTree

Community
---------

Share your questions and ideas with us! We love that. You can find us in our Gitter chatroom or just create an issue here on Github! We are also @IsomorphicGit on Twitter.

Contributing to `isomorphic-git`
--------------------------------

The development setup is similar to that of a large web application. The main difference is the ridiculous amount of hacks involved in the tests. We use Facebook's Jest for testing, which make doing TDD fast and fun, but we also used custom hacks so that the same tests will also run in the browser using Jasmine via Karma. We even have our own mock server for serving git repository test fixtures!

You'll need node.js installed, but everything else is a devDependency.

git clone https://github.com/isomorphic-git/isomorphic-git
cd isomorphic-git
npm install
npm test

The new release happens automatically after every PR merge. We use semantic release.

Check out the `CONTRIBUTING` document for more instructions.

Who is using isomorphic-git?
----------------------------

-   nde - a futuristic next-generation web IDE
-   git-app-manager - install "unhosted" websites locally by git cloning them
-   GIT Web Terminal
-   Next Editor
-   Clever Cloud
-   Stoplight Studio - a modern editor for API design and technical writing

Similar projects
----------------

-   js-git
-   es-git

Acknowledgments
---------------

Isomorphic-git would not have been possible without the pioneering work by @creationix and @chrisdickinson. Git is a tricky binary mess, and without their examples (and their modules!) we would not have been able to come even close to finishing this. They are geniuses ahead of their time.

Cross-browser device testing is provided by:

Contributors
------------

Thanks goes to these wonderful people (emoji key):

  
**William Hilton**  
📝 🐛 💻 🎨 📖 💡 ⚠️ ✅

  
**wDhTIG**  
🐛

  
**Marc MacLeod**  
🤔 🔍

  
**Brett Zamir**  
🤔

  
**Dan Allen**  
🐛 💻 🤔

  
**Tomáš Hübelbauer**  
🐛 💻

  
**Juan Campa**  
🐛 💻

  
**Ira Miller**  
🐛

  
**Rhys Arkins**  
💻

  
**Sean Larkin**  
💻

  
**Daniel Ruf**  
💻

  
**bokuweb**  
💻 📖 ⚠️

  
**Hiroki Osame**  
💻 📖

  
**Jakub Jankiewicz**  
💬 🐛 💻 💡 ⚠️

  
**howardgod**  
🐛 💻

  
**burningTyger**  
🐛

  
**Melvin Carvalho**  
📖

  
**akaJes**  
💻

  
**Dima Sabanin**  
🐛 💻

  
**Koutaro Chikuba**  
🐛 💻

  
**Hubert SABLONNIÈRE**  
💻 ⚠️ 🤔 🔍

  
**David Duarte**  
💻

  
**Thomas Pytleski**  
🐛 💻

  
**Vadim Markovtsev**  
🐛

  
**Yu Shimura**  
🤔 💻 ⚠️

  
**Dan Lynch**  
💻

  
**Jeffrey Wescott**  
🐛 💻

  
**zebzhao**  
💻

  
**Tyler Smith**  
🐛

  
**Bram Borggreve**  
🐛

  
**Stefan Guggisberg**  
🐛 💻 ⚠️

  
**Catalin Pirvu**  
💻

  
**Nicholas Nelson**  
💻 ⚠️

  
**Anna Henningsen**  
💻

  
**Fabian Henneke**  
🐛 💻

  
**djencks**  
🐛 💻 ⚠️

  
**Clemens Wolff**  
💻 📖 ⚠️

  
**Sojin Park**  
💻

  
**Edward Faulkner**  
💻

  
**Khải**  
🐛

  
**Corbin Crutchley**  
💻 📖 ⚠️

  
**Riceball LEE**  
💻 📖 ⚠️

  
**lin onetwo**  
💻

  
**林法鑫**  
🐛

  
**Will Stott**  
💻 ⚠️

  
**Seth Nickell**  
🐛

  
**Alex Titarenko**  
💻

  
**Misha Kaletsky**  
💻

  
**Richard C. Zulch**  
💻 📖

  
**mkizka**  
💻

  
**RyotaK**  
🐛

  
**Noah Hummel**  
💻 ⚠️

  
**Mike Lewis**  
📖

  
**Sam Verschueren**  
💻

  
**Vitor Luiz Cavalcanti**  
📖

  
**Shane McLaughlin**  
💻 📖 ⚠️

  
**Sean Poulter**  
🚧 💻 📖 ⚠️

  
**araknast**  
💻 ⚠️ 📖

  
**Rafael Raab**  
💻 📖

  
**Lukáš Cezner**  
💻 📖 ⚠️ 🐛

  
**dead-end**  
💻 📖 ⚠️

  
**Barry**  
💻 📖 ⚠️

  
**Alireza Mirian**  
💻 📖 ⚠️ 🐛

  
**DanilKazanov**  
💻 📖 ⚠️

  
**Eyal Hisco**  
🐛

  
**Sebastien**  
💻

  
**Yaroslav Halchenko**  
📖

  
**Alex Villarreal**  
💻

  
**Modesty Zhang**  
💻 📖 ⚠️

  
**Ben Morrow**  
💻

  
**jayree**  
💻 ⚠️

  
**Lucas Martin Segurado**  
📖 🐛

  
**Leon Kaucher**  
💻 ⚠️

  
**Gili Shohat**  
💻 📖 ⚠️

  
**Habib**  
💻 📖 ⚠️

  
**Vinzent**  
💻

  
**James Prevett**  
💻 ⚠️ 🚧

  
**Patrick Kranz**  
💻 📖 ⚠️

  
**Luke Cotter**  
💻

  
**Tom Larkworthy**  
📖

  
**Mostafa Mahmoud**  
💻 ⚠️ 💬

  
**Aniket Bhosale**  
💻 📖 ⚠️

  
**Mathias Nisted Velling**  
💻 ⚠️

  
**acandoo**  
📦 📓

  
**Patrick Kranz**  
💻 📖 ⚠️

  
**Luke Cotter**  
💻

  
**Tom Larkworthy**  
📖

  
**Mostafa Mahmoud**  
💻 ⚠️ 💬

  
**Aniket Bhosale**  
💻 📖 ⚠️

  
**Mathias Nisted Velling**  
💻 ⚠️

  
**acandoo**  
📦 📓

  
**Bekatan Satyev**  
💻 ⚠️

  
**Hemanth Kini**  
💻

  
**Anish Awasthi**  
💻 📖 ⚠️

  
**fetsorn**  
📖

  
**xiaoboost**  
💻 📖 ⚠️

  
**Mateusz Burzyński**  
💻 ⚠️

This project follows the all-contributors specification. Contributions of any kind welcome!

### Backers

Thank you to all our backers! 🙏 \[Become a backer\]

### Sponsors

Support this project by becoming a sponsor. Your logo will show up here with a link to your website. \[Become a sponsor\]

License
-------

This work is released under The MIT License
