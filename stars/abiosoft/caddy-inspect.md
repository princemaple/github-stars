---
project: caddy-inspect
stars: 28
description: HTTP request inspector for Caddy web server
url: https://github.com/abiosoft/caddy-inspect
---

caddy-inspect
=============

The Inspect plugin provides an easy way to inspect HTTP requests in Caddy.

The Caddyfile is already easy to write. The Inspect plugin takes it a step further by allowing you to place breakpoints in the Caddyfile and ascertain the behaviour of Caddy.

Features
--------

-   Insert a breakpoint anywhere in the Caddyfile with the `inspect` keyword.
-   Inspecting HTTP and Caddy contexts
-   Intercepting and terminating HTTP requests and responses
-   Works in the browser, zero setup required.

Installation
------------

```
xcaddy build --with github.com/abiosoft/caddy-inspect
```

Getting Started
---------------

### Specify breakpoints in the Caddyfile

Place the `inspect` keyword anywhere an HTTP directive is supported in the Caddyfile. The keyword can be specified multiple times.

:8080

route /api {
    rewrite /api/\* /api/v1{uri}
    inspect
    ...
}

### Start Caddy

Caddy can be started with the `--watch` flag to autoreload the Caddyfile on each modification.

caddy run --watch

### Access the Inspect console

Open http://localhost:2020 in the browser to access the console.

Note

Another port would be assigned if `2020` is not available. The URL can be confirmed in the Caddy logs.

### Enjoy

Any HTTP request(s) made to a route containing the `inspect` keyword would pause the request and activate the console.

Caveats
-------

Caution

This plugin is intended for development purposes only, sensitive information may be exposed if used in a production environment.

-   The plugin is tailored towards Caddyfile config. However, JSON config can be used with limited experience.
-   Due to the in-built order of directives in Caddy, `inspect` is more predictable in a `route` block. Otherwise, it is ordered after the `encode` directive.
-   The information displayed are read-only and cannot be modified.
-   HTTP request and response bodies cannot be inspected. It is a deliberate limitation until there is a strong argument in favour.
-   The plugin stemmed from a personal use-case. Feedbacks would be appreciated to accommodate more use-cases.

Attribution
-----------

The Caddy logo is a trademark of Caddy Web Server.

License
-------

MIT

Sponsoring
----------

You can support the author by donating on Github Sponsors or Buy me a coffee.
