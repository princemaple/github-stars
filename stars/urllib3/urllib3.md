---
project: urllib3
stars: 3998
description: urllib3 is a user-friendly HTTP client library for Python
url: https://github.com/urllib3/urllib3
---

==

  

urllib3 is a powerful, _user-friendly_ HTTP client for Python. urllib3 brings many critical features that are missing from the Python standard libraries:

-   Thread safety.
-   Connection pooling.
-   Client-side SSL/TLS verification.
-   File uploads with multipart encoding.
-   Helpers for retrying requests and dealing with HTTP redirects.
-   Support for gzip, deflate, brotli, and zstd encoding.
-   Proxy support for HTTP and SOCKS.
-   100% test coverage.

... and many more features, but most importantly: Our maintainers have a 15+ year track record of maintaining urllib3 with the highest code standards and attention to security and safety.

Much of the Python ecosystem already uses urllib3 and you should too.

Installing
----------

urllib3 can be installed with pip:

$ python -m pip install urllib3

Alternatively, you can grab the latest source code from GitHub:

$ git clone https://github.com/urllib3/urllib3.git
$ cd urllib3
$ pip install .

Getting Started
---------------

urllib3 is easy to use:

\>\>> import urllib3
\>\>> resp \= urllib3.request("GET", "http://httpbin.org/robots.txt")
\>\>> resp.status
200
\>\>> resp.data
b"User-agent: \*\\nDisallow: /deny\\n"

urllib3 has usage and reference documentation at urllib3.readthedocs.io.

Community
---------

urllib3 has a community Discord channel for asking questions and collaborating with other contributors. Drop by and say hello 👋

Contributing
------------

urllib3 happily accepts contributions. Please see our contributing documentation for some tips on getting started.

Security Disclosures
--------------------

To report a security vulnerability, please use the Tidelift security contact. Tidelift will coordinate the fix and disclosure with maintainers.

Maintainers
-----------

Meet our maintainers since 2008:

-   Current Lead: @illia-v (Illia Volochii)
-   @sethmlarson (Seth M. Larson)
-   @pquentin (Quentin Pradet)
-   @theacodes (Thea Flowers)
-   @haikuginger (Jess Shapiro)
-   @lukasa (Cory Benfield)
-   @sigmavirus24 (Ian Stapleton Cordasco)
-   @shazow (Andrey Petrov)

👋

Sponsorship
-----------

If your company benefits from this library, please consider sponsoring its development.

For Enterprise
--------------

Professional support for urllib3 is available as part of the Tidelift Subscription. Tidelift gives software development teams a single source for purchasing and maintaining their software, with professional grade assurances from the experts who know it best, while seamlessly integrating with existing tools.
