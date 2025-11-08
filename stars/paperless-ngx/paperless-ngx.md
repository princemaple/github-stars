---
project: paperless-ngx
stars: 34142
description: A community-supported supercharged document management system: scan, index and archive all your documents
url: https://github.com/paperless-ngx/paperless-ngx
---

Paperless-ngx
=============

Paperless-ngx is a document management system that transforms your physical documents into a searchable online archive so you can keep, well, _less paper_.

Paperless-ngx is the official successor to the original Paperless & Paperless-ng projects and is designed to distribute the responsibility of advancing and supporting the project among a team of people. Consider joining us!

Thanks to the generous folks at DigitalOcean, a demo is available at demo.paperless-ngx.com using login `demo` / `demo`. _Note: demo content is reset frequently and confidential information should not be uploaded._

-   Features
-   Getting started
-   Contributing
    -   Community Support
    -   Translation
    -   Feature Requests
    -   Bugs
-   Related Projects
-   Important Note

This project is supported by:  

Features
========

A full list of features and screenshots are available in the documentation.

Getting started
===============

The easiest way to deploy paperless is `docker compose`. The files in the `/docker/compose` directory are configured to pull the image from the GitHub container registry.

If you'd like to jump right in, you can configure a `docker compose` environment with our install script:

bash -c "$(curl -L https://raw.githubusercontent.com/paperless-ngx/paperless-ngx/main/install-paperless-ngx.sh)"

More details and step-by-step guides for alternative installation methods can be found in the documentation.

Migrating from Paperless-ng is easy, just drop in the new docker image! See the documentation on migrating for more details.

### Documentation

The documentation for Paperless-ngx is available at https://docs.paperless-ngx.com.

Contributing
============

If you feel like contributing to the project, please do! Bug fixes, enhancements, visual fixes etc. are always welcome. If you want to implement something big: Please start a discussion about that! The documentation has some basic information on how to get started.

Community Support
-----------------

People interested in continuing the work on paperless-ngx are encouraged to reach out here on github and in the Matrix Room. If you would like to contribute to the project on an ongoing basis there are multiple teams (frontend, ci/cd, etc) that could use your help so please reach out!

Translation
-----------

Paperless-ngx is available in many languages that are coordinated on Crowdin. If you want to help out by translating paperless-ngx into your language, please head over to https://crowdin.com/project/paperless-ngx, and thank you! More details can be found in CONTRIBUTING.md.

Feature Requests
----------------

Feature requests can be submitted via GitHub Discussions, you can search for existing ideas, add your own and vote for the ones you care about.

Bugs
----

For bugs please open an issue or start a discussion if you have questions.

Related Projects
================

Please see the wiki for a user-maintained list of related projects and software that is compatible with Paperless-ngx.

Important Note
==============

> Document scanners are typically used to scan sensitive documents like your social insurance number, tax records, invoices, etc. **Paperless-ngx should never be run on an untrusted host** because information is stored in clear text without encryption. No guarantees are made regarding security (but we do try!) and you use the app at your own risk. **The safest way to run Paperless-ngx is on a local server in your own home with backups in place**.
