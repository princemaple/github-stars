---
project: uBlock-Origin-dev-filter
stars: 2320
description: Filters to block and remove copycat-websites from DuckDuckGo, Google and other search engines. Specific to dev websites like StackOverflow or GitHub.
url: https://github.com/quenhus/uBlock-Origin-dev-filter
---

uBlock-Origin-dev-filter
========================

Filters to block and remove copycat-websites from DuckDuckGo, Google and other search engines. Used to be specific to dev websites like StackOverflow or GitHub, but it currently supports others like Wikipedia.

To use this tools, you should have uBlock Origin installed.

Import into uBlock Origin
-------------------------

Select the filters flavors you want, depending on your needs and search engine:

💻 **`dev`** supports StackOverflow + GitHub + NPM (the original dev-oriented filter)  
🌐 **`global`** supports StackOverflow + GitHub + NPM + Wikipedia + SEO Spam

dev

global

Google

DuckDuckGo

DuckDuckGo Lite

Google+DDG

Startpage

Brave

Ecosia

All Search Engines

  
**More granular versions** (StackOverflow-only, GitHub-only, ...)

StackOverflow

GitHub

NPM

Wikipedia

SEO Spam

Google

add in uBO

add in uBO

add in uBO

add in uBO

add in uBO

DuckDuckGo

add in uBO

add in uBO

add in uBO

add in uBO

add in uBO

DuckDuckGo Lite

add in uBO

add in uBO

add in uBO

add in uBO

add in uBO

Google+DDG

add in uBO

add in uBO

add in uBO

add in uBO

add in uBO

Startpage

add in uBO

add in uBO

add in uBO

add in uBO

add in uBO

Brave

add in uBO

add in uBO

add in uBO

add in uBO

add in uBO

Ecosia

add in uBO

add in uBO

add in uBO

add in uBO

add in uBO

All Search Engines

add in uBO

add in uBO

add in uBO

add in uBO

add in uBO

  
How to import uBlock filters manually

### Manually import filters

1.  Open uBlock Origin settings
2.  Under the "Filter lists" tab, scroll to the bottom where it says “Custom” and click the “Import” checkbox to reveal the custom URL textbox
3.  Append the URL `https://raw.githubusercontent.com/quenhus/uBlock-Origin-dev-filter/main/dist/google_duckduckgo/all.txt` in the textbox
4.  Press `Apply Changes` in the upper left

Note: In `dist/`, you can find filters for other search engines (Google, DuckDuckGo, Startpage or Brave). You can use and combine these filters by using the raw URL of `dist/` files.

Other filter formats (uBlacklist, hosts filter, ...)
----------------------------------------------------

This project also provide filter in other formats:

-   uBlacklist (more efficient than uBO in this case)
-   macOS userscript
-   Domains filter (can be used with a Pi-hole/Firewall)
-   DNS hosts filter (can be used in `/etc/hosts`)

dev

global

StackOverflow

GitHub

NPM

Wikipedia

SEO Spam

uBlacklist

Link

Link

Link

Link

Link

Link

Link

macOS userscript

Link

Link

Link

Link

Link

Link

Link

Domains filter

Link

Link

Link

Link

Link

Link

Link

DNS hosts filter

Link

Link

Link

Link

Link

Link

Link

Adding URL's
------------

Please create a pull-request or start an issue with evidence against the "copycats".

Security
--------

For simplicity and auto-updates, uBlock Origin filters rely on the last commit of the `main` branch, as every other uBO filters. For now, it seems this method does not raise security issues. However, you can import uBlock Origin filters with a reference to a given commit, not the `main` branch. Filters won't auto-update but they will be auditable by your own eyes.

Scope of this filter
--------------------

To me, a copycat is a website that:

-   **mirrors most of GitHub/SO content**, automatically and without useful additional work on the content,
-   **prevents** the user to **interact** easily with the resource (upvote, comment or reply),
-   might **use SEO techniques** to catch users who would have otherwise reached the original resource,
-   overall, **offers no benefits** for users over the original resource.

To be more precise:

-   I do not consider automatic translation as a benefit;
-   I do consider a mirror with clear attribution to be a copycat;
-   I do not consider a mirror created for privacy concern to be a copycat, except if it uses aggressive SEO techniques;
-   This uBlock filter is my own filter, for my usage and **can't obviously satisfy everyone**.

Sources
-------

-   uBlacklist Stack Overflow Translation
-   uBlacklist GitHub Translation
-   uBlock Origin - Shitty Copy-Paste websites filter
-   Quenhus Stackoverflow/Github copy-cats

Do your own
-----------

1.  List URL that you want to block in a `.txt` in the `data/` folder
2.  Use `src/generate.py`, which generate files in `dist/` you can use as uBlock filters

Note: You can use letsblock.it to create your own filter.
