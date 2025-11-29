---
project: swc
stars: 32974
description: Rust-based platform for the Web
url: https://github.com/swc-project/swc
---

Make the web (development) faster.

SWC (stands for `Speedy Web Compiler`) is a super-fast TypeScript / JavaScript compiler written in Rust. It's a library for Rust and JavaScript at the same time. If you are using SWC from Rust, see rustdoc and for most users, your entry point for using the library will be parser.

Also, SWC tries to ensure that

> If you select the latest version of each crates, it will work

for rust users.

MSRV of crates is currently `1.73`.

To update all SWC crates you use, you can run `curl https://raw.githubusercontent.com/swc-project/swc/main/scripts/update-all-swc-crates.sh | bash -s`. This script will update all dependencies to the latest version and run `cargo build` to ensure that everything works. Note that you need

-   `jq`
-   `cargo upgrade`

command to run the script.

Supported Node Versions:

-   Node v10+ for usage
-   Node v20+ for development

* * *

If you are using SWC from JavaScript, please refer to docs on the website.

Documentation
=============

Check out the documentation in the website.

Features
========

Please see comparison with babel.

Performance
===========

Please see benchmark results on the website.

Supporting development
======================

Supporting swc
--------------

Star History
------------

Powered by
----------

Sponsors
--------

SWC is a community-driven project, and is maintained by a group of volunteers. If you'd like to help support the future of the project, please consider:

-   Giving developer time on the project. (Message us on Discord (preferred) or Github discussions for guidance!)
-   Giving funds by becoming a sponsor (see https://opencollective.com/swc)!

Contributing
------------

See CONTRIBUTING.md. You may also find the architecture documentation useful (ARCHITECTURE.md).

License
-------

SWC is primarily distributed under the terms of the Apache License (Version 2.0).

See LICENSE for details.
