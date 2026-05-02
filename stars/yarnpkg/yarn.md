---
project: yarn
stars: 41509
description: The 1.x line is frozen - features and bugfixes now happen on https://github.com/yarnpkg/berry
url: https://github.com/yarnpkg/yarn
---

> ℹ️ Important note
> -----------------
> 
> This repository holds the sources for Yarn 1.x (latest version at the time of this writing being 1.22). New releases (at this time the 3.2.3, although we're currently working on our next major) are tracked on the yarnpkg/berry repository, this one here being mostly kept for historical purposes and the occasional hotfix we publish to make the migration from 1.x to later releases easier.
> 
> If you hit bugs or issues with Yarn 1.x, we strongly suggest you migrate to the latest release - at this point they have been maintained longer than 1.x, and many classes of problems have already been addressed there. By using the `nodeLinker` setting you'll also have the choice of how you want to install your packages: node\_modules like npm, symlinks like pnpm, or manifest files via Yarn PnP.

* * *

Fast, reliable, and secure dependency management.

* * *

**Fast:** Yarn caches every package it has downloaded, so it never needs to download the same package again. It also does almost everything concurrently to maximize resource utilization. This means even faster installs.

**Reliable:** Using a detailed but concise lockfile format and a deterministic algorithm for install operations, Yarn is able to guarantee that any installation that works on one system will work exactly the same on another system.

**Secure:** Yarn uses checksums to verify the integrity of every installed package before its code is executed.

Features
--------

-   **Offline Mode.** If you've installed a package before, then you can install it again without an internet connection.
-   **Deterministic.** The same dependencies will be installed in the same exact way on any machine, regardless of installation order.
-   **Network Performance.** Yarn efficiently queues requests and avoids request waterfalls in order to maximize network utilization.
-   **Network Resilience.** A single request that fails will not cause the entire installation to fail. Requests are automatically retried upon failure.
-   **Flat Mode.** Yarn resolves mismatched versions of dependencies to a single version to avoid creating duplicates.
-   **More emojis.** 🐈

Our supports
------------

### Gold sponsors

**All your environment variables, in one place**. Stop struggling with scattered API keys, hacking together home-brewed tools, and avoiding access controls. Keep your team and servers in sync with **Doppler**.

**Your app, enterprise-ready**. Start selling to enterprise customers with just a few lines of code. Add Single Sign-On (and more) in minutes instead of months with **WorkOS**.

Installing Yarn
---------------

Read the Installation Guide on our website for detailed instructions on how to install Yarn.

Using Yarn
----------

Read the Usage Guide on our website for detailed instructions on how to use Yarn.

Contributing to Yarn
--------------------

The 1.x codebase is fairly old and will only accept security fixes. For new features or bugfixes, please see our new repository and its contribution guide.

Prior art
---------

Yarn wouldn't exist if it wasn't for excellent prior art. Yarn has been inspired by the following projects:

-   Bundler
-   Cargo
-   npm

Credits
-------

Thanks to Sam Holmes for donating the npm package name!
