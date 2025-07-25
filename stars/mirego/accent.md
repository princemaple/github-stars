---
project: accent
stars: 1413
description: The first developer-oriented translation tool. True asynchronous flow between translators and your team.
url: https://github.com/mirego/accent
---

  
**The first developer-oriented translation tool**  
True asynchronous flow between translators and your team.  

Demo • Website • GraphiQL

Accent provides a powerful abstraction around the process maintaining translations in a web/native app.

-   **History**. Full history control and actions rollback. _Who_ did _what_, _when_.
-   **UI**. Simple yet powerful UI to enable translator and developer to be productive.
-   **CLI**. Command line tool to easily add Accent to your developer flow.
-   **Collaboration**. Centralize your discussions around translations.
-   **GraphQL**. The API that powers the UI is open and documented. It’s easy to build a plugin/cli/library around Accent.

Contents
--------

Section

Description

🚀 Getting started

Quickly setup a working app

🚧 Requirements

Dependencies required to run Accent’ stack

🎛 Mix commands

How to execute mix task with the Twelve-Factor pattern

🏎 Quickstart

Steps to run the project, from API to webapp, with or without Docker

🌳 Environment variables

Required and optional env var used

✅ Tests

How to run the extensive tests suite

🚀 Heroku

Easy deployment setup with Heroku

🌎 Contribute

How to contribute to this repo

🚀 Getting started
------------------

Easiest way to run an instance of Accent is by using the offical docker image: https://hub.docker.com/r/mirego/accent

1.  The only external dependancy is a PostgreSQL database.
2.  Create a `.env` file. Example:

```
DATABASE_URL=postgresql://postgres@docker.for.mac.host.internal/accent_development
DUMMY_LOGIN_ENABLED=1
# Required for session management. Must be a 64-byte string.
# Generate one using: openssl rand -hex 64
SECRET_KEY_BASE=KEY
```

1.  Run the image

$ docker run --env-file .env -p 4000:4000 mirego/accent

This will start the webserver on port 4000, migrate the database to have an up and running Accent instance!

🚧 Requirements
---------------

-   `erlang ~> 26.1`
-   `elixir ~> 1.15`
-   `postgres >= 9.4`
-   `node.js >= 16.19`
-   `libyaml >= 0.1.7`

🎛 Executing mix commands
-------------------------

The app is modeled with the _Twelve-Factor App_ architecture, all configurations are stored in the environment.

When executing `mix` commands, you should always make sure that the required environment variables are present. You can `source`, use nv or a custom l33t bash script.

Every following steps assume you have this kind of system.

But Accent can be run with default environment variables if you have a PostgreSQL user named `postgres` listening on port `5432` on `localhost`.

### Example

With `nv` you inject the environment keys in the context with:

$ nv .env mix <mix command\>

🏎 Quickstart
-------------

_This is the full development setup. To simply run the app, see the _Getting started_ instructions_

1.  If you don’t already have it, install `nodejs` with `brew install nodejs`
2.  If you don’t already have it, install `elixir` with `brew install elixir`
3.  If you don’t already have it, install `libyaml` with `brew install libyaml`
4.  If you don’t already have it, install `postgres` with `brew install postgres` or the Docker setup as described below.
5.  Install dependencies with `make dependencies`
6.  Create and migrate your database with `mix ecto.setup`
7.  Start Phoenix endpoint with `mix phx.server`

_That’s it!_ You should now be able to open the app at `http://localhost:4000`

### Makefile

The Makefile should be the main entry for common tasks such as tests, linting, Docker, etc. This simplifies the development process since you don’t have to search for which service provides which command. `mix`, `npm`, `prettier`, `docker`, `stylelint`, etc are all used in the Makefile.

### Docker

For the production setup, we use Docker to build an OTP release of the app. With docker-compose, you can run the image locally. Here are the steps to have a working app running locally with Docker:

_When running the production env, you need to provide a valid authentication setup in the `environment` section in `docker-compose.yml` file._ See the following sections to see available variables to enable third-party logins or dummy login (email only, no password).

1.  Run `make build` to build the OTP release with Docker
2.  Run `make dev-start-postgresql` to start an instance of Postgresql. The instance will run on port 5432 with the `postgres` user. You can change those values in the `docker-compose.yml` file.
3.  Run `make dev-start-application` to start the app! The release hook of the release will execute migrations and seeds before starting the webserver on port 4000 (again you can change the settings in `docker-compose.yml`)

_That’s it! You now have a working Accent instance without installing Elixir or NodeJS!_

🌳 Environment variables
------------------------

Accent provides a default value for every required environment variable. This means that with the right PostgreSQL setup, you can just run `mix phx.server`.

Variable

Default

Description

`DATABASE_URL`

`postgres://localhost/accent_development`

A valid database URL

`PORT`

`4000`

A port to run the app on

`SECRET_KEY_BASE`

_DEFAULT\_UNSAFE\_KEY_

The secret key that is used to encrypt session (cookie)

### Production setup

Variable

Default

Description

`RESTRICTED_PROJECT_CREATOR_EMAIL_DOMAIN`

_none_

If specified, only authenticated users from this domain name will be able to create new projects.

`FORCE_SSL`

_false_

If the app should always be served by https (and wss for websocket)

`SENTRY_DSN`

_none_

The _secret_ Sentry DSN used to collect API runtime errors

`WEBAPP_SENTRY_DSN`

_none_

The _public_ Sentry DSN used to collect Webapp runtime errors

`CANONICAL_URL`

_none_

The URL of the app. Used in sent emails and to redirect from external services to the app in the authentication flow.

`DISABLE_CANONICAL_HOST_REDIRECT`

_none_

Remove the redirect to the canonical host URL. Use with caution.

`STATIC_URL`

_none_

The URL of the app. Default to the CANONICAL\_URL value.

`WEBAPP_SKIP_SUBRESOURCE_INTEGRITY`

_none_

Remove integrity attributes on link and script tag. Useful when using a proxy that compress resources before serving them.

`DATABASE_SSL`

_false_

If SSL should be used to connect to the database

`DATABASE_POOL_SIZE`

_10_

The size of the pool used by the database connection module

`MACHINE_TRANSLATIONS_VAULT_KEY`

_DEFAULT\_UNSAFE\_VAULT\_KEY_

The secret key that is used to encrypt machine translations services config key

`TZDATA_AUTOUPDATE_DISABLED`

_none_

Turn off automatic updates for Tzdata, needed when running read-only containers

`SECRET_KEY_BASE`

_DEFAULT\_UNSAFE\_KEY_

The secret key that is used to encrypt session (cookie)

### Authentication setup

Various login providers are included in Accent using Ueberauth to abstract services.

Variable

Default

Description

`DUMMY_LOGIN_ENABLED`

_none_

If specified, the password-less authentication (with only the email) will be available.

`GITHUB_CLIENT_ID`

_none_

`GITHUB_CLIENT_SECRET`

_none_

`GITLAB_CLIENT_ID`

_none_

`GITLAB_CLIENT_SECRET`

_none_

`GITLAB_SITE_URL`

`https://gitlab.com`

`GOOGLE_API_CLIENT_ID`

_none_

`GOOGLE_API_CLIENT_SECRET`

_none_

`SLACK_CLIENT_ID`

_none_

`SLACK_CLIENT_SECRET`

_none_

`SLACK_TEAM_ID`

_none_

`DISCORD_CLIENT_ID`

_none_

`DISCORD_CLIENT_SECRET`

_none_

`MICROSOFT_CLIENT_ID`

_none_

`MICROSOFT_CLIENT_SECRET`

_none_

`MICROSOFT_TENANT_ID`

_none_

`OIDC_CLIENT_ID`

_none_

`OIDC_CLIENT_SECRET`

_none_

`OIDC_DISCOVERY_URI`

_none_

`OIDC_UID_FIELD`

`sub`

`OIDC_SCOPE`

`openid profile email`

### Email setup

If you want to send emails, you’ll have to configure the following environment variables:

Variable

Default

Description

`MAILER_FROM`

_none_

The email address used to send emails.

`SENDGRID_API_KEY`

_none_

Use SendGrid to send emails

`MANDRILL_API_KEY`

_none_

Use Mandrill to send emails

`MAILGUN_API_KEY`

_none_

Use Mailgun to send emails

`MAILGUN_DOMAIN`

none

Use a custom domain in Mailgun

`MAILGUN_BASE_URI`

none

Send emails from a different server

`SMTP_ADDRESS`

_none_

Use an SMTP server to send your emails.

`SMTP_API_HEADER`

_none_

An optional API header that will be added to sent emails.

`SMTP_PORT`

_none_

The port ex: (25, 465, 587).

`SMTP_PASSWORD`

_none_

The password for authentification.

`SMTP_USERNAME`

_none_

The username for authentification.

### Metrics and monitoring setup

If you want to track performance of Accent, you can configure NewRelic with the following environment variables:

Variable

Default

Description

`NEW_RELIC_APP_NAME`

_none_

Service APM name

`NEW_RELIC_LICENSE_KEY`

_none_

License key

Or use the built-in metrics UI from TelemetryUI:

Variable

Default

Description

`METRICS_BASIC_AUTH`

_none_

username:password to HTTP basic auth login on the pre-configured dashboard

### Kubernetes helm chart setup

You can setup the project with a helm chart like this one. This project uses a fork by andreymaznyak and not this canonical repository. The specs and values may need to be updated if you use this repo.

✅ Tests
-------

### API

Accent provides a default value for every required environment variable. This means that with the right PostgreSQL setup (and a few setup commands), you can just run `mix test`.

$ npm --prefix webapp run build
$ mix ecto.setup
$ mix test

The full check that runs in the CI environment can be executed with `./priv/scripts/ci-check.sh`.

🚀 Deploy on Heroku
-------------------

An Heroku-compatible `app.json` makes it easy to deploy the application on Heroku.

### Using Heroku CLI

_Based on this guide_

```
$> heroku create
Creating app... done, ⬢ peaceful-badlands-85887
https://peaceful-badlands-85887.herokuapp.com/ | https://git.heroku.com/peaceful-badlands-85887.git

$> heroku addons:create heroku-postgresql:hobby-dev --app peaceful-badlands-85887
Creating heroku-postgresql:hobby-dev on ⬢ peaceful-badlands-85887... free
Database has been created and is available

$> heroku config:set FORCE_SSL=true DATABASE_SSL=true DUMMY_LOGIN_ENABLED=true --app peaceful-badlands-85887
Setting FORCE_SSL, DATABASE_SSL, DUMMY_LOGIN_ENABLED and restarting ⬢ peaceful-badlands-85887... done

$> heroku container:push web --app peaceful-badlands-85887
=== Building web
Your image has been successfully pushed. You can now release it with the 'container:release' command.

$> heroku container:release web --app peaceful-badlands-85887
Releasing images web to peaceful-badlands-85887... done
```

🌎 Contribute
-------------

Before opening a pull request, please open an issue first.

Once you’ve made your additions and the test suite passes, go ahead and open a PR!

Don’t forget to run the `./priv/scripts/ci-check.sh` script to make sure that the CI build will pass :)

License
-------

Accent is © 2015-2019 Mirego and may be freely distributed under the New BSD license. See the `LICENSE.md` file.

About Mirego
------------

Mirego is a team of passionate people who believe that work is a place where you can innovate and have fun. We’re a team of talented people who imagine and build beautiful Web and mobile applications. We come together to share ideas and change the world.

We also love open-source software and we try to give back to the community as much as we can.
