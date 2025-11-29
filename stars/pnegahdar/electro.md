---
project: electro
stars: 80
description: ⚡️ Personal Github pages lite. Share prototypes with teammates. Host static sites. Share documents.
url: https://github.com/pnegahdar/electro
---

Electro - A dynamic git repo static server
==========================================

Personal Github pages lite. Share prototypes with teammates. Host static sites. Share documents.

### Demo: https://electro.pnegahdar.com

### Features:

-   Automatic **HTTPs** through LetsEncrypt
-   **No restarts**, add a new site and access it immediately.
-   Serve from any **git** repo/branch/subdirectory
-   Git repositories **auto update** to serve newest changes on a branch
-   Simple user **interface** to add and remove sites.
-   Serve each site on a **multiple hostnames**
-   Add http basic **auth** to any of the sites to protect them from public access
-   **Protect** public sites with deletion passwords.
-   Single binary, **zero** external dependencies (including git)
-   Run as pid 1 or docker entrypoint, includes **reaper**.

### Screenshot

### Getting started

#### Install

OSX:

curl -SsL https://github.com/pnegahdar/electro/releases/download/0.1.0/darwin\_amd64 \> /usr/local/bin/electro && \\
        chmod +x /usr/local/bin/electro

Linux:

curl -SsL https://github.com/pnegahdar/electro/releases/download/0.1.0/linux\_amd64 \> /usr/local/bin/electro && \\
        chmod +x /usr/local/bin/electro

Dockerfile

ENV ELECTRO\_VERSION 0.1.0
ADD https://github.com/pnegahdar/electro/releases/download/${ELECTRO\_VERSION}/linux\_amd64 /usr/local/bin/electro
RUN chmod +x /usr/local/bin/electro

Prebuilt:

export WILDCARD\_DOMAIN="site.domain.com"
docker run -d --restart=always \\
        -p 80:80 -p 443:443 \\
        -v /var/data/electro:/var/data/electro \\
        pnegahdar/electro \\
        electro start --listen-http :80 --listen-https :443 --data-dir /var/data/electro --wildcard ${WILDCARD\_DOMAIN}

#### Run

Create a wildcard domain and point it to the server.

electro start --wildcard site.domain.com --listen-http :80 --listen-https :443

electro start --help
Start the server.

Usage:
  electro start \[flags\]

Flags:
  -w, --wildcard string         The wildcard domain to serve e.g electro.site.com
  -l, --listen-http string      The address to listen for http connections. e.g. 0.0.0.0:80, :5000, etc. (default ":4200")
  -s, --listen-https string     The address to listen for https servers. https server not started when ommited.
  -p, --admin-password string   The password for the admin dashboard and api. Must provide username as well.
  -u, --admin-username string   The username for the admin dashboard and api. Must provide password as well.
  -d, --data-dir string         The directory to store the state and certificates. (default "~/.electro")

#### Contributing

Clone the repo. This project uses glide for dependency management. These commands assume glide is installed, go paths are set, go bin is in your path and you have yarn and node.

# install deps
glide install

# build
make build

# distrubtable build: osx and linux with static assets embedded in binary.
make distribute

# Run the go application
make build && electro-dev start --wildcard test.com

# Run the static server
cd fe/ && yarn install && yarn start

# fmt changes
make fmt
