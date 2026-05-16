---
project: jscpd
stars: 5655
description: Copy/paste detector for programming source code, supports 223 formats. AI-ready with token-efficient reporter, skill and MCP server.
url: https://github.com/kucherenko/jscpd
---

jscpd
=====

> Copy/paste detector for programming source code, supports 223 formats. AI-ready with AI skills, MCP server and token-efficient reporter.

Copy/paste is a common technical debt on a lot of projects. The jscpd gives the ability to find duplicated blocks implemented on more than 223 programming languages and digital formats of documents. The jscpd tool implements Rabin-Karp algorithm for searching duplications.

Packages of jscpd
-----------------

name

version

description

jscpd

main package for jscpd (cli and API for detections included)

jscpd-server

jscpd server application

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

jscpd-sarif-reporter

SARIF reporter for jscpd (GitHub Code Scanning compatible)

AI-Ready
--------

jscpd integrates into AI-powered development workflows through three complementary mechanisms.

### AI Reporter

The `ai` reporter produces compact, token-efficient output designed to be piped directly into an LLM prompt or agentic pipeline. It uses common-path-prefix compression and omits code fragments and colors — just the clone locations and a summary.

jscpd --reporters ai /path/to/source

Example output:

```
src/utils/ auth.ts:10-25 ~ helpers.ts:40-55
src/utils/auth.ts 30-45 ~ 80-95
src/ utils/auth.ts:10-25 ~ api/routes.ts:5-20
---
23 clones · 4.2% duplication
```

Benchmarked on the `fixtures/` directory (91 clones, 132 files):

Reporter

Output size

Estimated tokens

default (console)

~21,800 chars

~5,400

`ai`

~4,500 chars

~1,100

~79% fewer tokens than the default console reporter.

### Agent Skills

jscpd ships two AI agent skills that teach coding assistants how to use jscpd and refactor detected duplications:

**jscpd** — tool reference skill. Covers all CLI options, the AI reporter output format, and configuration file syntax. Install with:

npx skills add kucherenko/jscpd --skill jscpd

**dry-refactoring** — refactoring workflow skill. A guided process for reading clone output, choosing the right extraction strategy, applying the refactor, and verifying the clone is eliminated. Install with:

npx skills add kucherenko/jscpd --skill dry-refactoring

After installation, ask your agent to "find and fix code duplication" and it will invoke jscpd with the right options and act on the results.

### MCP Server

jscpd-server implements the Model Context Protocol (MCP), exposing jscpd's detection capabilities as tools that AI assistants can call directly from the editor. Start the server against your codebase once, then let your AI assistant check any snippet for duplication on demand — no CLI invocation needed.

npm install -g jscpd-server
jscpd-server /path/to/project

Add to your MCP client config (e.g. Claude Desktop):

{
  "mcpServers": {
    "jscpd": {
      "type": "streamable-http",
      "url": "http://localhost:3000/mcp"
    }
  }
}

Available MCP tools: `check_duplication`, `get_statistics`, `check_current_directory`. Full API docs at apps/jscpd-server.

What's New
----------

**v4.2.x**

-   **Custom tokenizer backend** — replaced the `prismjs` npm package with an own backend built on the reprism grammar engine. ~11.5% faster tokenization on real projects (avg 1126ms → 997ms on a 548-file, 223-format scan).
-   **Cross-format detection** — Vue SFC (`.vue`), Svelte (`.svelte`), Astro (`.astro`), and Markdown files are now tokenized per-block/per-section, enabling duplicate detection across file types (e.g. a `<script>` block in a `.vue` file vs a `.ts` file).
-   **New formats**: Apex, CFML/ColdFusion, GDScript, and 70+ additional formats (223 total, up from 152)
-   **Shebang detection**: auto-detect language for extensionless executable scripts
-   **`--store-path`**: configure LevelDB cache directory for parallel runs
-   **`--skipComments`**: shorthand flag for `--mode weak`
-   **`--formats-names`**: map specific filenames (e.g. `Makefile`, `Dockerfile`) to a format
-   **`--noTips`**: suppress tip output in CI environments

### Bug Fixes

-   **Entire-file duplicates silently dropped** — RabinKarp flushed the pending clone on a store _hit_ at end-of-file instead of on a _miss_, causing files that are complete copies of each other to go undetected. Fixed in `@jscpd/core` (#728).
-   **ReDoS hang on Lisp/Elisp files** — the Lisp string regex `/"(?:[^"\\]*|\\.)*"/` could catastrophically backtrack (O(2ⁿ)) on unterminated strings. Replaced with a linear alternative. Fixed in `@jscpd/tokenizer` (#737).
-   **Process crash on malformed `package.json`** — when jscpd was run in a directory containing invalid JSON in `package.json`, `readJSONSync` threw an unhandled `SyntaxError` that killed the process. Now emits a warning and continues with an empty config (#739).
-   **Vue SFC cross-file detection broken** — the detector used the file-level format (`vue`) as the store namespace for all SFC blocks, so a `<script>` block in one `.vue` file could never match a `<script>` block in another. The namespace now reflects each block's resolved sub-format (`javascript`, `typescript`, `scss`, etc.).
-   **Vue SFC incorrect column numbers** — tokens on the first line of a block carried block-relative column 1 instead of the file-absolute column. Fixed in `@jscpd/tokenizer`.
-   **50 dependency security vulnerabilities** remediated across the monorepo (Dependabot batches #DR-43 and #DR-7).

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

JSCPD Server
------------

JSCPD Server is a standalone application that provides an API for detecting code duplication. It can be used to integrate duplication detection into your services or tools.

### Installation

$ npm install -g jscpd-server

### Usage

Start the server:

$ jscpd-server

Check code for duplication:

$ curl -X POST http://localhost:3000/api/check \\
  -H "Content-Type: application/json" \\
  -d '{
    "code": "console.log(\\"hello\\");\\nconsole.log(\\"world\\");",
    "format": "javascript"
  }'

More information about server here.

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
-   OpenClaw is a personal AI assistant that runs on your own devices, supporting 20+ messaging channels and multi-platform companion apps.

Backers
-------

Thank you to all our backers! 🙏 \[Become a backer\]

Sponsors
--------

Support this project by becoming a sponsor. Your logo will show up here with a link to your website. \[Become a sponsor\]

Star History
------------

License
-------

MIT © Andrey Kucherenko
