---
project: umami
stars: 38763
description: Umami is a privacy-first analytics platform. Traffic, campaigns, behavior, conversions, and revenue in one place — no cookies, no surveillance, self-hosted or in the cloud.
url: https://github.com/umami-software/umami
---

Umami
=====

_Umami is a privacy-first analytics platform. Traffic, campaigns, behavior, conversions, and revenue in one place — no cookies, no surveillance, self-hosted or in the cloud._

* * *

🚀 Getting Started
------------------

A detailed getting started guide can be found at umami.is/docs.

* * *

🛠 Installing from Source
-------------------------

### Requirements

-   A server with Node.js version 18.18+.
-   A PostgreSQL database version v12.14+.

### Get the source code and install packages

git clone https://github.com/umami-software/umami.git
cd umami
pnpm install

### Configure Umami

Create an `.env` file with the following:

DATABASE\_URL=connection-url

Optional: set `API_URL` to change the base URL used by internal UI API calls. Relative paths are served under `BASE_PATH`; absolute URLs are proxied through the local `/api` route. For example, `API_URL=/internal-api` or `API_URL=https://api.example.com/api`.

Optional: set `TWO_FACTOR_ENCRYPTION_KEY` to a 64-character hex string to enable two-factor authentication. Generate one with `openssl rand -hex 32`. Two-factor authentication is unavailable and cannot be required until this key is set.

The connection URL format:

postgresql://username:mypassword@localhost:5432/mydb

### Build the Application

pnpm run build

The build step will create tables in your database if you are installing for the first time. It will also create a login user with username **admin** and password **umami**.

### Start the Application

pnpm run start

By default, this will launch the application on `http://localhost:3000`. You will need to either proxy requests from your web server or change the port to serve the application directly.

* * *

🐳 Installing with Docker
-------------------------

Umami provides Docker images as well as a Docker compose file for easy deployment.

Docker image:

docker pull docker.umami.is/umami-software/umami:latest

Docker compose (Runs Umami with a PostgreSQL database):

docker compose up -d

* * *

🔄 Getting Updates
------------------

To get the latest features, simply do a pull, install any new dependencies, and rebuild:

git pull
pnpm install
pnpm build

To update the Docker image, simply pull the new images and rebuild:

docker compose pull
docker compose up --force-recreate -d

* * *

🛟 Support
----------
