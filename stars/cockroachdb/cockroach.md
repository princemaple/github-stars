---
project: cockroach
stars: 31480
description: CockroachDB — the cloud native, distributed SQL database designed for high availability, effortless scale, and control over data placement.
url: https://github.com/cockroachdb/cockroach
---

* * *

CockroachDB is a cloud-native distributed SQL database designed to build, scale, and manage modern, data-intensive applications.

-   What is CockroachDB?
-   Docs
-   Starting with Cockroach Cloud
-   Starting with CockroachDB
-   Client Drivers
-   Deployment
-   Need Help?
-   Contributing
-   Design
-   Comparison with Other Databases
-   See Also

What is CockroachDB?
--------------------

CockroachDB is a distributed SQL database built on a transactional and strongly-consistent key-value store. It **scales** horizontally; **survives** disk, machine, rack, and even datacenter failures with minimal latency disruption and no manual intervention; supports **strongly-consistent** ACID transactions; and provides a familiar **SQL** API for structuring, manipulating, and querying data.

For more details, see our product overview, FAQ or architecture document.

Docs
----

For guidance on installation, development, deployment, and administration, see our User Documentation.

Starting with CockroachCloud
----------------------------

We can run CockroachDB for you, so you don't have to run your own cluster.

See our online documentation: Quickstart with CockroachCloud

Starting with CockroachDB
-------------------------

1.  Install CockroachDB: using a pre-built executable or build it from source.
2.  Start a local cluster and connect to it via the built-in SQL client.
3.  Learn more about CockroachDB SQL.
4.  Use a PostgreSQL-compatible driver or ORM to build an app with CockroachDB.
5.  Explore core features, such as data replication, automatic rebalancing, and fault tolerance and recovery.

Client Drivers
--------------

CockroachDB supports the PostgreSQL wire protocol, so you can use any available PostgreSQL client drivers to connect from various languages.

-   For recommended drivers that we've tested, see Install Client Drivers.
-   For tutorials using these drivers, as well as supported ORMs, see Example Apps.

Deployment
----------

-   CockroachCloud - Steps to create a free CockroachCloud cluster on your preferred Cloud platform.
-   Manual - Steps to deploy a CockroachDB cluster manually on multiple machines.
-   Cloud - Guides for deploying CockroachDB on various cloud platforms.
-   Orchestration - Guides for running CockroachDB with popular open-source orchestration systems.

Need Help?
----------

-   CockroachDB Community Slack - Join our slack to connect with our engineers and other users running CockroachDB.
-   CockroachDB Forum and Stack Overflow - Ask questions, find answers, and help other users.
-   Troubleshooting documentation - Learn how to troubleshoot common errors, cluster setup, and SQL query behavior.
-   For filing bugs, suggesting improvements, or requesting new features, help us out by opening an issue.

Building from source
--------------------

See our wiki for more details.

Contributing
------------

We welcome your contributions! If you're looking for issues to work on, try looking at the good first issue list. We do our best to tag issues suitable for new external contributors with that label, so it's a great way to find something you can help with!

See our wiki for more details.

Engineering discussions take place on our public mailing list, cockroach-db@googlegroups.com. Also please join our Community Slack (there's a dedicated #contributors channel!) to ask questions, discuss your ideas, and connect with other contributors.

Design
------

For an in-depth discussion of the CockroachDB architecture, see our Architecture Guide. For the original design motivation, see our design doc.

Licensing
---------

All versions released after November 18, 2024, including patch fixes for prior versions 23.1 onward, are published under the CockroachDB Software License (CSL). Source code in a given file is licensed under the CSL and the copyright belongs to The Cockroach Authors unless otherwise noted in the file or in a LICENSE or README file located in the same or parent directory of the file.

Comparison with Other Databases
-------------------------------

To see how key features of CockroachDB stack up against other databases, check out CockroachDB in Comparison.

See Also
--------

-   Tech Talks (by CockroachDB founders, engineers, and customers!)
-   CockroachDB User Documentation
-   The CockroachDB Blog
-   Key design documents
    -   Serializable, Lockless, Distributed: Isolation in CockroachDB
    -   Consensus, Made Thrive
    -   Trust, But Verify: How CockroachDB Checks Replication
    -   Living Without Atomic Clocks
    -   The CockroachDB Architecture Document
