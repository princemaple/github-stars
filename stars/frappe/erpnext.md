---
project: erpnext
stars: 36127
description: Free and Open Source Enterprise Resource Planning (ERP)
url: https://github.com/frappe/erpnext
---

ERPNext
-------

Powerful, Intuitive and Open-Source ERP

  
  

Live Demo - Website - Documentation

ERPNext
-------

100% Open-Source ERP System to help you run your business.

### Motivation

Running a business is a complex task - handling invoices, tracking stock, managing personnel, and other daily operations. In a market where software is sold separately to manage each of these tasks, ERPNext does all of the above and more, for free.

### Key Features

-   **Accounting**: All the tools you need to manage cash flow in one place, right from recording transactions to summarizing and analyzing financial reports.
-   **Order Management**: Track inventory levels, replenish stock, and manage sales orders, customers, suppliers, shipments, deliverables, and order fulfillment.
-   **Manufacturing**: Simplifies the production cycle, helps track material consumption, exhibits capacity planning, handles subcontracting, and more!
-   **Asset Management**: From purchase to disposal, IT infrastructure to equipment. Covers every branch of your organization, all in one centralized system.
-   **Projects**: Deliver both internal and external projects on time, budget and profitability. Track tasks, timesheets, and issues by project.

More

### Under the Hood

-   **Frappe Framework**: A full-stack web application framework written in Python and JavaScript. The framework provides a robust foundation for building web applications, including a database abstraction layer, user authentication, and a REST API.
    
-   **Frappe UI**: A Vue-based UI library, to provide a modern user interface. The Frappe UI library provides a variety of components that can be used to build single-page applications on top of the Frappe Framework.
    

Production Setup
----------------

### Managed Hosting

You can try Frappe Cloud, a simple, user-friendly, and sophisticated open-source platform to host Frappe applications reliably and securely.

It handles installation, setup, upgrades, monitoring, maintenance, and support of your Frappe deployments. It is a fully featured developer platform with an ability to manage and control multiple Frappe deployments.

### Self-Hosted

#### Docker

See Frappe Docker Documentation for full documentation & FAQ on Docker setup

#### Prerequisites

-   Docker
-   Docker Compose v2
-   git

> For Docker basics and best practices refer to Docker's documentation

### Try on your environment

> **⚠️ Disposable demo only**
> 
> **This setup is intended for quick evaluation. Expect to throw the environment away.** You will not be able to install custom apps to this setup. For production deployments, custom configurations, and detailed explanations, see the full documentation.

First clone the repo:

git clone https://github.com/frappe/frappe\_docker
cd frappe\_docker

Then run:

docker compose -f pwd.yml up -d

Wait for a couple of minutes for ERPNext site to be created or check the `create-site` container logs before opening browser on port `8080`. (username: `Administrator`, password: `admin`)

See Frappe Docker for ARM based docker setup

Development Setup
-----------------

### Manual Install

The Easy Way: our install script for bench will install all dependencies (e.g. MariaDB). See https://github.com/frappe/bench for more details.

New passwords will be created for the ERPNext "Administrator" user, the MariaDB root user, and the Frappe user (the script displays the passwords and saves them to ~/frappe\_passwords.txt).

### Local

To setup the repository locally follow the steps mentioned below:

1.  Setup bench by following the Installation Steps and start the server
    
    ```
    bench start
    ```
    
2.  In a separate terminal window, run the following commands:
    
    ```
    # Create a new site
    bench new-site erpnext.localhost
    ```
    
3.  Get the ERPNext app and install it
    
    ```
    # Get the ERPNext app
    bench get-app https://github.com/frappe/erpnext
    
    # Install the app
    bench --site erpnext.localhost install-app erpnext
    ```
    
4.  Open the URL `http://erpnext.localhost:8000/app` in your browser, you should see the app running
    

Learning and Community
----------------------

1.  Frappe School - Learn Frappe Framework and ERPNext from the various courses by the maintainers or from the community.
2.  Official documentation - Extensive documentation for ERPNext.
3.  Discussion Forum - Engage with the community of ERPNext users and service providers.
4.  Telegram Group - Get instant help from huge community of users.

Contributing
------------

1.  Issue Guidelines
2.  Report Security Vulnerabilities
3.  Pull Request Requirements
4.  Translations

Logo and Trademark Policy
-------------------------

Please read our Logo and Trademark Policy.
