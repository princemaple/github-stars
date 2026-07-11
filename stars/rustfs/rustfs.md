---
project: rustfs
stars: 29727
description: 🚀2.3x faster than MinIO for 4KB object payloads. RustFS is an open-source, S3-compatible high-performance object storage system supporting migration and coexistence with other S3-compatible platforms such as MinIO and Ceph.
url: https://github.com/rustfs/rustfs
---

RustFS is a high-performance, distributed object storage system built in Rust.

Getting Started · Docs · Bug reports · Discussions

English | 简体中文 | Deutsch | Español | français | 日本語 | 한국어 | Portuguese | Русский

RustFS is a high-performance, distributed object storage system built in Rust—one of the most loved programming languages worldwide. RustFS combines the simplicity of MinIO with the memory safety and raw performance of Rust. It offers broad S3 API compatibility for supported features, is completely open-source, and is optimized for data lakes, AI, and big data workloads.

Unlike other storage systems, RustFS is released under the permissible Apache 2.0 license, avoiding the restrictions of AGPL. With Rust as its foundation, RustFS delivers superior speed and secure distributed features for next-generation object storage.

Feature & Status
----------------

-   **High Performance**: Built with Rust to ensure maximum speed and resource efficiency.
-   **Distributed Architecture**: Scalable and fault-tolerant design suitable for large-scale deployments.
-   **S3 Compatibility**: Seamless integration with common S3-compatible applications and tools; current coverage is tracked in the S3 compatibility matrix.
-   **OpenStack Swift API**: Native support for Swift protocol with Keystone authentication.
-   **OpenStack Keystone Integration**: Native support for OpenStack Keystone authentication with X-Auth-Token headers.
-   **Data Lake Support**: Optimized for high-throughput big data and AI workloads.
-   **Open Source**: Licensed under Apache 2.0, encouraging unrestricted community contributions and commercial usage.
-   **User-Friendly**: Designed with simplicity in mind for easy deployment and management.

Feature

Status

Feature

Status

**S3 Core Features**

✅ Available

**Bitrot Protection**

✅ Available

**Upload / Download**

✅ Available

**Single Node Mode**

✅ Available

**Versioning**

✅ Available

**Bucket Replication**

✅ Available

**Logging**

✅ Available

**Lifecycle Management**

🚧 Under Testing

**Event Notifications**

✅ Available

**Distributed Mode**

🚧 Under Testing

**K8s Helm Charts**

✅ Available

**RustFS KMS**

🚧 Under Testing

**Keystone Auth**

✅ Available

**Multi-Tenancy**

✅ Available

**Swift API**

✅ Available

**Swift Metadata Ops**

🚧 Partial

RustFS vs MinIO Performance
---------------------------

**Stress Test Environment:**

Type

Parameter

Remark

CPU

2 Core

Intel Xeon (Sapphire Rapids) Platinum 8475B, 2.7/3.2 GHz

Memory

4GB

Network

15Gbps

Drive

40GB x 4

IOPS 3800 / Drive

rustfs.mp4

### RustFS vs Other Object Storage

Feature

RustFS

Other Object Storage

**Console Experience**

**Powerful Console**  
Comprehensive management interface.

**Basic / Limited Console**  
Often overly simple or lacking critical features.

**Language & Safety**

**Rust-based**  
Memory safety by design.

**Go or C-based**  
Potential for memory GC pauses or leaks.

**Data Sovereignty**

**No Telemetry / Full Compliance**  
Guards against unauthorized cross-border data egress. Compliant with GDPR (EU/UK), CCPA (US), and APPI (Japan).

**Potential Risk**  
Possible legal exposure and unwanted data telemetry.

**Licensing**

**Permissive Apache 2.0**  
Business-friendly, no "poison pill" clauses.

**Restrictive AGPL v3**  
Risk of license traps and intellectual property pollution.

**Compatibility**

**S3-Compatible Core**  
Works with common S3-compatible clients, with coverage tracked in the compatibility matrix.

**Variable Compatibility**  
May lack support for local cloud vendors or specific APIs.

**Edge & IoT**

**Strong Edge Support**  
Ideal for secure, innovative edge devices.

**Weak Edge Support**  
Often too heavy for edge gateways.

**Risk Profile**

**Enterprise Risk Mitigation**  
Clear IP rights and safe for commercial use.

**Legal Risks**  
Intellectual property ambiguity and usage restrictions.

Staying ahead
-------------

Star RustFS on GitHub and be instantly notified of new releases.

Quickstart
----------

To get started with RustFS, follow these steps:

### 1\. One-click Installation (Option 1)

curl -O https://rustfs.com/install\_rustfs.sh && bash install\_rustfs.sh

### 2\. Docker Quick Start (Option 2)

The RustFS container runs as a non-root user `rustfs` (UID/GID `10001:10001`). If you bind-mount host directories with Docker or Compose, every mounted path must be writable by that user, otherwise startup may fail with permission denied errors. This applies to data directories, log directories, and TLS certificate directories when `RUSTFS_TLS_PATH` is enabled.

# Create data and logs directories
mkdir -p data logs

# Change the owner of these directories
chown -R 10001:10001 data logs

# Using latest version
docker run -d -p 9000:9000 -p 9001:9001 -v $(pwd)/data:/data -v $(pwd)/logs:/logs rustfs/rustfs:latest

# Using specific version
docker run -d -p 9000:9000 -p 9001:9001 -v $(pwd)/data:/data -v $(pwd)/logs:/logs rustfs/rustfs:1.0.0-beta.8

If you use podman instead of docker, you can install the RustFS with the below command

# Create data and logs directories
mkdir -p data logs

# Run the container (podman will automatically set the folders ownership)
podman run -d -p 9000:9000 -p 9001:9001 -v $(pwd)/data:/data:Z,U -v $(pwd)/logs:/logs:Z,U rustfs/rustfs:latest

If you enable TLS with a bind-mounted certificate directory, prepare that mount the same way:

mkdir -p certs
chown -R 10001:10001 certs

You can also use Docker Compose. Using the `docker-compose-simple.yml` file in the root directory:

docker compose -f docker-compose-simple.yml up -d

Before running Compose with host bind mounts:

-   Ensure every mounted host path is writable by `10001:10001`.
-   If you enable TLS, ensure the certificate mount for `/opt/tls` is also readable by `10001:10001`.
-   If matching host ownership is not practical, run the `rustfs` service with `user: "<host-uid>:<host-gid>"` instead.
-   `docker-compose-simple.yml` includes a `volume-permission-helper` service for named volumes. `docker-compose-simple.yml` relies on you to prepare bind-mounted host paths in advance.

Similarly, you can run the command with podman

podman compose -f docker-compose-simple.yml up -d

Webhook notification quick start (Docker):

docker run -d --name rustfs -p 9000:9000 \\
  -e RUSTFS\_NOTIFY\_ENABLE=true \\
  -e RUSTFS\_NOTIFY\_WEBHOOK\_ENABLE\_PRIMARY=on \\
  -e RUSTFS\_NOTIFY\_WEBHOOK\_ENDPOINT\_PRIMARY=http://<host-ip\>:3020/webhook \\
  -e RUSTFS\_NOTIFY\_WEBHOOK\_QUEUE\_DIR\_PRIMARY=/tmp/rustfs-events \\
  rustfs/rustfs:latest

Notes:

-   `RUSTFS_NOTIFY_ENABLE=true` enables the global notify module switch.
-   For ARN `arn:rustfs:sqs::primary:webhook`, use instance-scoped env vars with `_PRIMARY`.
-   If queue dir is omitted, default is `/opt/rustfs/events`; ensure it is writable by the container runtime user.
-   `RUSTFS_NOTIFY_WEBHOOK_SKIP_TLS_VERIFY_PRIMARY` defaults to `false`; enabling it skips webhook TLS certificate verification, allows MITM attacks, and emits a startup warning. Prefer `RUSTFS_NOTIFY_WEBHOOK_CLIENT_CA_PRIMARY` for private CAs.

**NOTE**: We recommend reviewing the `docker-compose.yml` file before running. It defines several services including Grafana, Prometheus, and Jaeger, which are helpful for RustFS observability. If you wish to start Redis or Nginx containers, you can specify the corresponding profiles.

### 3\. Build from Source (Option 3) - Advanced Users

For developers who want to build RustFS Docker images from source with multi-architecture support:

# Build multi-architecture images locally
./docker-buildx.sh --build-arg RELEASE=latest

# Build and push to registry
./docker-buildx.sh --push

# Build specific version
./docker-buildx.sh --release v1.0.0 --push

# Build for custom registry
./docker-buildx.sh --registry your-registry.com --namespace yourname --push

The `docker-buildx.sh` script supports:

-   **Multi-architecture builds**: `linux/amd64`, `linux/arm64`
-   **Automatic version detection**: Uses git tags or commit hashes
-   **Registry flexibility**: Supports Docker Hub, GitHub Container Registry, etc.
-   **Build optimization**: Includes caching and parallel builds

You can also use Make targets for convenience:

make docker-buildx                    # Build locally
make docker-buildx-push               # Build and push
make docker-buildx-version VERSION=v1.0.0  # Build specific version
make help-docker                      # Show all Docker-related commands

> **Heads-up (macOS cross-compilation)**: macOS keeps the default `ulimit -n` at 256, so `cargo zigbuild` or `./build-rustfs.sh --platform ...` may fail with `ProcessFdQuotaExceeded` when targeting Linux. The build script attempts to raise the limit automatically, but if you still see the warning, run `ulimit -n 4096` (or higher) in your shell before building.

### 4\. Build with Helm Chart (Option 4) - Cloud Native

Follow the instructions in the Helm Chart README to install RustFS on a Kubernetes cluster.

For scanner pacing, cycle budgets, bitrot cadence, lifecycle transition status, and single-node single-disk idle CPU tuning, see Scanner Runtime Controls. For repeatable scanner-pressure validation, see Scanner Benchmark Runbook.

### 5\. Nix Flake (Option 5)

If you have Nix with flakes enabled:

# Run directly without installing
nix run github:rustfs/rustfs

# Build the binary
nix build github:rustfs/rustfs
./result/bin/rustfs --help

# Or from a local checkout
nix build
nix run

### 6\. X-CMD (Option 6)

If you are an x-cmd user:

# Run directly without installing
x rustfs

# Download the binary and install it to the global environment
x env use rustfs
rustfs --help

* * *

### Accessing RustFS

1.  **Access the Console**: Open your web browser and navigate to `http://localhost:9001` to access the RustFS console.
    -   Default credentials: `rustfsadmin` / `rustfsadmin`
2.  **Create a Bucket**: Use the console to create a new bucket for your objects.
3.  **Upload Objects**: You can upload files directly through the console or use S3-compatible APIs/clients to interact with your RustFS instance.

**NOTE**: To access the RustFS instance via `https`, please refer to the TLS Configuration Docs.

### OIDC Roles Claim (Microsoft Entra ID)

RustFS supports mapping an OIDC claim containing role values into the existing authorization pipeline. The `roles_claim` setting is **optional**: when unset or empty, only the `groups` claim contributes to authorization (same as older RustFS releases). For Microsoft Entra ID app roles, set `roles_claim=roles` so both console admin checks and bucket IAM policies can evaluate those roles.

Example environment configuration (opt-in roles claim):

RUSTFS\_IDENTITY\_OPENID\_ENABLE=on
RUSTFS\_IDENTITY\_OPENID\_CONFIG\_URL="https://login.microsoftonline.com/<tenant-id>/v2.0/.well-known/openid-configuration"
RUSTFS\_IDENTITY\_OPENID\_CLIENT\_ID="<client-id>"
RUSTFS\_IDENTITY\_OPENID\_CLIENT\_SECRET="<client-secret>"
RUSTFS\_IDENTITY\_OPENID\_SCOPES="openid,profile,email"
RUSTFS\_IDENTITY\_OPENID\_GROUPS\_CLAIM="groups"
RUSTFS\_IDENTITY\_OPENID\_ROLES\_CLAIM="roles"

Policy condition example (evaluate app roles directly with `jwt:roles`; when `roles_claim` is configured, RustFS also merges those values into `jwt:groups` for backward compatibility with older policies):

{
  "Version": "2012-10-17",
  "Statement": \[
    {
      "Effect": "Allow",
      "Action": \["admin:\*"\],
      "Resource": \["arn:aws:s3:::\*"\],
      "Condition": {
        "ForAnyValue:StringEquals": {
          "jwt:roles": \["RustFS.ConsoleAdmin"\]
        }
      }
    }
  \]
}

Documentation
-------------

For detailed documentation, including configuration options, API references, and advanced usage, please visit our Documentation.

Getting Help
------------

If you have any questions or need assistance:

-   Check the FAQ for common issues and solutions.
-   Join our GitHub Discussions to ask questions and share your experiences.
-   Open an issue on our GitHub Issues page for bug reports or feature requests.

Links
-----

-   Documentation - The manual you should read
-   Changelog - What we broke and fixed
-   GitHub Discussions - Where the community lives
-   Discord - Chat with the RustFS community

Contact
-------

-   **Bugs**: GitHub Issues
-   **Business**: hello@rustfs.com
-   **Jobs**: jobs@rustfs.com
-   **General Discussion**: GitHub Discussions
-   **Contributing**: CONTRIBUTING.md

Contributors
------------

RustFS is a community-driven project, and we appreciate all contributions. Check out the Contributors page to see the amazing people who have helped make RustFS better.

Star History
------------

License
-------

Apache 2.0

**RustFS** is a trademark of RustFS, Inc. All other trademarks are the property of their respective owners.
