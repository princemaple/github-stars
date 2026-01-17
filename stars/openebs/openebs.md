---
project: openebs
stars: 9586
description: A popular & widely deployed Open Source Container Native Storage platform for Stateful Persistent Applications on Kubernetes.
url: https://github.com/openebs/openebs
---

OpenEBS - Cloud Native Storage
------------------------------

Overview
--------

OpenEBS is an open-source Container Native Storage solution that provides persistent storage for Kubernetes workloads. It enables dynamic provisioning of storage resources using containerized storage controllers, making it highly flexible and cloud-native. OpenEBS supports various storage engines, including LocalPVs for direct node storage and Replicated PV advanced data replication and resilience. It is designed to integrate seamlessly with Kubernetes, offering benefits like storage policies, resize, thin-provisioning, snapshots, and restore capabilities, making it an ideal choice for stateful applications.

OpenEBS offers two primary storage approaches for Kubernetes workloads: Local Storage and Replicated Storage. Below is a comparative overview:

Feature

Local Storage

Replicated Storage

**Data Availability**

Limited to the node where the volume is provisioned; not suitable for high-availability requirements.

Synchronously replicates data across multiple nodes, ensuring high availability and durability.

**Use Cases**

Ideal for applications managing their own replication and availability, such as distributed databases like MongoDB and Cassandra.

Suitable for stateful workloads requiring storage-level replication and high availability, like Percona/ Standalone DBs, and GitLab.

**Performance**

Provides near-disk performance with minimal overhead.

Designed for high performance, leveraging NVMe-oF semantics for low-latency access.

**Limitations**

Not highly available; node failure leads to data unavailability.

Requires sufficient resources (CPU, RAM, NVMe) for optimal performance.

**Snapshot and Cloning**

Supported when backed by advanced filesystems like LVM or ZFS.

Supported, providing enterprise storage capabilities.

**Backup and Restore**

Supported via Velero, using Restic for local volumes.

Supported via Velero, ensuring data protection and recovery.

In summary, **Local Storage** is a good choice when your application can manage its own replication and high availability, and **Replicated Storage** when you require storage-level replication, enhanced data durability and network-based storage access.

Below are the sub-projects or the major storage solutions under the OpenEBS Umbrella. Visit the individual repositories to learn more about their usage and architecture.

Sub-Project

Local PV Hostpath

Local PV ZFS

Local PV LVM

Local PV Rawfile (_**Experimental**_)

Mayastor

Type

Single-node

Single-node

Single-node

Single-node

Multi-node

What is it for?

Replacement for in-Tree Kubernetes CSI Hostpath

Storage engine for ZFS managed backend storage

Storage engine for LVM2 managed backend storage

Experimental engine for using an extent file as block storage

General purpose replicated enterprise storage

Designed for

Developers or DevOps

ZFS users and production deployments

LVM2 users and production deployments

Developers

Enterprises and production deployments

Features

Everything in Kubernetes Hostpath, plus: - Dynamic provisioning, Zero configuration, No CSI driver

Provision ZFS datasets, Provision ZFS volumes, Dynamic provisioning, ZFS resilience, ZFS RAID protection, CSI driver

Provision LVM2 volumes, Dynamic provisioning, LVM2 RAID protection, CSI driver

Provision file system from local files as persistent volumes, CSI driver

Replicated storage NVMe / RDMA, Snapshots, Clones, High availability, CSI driver

Status

Stable, deployable in PROD

Stable, deployable in PROD

Stable, deployable in PROD

Beta, undergoing evaluation & integration

Stable, deployable in PROD

Current Version

release v0.80

### Why OpenEBS?

OpenEBS offers several compelling advantages for managing storage in Kubernetes environments:

-   **Cloud-Native Architecture**: Designed as a cloud-native solution, OpenEBS integrates seamlessly with Kubernetes, most of the storage engines are CSI compliant.
-   **Solutions for wide range of workloads**: Solutions for both workloads which need or may not need replication.
-   **Avoidance of Cloud Lock-In**: By abstracting storage management, OpenEBS facilitates the movement of data across various Kubernetes environments, whether on-premises or in the cloud, thereby reducing dependency on a single cloud provider.
-   **Cost Efficiency**: With features like thin provisioning OpenEBS enables dynamic allocation of storage resources, potentially reducing storage by preventing overprovisioning and allowing for on-the-fly storage expansion.
-   **High Availability with Lower Blast Radius**: OpenEBS enhances application resilience by synchronously replicating data across multiple nodes, ensuring high availability. In the event of a node failure, only the data on that specific node is affected, minimizing the impact on the overall system.

These features make OpenEBS a robust and flexible solution for managing persistent storage in Kubernetes environments.

### Documents

-   Official Documentation
-   Governance Documentation
-   Contributing to OpenEBS
-   OpenEBS Security Guidelines
-   Release Process
-   Roadmap Tracker

### Community

-   Homepage: openebs.io
-   Maintainers' email: openebs-team@googlegroups.com
-   Slack:
    -   #openebs
    -   #openebs-dev
-   Twitter: @openebs
-   Community Meeting: OpenEBS holds a monthly community meeting via Zoom on the last Thursday of the month, at 14:00 UTC.
    -   Add to calendar
-   Community Meeting Recordings: Youtube

Star History
------------

Activity dashboard
------------------

License Compliance
------------------

OpenEBS is a CNCF Sandbox Project
---------------------------------
