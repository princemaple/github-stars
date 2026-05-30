---
project: observer_live
stars: 212
description: A port of observer_cli using LiveView
url: https://github.com/zorbash/observer_live
---

ObserverLive
============

This is a port of observer\_cli using phoenix and LiveView.

⚠️ It's still a work in progress and has not been tested in production.

Blog post: observer\_live

Demo: Try it

Video:

For other LiveView examples and demos see here.

Roadmap
-------

This project may have started as a demo for the capabilities of LiveView, but I'm keen to port the rest of observer\_cli's ports. Any help is welcome!

Remaining work:

**System - Cache Hit Info**

See: source

**ETS**

See: source

**Mnesia**

See: source

**App**

See: source

If you're interested to help, submit a PR. For questions find me on elixir-lang.slack.com

Development
-----------

To run it locally:

-   Install dependencies with `mix deps.get`
-   Create and migrate your database with `mix ecto.setup`
-   Install Node.js dependencies with `cd assets && npm install`
-   Start Phoenix endpoint with `mix phx.server`

Now you can visit `localhost:4000` from your browser.

License
-------

Copyright (c) 2019 Dimitris Zorbas, MIT License.
