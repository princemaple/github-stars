---
project: browserhacks
stars: 1264
description: An extensive list of CSS/JS browserhacks from all over the interwebs.
---

Browserhacks.com
================

What’s this?
------------

Browserhacks is an extensive list of browser specific CSS and JavaScript hacks from all over the interwebs.

Please keep in mind using a hack is not always the perfect solution. It can be useful to fix some weird browser specific bug, but in most cases you should fix your CSS/JS.

How to?
-------

1.  Pick the hack you want
2.  Copy it into your stylesheet
3.  Add the styles you want between the braces
4.  Enjoy the new styles for the browser you targeted!

Created by
----------

-   Tim Pietrusky
-   Kitty Giraudel
-   Fabrice Weinberg

Updates by
----------

-   Jeff Clayton

Thanks to
---------

-   Joshua Hibbert for the design
-   Jeff Clayton for his help with testing hacks and creating new ones, now also an administrator
-   Sara Soueidan, Ana Tudor, Mads Cordes for their kind help
-   Paul Irish for his great post on CSS hacks
-   Keith Clarke for his @media block CSS hacks
-   Nicolas Gallagher for his IE CSS hacks
-   And various nice contributors :)

Deployment
----------

The site is a Jekyll setup hosted on GitHub Pages. Simply update the `gh-pages` branch to update the site (direct edit on GitHub, manual push or pull-request merge).

Adding new hacks
----------------

Adding a new hack is as simple as adding a new entry in `_data/hacks.json`. Like this:

{
  "type": "selector",
  "browsers": {
    "ch": "\*",
    "op": "14+"
  },
  "label": "A label for your hack if necessary.",
  "language": "css",
  "code": \[
    ".selector:not(\*:root) {}"
  \],
  "test": \[
    ".selector:not(\*:root) { background: lightgreen; }"
  \]
}

The **type** key defines which type of hack it is; valid types are listed in `_data/hackTypes.json`.

The **browsers** key is an object mapping a browser’s shortname to a version expression; valid browsers are listed in `_data/browsers.json`. Versions can be:

-   strict version (e.g. `42`)
-   strict versiond (e.g. `42|43`)
-   version and up (e.g. `42+`)
-   version and below (e.g. `42-`)
-   any version (e.g. `*`)

The **label** key can be left empty, or describe the hack if it is necessary.

The **language** key defines how to display the hack, and how to create the dynamic test for it. Possible languages are `css`, `javascript` and `markup`.

The **code** key is an array of expressions for the hack. Certain hacks can be written in several forms, hence the need for an array.

The **test** key is an array of expressions for the test. It should be a direct copy of the `code` array, except the braces should be filled with a `background: lightgreen;` in case of a selector, or `.selector { background: lightgreen; }` in case of a media expression. Take example on other existing hacks.

Once you’ve done that, simply run `npm run build` to complete the hack with a unique ID, a human-readable version, a check for whether or not it’s a legacy hack, and create dynamic tests.