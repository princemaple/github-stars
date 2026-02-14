---
project: listmonk
stars: 19043
description: High performance, self-hosted, newsletter and mailing list manager with a modern dashboard. Single binary app.
url: https://github.com/knadh/listmonk
---

listmonk is a standalone, self-hosted, newsletter and mailing list manager. It is fast, feature-rich, and packed into a single binary. It uses a PostgreSQL database as its data store.

Visit listmonk.app for more info. Check out the **live demo**.

Installation
------------

### Docker

The latest image is available on DockerHub at `listmonk/listmonk:latest`. Download and use the sample docker-compose.yml.

# Download the compose file to the current directory.
curl -LO https://github.com/knadh/listmonk/raw/master/docker-compose.yml

# Run the services in the background.
docker compose up -d

Visit `http://localhost:9000`

See installation docs

* * *

### Binary

-   Download the latest release and extract the listmonk binary.
-   `./listmonk --new-config` to generate config.toml. Edit it.
-   `./listmonk --install` to setup the Postgres DB (or `--upgrade` to upgrade an existing DB. Upgrades are idempotent and running them multiple times have no side effects).
-   Run `./listmonk` and visit `http://localhost:9000`

See installation docs

* * *

Developers
----------

listmonk is free and open source software licensed under AGPLv3. If you are interested in contributing, refer to the developer setup. The backend is written in Go and the frontend is Vue with Buefy for UI.

License
-------

listmonk is licensed under the AGPL v3 license.
