---
project: jscpd
stars: 5102
description: Copy/paste detector for programming source code.
url: https://github.com/kucherenko/jscpd
---

jscpd
-----

> Copy/paste detector for programming source code, supports 150+ formats.

Copy/paste is a common technical debt on a lot of projects. The jscpd gives the ability to find duplicated blocks implemented on more than 150 programming languages and digital formats of documents. The jscpd tool implements Rabin-Karp algorithm for searching duplications.

Packages of jscpd
-----------------

name

version

description

jscpd

main package for jscpd (cli and API for detections included)

@jscpd/core

core detection algorithm, can be used for detect duplication in different environments, one dependency to eventemitter3

@jscpd/finder

detector of duplication in files

@jscpd/tokenizer

tool for tokenize programming source code

@jscpd/leveldb-store

LevelDB store, used for big repositories, slower than default store

@jscpd/html-reporter

Html reporter for jscpd

@jscpd/badge-reporter

Badge reporter for jscpd

Installation
------------

$ npm install -g jscpd

Usage
-----

$ npx jscpd /path/to/source

or

$ jscpd /path/to/code

or

$ jscpd --pattern "src/\*\*/\*.js"

More information about cli here.

Programming API
---------------

For integration copy/paste detection to your application you can use programming API:

`jscpd` Promise API

import {IClone} from '@jscpd/core';
import {jscpd} from 'jscpd';

const clones: Promise<IClone\[\]\> \= jscpd(process.argv);

`jscpd` async/await API

import {IClone} from '@jscpd/core';
import {jscpd} from 'jscpd';
(async () \=> {
  const clones: IClone\[\] \= await jscpd(\['', '', \_\_dirname + '/../fixtures', '-m', 'weak', '--silent'\]);
  console.log(clones);
})();

`detectClones` API

import {detectClones} from "jscpd";

(async () \=> {
  const clones \= await detectClones({
    path: \[
      \_\_dirname + '/../fixtures'
    \],
    silent: true
  });
  console.log(clones);
})()

`detectClones` with persist store

import {detectClones} from "jscpd";
import {IMapFrame, MemoryStore} from "@jscpd/core";

(async () \=> {
  const store \= new MemoryStore<IMapFrame\>();

  await detectClones({
    path: \[
      \_\_dirname + '/../fixtures'
    \],
  }, store);

  await detectClones({
    path: \[
      \_\_dirname + '/../fixtures'
    \],
    silent: true
  }, store);
})()

In case of deep customisation of detection process you can build your own tool with `@jscpd/core`, `@jscpd/finder` and `@jscpd/tokenizer`.

Start contribution
------------------

-   Fork the repo kucherenko/jscpd
-   Clone forked version (`git clone https://github.com/{your-id}/jscpd`)
-   Install dependencies (`pnpm install`)
-   Run the project in dev mode: `pnpm dev` (watch changes and rebuild the packages)
-   Add your changes
-   Add tests and check it with `pnpm test`
-   Build your project `pnpm build`
-   Create PR

Who uses jscpd
--------------

-   GitHub Super Linter is combination of multiple linters to install as a GitHub Action
-   Code-Inspector is a code analysis and technical debt management service.
-   Mega-Linter is a 100% open-source linters aggregator for CI (GitHub Action & other CI tools) or to run locally
-   Codacy automatically analyzes your source code and identifies issues as you go, helping you develop software more efficiently with fewer issues down the line.
-   Natural is a general natural language facility for nodejs. It offers a broad range of functionalities for natural language processing.

Backers
-------

Thank you to all our backers! 🙏 \[Become a backer\]

Sponsors
--------

Support this project by becoming a sponsor. Your logo will show up here with a link to your website. \[Become a sponsor\]

License
-------

MIT © Andrey Kucherenko
