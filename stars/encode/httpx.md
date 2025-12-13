---
project: httpx
stars: 14836
description: A next generation HTTP client for Python. 🦋
url: https://github.com/encode/httpx
---

**HTTPX** _\- A next-generation HTTP client for Python._

HTTPX is a fully featured HTTP client library for Python 3. It includes **an integrated command line client**, has support for both **HTTP/1.1 and HTTP/2**, and provides both **sync and async APIs**.

* * *

Install HTTPX using pip:

$ pip install httpx

Now, let's get started:

\>>> import httpx
>>> r \= httpx.get('https://www.example.org/')
>>> r
<Response \[200 OK\]>
>>> r.status\_code
200
>>> r.headers\['content-type'\]
'text/html; charset=UTF-8'
>>> r.text
'<!doctype html>\\n<html>\\n<head>\\n<title>Example Domain</title>...'

Or, using the command-line client.

$ pip install 'httpx\[cli\]'  # The command line client is an optional dependency.

Which now allows us to use HTTPX directly from the command-line...

Sending a request...

Features
--------

HTTPX builds on the well-established usability of `requests`, and gives you:

-   A broadly requests-compatible API.
-   An integrated command-line client.
-   HTTP/1.1 and HTTP/2 support.
-   Standard synchronous interface, but with async support if you need it.
-   Ability to make requests directly to WSGI applications or ASGI applications.
-   Strict timeouts everywhere.
-   Fully type annotated.
-   100% test coverage.

Plus all the standard features of `requests`...

-   International Domains and URLs
-   Keep-Alive & Connection Pooling
-   Sessions with Cookie Persistence
-   Browser-style SSL Verification
-   Basic/Digest Authentication
-   Elegant Key/Value Cookies
-   Automatic Decompression
-   Automatic Content Decoding
-   Unicode Response Bodies
-   Multipart File Uploads
-   HTTP(S) Proxy Support
-   Connection Timeouts
-   Streaming Downloads
-   .netrc Support
-   Chunked Requests

Installation
------------

Install with pip:

$ pip install httpx

Or, to include the optional HTTP/2 support, use:

$ pip install httpx\[http2\]

HTTPX requires Python 3.9+.

Documentation
-------------

Project documentation is available at https://www.python-httpx.org/.

For a run-through of all the basics, head over to the QuickStart.

For more advanced topics, see the Advanced Usage section, the async support section, or the HTTP/2 section.

The Developer Interface provides a comprehensive API reference.

To find out about tools that integrate with HTTPX, see Third Party Packages.

Contribute
----------

If you want to contribute with HTTPX check out the Contributing Guide to learn how to start.

Dependencies
------------

The HTTPX project relies on these excellent libraries:

-   `httpcore` - The underlying transport implementation for `httpx`.
    -   `h11` - HTTP/1.1 support.
-   `certifi` - SSL certificates.
-   `idna` - Internationalized domain name support.
-   `sniffio` - Async library autodetection.

As well as these optional installs:

-   `h2` - HTTP/2 support. _(Optional, with `httpx[http2]`)_
-   `socksio` - SOCKS proxy support. _(Optional, with `httpx[socks]`)_
-   `rich` - Rich terminal support. _(Optional, with `httpx[cli]`)_
-   `click` - Command line client support. _(Optional, with `httpx[cli]`)_
-   `brotli` or `brotlicffi` - Decoding for "brotli" compressed responses. _(Optional, with `httpx[brotli]`)_
-   `zstandard` - Decoding for "zstd" compressed responses. _(Optional, with `httpx[zstd]`)_

A huge amount of credit is due to `requests` for the API layout that much of this work follows, as well as to `urllib3` for plenty of design inspiration around the lower-level networking details.

* * *

_HTTPX is BSD licensed code.  
Designed & crafted with care._  
— 🦋 —
