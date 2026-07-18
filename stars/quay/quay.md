---
project: quay
stars: 2801
description: Build, Store, and Distribute your Applications and Containers
url: https://github.com/quay/quay
---

Project Quay
============

⚠️ The `master` branch may be in an _unstable or even broken state_ during development. Please use releases instead of the `master` branch in order to get stable software.

Project Quay builds, stores, and distributes your container images.

High-level features include:

-   Docker Registry Protocol v2
-   Docker Manifest Schema v2.1, v2.2
-   OCI spec v1.1 support oci
-   Authentication provided by LDAP, Keystone, OIDC, Google, and GitHub
-   ACLs, team management, and auditability logs
-   Geo-replicated storage provided by local filesystems, S3, GCS, Swift, Ceph and ODF
-   Continuous Integration integrated with GitHub, Bitbucket, GitLab, and git
-   Security Vulnerability Analysis via Clair
-   Swagger\-compliant HTTP API

Getting Started
---------------

-   Explore a live instance of Project Quay hosted at Quay.io
-   Watch talks given about Project Quay
-   Review the documentation for Red Hat Quay
-   Get up and running with our getting started guide for developing or deploying Quay
-   Deploy on Kubernetes using the Quay Operator

Community
---------

-   Mailing List: quay-sig@googlegroups.com
-   IRC: #quay on libera.chat
-   Bug tracking: Red Hat JIRA
-   Security Issues: See SECURITY.md
-   Community meetings held the first Wednesday of every month 11:00 AM EST: meeting link

License
-------

Project Quay is under the Apache 2.0 license. See the LICENSE file for details.

Contextification Addendum
-------------------------

### Repository Map

flowchart LR
    clients\[Docker, Podman, UI, API clients\]
    app\[Flask application\]
    api\[endpoints/api\]
    registry\[endpoints/v2\]
    data\[data/model and data/registry\_model\]
    db\[(PostgreSQL)\]
    redis\[(Redis)\]
    storage\[storage backends\]
    workers\[workers\]
    ui\[web/ and static/\]

    clients --> app
    app --> api
    app --> registry
    app --> ui
    api --> data
    registry --> data
    data --> db
    data --> redis
    registry --> storage
    workers --> data
    workers --> storage

Loading

Key paths: `data/database.py` is the schema source of truth, `endpoints/v2/` serves registry protocol traffic, `workers/` runs async jobs, `web/` is the React UI, and `config-tool/` validates config.

### Development Shortcuts

make local-dev-up
make local-dev-up-with-clair
TEST=true PYTHONPATH="." pytest path/to/test.py -v
make unit-test
make registry-test
make types-test

Local UI notes:

-   Legacy Angular UI (`static/`) is started by `make local-dev-up` and is available at `http://localhost:8080`.
    
-   New React UI (`web/`) runs separately at `http://localhost:9000`; after `make local-dev-up`, run:
    
    cd web
    npm install
    npm start
    
-   If backend code changes are not reflected in the local stack, restart the Quay container:
    
    podman restart quay-quay
    

Related repos: quay-operator, quay-builder, quay-tests, quay-fbcs, and quay-konflux-components.
