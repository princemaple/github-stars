---
project: black
stars: 41362
description: The uncompromising Python code formatter
url: https://github.com/psf/black
---

The Uncompromising Code Formatter
---------------------------------

> “Any color you like.”

_Black_ is the uncompromising Python code formatter. By using it, you agree to cede control over minutiae of hand-formatting. In return, _Black_ gives you speed, determinism, and freedom from `pycodestyle` nagging about formatting. You will save time and mental energy for more important matters.

Blackened code looks the same regardless of the project you're reading. Formatting becomes transparent after a while and you can focus on the content instead.

_Black_ makes code review faster by producing the smallest diffs possible.

Try it out now using the Black Playground. Watch the PyCon 2019 talk to learn more.

* * *

**Read the documentation on ReadTheDocs!**

* * *

Installation and usage
----------------------

### Installation

_Black_ can be installed by running `pip install black`. It requires Python 3.10+ to run. If you want to format Jupyter Notebooks, install with `pip install "black[jupyter]"`.

### Usage

To get started right away with sensible defaults:

black {source\_file\_or\_directory}

You can run _Black_ as a package if running it as a script doesn't work:

python -m black {source\_file\_or\_directory}

Further information can be found in our docs:

-   Usage and Configuration

_Black_ is already successfully used by many projects, small and big. _Black_ has a comprehensive test suite, with efficient parallel tests, and our own auto formatting and parallel Continuous Integration runner. Now that we have become stable, you should not expect large formatting changes in the future. Stylistic changes will mostly be responses to bug reports and support for new Python syntax. For more information please refer to The Black Code Style.

Also, as a safety measure which slows down processing, _Black_ will check that the reformatted code still produces a valid AST that is effectively equivalent to the original (see the Pragmatism section for details). If you're feeling confident, use `--fast`.

The _Black_ code style
----------------------

_Black_ is a PEP 8 compliant opinionated formatter. _Black_ reformats entire files in place. Style configuration options are deliberately limited and rarely added. It doesn't take previous formatting into account (see Pragmatism for exceptions).

Our documentation covers the current _Black_ code style, but planned changes to it are also documented. They're both worth taking a look at:

-   The _Black_ Code Style: Current style
-   The _Black_ Code Style: Future style

Changes to the _Black_ code style are bound by the Stability Policy:

-   The _Black_ Code Style: Stability Policy

Please refer to this document before submitting an issue. What seems like a bug might be intended behaviour.

### Pragmatism

Early versions of _Black_ used to be absolutist in some respects. They took after its initial author. This was fine at the time as it made the implementation simpler and there were not many users anyway. Not many edge cases were reported. As a mature tool, _Black_ does make some exceptions to rules it otherwise holds.

-   The _Black_ code style: Pragmatism

Please refer to this document before submitting an issue just like with the document above. What seems like a bug might be intended behaviour.

Configuration
-------------

_Black_ is able to read project-specific default values for its command line options from a `pyproject.toml` file. This is especially useful for specifying custom `--include` and `--exclude`/`--force-exclude`/`--extend-exclude` patterns for your project.

You can find more details in our documentation:

-   The basics: Configuration via a file

And if you're looking for more general configuration documentation:

-   Usage and Configuration

**Pro-tip**: If you're asking yourself "Do I need to configure anything?" the answer is "No". _Black_ is all about sensible defaults. Applying those defaults will have your code in compliance with many other _Black_ formatted projects.

Used by
-------

The following notable open-source projects trust _Black_ with enforcing a consistent code style: pytest, tox, Pyramid, Django, Django Channels, Hypothesis, attrs, SQLAlchemy, Poetry, PyPA applications (Warehouse, Bandersnatch, Pipenv, virtualenv), pandas, Pillow, Twisted, LocalStack, every Datadog Agent Integration, Home Assistant, Zulip, Kedro, OpenOA, FLORIS, ORBIT, WOMBAT, and many more.

The following organizations use _Black_: Dropbox, KeepTruckin, Lyft, Mozilla, Quora, Duolingo, QuantumBlack, Tesla, Archer Aviation.

Are we missing anyone? Let us know.

Testimonials
------------

**Mike Bayer**, author of `SQLAlchemy`:

> I can't think of any single tool in my entire programming career that has given me a bigger productivity increase by its introduction. I can now do refactorings in about 1% of the keystrokes that it would have taken me previously when we had no way for code to format itself.

**Dusty Phillips**, writer:

> _Black_ is opinionated so you don't have to be.

**Hynek Schlawack**, creator of `attrs`, core developer of Twisted and CPython:

> An auto-formatter that doesn't suck is all I want for Xmas!

**Carl Meyer**, Django core developer:

> At least the name is good.

**Kenneth Reitz**, creator of `requests` and `pipenv`:

> This vastly improves the formatting of our code. Thanks a ton!

Show your style
---------------

Use the badge in your project's README.md:

\[!\[Code style: black\](https://img.shields.io/badge/code%20style-black-000000.svg)\](https://github.com/psf/black)

Using the badge in README.rst:

.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
    :target: https://github.com/psf/black

Looks like this:

License
-------

MIT

Contributing
------------

Welcome! Happy to see you willing to make the project better. You can get started by reading this:

-   Contributing: The basics

You can also take a look at the rest of the contributing docs or talk with the developers:

-   Contributing documentation
-   Chat on Discord

Change log
----------

The log has become rather long. It moved to its own file.

See CHANGES.

Authors
-------

The author list is quite long nowadays, so it lives in its own file.

See AUTHORS.md

Code of Conduct
---------------

Everyone participating in the _Black_ project, and in particular in the issue tracker, pull requests, and social media activity, is expected to treat other people with respect and more generally to follow the guidelines articulated in the Python Community Code of Conduct.

At the same time, humor is encouraged. In fact, basic familiarity with Monty Python's Flying Circus is expected. We are not savages.

And if you _really_ need to slap somebody, do it with a fish while dancing.
