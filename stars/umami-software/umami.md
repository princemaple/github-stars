---
project: umami
stars: 33525
description: Umami is a modern, privacy-focused analytics platform. A better, open-source alternative to Google Analytics, Mixpanel and Amplitude.
url: https://github.com/umami-software/umami
---

Umami
=====

_Umami is a simple, fast, privacy-focused alternative to Google Analytics._

* * *

🚀 Getting Started
------------------

A detailed getting started guide can be found at umami.is/docs.

* * *

🛠 Installing from Source
-------------------------

### Requirements

-   A server with Node.js version 18.18 or newer
-   A database. Umami supports PostgreSQL (minimum v12.14) databases.

### Get the Source Code and Install Packages

git clone https://github.com/umami-software/umami.git
cd umami
pnpm install

### Configure Umami

Create an `.env` file with the following:

DATABASE\_URL=connection-url

The connection URL format:

postgresql://username:mypassword@localhost:5432/mydb

### Build the Application

pnpm run build

_The build step will create tables in your database if you are installing for the first time. It will also create a login user with username **admin** and password **umami**._

### Start the Application

pnpm run start

_By default, this will launch the application on `http://localhost:3000`. You will need to either proxy requests from your web server or change the port to serve the application directly._

* * *

🐳 Installing with Docker
-------------------------

To build the Umami container and start up a Postgres database, run:

docker compose up -d

Alternatively, to pull just the Umami Docker image with PostgreSQL support:

docker pull docker.umami.is/umami-software/umami:latest

* * *

🔄 Getting Updates
------------------

Warning

If you are updating from Umami V2, image "postgresql-latest" is deprecated. You must change it to "latest". e.g., rename `docker.umami.is/umami-software/umami:postgresql-latest` to `docker.umami.is/umami-software/umami:latest`.

To get the latest features, simply do a pull, install any new dependencies, and rebuild:

git pull
pnpm install
pnpm run build

To update the Docker image, simply pull the new images and rebuild:

docker compose pull
docker compose up --force-recreate -d

* * *

🛟 Support
----------
