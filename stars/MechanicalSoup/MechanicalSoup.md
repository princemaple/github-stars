---
project: MechanicalSoup
stars: 4836
description: A Python library for automating interaction with websites.
url: https://github.com/MechanicalSoup/MechanicalSoup
---

Home page
---------

https://mechanicalsoup.readthedocs.io/

Overview
--------

A Python library for automating interaction with websites. MechanicalSoup automatically stores and sends cookies, follows redirects, and can follow links and submit forms. It doesn't do JavaScript.

MechanicalSoup was created by M Hickford, who was a fond user of the Mechanize library. Unfortunately, Mechanize was incompatible with Python 3 until 2019 and its development stalled for several years. MechanicalSoup provides a similar API, built on Python giants Requests (for HTTP sessions) and BeautifulSoup (for document navigation). Since 2017 it is a project actively maintained by a small team including @hemberger and @moy.

Installation
------------

PyPy3 is also supported (and tested against).

Download and install the latest released version from PyPI:

pip install MechanicalSoup

Download and install the development version from GitHub:

pip install git+https://github.com/MechanicalSoup/MechanicalSoup

Installing from source (installs the version in the current working directory):

pip install .

(In all cases, add `--user` to the `install` command to install in the current user's home directory.)

Documentation
-------------

The full documentation is available on https://mechanicalsoup.readthedocs.io/. You may want to jump directly to the automatically generated API documentation.

Example
-------

From examples/expl\_qwant.py, code to get the results from a Qwant search:

"""Example usage of MechanicalSoup to get the results from the Qwant
search engine.
"""

import re
import mechanicalsoup
import html
import urllib.parse

\# Connect to Qwant
browser \= mechanicalsoup.StatefulBrowser(user\_agent\='MechanicalSoup')
browser.open("https://lite.qwant.com/")

\# Fill-in the search form
browser.select\_form('#search-form')
browser\["q"\] \= "MechanicalSoup"
browser.submit\_selected()

\# Display the results
for link in browser.page.select('.result a'):
    \# Qwant shows redirection links, not the actual URL, so extract
    \# the actual URL from the redirect link:
    href \= link.attrs\['href'\]
    m \= re.match(r"^/redirect/\[^/\]\*/(.\*)$", href)
    if m:
        href \= urllib.parse.unquote(m.group(1))
    print(link.text, '->', href)

More examples are available in examples/.

For an example with a more complex form (checkboxes, radio buttons and textareas), read tests/test\_browser.py and tests/test\_form.py.

Development
-----------

Instructions for building, testing and contributing to MechanicalSoup: see CONTRIBUTING.rst.

Common problems
---------------

Read the FAQ.
