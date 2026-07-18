---
project: gitea
stars: 56895
description: Git with a cup of tea! Painless self-hosted all-in-one software development service, including Git hosting, code review, team collaboration, package registry and CI/CD
url: https://github.com/go-gitea/gitea
---

Gitea
=====

繁體中文 | 简体中文

Purpose
-------

The goal of Gitea is to make the easiest, fastest, and most painless way of setting up a self-hosted all-in-one software development service, including Git hosting, code management, code review, issue tracking, project kanban, wiki, team collaboration, package registry and CI/CD which can reuse GitHub Actions.

As Gitea is written in Go, it works across **all** the platforms and architectures that are supported by Go, including Linux, macOS, FreeBSD/OpenBSD and Windows on x86, amd64, ARM, RISC-V 64 and PowerPC architectures.

For online demonstrations, you can visit demo.gitea.com.

For accessing free Gitea service (with a limited number of repositories), you can visit gitea.com.

To quickly deploy your own dedicated Gitea instance on Gitea Cloud, you can start a free trial at cloud.gitea.com, or use container (docker/podman/etc) to deploy on your own server with the official image.

Documentation
-------------

You can find comprehensive documentation on our official documentation website.

It includes installation, administration, usage, development, contributing guides, and more to help you get started and explore all features effectively.

If you have any suggestions or would like to contribute to it, you can visit the documentation repository

Building
--------

See docs/build-setup.md for prerequisites and docs/development.md for setting up a local development environment, linting, and testing.

If you'd like to build from source or make a distribution package, see docs/build-source.md for more information.

After building, you can run `./gitea web` to start the server, or `./gitea help` to see all available commands.

Contributing
------------

Expected workflow is: Fork -> Patch -> Push -> Pull Request

Note

1.  **YOU MUST READ THE CONTRIBUTORS GUIDE BEFORE STARTING TO WORK ON A PULL REQUEST.**
2.  New to the codebase? The development guide walks through setting up a local environment and building from source.
3.  If you have found a vulnerability in the project, please write privately to **security@gitea.io**. Thanks!

Translating
-----------

Translations are done through Crowdin. If you want to translate to a new language, ask one of the managers in the Crowdin project to add a new language there.

You can also just create an issue for adding a language or ask on Discord on the #translation channel. If you need context or find some translation issues, you can leave a comment on the string or ask on Discord. For general translation questions there is a section in the docs. Currently a bit empty, but we hope to fill it as questions pop up.

Get more information from documentation.

Official and Third-Party Projects
---------------------------------

We provide an official go-sdk, a CLI tool called tea and an action runner for Gitea Action.

We maintain a list of Gitea-related projects at gitea/awesome-gitea, where you can discover more third-party projects, including SDKs, plugins, themes, and more.

Communication
-------------

If you have questions that are not covered by the documentation, you can get in contact with us on our Discord server or create a post in the discourse forum.

Authors
-------

-   Maintainers
-   Contributors
-   Translators

Backers
-------

Thank you to all our backers! 🙏 \[Become a backer\]

Sponsors
--------

Support this project by becoming a sponsor. Your logo will show up here with a link to your website. \[Become a sponsor\]

FAQ
---

**How do you pronounce Gitea?**

Gitea is pronounced /ɡɪ’ti:/ as in "gi-tea" with a hard g.

**How do I configure Gitea?**

For dynamic config options, you can change it on your admin panel's configuration section.

For static config options, you can edit your `app.ini` file and resart the instance. See app.example.ini or configuration documentation for more details.

**Where can I find the security patches?**

In the release log or the change log, search for the keyword `SECURITY` to find the security patches.

(more FAQs are listed in FAQ documentation)

License
-------

This project is licensed under the MIT License. See the LICENSE file for the full license text.

Further information
-------------------

Looking for an overview of the interface? Check it out the screenshots!

### Login/Register Page

### User Dashboard

### User Profile

### Explore

### Repository

#### Repository Issue

#### Repository Pull Requests

#### Repository Actions

#### Repository Activity

### Organization
