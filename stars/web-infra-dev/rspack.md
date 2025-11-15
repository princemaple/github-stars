---
project: rspack
stars: 12224
description: The fast Rust-based JavaScript bundler with webpack-compatible API 🦀️
url: https://github.com/web-infra-dev/rspack
---

Rspack
======

English | 简体中文

Rspack is a high performance JavaScript bundler written in Rust. It offers strong compatibility with the webpack ecosystem, allowing for seamless replacement of webpack, and provides lightning fast build speeds.

✨ Features
----------

-   🚀 **Fast Startup**: Based on Rust, the build speed is extremely fast, bringing you the ultimate development experience.
-   ⚡ **Lightning HMR**: With a built-in incremental compilation mechanism, HMR is extremely fast and fully capable of developing large-scale projects.
-   📦 **Webpack Compatible**: Compatible with plugins and loaders in the webpack ecosystem, seamlessly integrating excellent libraries built by the community.
-   🎨 **Module Federation**: Provide first-class support for Module Federation to facilitate the development of large-scale web applications.
-   🛠️ **Production Optimization**: Various optimization strategies are built in by default, such as tree shaking, minification, etc.
-   🎯 **Framework Agnostic**: Not bound to any frontend framework, ensuring enough flexibility.

Read Introduction for details.

🦀 Rstack
---------

Rstack is a unified JavaScript toolchain centered on Rspack, with high performance and consistent architecture.

Name

Description

Version

Rspack

Bundler

Rsbuild

Build tool

Rslib

Library development tool

Rspress

Static site generator

Rsdoctor

Build analyzer

Rstest

Testing framework

Rslint

Linter

Getting started
---------------

See Quick start.

Contribution
------------

Please read the contributing guide and let's build Rspack together.

### Code of conduct

This repo has adopted the ByteDance Open Source Code of Conduct. Please check Code of conduct for more details.

Community
---------

Come chat with us on Discord! Rspack team and Rspack users are active there, and we're always looking for contributions.

Links
-----

Name

Description

awesome-rspack

A curated list of awesome things related to Rspack

Rspack 1.x documentation

Documentation for Rspack 1.x (latest)

Rspack 0.x documentation

Documentation for Rspack 0.x version

rspack-dev-server

Dev server for Rspack

rstack-examples

Examples showcasing Rstack

rspack-sources

Rust port of webpack-sources

rstack-design-resources

Design resources for Rstack

Contributors
------------

Benchmark
---------

See Benchmark.

Credits
-------

Thanks to:

-   The webpack team and community for creating a great bundler and ecosystem from which we draw a lot of inspiration.
-   @sokra for the great work on the webpack project.
-   @ScriptedAlchemy for creating Module Federation and helping Rspack connect with the community.
-   The SWC project created by @kdy1, which powers Rspack's code parsing, transformation and minification.
-   The esbuild project created by @evanw, which inspired the concurrent architecture of Rspack.
-   The NAPI-RS project created by @Brooooooklyn, which powers Rspack's node-binding implementation.
-   The Parcel project created by @devongovett which is the pioneer of rust bundler and inspired Rspack's incremental rebuild design.
-   The Vite project created by Evan You which inspired Rspack's compatibility design of webpack's ecosystem.
-   The `rolldown-legacy` project created by old Rolldown team, It's the predecessor of the rolldown project, which explores the possibility of making a performant bundler in Rust with Rollup-compatible API. It inspires the design principles of Rspack.
-   The html-webpack-plugin project created by @jantimon, `@rspack/html-plugin` is a fork of html-webpack-plugin to avoid some webpack API usage not supported in Rspack.
-   The Turbopack project which inspired the AST path logic of Rspack.
-   The react-refresh-webpack-plugin created by @pmmmwh, which inspires implement react refresh rspack plugin.
-   The prefresh created by @Jovi De Croock, which inspires implement preact refresh rspack plugin.
-   The mini-css-extract-plugin project created by @sokra which inspired implement css extract plugin.
-   The copy-webpack-plugin project created by @kevlened which inspired implement copy rspack plugin.
-   The webpack-subresource-integrity project created by @jscheid, which inspires implement subresource integrity rspack plugin.
-   The circular-dependency-plugin project created by @aackerman, which inspres implement circular dependency rspack plugin.
-   The tracing-chrome project created by thoren-d, which inspires the implementation of Rspack tracing.

License
-------

Rspack is MIT licensed.
