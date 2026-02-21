---
project: documenso
stars: 12429
description: The Open Source DocuSign Alternative.
url: https://github.com/documenso/documenso
---

The Open Source DocuSign Alternative.  
**Learn more »**  
  
Discord · Website · Issues · Upcoming Releases · Roadmap

About Documenso
---------------

Signing documents digitally should be fast and easy and should be the best practice for every document signed worldwide. This is technically quite easy today, but it also introduces a new party to every signature: The signing tool providers. While this is not a problem in itself, it should make us think about how we want these providers of trust to work. Documenso aims to be the world's most trusted document-signing tool. This trust is built by empowering you to self-host Documenso and review how it works under the hood.

Join us in creating the next generation of open trust infrastructure.

Recognition
-----------

Community and Next Steps 🎯
---------------------------

-   Check out the first source code release in this repository and test it.
-   Tell us what you think in the Discussions.
-   Join the Discord server for any questions and getting to know to other community members.
-   ⭐ the repository to help us raise awareness.
-   Spread the word on Twitter that Documenso is working towards a more open signing tool.
-   Fix or create issues, that are needed for the first production release.

Contributing
------------

-   To contribute, please see our contribution guide.

Contact us
----------

Contact us if you are interested in our Enterprise plan for large organizations that need extra flexibility and control.

Tech Stack
----------

-   Typescript - Language
-   ReactRouter - Framework
-   Prisma - ORM
-   Tailwind - CSS
-   shadcn/ui - Component Library
-   react-email - Email Templates
-   tRPC - API
-   @documenso/pdf-sign - PDF Signatures (launching soon)
-   React-PDF - Viewing PDFs
-   PDF-Lib - PDF manipulation
-   Stripe - Payments

Local Development
-----------------

### Requirements

To run Documenso locally, you will need

-   Node.js (v22 or above)
-   Postgres SQL Database
-   Docker (optional)

### Developer Quickstart

> **Note**: This is a quickstart for developers. It assumes that you have both docker and docker-compose installed on your machine.

Want to get up and running quickly? Follow these steps:

1.  Fork this repository to your GitHub account.

After forking the repository, clone it to your local device by using the following command:

git clone https://github.com/<your-username\>/documenso

1.  Set up your `.env` file using the recommendations in the `.env.example` file. Alternatively, just run `cp .env.example .env` to get started with our handpicked defaults.
    
2.  Run `npm run dx` in the root directory
    
    -   This will spin up a postgres database and inbucket mailserver in a docker container.
3.  Run `npm run dev` in the root directory
    
4.  Want it even faster? Just use
    

npm run d

#### Access Points for Your Application

1.  **App** - http://localhost:3000
    
2.  **Incoming Mail Access** - http://localhost:9000
    
3.  **Database Connection Details**
    
    -   **Port**: 54320
    -   **Connection**: Use your favorite database client to connect using the provided port.
4.  **S3 Storage Dashboard** - http://localhost:9001
    

Developer Setup
---------------

### Manual Setup

Follow these steps to setup Documenso on your local machine:

1.  Fork this repository to your GitHub account.

After forking the repository, clone it to your local device by using the following command:

git clone https://github.com/<your-username\>/documenso

1.  Run `npm i` in the root directory
    
2.  Create your `.env` from the `.env.example`. You can use `cp .env.example .env` to get started with our handpicked defaults.
    
3.  Set the following environment variables:
    
    -   NEXTAUTH\_SECRET
    -   NEXT\_PUBLIC\_WEBAPP\_URL
    -   NEXT\_PRIVATE\_DATABASE\_URL
    -   NEXT\_PRIVATE\_DIRECT\_DATABASE\_URL
    -   NEXT\_PRIVATE\_SMTP\_FROM\_NAME
    -   NEXT\_PRIVATE\_SMTP\_FROM\_ADDRESS
4.  Create the database schema by running `npm run prisma:migrate-dev`
    
5.  Run `npm run translate:compile` in the root directory to compile lingui
    
6.  Run `npm run dev` in the root directory to start
    
7.  Register a new user at http://localhost:3000/signup
    

* * *

-   Optional: Seed the database using `npm run prisma:seed -w @documenso/prisma` to create a test user and document.
-   Optional: Create your own signing certificate.
    -   To generate your own using these steps and a Linux Terminal or Windows Subsystem for Linux (WSL), see **Create your own signing certificate**.

### Run in Gitpod

-   Click below to launch a ready-to-use Gitpod workspace in your browser.

### Run in DevContainer

We support DevContainers for VSCode. Click here to get started.

### Video walkthrough

If you're a visual learner and prefer to watch a video walkthrough of setting up Documenso locally, check out this video:

Docker
------

We provide a Docker container for Documenso, which is published on both DockerHub and GitHub Container Registry.

-   DockerHub: https://hub.docker.com/r/documenso/documenso
-   GitHub Container Registry: https://ghcr.io/documenso/documenso

You can pull the Docker image from either of these registries and run it with your preferred container hosting provider.

Please note that you will need to provide environment variables for connecting to the database, mailserver, and so forth.

For detailed instructions on how to configure and run the Docker container, please refer to the Docker README in the `docker` directory.

Self Hosting
------------

We support a variety of deployment methods, and are actively working on adding more. Stay tuned for updates!

### Fetch, configure, and build

First, clone the code from Github:

```
git clone https://github.com/documenso/documenso.git
```

Then, inside the `documenso` folder, copy the example env file:

```
cp .env.example .env
```

The following environment variables must be set:

-   `NEXTAUTH_SECRET`
-   `NEXT_PUBLIC_WEBAPP_URL`
-   `NEXT_PRIVATE_DATABASE_URL`
-   `NEXT_PRIVATE_DIRECT_DATABASE_URL`
-   `NEXT_PRIVATE_SMTP_FROM_NAME`
-   `NEXT_PRIVATE_SMTP_FROM_ADDRESS`

> If you are using a reverse proxy in front of Documenso, don't forget to provide the public URL for the `NEXT_PUBLIC_WEBAPP_URL` variable!

Now you can install the dependencies and build it:

```
npm i
npm run build
npm run prisma:migrate-deploy
```

Finally, you can start it with:

```
cd apps/remix
npm run start
```

This will start the server on `localhost:3000`. For now, any reverse proxy can then do the frontend and SSL termination.

> If you want to run with another port than 3000, you can start the application with `next -p <ANY PORT>` from the `apps/remix` folder.

### Run as a service

You can use a systemd service file to run the app. Here is a simple example of the service running on port 3500 (using 3000 by default):

\[Unit\]
Description=documenso
After=network.target

\[Service\]
Environment=PATH=/path/to/your/node/binaries
Type=simple
User=www-data
WorkingDirectory=/var/www/documenso/apps/remix
ExecStart=/usr/bin/next start -p 3500
TimeoutSec=15
Restart=always

\[Install\]
WantedBy=multi-user.target

### Railway

### Render

### Koyeb

Elestio
-------

Troubleshooting
---------------

### I'm not receiving any emails when using the developer quickstart.

When using the developer quickstart, an Inbucket server will be spun up in a docker container that will store all outgoing emails locally for you to view.

The Web UI can be found at http://localhost:9000, while the SMTP port will be on localhost:2500.

### Support IPv6

If you are deploying to a cluster that uses only IPv6, You can use a custom command to pass a parameter to the Remix start command

For local docker run

docker run -it documenso:latest npm run start -- -H ::

For k8s or docker-compose

containers:
  - name: documenso
    image: documenso:latest
    imagePullPolicy: IfNotPresent
    command:
      - npm
    args:
      - run
      - start
      - \--
      - \-H
      - '::'

### I can't see environment variables in my package scripts.

Wrap your package script with the `with:env` script like such:

```
npm run with:env -- npm run myscript
```

The same can be done when using `npx` for one of the bin scripts:

```
npm run with:env -- npx myscript
```

This will load environment variables from your `.env` and `.env.local` files.

Repo Activity
-------------
