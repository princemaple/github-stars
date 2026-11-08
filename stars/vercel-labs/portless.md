---
project: portless
stars: 12864
description: Replace port numbers with stable, named local URLs. For humans and agents.
url: https://github.com/vercel-labs/portless
---

portless
========

Replace port numbers with stable, named .localhost URLs for local development. For humans and agents.

\- "dev": "next dev"                  # http://localhost:3000
+ "dev": "portless run next dev"     # https://myapp.localhost

portless runs a local reverse proxy and gives each dev server a name. Your app listens on a free port that portless assigns, and you open `https://<name>.localhost` instead of remembering which port it took. The URL stays the same across restarts, so bookmarks, cookies, OAuth redirects, and an agent's test script keep pointing at the right app.

Install
-------

npm install -g portless

To pin the version per project, install it as a dev dependency with `npm install -D portless`. portless is pre-1.0, so contributors may run different versions, and a change to the state directory format between releases can require running `portless trust` again.

Quick start
-----------

From a project with a `"dev"` script in `package.json`:

portless
# -> runs "dev", https://<project>.localhost

The name comes from `package.json`, the git root, or the directory. Pass a name and a command to choose both:

portless myapp next dev
# -> https://myapp.localhost

-   The proxy starts on the first run. It serves HTTPS with HTTP/2 on port 443, so the first run creates a local certificate authority, adds it to the system trust store, and may ask for `sudo`. Use `--no-tls` for plain HTTP, or `--unprivileged` to skip `sudo` (Unprivileged mode).
-   `portless run <cmd>` infers the name and detects git worktrees. In a linked worktree, the last `/` segment of the branch becomes a subdomain, so `fix-ui.myapp.localhost` and `myapp.localhost` run side by side. Use `--prefix` or `PORTLESS_PREFIX` to set the label, or configure the label style and hostname template.
-   A name with dots is a subdomain: `portless api.myapp pnpm start` serves `https://api.myapp.localhost`.
-   `PORTLESS=0 pnpm dev` runs the command directly, without the proxy.

The full walkthrough is in Getting started.

How it works
------------

Each app gets a random port from 4000 to 4999 through the `PORT` environment variable, and registers a route from its hostname to that port. The proxy forwards `https://<name>.localhost` to the route. Most frameworks read `PORT`. For those that don't, such as Vite, Astro, Angular, Expo, and Wrangler, portless adds the matching port and host flags to the command (Port assignment).

Outside LAN mode, the proxy listens only on `127.0.0.1` and `::1`. It keeps `/etc/hosts` in sync for route hostnames, which custom TLDs such as `.test` need. If a route hostname will not resolve, the command that registered it warns and points you to `portless hosts sync`.

To reach an app from another device or share it, use LAN mode for phones on the same network, or Tailscale, ngrok, or a Cloudflare quick tunnel with `--tailscale`, `--ngrok`, or `--cloudflare`.

### Upstream aliases

Use `--upstream` to route an alias to an HTTP or HTTPS service listening on loopback:

portless alias api 8080 --upstream https
portless alias api 8080 --upstream https://api.internal
portless alias api 8080 --upstream http://api.internal

The positional port always dials loopback. `https` enables TLS and preserves the incoming Host header. An `https://` authority enables TLS and overrides Host with the full authority, including its optional port. SNI uses a DNS hostname without the port; IP addresses are not sent as SNI. An `http://` authority overrides Host without TLS. This setting does not change client-facing proxy TLS. Authorities accept only a hostname or IP address with an optional port, without credentials, paths, queries, fragments, or whitespace.

Upstream TLS connects only to an HTTP/1.1 backend on loopback. Portless disables certificate verification, so TLS does not authenticate backend identity, even through an SSH tunnel. Restart the proxy daemon after upgrading portless.

Configuration
-------------

An optional `portless.json` sets the name and script. In a monorepo, one file at the root covers every workspace package, and `portless` from the root starts all of them:

{
  "apps": {
    "apps/web": { "name": "myapp" },
    "apps/api": { "name": "api.myapp" }
  }
}

A `"portless"` key in `package.json` works too. Fields, precedence, Turborepo setup, and environment variables are in Configuration.

For AI agents
-------------

Install the portless skill into an agent harness from skills.sh:

npx skills add vercel-labs/portless

For MCP clients, `portless mcp` starts an MCP server over stdio. The default `core` profile lists routes, looks up URLs, and manages static aliases. `--tools all` adds proxy control and diagnostics:

{ "mcpServers": { "portless": { "command": "portless", "args": \["mcp"\] } } }

The server does not start dev servers. Agents run `portless run <cmd>` in a shell. See MCP server.

Commands
--------

Run `portless --help` for the full list, or `portless <command> --help` for one command.

Group

Commands

Docs

Run apps

`portless`, `run`, `<name> <cmd>`, `get`

Run an app, Get a service URL

Static routes

`alias`, `compose up`, `compose down`

Alias, Docker Compose

Proxy

`proxy start`, `proxy stop`, `service install`, `service status`, `service uninstall`

Proxy control, OS startup service

HTTPS and DNS

`trust`, `hosts sync`, `hosts clean`

HTTPS, Hosts

Inspect and clean up

`list`, `doctor`, `prune`, `clean`

Doctor, Prune orphans, Clean up

Agents

`mcp`

MCP server

Run `portless doctor` first when a URL does not load. It checks the proxy, routes, DNS, and CA trust without changing anything, and prints suggested fixes.

Platforms
---------

portless runs on macOS, Linux, and Windows with Node.js 24 or later. `--tailscale` and `--funnel` need the Tailscale CLI, `--ngrok` needs the ngrok CLI, and `--cloudflare` needs `cloudflared`.

Development
-----------

This repo is a pnpm workspace with Turborepo. The published package is `packages/portless/`, and the docs site is `apps/docs/`. Use Node.js 24 or later and pnpm 11:

pnpm install
pnpm build
pnpm test
pnpm lint
pnpm type-check
pnpm format

AGENTS.md lists the files to update with each change and the release process.

Documentation
-------------

-   portless.sh: getting started, commands, HTTPS, and configuration
-   Why portless: the problems named URLs solve
-   Changelog

License
-------

Apache-2.0
