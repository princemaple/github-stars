---
project: stripe-cli
stars: 1810
description: A command-line tool for Stripe
url: https://github.com/stripe/stripe-cli
---

Stripe CLI
==========

The Stripe CLI helps you build, test, and manage your Stripe integration right from the terminal.

**With the CLI, you can:**

-   Securely test webhooks without relying on 3rd party software
-   Trigger webhook events or resend events for easy testing
-   Tail your API request logs in real-time
-   Create, retrieve, update, or delete API objects.

Installation
------------

Stripe CLI is available for macOS, Windows, and Linux for distros like Ubuntu, Debian, RedHat and CentOS.

### macOS

Stripe CLI is available on macOS via Homebrew:

brew install stripe/stripe-cli/stripe

### Linux

Refer to the installation instructions for available Linux installation options.

### Windows

Stripe CLI is available on Windows via the Scoop package manager:

scoop bucket add stripe https://github.com/stripe/scoop-stripe-cli.git
scoop install stripe

### Docker

The CLI is also available as a Docker image: `stripe/stripe-cli`.

docker run --rm -it stripe/stripe-cli version
stripe version x.y.z (beta)

**Password Store Setup with Docker**

While test mode doesn’t require password store, you will need to set it up if you wish to perform live mode requests.

> You can also make live mode requests on a per command basis by attaching the `--api-key` flag.

1.  Create `entrypoint.sh`

#!/bin/sh
if ! \[ \-f ~/.gnupg/trustdb.gpg \] ; then
  chmod 700 ~/.gnupg/
  gpg --quick-generate-key stripe-live # This will generate a gpg key called "stripe-live"
fi
if ! \[ \-f ~/.password-store/.gpg-id \] ; then
  pass init stripe-live # This will initialize a password store record named "stripe-live", using the gpg key above
  pass insert stripe-live # This will insert value for the password store "stripe-live", which we will put Stripe Live Secret Key in
fi

string="$@"
liveflag="\--live"

if \[ \-z "${string##\*$liveflag\*}" \] ;then
  OPTS="\--api-key $(pass show stripe-live)" # This will use the content of the password store "stripe-live" which was inserted in line 8
fi

#pass insert stripe-live
/bin/stripe  $@ $OPTS

1.  Create a docker file `Dockerfile-cli`

FROM  stripe/stripe-cli:vx.x.x
RUN  apk  add  pass  gpg-agent
COPY  ./entrypoint.sh  /entrypoint.sh
ENTRYPOINT  \[ "/entrypoint.sh" \]

1.  Build the docker image

docker build -t stripe-cli -f Dockerfile-cli .

1.  Run the docker image with password volumes, replacing `$command` with the appropraite Stripe CLI command (i.e `customers list`)

docker run --rm -it -v stripe-config://root/.config/stripe/ -v stripe-gpg://root/.gnupg/ -v stripe-pass://root/.password-store/ stripe-cli $command

> For live mode requests append `--live` after `$command`.

### Without package managers

Instructions are also available for installing and using the CLI without a package manager.

Usage
-----

Installing the CLI provides access to the `stripe` command.

stripe \[command\]

# Run \`\--help\` for detailed information about CLI commands
stripe \[command\] help

Commands
--------

The Stripe CLI supports a broad range of commands. Below are some of the most used ones:

-   `login`
-   `listen`
-   `trigger`
-   `logs tail`
-   `events resend`
-   `samples`
-   `serve`
-   `status`
-   `config`
-   `open`
-   `get`, `post` & `delete` commands
-   `resource` commands

Documentation
-------------

For a full reference, see the CLI reference site

Telemetry
---------

The Stripe CLI includes a telemetry feature that collects some usage data. See our telemetry reference for details.

Feedback
--------

Got feedback for us? Please don't hesitate to tell us on feedback.

Contributing
------------

See Developing the Stripe CLI for more info on how to make contributions to this project.

License
-------

Copyright (c) Stripe. All rights reserved.

Licensed under the Apache License 2.0 license.
