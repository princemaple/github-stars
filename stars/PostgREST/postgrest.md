---
project: postgrest
stars: 26284
description: REST API for any Postgres database
url: https://github.com/PostgREST/postgrest
---

PostgREST serves a fully RESTful API from any existing PostgreSQL database. It provides a cleaner, more standards-compliant, faster API than you are likely to write from scratch.

Sponsors
--------

Big thanks to our sponsors! You can join them by supporting PostgREST on Patreon.

Usage
-----

1.  See the docs for how to install PostgREST on your platform. You can also use Docker.
    
2.  Invoke for help:
    
    postgrest --help
    

Documentation
-------------

Latest documentation is at postgrest.org. You can contribute to the docs in PostgREST/postgrest/docs.

Performance
-----------

TLDR; subsecond response times for up to 2000 requests/sec on Heroku free tier. If you're used to servers written in interpreted languages, prepare to be pleasantly surprised by PostgREST performance.

Three factors contribute to the speed. First the server is written in Haskell using the Warp HTTP server (aka a compiled language with lightweight threads). Next it delegates as much calculation as possible to the database including

-   Serializing JSON responses directly in SQL
-   Data validation
-   Authorization
-   Combined row counting and retrieval
-   Data post in single command (`returning *`)

Finally it uses the database efficiently with the Hasql library by

-   Keeping a pool of db connections
-   Using the PostgreSQL binary protocol
-   Being stateless to allow horizontal scaling

Security
--------

PostgREST handles authentication (via JSON Web Tokens) and delegates authorization to the role information defined in the database. This ensures there is a single declarative source of truth for security. When dealing with the database the server assumes the identity of the currently authenticated user, and for the duration of the connection cannot do anything the user themselves couldn't. Other forms of authentication can be built on top of the JWT primitive. See the docs for more information.

Versioning
----------

A robust long-lived API needs the freedom to exist in multiple versions. PostgREST does versioning through database schemas. This allows you to expose tables and views without making the app brittle. Underlying tables can be superseded and hidden behind public facing views.

Self-documentation
------------------

PostgREST uses the OpenAPI standard to generate up-to-date documentation for APIs. You can use a tool like Swagger-UI to render interactive documentation for demo requests against the live API server.

This project uses HTTP to communicate other metadata as well. For instance the number of rows returned by an endpoint is reported by - and limited with - range headers. More about that.

Data Integrity
--------------

Rather than relying on an Object Relational Mapper and custom imperative coding, this system requires you to put declarative constraints directly into your database. Hence no application can corrupt your data (including your API server).

The PostgREST exposes HTTP interface with safeguards to prevent surprises, such as enforcing idempotent PUT requests.

See examples of PostgreSQL constraints and the API guide.

Supporting development
----------------------

You can help PostgREST ongoing maintenance and development by making a regular donation through Patreon https://www.patreon.com/postgrest

Every donation will be spent on making PostgREST better for the whole community.

Contributing
------------

Contributions are always welcome and appreciated. Please see the Contributing guidelines.

Thanks
------

The PostgREST organization is grateful to:

-   The project sponsors and backers who support PostgREST's development.
-   The project contributors who have improved PostgREST immensely with their code and good judgement. See more details in the changelog.

The cool logo came from Mikey Casalaina.
