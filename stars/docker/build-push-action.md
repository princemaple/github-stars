---
project: build-push-action
stars: 5039
description: GitHub Action to build and push Docker images with Buildx
url: https://github.com/docker/build-push-action
---

About
-----

GitHub Action to build and push Docker images with Buildx with full support of the features provided by Moby BuildKit builder toolkit. This includes multi-platform build, secrets, remote cache, etc. and different builder deployment/namespacing options.

* * *

-   Usage
    -   Git context
    -   Path context
-   Examples
-   Summaries
-   Customizing
    -   inputs
    -   outputs
    -   environment variables
-   Troubleshooting
-   Contributing

Usage
-----

In the examples below we are also using 3 other actions:

-   `setup-buildx` action will create and boot a builder using by default the `docker-container` driver. This is **not required but recommended** using it to be able to build multi-platform images, export cache, etc.
-   `setup-qemu` action can be useful if you want to add emulation support with QEMU to be able to build against more platforms.
-   `login` action will take care to log in against a Docker registry.

### Git context

By default, this action uses the Git context, so you don't need to use the `actions/checkout` action to check out the repository as this will be done directly by BuildKit.

The git reference will be based on the event that triggered your workflow and will result in the following context: `https://github.com/<owner>/<repo>.git#<ref>`.

name: ci

on:
  push:

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      -
        name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ vars.DOCKERHUB\_USERNAME }}
          password: ${{ secrets.DOCKERHUB\_TOKEN }}
      -
        name: Set up QEMU
        uses: docker/setup-qemu-action@v3
      -
        name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3
      -
        name: Build and push
        uses: docker/build-push-action@v6
        with:
          push: true
          tags: user/app:latest

Be careful because **any file mutation in the steps that precede the build step will be ignored, including processing of the `.dockerignore` file** since the context is based on the Git reference. However, you can use the Path context using the `context` input alongside the `actions/checkout` action to remove this restriction.

Default Git context can also be provided using the Handlebars template expression `{{defaultContext}}`. Here we can use it to provide a subdirectory to the default Git context:

      -
        name: Build and push
        uses: docker/build-push-action@v6
        with:
          context: "{{defaultContext}}:mysubdir"
          push: true
          tags: user/app:latest

Building from the current repository automatically uses the GitHub Token, so it does not need to be passed. If you want to authenticate against another private repository, you have to use a secret named `GIT_AUTH_TOKEN` to be able to authenticate against it with Buildx:

      -
        name: Build and push
        uses: docker/build-push-action@v6
        with:
          push: true
          tags: user/app:latest
          secrets: |
            GIT\_AUTH\_TOKEN=${{ secrets.MYTOKEN }}

### Path context

name: ci

on:
  push:

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      -
        name: Checkout
        uses: actions/checkout@v5
      -
        name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ vars.DOCKERHUB\_USERNAME }}
          password: ${{ secrets.DOCKERHUB\_TOKEN }}
      -
        name: Set up QEMU
        uses: docker/setup-qemu-action@v3
      -
        name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3
      -
        name: Build and push
        uses: docker/build-push-action@v6
        with:
          context: .
          push: true
          tags: user/app:latest

Examples
--------

-   Multi-platform image
-   Secrets
-   Push to multi-registries
-   Manage tags and labels
-   Cache management
-   Export to Docker
-   Test before push
-   Validating build configuration
-   Local registry
-   Share built image between jobs
-   Named contexts
-   Copy image between registries
-   Update Docker Hub repo description
-   SBOM and provenance attestations
-   Annotations
-   Reproducible builds

Summaries
---------

This action generates a job summary that provides a detailed overview of the build execution. The summary shows an overview of all the steps executed during the build, including the build inputs and eventual errors.

The summary also includes a link for downloading the build record with additional details about the build, including build stats, logs, outputs, and more. The build record can be imported to Docker Desktop for inspecting the build in greater detail.

Warning

If you're using the `actions/download-artifact` action in your workflow, you need to ignore the build record artifacts if `name` and `pattern` inputs are not specified (defaults to download all artifacts of the workflow), otherwise the action will fail:

\- uses: actions/download-artifact@v4
  with:
    pattern: "!\*.dockerbuild"

More info: actions/toolkit#1874

Summaries are enabled by default, but can be disabled with the `DOCKER_BUILD_SUMMARY` environment variable.

For more information about summaries, refer to the documentation.

Customizing
-----------

### inputs

The following inputs can be used as `step.with` keys:

> `List` type is a newline-delimited string
> 
> cache-from: |
>   user/app:cache
>   type=local,src=path/to/dir

> `CSV` type is a comma-delimited string
> 
> tags: name/app:latest,name/app:1.0.0

Name

Type

Description

`add-hosts`

List/CSV

List of customs host-to-IP mapping (e.g., `docker:10.180.0.1`)

`allow`

List/CSV

List of extra privileged entitlement (e.g., `network.host,security.insecure`)

`annotations`

List

List of annotation to set to the image

`attests`

List

List of attestation parameters (e.g., `type=sbom,generator=image`)

`builder`

String

Builder instance (see setup-buildx action)

`build-args`

List

List of build-time variables

`build-contexts`

List

List of additional build contexts (e.g., `name=path`)

`cache-from`

List

List of external cache sources (e.g., `type=local,src=path/to/dir`)

`cache-to`

List

List of cache export destinations (e.g., `type=local,dest=path/to/dir`)

`call`

String

Set method for evaluating build (e.g., `check`)

`cgroup-parent`

String

Optional parent cgroup for the container used in the build

`context`

String

Build's context is the set of files located in the specified `PATH` or `URL` (default Git context)

`file`

String

Path to the Dockerfile. (default `{context}/Dockerfile`)

`labels`

List

List of metadata for an image

`load`

Bool

Load is a shorthand for `--output=type=docker` (default `false`)

`network`

String

Set the networking mode for the `RUN` instructions during build

`no-cache`

Bool

Do not use cache when building the image (default `false`)

`no-cache-filters`

List/CSV

Do not cache specified stages

`outputs`

List

List of output destinations (format: `type=local,dest=path`)

`platforms`

List/CSV

List of target platforms for build

`provenance`

Bool/String

Generate provenance attestation for the build (shorthand for `--attest=type=provenance`)

`pull`

Bool

Always attempt to pull all referenced images (default `false`)

`push`

Bool

Push is a shorthand for `--output=type=registry` (default `false`)

`sbom`

Bool/String

Generate SBOM attestation for the build (shorthand for `--attest=type=sbom`)

`secrets`

List

List of secrets to expose to the build (e.g., `key=string`, `GIT_AUTH_TOKEN=mytoken`)

`secret-envs`

List/CSV

List of secret env vars to expose to the build (e.g., `key=envname`, `MY_SECRET=MY_ENV_VAR`)

`secret-files`

List

List of secret files to expose to the build (e.g., `key=filename`, `MY_SECRET=./secret.txt`)

`shm-size`

String

Size of `/dev/shm` (e.g., `2g`)

`ssh`

List

List of SSH agent socket or keys to expose to the build

`tags`

List/CSV

List of tags

`target`

String

Sets the target stage to build

`ulimit`

List

Ulimit options (e.g., `nofile=1024:1024`)

`github-token`

String

GitHub Token used to authenticate against a repository for Git context (default `${{ github.token }}`)

### outputs

The following outputs are available:

Name

Type

Description

`imageid`

String

Image ID

`digest`

String

Image digest

`metadata`

JSON

Build result metadata

### environment variables

Name

Type

Default

Description

`DOCKER_BUILD_CHECKS_ANNOTATIONS`

Bool

`true`

If `false`, GitHub annotations are not generated for build checks

`DOCKER_BUILD_SUMMARY`

Bool

`true`

If `false`, build summary generation is disabled

`DOCKER_BUILD_RECORD_UPLOAD`

Bool

`true`

If `false`, build record upload as GitHub artifact is disabled

`DOCKER_BUILD_RECORD_RETENTION_DAYS`

Number

Duration after which build record artifact will expire in days. Defaults to repository/org retention settings if unset or `0`

`DOCKER_BUILD_EXPORT_LEGACY`

Bool

`false`

If `true`, exports build using legacy export-build tool instead of `buildx history export` command

Troubleshooting
---------------

See TROUBLESHOOTING.md

Contributing
------------

Want to contribute? Awesome! You can find information about contributing to this project in the CONTRIBUTING.md
