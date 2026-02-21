---
project: builder
stars: 1886
description: Craft beautiful websites effortlessly with an intuitive visual builder and publish them instantly
url: https://github.com/frappe/builder
---

Frappe Builder
==============

**Crafting Web Pages Made Effortless**

Website - Documentation

Frappe Builder
--------------

Frappe Builder is a low-code website builder designed for simplicity, speed, and flexibility. Craft beautiful websites effortlessly with an intuitive visual builder. Whether you're a designer looking for ease or a developer seeking customization, Frappe Builder empowers you. It also features a click-to-publish option that gives you the complete end-to-end website creation experience.

### Motivation

Most existing solutions were either too complex, too restrictive, or difficult to integrate with the Frappe ecosystem. Additionally, pages built with these tools were often bloated with unnecessary scripts and styles. I wanted to take a stab at solving this problem while prioritising performance from day one. I aimed to address two major issues with this project: providing an intuitive way to design a web page and enabling one-click publishing. As a web developer, it helps me scratch my own itch, and I hope it helps others too.

### Key Features

-   **Intuitive Visual Builder:** Simplify your workflow with a Figma-like editor.
-   **Responsive Views:** Ensure your sites look great on any device without the fuss.
-   **Frappe CMS Integration:** Easily fetch data from your database and create dynamic pages.
-   **Scripting Capabilities:** Customize with client scripts, global scripts, and styles.
-   **One-Click Publishing:** Instantly share your creation with the world in a single click.
-   **Performance Excellence:** Frappe Builder does not bloat web pages with unnecessary scripts hence pages are highly performant, consistently scoring high on Google Lighthouse tests.
-   **Production Ready**: Frappe.io built on Frappe Builder, stands as a testament to its reliability in delivering production-ready solutions.

### Under the Hood

-   Frappe Framework: A full-stack web application framework.
-   Frappe UI: A Vue-based UI library, to provide a modern user interface.

Getting Started (Production)
----------------------------

### Managed Hosting

Get started with your personal or business site with a few clicks on Frappe Cloud - our official hosting service.

### Self Hosting

Follow these steps to set up Frappe Builder in production:

**Step 1**: Download the easy install script

wget https://frappe.io/easy-install.py

**Step 2**: Run the deployment command

python3 ./easy-install.py deploy \\
    --project=builder\_prod\_setup \\
    --email=email@example.com \\
    --image=ghcr.io/frappe/builder \\
    --version=stable \\
    --app=builder \\
    --sitename subdomain.domain.tld

Replace the following parameters with your values:

-   `email@example.com`: Your email address
-   `subdomain.domain.tld`: Your domain name where Builder will be hosted

The script will set up a production-ready instance of Frappe Builder with all the necessary configurations in about 5 minutes.

Getting Started (Development)
-----------------------------

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

### Local Setup

1.  Setup Bench.
2.  In the frappe-bench directory, run `bench start` and keep it running.
3.  Open a new terminal session and cd into `frappe-bench` directory and run following commands:

bench get-app builder
bench new-site builder.localhost --install-app builder
bench browse builder.localhost --user Administrator
bench --site builder.localhost set-config ignore\_csrf 1 # prevents CSRFToken errors while using the vite dev server

1.  Access the builder page at `builder.localhost:8000/builder` in your web browser.

**For Frontend Development**

1.  Open a new terminal session and run the following commands:

cd frappe-bench/apps/builder
yarn install
yarn dev --host

1.  Now, you can access the site on vite dev server at `http://builder.localhost:8080`

**Note:** You'll find all the code related to Builder's frontend inside `frappe-bench/apps/builder/frontend`

### Links

-   Telegram Public Group
-   Discuss Forum
-   Documentation
-   Figma Plugin (Beta)
