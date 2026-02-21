---
project: flux2
stars: 7893
description: Open and extensible continuous delivery solution for Kubernetes. Powered by GitOps Toolkit.
url: https://github.com/fluxcd/flux2
---

Flux version 2
==============

Flux is a tool for keeping Kubernetes clusters in sync with sources of configuration (like Git repositories and OCI artifacts), and automating updates to configuration when there is new code to deploy.

Flux version 2 ("v2") is built from the ground up to use Kubernetes' API extension system, and to integrate with Prometheus and other core components of the Kubernetes ecosystem. In version 2, Flux supports multi-tenancy and support for syncing an arbitrary number of Git repositories, among other long-requested features.

Flux v2 is constructed with the GitOps Toolkit, a set of composable APIs and specialized tools for building Continuous Delivery on top of Kubernetes.

Flux is a Cloud Native Computing Foundation (CNCF) graduated project, used in production by various organisations and cloud providers.

Quickstart and documentation
----------------------------

To get started check out this guide on how to bootstrap Flux on Kubernetes and deploy a sample application in a GitOps manner.

For more comprehensive documentation, see the following guides:

-   Ways of structuring your repositories
-   Manage Helm Releases
-   Automate image updates to Git
-   Manage Kubernetes secrets with Flux and SOPS

If you need help, please refer to our **Support page**.

GitOps Toolkit
--------------

The GitOps Toolkit is the set of APIs and controllers that make up the runtime for Flux v2. The APIs comprise Kubernetes custom resources, which can be created and updated by a cluster user, or by other automation tooling.

You can use the toolkit to extend Flux, or to build your own systems for continuous delivery -- see the developer guides.

### Components

-   Source Controllers
    -   GitRepository CRD
    -   OCIRepository CRD
    -   HelmRepository CRD
    -   HelmChart CRD
    -   Bucket CRD
    -   ExternalArtifact CRD
    -   ArtifactGenerator CRD
-   Kustomize Controller
    -   Kustomization CRD
-   Helm Controller
    -   HelmRelease CRD
-   Notification Controller
    -   Provider CRD
    -   Alert CRD
    -   Receiver CRD
-   Image Automation Controllers
    -   ImageRepository CRD
    -   ImagePolicy CRD
    -   ImageUpdateAutomation CRD

Community
---------

Need help or want to contribute? Please see the links below. The Flux project is always looking for new contributors and there are a multitude of ways to get involved.

-   Getting Started?
    -   Look at our Get Started guide and give us feedback
-   Need help?
    -   First: Ask questions on our GH Discussions page.
    -   Second: Talk to us in the #flux channel on CNCF Slack.
    -   Please follow our Support Guidelines (in short: be nice, be respectful of volunteers' time, understand that maintainers and contributors cannot respond to all DMs, and keep discussions in the public #flux channel as much as possible).
-   Have feature proposals or want to contribute?
    -   Propose features on our GitHub Discussions page.
    -   Join our upcoming dev meetings (meeting access and agenda).
    -   Join the flux-dev mailing list.
    -   Check out how to contribute to the project.
    -   Check out the project roadmap.

### Events

Check out our **events calendar**, both with upcoming talks, events and meetings you can attend. Or view the **resources section** with past events videos you can watch.

We look forward to seeing you with us!
