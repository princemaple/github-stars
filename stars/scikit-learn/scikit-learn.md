---
project: scikit-learn
stars: 60378
description: scikit-learn: machine learning in Python
url: https://github.com/scikit-learn/scikit-learn
---

**scikit-learn** is a Python module for machine learning built on top of SciPy and is distributed under the 3-Clause BSD license.

The project was started in 2007 by David Cournapeau as a Google Summer of Code project, and since then many volunteers have contributed. See the About us page for a list of core contributors.

It is currently maintained by a team of volunteers.

Website: https://scikit-learn.org

Installation
------------

### Dependencies

scikit-learn requires:

-   Python (>= 3.9)
-   NumPy (>= 1.19.5)
-   SciPy (>= 1.6.0)
-   joblib (>= 1.2.0)
-   threadpoolctl (>= 3.1.0)

* * *

**Scikit-learn 0.20 was the last version to support Python 2.7 and Python 3.4.** scikit-learn 1.0 and later require Python 3.7 or newer. scikit-learn 1.1 and later require Python 3.8 or newer.

Scikit-learn plotting capabilities (i.e., functions start with `plot_` and classes end with `Display`) require Matplotlib (>= 3.3.4). For running the examples Matplotlib >= 3.3.4 is required. A few examples require scikit-image >= 0.17.2, a few examples require pandas >= 1.1.5, some examples require seaborn >= 0.9.0 and plotly >= 5.14.0.

### User installation

If you already have a working installation of NumPy and SciPy, the easiest way to install scikit-learn is using `pip`:

pip install -U scikit-learn

or `conda`:

conda install -c conda-forge scikit-learn

The documentation includes more detailed installation instructions.

Changelog
---------

See the changelog for a history of notable changes to scikit-learn.

Development
-----------

We welcome new contributors of all experience levels. The scikit-learn community goals are to be helpful, welcoming, and effective. The Development Guide has detailed information about contributing code, documentation, tests, and more. We've included some basic information in this README.

### Important links

-   Official source code repo: https://github.com/scikit-learn/scikit-learn
-   Download releases: https://pypi.org/project/scikit-learn/
-   Issue tracker: https://github.com/scikit-learn/scikit-learn/issues

### Source code

You can check the latest sources with the command:

git clone https://github.com/scikit-learn/scikit-learn.git

### Contributing

To learn more about making a contribution to scikit-learn, please see our Contributing guide.

### Testing

After installation, you can launch the test suite from outside the source directory (you will need to have `pytest` >= 7.1.2 installed):

pytest sklearn

See the web page https://scikit-learn.org/dev/developers/contributing.html#testing-and-improving-test-coverage for more information.

> Random number generation can be controlled during testing by setting the `SKLEARN_SEED` environment variable.

### Submitting a Pull Request

Before opening a Pull Request, have a look at the full Contributing page to make sure your code complies with our guidelines: https://scikit-learn.org/stable/developers/index.html

Project History
---------------

The project was started in 2007 by David Cournapeau as a Google Summer of Code project, and since then many volunteers have contributed. See the About us page for a list of core contributors.

The project is currently maintained by a team of volunteers.

**Note**: scikit-learn was previously referred to as scikits.learn.

Help and Support
----------------

### Documentation

-   HTML documentation (stable release): https://scikit-learn.org
-   HTML documentation (development version): https://scikit-learn.org/dev/
-   FAQ: https://scikit-learn.org/stable/faq.html

### Communication

-   Mailing list: https://mail.python.org/mailman/listinfo/scikit-learn
-   Logos & Branding: https://github.com/scikit-learn/scikit-learn/tree/main/doc/logos
-   Blog: https://blog.scikit-learn.org
-   Calendar: https://blog.scikit-learn.org/calendar/
-   Twitter: https://twitter.com/scikit\_learn
-   Stack Overflow: https://stackoverflow.com/questions/tagged/scikit-learn
-   GitHub Discussions: https://github.com/scikit-learn/scikit-learn/discussions
-   Website: https://scikit-learn.org
-   LinkedIn: https://www.linkedin.com/company/scikit-learn
-   Bluesky: https://bsky.app/profile/scikit-learn.org
-   YouTube: https://www.youtube.com/channel/UCJosFjYm0ZYVUARxuOZqnnw/playlists
-   Facebook: https://www.facebook.com/scikitlearnofficial/
-   Instagram: https://www.instagram.com/scikitlearnofficial/
-   TikTok: https://www.tiktok.com/@scikit.learn
-   Mastodon: https://mastodon.social/@sklearn@fosstodon.org
-   Discord: https://discord.gg/h9qyrK8Jc8

### Citation

If you use scikit-learn in a scientific publication, we would appreciate citations: https://scikit-learn.org/stable/about.html#citing-scikit-learn