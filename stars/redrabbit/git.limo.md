---
project: git.limo
stars: 508
description: A Git source code management tool powered by Elixir with easy installation & high extensibility.
url: https://github.com/redrabbit/git.limo
---

git.limo
========

A Git source code management tool written in Elixir.

-   Simple yet intuitive web interface.
-   Git HTTP and SSH support.
-   Fully integrated GraphQL API.
-   Customizable Git storage backend.
-   Distributed setup (cluster).
-   Issue tracker.
-   Code reviews.
-   Continuous integration.

Install dependencies
--------------------

First, ensure you have libgit2 installed on your system:

#### Mac OS

brew install libgit2

#### Ubuntu

sudo apt-get install libgit2-dev

You will also need Node.js to compile Web assets and PostgreSQL to store your application data.

Clone and compile
-----------------

Clone the latest version of the project:

git clone https://github.com/almightycouch/gitgud.git

Download Hex dependencies and compile everything:

mix deps.get
mix compile

Install Javascript dependencies
-------------------------------

Install all NPM packages required by Webpack to generate Web assets:

npm install --prefix apps/gitgud\_web/assets

Generate SSH public keys
------------------------

In order to provide SSH as a Git transport protocol, you must generate a valid SSH public key for the server:

ssh-keygen -m PEM -t rsa -f apps/gitgud/priv/ssh-keys/ssh\_host\_rsa\_key

Setup database
--------------

The last step before running the server is to create and initialise the SQL database:

mix ecto.setup

Run server
----------

Finally, start both HTTP (port 4000) and SSH (port 8989) endpoints:

mix phx.server
