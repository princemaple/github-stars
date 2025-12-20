---
project: electric
stars: 9662
description: Real-time sync for Postgres.
url: https://github.com/electric-sql/electric
---

Electric
========

Real-time sync for Postgres.

**Table of Contents:**

-   Quick links
-   What is Electric?
-   Getting Started
-   HTTP API Docs
-   Developing Electric
    -   Mac setup
-   Contributing
-   Support

Quick links
-----------

-   Quickstart
-   Website
-   About
-   Docs
-   Demos (also see the `./examples` folder)

What is Electric?
-----------------

Sync is the magic ingredient behind fast, modern software. From apps like Figma and Linear to AI agents running on live local data.

Electric is a Postgres sync engine. It solves the hard problems of sync for you, including partial replication, fan-out, and data delivery. So you can build awesome software, without rolling your own sync.

Specifically, Electric is a read-path sync engine for Postgres. It syncs data out of Postgres into ... anything you like. The core sync protocol is based on a low-level HTTP API. This integrates with CDNs for highly-scalable data delivery.

Partial replication is managed using Shapes. Sync can be consumed directly or via client libraries and framework integrations.

Getting Started
---------------

See the Quickstart guide to get up and running. In short, you need to:

1.  have a Postgres database with logical replication enabled; and then to
2.  run Electric in front of it, connected via `DATABASE_URL`

For example, using Docker Compose from the root of this repo:

docker compose -f .support/docker-compose.yml up

You can then use the HTTP API to sync data from your Postgres. For example, to start syncing the whole `foo` table:

curl -i 'http://localhost:3000/v1/shape?table=foo&offset=-1'

Or use one of the clients or integrations, such as the `useShape` React hook:

import { useShape } from '@electric-sql/react'

function Component() {
  const { data } \= useShape({
    url: \`http://localhost:3000/v1/shape\`,
    params: {
      table: \`foo\`,
      where: \`title LIKE 'foo%'\`,
    },
  })

  return JSON.stringify(data)
}

Again, see the Quickstart and the Docs for more details.

HTTP API Docs
-------------

The HTTP API is defined in an OpenAPI spec in website/electric-api.yaml.

Developing Electric
-------------------

We use asdf to install Elixir, Erlang, and Node.js. Versions are defined in .tool-versions.

### Mac setup

brew install asdf
asdf plugin add nodejs
asdf plugin add pnpm
asdf plugin add elixir
asdf plugin add erlang
asdf install

You'll probably need to fiddle with your bash/zsh/etc rc file to load the right tool into your environment.

### Running Tests

Electric has comprehensive test suites for both Elixir and TypeScript components.

#### Prerequisites

Install dependencies (if not already done):

asdf install
pnpm install

Then start the test Postgres database:

cd packages/sync-service
mix start\_dev

This starts a Docker Compose setup with Postgres configured for logical replication on port 54321.

To stop the database:

mix stop\_dev

#### Elixir Tests

**Sync Service:**

cd packages/sync-service
mix test

For coverage reports:

mix coveralls.html

**Elixir Client:**

cd packages/elixir-client
mix test

#### TypeScript Tests

TypeScript tests require both the database and a running sync service.

In a separate terminal, start the sync service:

cd packages/sync-service
iex -S mix

Then run the tests:

**Individual Package:**

cd packages/typescript-client  # or any other TS package
pnpm test

**All TypeScript Packages:**

From the root directory:

pnpm -r test

For coverage:

pnpm coverage

Contributing
------------

See the:

-   Guide to Contributing
-   Contributor License Agreement
-   Community Guidelines

Support
-------

We have an open community Discord. Come and say hello and let us know if you have any questions or need any help getting things running.

It's also super helpful if you leave the project a star here at the top of the page☝️
