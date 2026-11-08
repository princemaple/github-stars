---
project: builder
stars: 2474
description: Craft beautiful websites effortlessly with an intuitive visual builder and publish them instantly
url: https://github.com/frappe/builder
---

Frappe Builder
==============

**Crafting Web Pages Made Effortless**

Website - Documentation

Frappe Builder
--------------

Frappe Builder is an open-source website builder. You design pages on a visual canvas, fill them with content from your Frappe database when you need to, and publish with one click.

### Motivation

Most existing solutions were either too complex, too restrictive, or difficult to integrate with the Frappe ecosystem. Additionally, pages built with these tools were often bloated with unnecessary scripts and styles. I wanted to take a stab at solving this problem while prioritising performance from day one. I aimed to address two major issues with this project: providing an intuitive way to design a web page and enabling one-click publishing. As a web developer, it helps me scratch my own itch, and I hope it helps others too.

### Key Features

#### Visual editor

Drag blocks onto the canvas and style them from the properties panel, much like you would in Figma. Desktop, tablet and mobile views sit side by side, and a change you make in the tablet or mobile view applies only to that screen size.

#### Bob, the AI assistant

Describe the page you want and Bob builds it on the canvas, using the colours, fonts and components your site already has, so new pages match the rest of your site. Ask for changes the same way: a shorter headline, warmer colours, an enquiry form. If a form needs somewhere to store submissions, Bob asks before creating it, and the entries show up in Desk, Frappe's admin. You can revert anything Bob changes.

#### Pages from your data

Builder runs on the Frappe Framework, so a page can show records straight from your database. A few lines of Python in the page's data script fetch them, and a block can repeat once per record to make a blog index, a product grid or a team page. With a route like `/blog/:slug`, one design gives every post its own page.

#### Reusable components

Save a header, a card or any group of blocks as a component and use it on as many pages as you like. Edit it once and every page that uses it updates. Props let each copy show different content.

#### Fast pages

Published pages are plain HTML and CSS. No JavaScript runs unless you add some, and there is no framework to download before the page appears. frappe.io is built with Builder.

Google Lighthouse (mobile) on nearly identical pages built with each tool, as published on frappe.io/builder.

#### Also included

-   One-click publishing, with version history for every page
-   Page analytics: views, visitors and referrers, without a third-party script
-   Colour and font tokens, each with a light and a dark value
-   Hover, focus and active styles, set without writing CSS
-   Pages that only signed-in users can see
-   Uploaded images converted to WebP automatically
-   Client scripts and global scripts for custom behaviour
-   A Figma plugin to bring in designs from Figma
-   A skill that lets Claude Code, Codex and other coding agents build and publish pages for you (setup)

### Under the Hood

-   Frappe Framework: A full-stack web application framework.
-   Frappe UI: A Vue-based UI library, to provide a modern user interface.

Getting Started (Production)
----------------------------

### Managed Hosting

Get started with your personal or business site with a few clicks on Frappe Cloud - our official hosting service.

### Self Hosting

Pilot is Frappe's tool for running benches and sites on your own server. It installs Frappe, manages sites and backups, and sets up production with nginx and TLS. Pilot needs Frappe v16 or later and is still in pre-release. Production servers need Linux; macOS works for local development.

**Step 1**: Install Pilot

curl -fsSL https://raw.githubusercontent.com/frappe/pilot/develop/install.sh | bash

**Step 2**: Create a bench. The first `start` prints the URL of a setup wizard, where you pick the Frappe branch (`version-16`) and set passwords.

pilot new main
pilot -b main start

**Step 3**: Add Builder and create your site

pilot -b main get-app https://github.com/frappe/builder --branch master
pilot -b main new-site subdomain.domain.tld --admin-password <password\>
pilot -b main install-app subdomain.domain.tld builder

**Step 4**: Go to production

pilot -b main setup production --admin-domain admin.domain.tld --tls --letsencrypt-email email@example.com

Pilot's production guide covers process managers, domains and TLS. To run production with bench instead, follow Frappe's production setup.

Getting Started (Development)
-----------------------------

### With a Coding Agent

Add the `frappe-builder` skill to Claude Code, Codex, OpenCode or another coding agent:

npx skills add frappe/builder

Then ask it to set up a local Builder site. It uses your existing bench if you have one and creates one if you don't. After that it can build, edit and publish pages for you, on your local site or on any Frappe site you sign in to through frappectl.

### Pilot

On Linux or macOS, install Pilot and create a bench. In the setup wizard, pick Frappe's `develop` branch.

pilot new dev
pilot -b dev start

In a new terminal, add Builder and create a site:

pilot -b dev get-app https://github.com/frappe/builder --branch develop
pilot -b dev new-site builder.localhost
pilot -b dev install-app builder.localhost builder
pilot -b dev frappe --site builder.localhost set-config ignore\_csrf 1 # prevents CSRFToken errors while using the vite dev server

Open http://builder.localhost:8000/builder and log in as `Administrator` / `admin`. Pilot moves to the next free port if 8000 is taken.

### Existing Bench

If you already have a bench on Frappe's `develop` branch, run `bench start` and keep it running. Then, in a new terminal inside `frappe-bench`:

bench get-app builder --branch develop
bench new-site builder.localhost --install-app builder
bench browse builder.localhost --user Administrator
bench --site builder.localhost set-config ignore\_csrf 1 # prevents CSRFToken errors while using the vite dev server

The editor is at `builder.localhost:8000/builder`.

### Docker

You need Docker, docker-compose and git setup on your machine. Refer Docker documentation. After that, run following command:

**Step 1**: Setup folder and download the required files

mkdir frappe-builder && cd frappe-builder
wget -O docker-compose.yml https://raw.githubusercontent.com/frappe/builder/develop/docker/docker-compose.yml
wget -O init.sh https://raw.githubusercontent.com/frappe/builder/develop/docker/init.sh

**Step 2**: Run the container

docker compose up

Wait until the setup script creates a site and you see `Current Site set to builder.localhost` in the terminal. Once done, the site http://builder.localhost:8000 should now be available.

**Credentials:** Username: `Administrator` Password: `admin`

### Frontend Development

In a new terminal, from `apps/builder` inside your bench:

yarn dev-setup
yarn dev --host

Now, you can access the site on vite dev server at `http://builder.localhost:8080`

**Note:** You'll find all the code related to Builder's frontend inside `apps/builder/frontend`

### Links

-   Telegram Public Group
-   Discuss Forum
-   Documentation
-   Figma Plugin (Beta)
-   Frappe Script Editor
-   Translations
