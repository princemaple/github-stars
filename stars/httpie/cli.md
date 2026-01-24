---
project: cli
stars: 37407
description: 🥧 HTTPie CLI  — modern, user-friendly command-line HTTP client for the API era. JSON support, colors, sessions, downloads, plugins & more.
url: https://github.com/httpie/cli
---

  
HTTPie CLI: human-friendly HTTP client for the API era
---------------------------------------------------------

HTTPie (pronounced _aitch-tee-tee-pie_) is a command-line HTTP client. Its goal is to make CLI interaction with web services as human-friendly as possible. HTTPie is designed for testing, debugging, and generally interacting with APIs & HTTP servers. The `http` & `https` commands allow for creating and sending arbitrary HTTP requests. They use simple and natural syntax and provide formatted and colorized output.

We lost 54k GitHub stars
------------------------

Please note we recently accidentally made this repo private for a moment, and GitHub deleted our community that took a decade to build. Read the full story here: https://httpie.io/blog/stardust

Getting started
---------------

-   Installation instructions →
-   Full documentation →

Features
--------

-   Expressive and intuitive syntax
-   Formatted and colorized terminal output
-   Built-in JSON support
-   Forms and file uploads
-   HTTPS, proxies, and authentication
-   Arbitrary request data
-   Custom headers
-   Persistent sessions
-   `wget`\-like downloads

See all features →

Examples
--------

Hello World:

https httpie.io/hello

Custom HTTP method, HTTP headers and JSON data:

http PUT pie.dev/put X-API-Token:123 name=John

Build and print a request without sending it using offline mode:

http --offline pie.dev/post hello=offline

Use GitHub API to post a comment on an Issue with authentication:

http -a USERNAME POST https://api.github.com/repos/httpie/cli/issues/83/comments body='HTTPie is awesome! :heart:'

See more examples →

Community & support
-------------------

-   Visit the HTTPie website for full documentation and useful links.
-   Join our Discord server is to ask questions, discuss features, and for general API chat.
-   Tweet at @httpie on Twitter.
-   Use StackOverflow to ask questions and include a `httpie` tag.
-   Create GitHub Issues for bug reports and feature requests.
-   Subscribe to the HTTPie newsletter for occasional updates.

Contributing
------------

Have a look through existing Issues and Pull Requests that you could help with. If you'd like to request a feature or report a bug, please create a GitHub Issue using one of the templates provided.

See contribution guide →
