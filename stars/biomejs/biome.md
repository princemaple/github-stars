---
project: biome
stars: 22572
description: A toolchain for web projects, aimed to provide functionalities to maintain them. Biome offers formatter and linter, usable via CLI and LSP.
url: https://github.com/biomejs/biome
---

  
  

हिन्दी | English | Español | Français | 繁體中文 | 简体中文 | 日本語 | Polski | Português do Brasil | 한국어 | Русский | Українська

  

**Biome** is a performant toolchain for web projects, it aims to provide developer tools to maintain the health of said projects.

**Biome is a fast formatter** for _JavaScript_, _TypeScript_, _JSX_, _JSON_, _CSS_ and _GraphQL_ that scores **97% compatibility with _Prettier_**.

**Biome is a performant linter** for _JavaScript_, _TypeScript_, _JSX_, _JSON_, _CSS_, and _GraphQL_ that features **more than 340 rules** from ESLint, typescript-eslint, and other sources. It **outputs detailed and contextualized diagnostics** that help you to improve your code and become a better programmer!

**Biome** is designed from the start to be used interactively within an editor. It can format and lint malformed code as you are writing it.

### Installation

npm install --save-dev --save-exact @biomejs/biome

### Usage

# format files
npx @biomejs/biome format --write

# lint files and apply the safe fixes
npx @biomejs/biome lint --write

# run format, lint, etc. and apply the safe fixes
npx @biomejs/biome check --write

# check all files against format, lint, etc. in CI environments
npx @biomejs/biome ci

If you want to give Biome a run without installing it, use the online playground, compiled to WebAssembly.

Documentation
-------------

Check out our homepage to learn more about Biome, or directly head to the Getting Started guide to start using Biome.

More about Biome
----------------

**Biome** has sane defaults and it doesn't require configuration.

**Biome** aims to support all main languages of modern web development.

**Biome** doesn't require Node.js to function.

**Biome** has first-class LSP support, with a sophisticated parser that represents the source text in full fidelity and top-notch error recovery.

**Biome** wants to offer a high-quality _Developer Experience_, with descriptive diagnostics and great performance.

**Biome** unifies functionalities that have previously been separate tools. Building upon a shared base allows us to provide a cohesive experience for processing code, displaying errors, parallelize work, caching, and configuration.

Read more about our project philosophy.

**Biome** is MIT licensed or Apache 2.0 licensed and moderated under the Contributor Covenant Code of Conduct.

Funding
-------

You can fund the project in different ways

### Project sponsorship and funding

You can sponsor or fund the project via Open collective or GitHub sponsors

Biome offers a simple sponsorship program that allows companies to get visibility and recognition among various developers.

Biome offers enterprise support, where Core Contributors can be employed to work on company-focused projects.

Sponsors
--------

### Platinum Sponsors

### Silver Sponsors

### Bronze Sponsors
