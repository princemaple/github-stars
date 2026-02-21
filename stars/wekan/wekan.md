---
project: wekan
stars: 20845
description: The Open Source kanban, built with Meteor. GitHub issues/PRs are only for FLOSS Developers, not for support, support is at https://wekan.fi/commercial-support/ . New English strings for new features at imports/i18n/data/en.i18n.json . Non-English translations at https://app.transifex.com/wekan/wekan only.
url: https://github.com/wekan/wekan
---

WeKan ® - Open Source kanban
============================

Downloads
---------

https://wekan.fi/install/

Docker Containers
-----------------

-   GitHub
-   Quay
-   Docker Hub

docker-compose.yml at https://github.com/wekan/wekan/blob/main/docker-compose.yml

Standards
---------

-   WeKan and Standard for Public Code assessment was made at 2023-11. Currently Wekan meets 8 out of 16 criteria out of the box. Some others could be met with small changes.

Code stats
----------

-   CII Best Practices
-   Code Climate
-   Open Hub
-   OSS Insight

Translate WeKan ® at Transifex
------------------------------

Translations to non-English languages are accepted only at Transifex using webbrowser. New English strings of new features can be added as PRs to master branch file wekan/imports/i18n/data/en.i18n.json .

WeKan ® feature requests and bugs
---------------------------------

Please add most of your questions as GitHub issue: WeKan ® Feature Requests and Bugs. It's better than at chat where details get lost when chat scrolls up.

Discussions
-----------

IRC

Docker: Latest tag has newest release
-------------------------------------

You can use latest tag to get newest release tag. See bottom of #3874

FAQ
---

**NOTE**:

-   Please read the FAQ first
-   Please don't feed the trolls and spammers that are mentioned in the FAQ :)

About WeKan ®
-------------

WeKan ® is an completely Open Source and Free software collaborative kanban board application with MIT license.

Whether you’re maintaining a personal todo list, planning your holidays with some friends, or working in a team on your next revolutionary idea, Kanban boards are an unbeatable tool to keep your things organized. They give you a visual overview of the current state of your project, and make you productive by allowing you to focus on the few items that matter the most.

Since WeKan ® is a free software, you don’t have to trust us with your data and can install Wekan on your own computer or server. In fact we encourage you to do that by providing one-click installation on various platforms.

-   WeKan ® is used in most countries of the world.
-   WeKan ® largest user has 30k users using WeKan ® in their company.
-   WeKan ® has been translated to about 105 languages.
-   Features: WeKan ® has real-time user interface.
-   Platforms: WeKan ® supports many platforms. WeKan ® is critical part of new platforms Wekan is currently being integrated to.

Requirements
------------

-   1 GB RAM minimum free for WeKan ®. Production server should have minimum total 4 GB RAM. For thousands of users, for example with Docker: 3 frontend servers, each having 2 CPU and 2 wekan-app containers. One backend wekan-db server with many CPUs.
-   Enough disk space and alerts about low disk space. If you run out disk space, MongoDB database gets corrupted.
-   SECURITY: Updating to newest WeKan ® version very often. Please check you do not have automatic updates of Sandstorm or Snap turned off. Old versions have security issues because of old versions Node.js etc. Only newest WeKan ® is supported. WeKan ® on Sandstorm is not usually affected by any Standalone WeKan ® (Snap/Docker/Source) security issues.
-   Reporting all new bugs immediately. New features and fixes are added to WeKan ® many times a day.
-   Backups of WeKan ® database once a day miminum. Bugs, updates, users deleting list or card, harddrive full, harddrive crash etc can eat your data. There is no undo yet. Some bug can cause WeKan ® board to not load at all, requiring manual fixing of database content.

Roadmap and Demo
----------------

Roadmap - Public read-only board at WeKan ® demo.

Developer Documentation

-   There is many companies and individuals contributing code to WeKan ®, to add features and bugfixes many times a day.
-   Please add Add new Feature Requests and Bug Reports immediately.
-   Commercial Support.

We also welcome sponsors for features and bugfixes. By working directly with WeKan ® you get the benefit of active maintenance and new features added by growing WeKan ® developer community.

Getting Started with Development
--------------------------------

The default branch uses Meteor 2 with Node.js 14.

To contribute, create a fork and run `./rebuild-wekan.sh` (or `./rebuild-wekan.bat` on Windows) as detailed here. Once you're ready, please test your code and submit a pull request (PR).

Please refer to the developer documentation for more information.

Screenshot
----------

More screenshots at Features page

License
-------

WeKan ® is released under the very permissive MIT license, and made with Meteor.
