---
project: portainer
stars: 37767
description: Making Docker and Kubernetes management easy.
url: https://github.com/portainer/portainer
---

**Portainer Community Edition** is a lightweight service delivery platform for containerized applications that can be used to manage Docker, Swarm, Kubernetes and ACI environments. It is designed to be as simple to deploy as it is to use. The application allows you to manage all your orchestrator resources (containers, images, volumes, networks and more) through a ‘smart’ GUI and/or an extensive API.

Portainer consists of a single container that can run on any cluster. It can be deployed as a Linux container or a Windows native container.

**Portainer Business Edition** builds on the open-source base and includes a range of advanced features and functions (like RBAC and Support) that are specific to the needs of business users.

-   Compare Portainer CE and Compare Portainer BE
-   Take3 – get 3 free nodes of Portainer Business for as long as you want them
-   Portainer BE install guide

Latest Version
--------------

Portainer CE is updated regularly. We aim to do an update release every couple of months.

Getting started
---------------

-   Deploy Portainer
-   Documentation
-   Contribute to the project

Features & Functions
--------------------

View this table to see all of the Portainer CE functionality and compare to Portainer Business.

Getting help
------------

Portainer CE is an open source project and is supported by the community. You can buy a supported version of Portainer at portainer.io

Learn more about Portainer's community support channels here.

-   Issues: https://github.com/portainer/portainer/issues
-   Slack (chat): https://portainer.io/slack

You can join the Portainer Community by visiting https://www.portainer.io/join-our-community. This will give you advance notice of events, content and other related Portainer content.

Reporting bugs and contributing
-------------------------------

-   Want to report a bug or request a feature? Please open an issue.
-   Want to help us build **_portainer_**? Follow our contribution guidelines to build it locally and make a pull request.

Generating API types
--------------------

The frontend consumes a TypeScript API client (SDK functions and request/response types) that is generated from the Go API's Swagger annotations. Regenerate it after any API change — a new endpoint, a changed request/response shape, or a removed endpoint:

make generate-api

This runs the following pipeline:

```
Go Swagger annotations
  → dist/docs/swagger.yaml       (make docs-build, via swaggo/swag)
  → dist/docs/openapi.yaml       (swagger2openapi + validation)
  → app/react/portainer/generated-api/portainer/   (hey-api/openapi-ts)
```

The generator is configured in `openapi-ts.config.ts`, which controls the output path, plugins, and tag filters (for example, `deprecated` endpoints and `edge_agent`\-tagged routes are excluded).

The generated files live in `app/react/portainer/generated-api/portainer/` and must **not** be edited by hand — your changes would be overwritten on the next run. Import the generated SDK functions and types instead of writing direct HTTP calls:

-   `@api/sdk.gen` — SDK functions
-   `@api/types.gen` — request/response types

See Adding api docs for how to annotate handlers so they are picked up by the generator.

Security
--------

For information about reporting security vulnerabilities, please see our Security Policy.

Work for us
-----------

If you are a developer, and our code in this repo makes sense to you, we would love to hear from you. We are always on the hunt for awesome devs, either freelance or employed. Drop us a line to success@portainer.io with your details and/or visit our careers page.

Privacy
-------

**To make sure we focus our development effort in the right places we need to know which features get used most often. To give us this information we use Matomo Analytics, which is hosted in Germany and is fully GDPR compliant.**

When Portainer first starts, you are given the option to DISABLE analytics. If you **don't** choose to disable it, we collect anonymous usage as per our privacy policy. **Please note**, there is no personally identifiable information sent or stored at any time and we only use the data to help us improve Portainer.

Limitations
-----------

Portainer supports "Current - 2 docker versions only. Prior versions may operate, however these are not supported.

Licensing
---------

Portainer is licensed under the zlib license. See LICENSE for reference.

Portainer also contains code from open source projects. See ATTRIBUTIONS.md for a list.
