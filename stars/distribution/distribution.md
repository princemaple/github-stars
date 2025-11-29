---
project: distribution
stars: 10069
description: The toolkit to pack, ship, store, and deliver container content
url: https://github.com/distribution/distribution
---

The toolset to pack, ship, store, and deliver content.

This repository's main product is the Open Source Registry implementation for storing and distributing container images and other content using the OCI Distribution Specification. The goal of this project is to provide a simple, secure, and scalable base for building a large scale registry solution or running a simple private registry. It is a core library for many registry operators including Docker Hub, GitHub Container Registry, GitLab Container Registry and DigitalOcean Container Registry, as well as the CNCF Harbor Project, and VMware Harbor Registry.

This repository contains the following components:

**Component**

Description

**registry**

An implementation of the OCI Distribution Specification.

**libraries**

A rich set of libraries for interacting with distribution components. Please see godoc for details. **Note**: The interfaces for these libraries are **unstable**.

**documentation**

Full documentation is available at https://distribution.github.io/distribution.

### How does this integrate with Docker, containerd, and other OCI client?

Clients implement against the OCI specification and communicate with the registry using HTTP. This project contains a client implementation which is currently in use by Docker, however, it is deprecated for the implementation in containerd and will not support new features.

### What are the long term goals of the Distribution project?

The _Distribution_ project has the further long term goal of providing a secure tool chain for distributing content. The specifications, APIs and tools should be as useful with Docker as they are without.

Our goal is to design a professional grade and extensible content distribution system that allow users to:

-   Enjoy an efficient, secured and reliable way to store, manage, package and exchange content
-   Hack/roll their own on top of healthy open-source components
-   Implement their own home made solution through good specs, and solid extensions mechanism.

Contribution
------------

Please see CONTRIBUTING.md for details on how to contribute issues, fixes, and patches to this project. If you are contributing code, see the instructions for building a development environment.

Communication
-------------

For async communication and long running discussions please use issues and pull requests on the github repo. This will be the best place to discuss design and implementation.

For sync communication we have a #distribution channel in the CNCF Slack that everyone is welcome to join and chat about development.

Licenses
--------

The distribution codebase is released under the Apache 2.0 license. The README.md file, and files in the "docs" folder are licensed under the Creative Commons Attribution 4.0 International License. You may obtain a copy of the license, titled CC-BY-4.0, at http://creativecommons.org/licenses/by/4.0/.
