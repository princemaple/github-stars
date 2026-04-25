---
project: armor
stars: 1663
description: Uncomplicated, modern HTTP server
url: https://github.com/labstack/armor
---

What can it do today?
---------------------

-   Serve HTTP/2
-   Automatically install TLS certificates from https://letsencrypt.org
-   Proxy HTTP and WebSocket requests
-   Define virtual hosts with path level routing
-   Graceful shutdown
-   Limit request body
-   Serve static files
-   Log requests
-   Gzip response
-   Cross-origin Resource Sharing (CORS)
-   Security
    -   XSSProtection
    -   ContentTypeNosniff
    -   ContentSecurityPolicy
    -   HTTP Strict Transport Security (HSTS)
-   Add / Remove trailing slash from the URL with option to redirect
-   Redirect requests
-   http to https
-   http to https www
-   http to https non www
-   non www to www
-   www to non www
-   URL path rewrite

Most of the functionality is implemented via `Plugin` interface which makes writing a custom plugin super easy.

Get Started
-----------

What's on the roadmap?
----------------------

-   Website
-   Code coverage
-   Test cases
