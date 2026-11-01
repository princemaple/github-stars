---
project: scanopy
stars: 5921
description: Network diagrams that update themselves
url: https://github.com/scanopy/scanopy
---

Scanopy
=======

**Never maintain another network diagram.** Scanopy scans your network on a schedule and draws it as four views: L2, L3, workloads and applications.

curl -O https://raw.githubusercontent.com/scanopy/scanopy/refs/heads/main/docker-compose.yml
docker compose up -d

Open `http://<your-server-ip>:60072` and create your account. The first discovery starts on its own.

Prefer a hosted version? Try **Scanopy Cloud**. Full setup options are in the **docs**.

  
  

Scanopy replaces manual network diagrams with a continuously maintained model of what's actually running. A single daemon scans on a schedule and produces four views from each scan: L2 (physical), L3 (logical), workloads, and applications. Unlike diagrams drawn in draw.io that go stale the week they're saved, or IaC state that misses drift and resources provisioned outside the pipeline, Scanopy reflects the current state of your infrastructure. Export as SVG, Mermaid, or Confluence; embed live maps; or feed the model into your existing source of truth.

> 🏢 **Running Scanopy for your business?** The Commercial Edition adds a commercial license, more networks and seats, Confluence export, and support, all on your own infrastructure.

**L2 (Physical)**  
Every switch, every port, every link.

**L3 (Logical)**  
Subnets and how hosts connect across them.

**Workloads**  
Bare metal to hypervisors to containers.

**Applications**  
Services and their dependencies, grouped by application.

✨ Features
----------

**Map**

-   **Network topology**: Physical (L2) links port to port from LLDP, CDP, and switch forwarding tables, and logical (L3) topology subnet by subnet.
-   **Workload mapping**: VMs nested in their hypervisor, and containers inside the host that runs them.
-   **Application dependency mapping**: Tag each server with its application once and the map fills in its services. You mark the dependencies between them.

**Inventory**

-   **Device inventory**: Every host with its IP and MAC addresses, interfaces, open ports, services, and SNMP hardware facts. Search everything with `/`, filter by site or tag, and export to CSV or read it through the REST API.
-   **410+ service definitions**: Identifies databases, web servers, printers, cameras, and industrial devices (Modbus TCP, EtherNet/IP, OPC UA, BACnet) by open ports, service responses, and MAC vendor.
-   **VLANs & subnets**: Reads VLAN tables from your switches over SNMP, shows native and tagged VLANs per port, and links each VLAN to its subnets.

**Track & share**

-   **Scan digests and snapshots**: An email after each scheduled scan lists new, stale, and changed hosts. Snapshots record the network on a date for audits and change windows.
-   **Sharing, embeds & exports**: Read-only links with a password and expiry, live embeds in a wiki, and exports to image, document, diagram, and wiki formats.

**Discovery**

-   **No agent per device**: A daemon on Linux, macOS, Windows, or Docker scans the networks it can reach. Deploy as many as your segments need, each on its own schedule, at the rate and subnet scope you set.
-   **Integrations**: Docker, Aruba Instant On, Podman, Proxmox VE, UniFi Controller, Wake-on-LAN, SNMP, SSH, and gNMI.
-   **Multi-user + RBAC**: Admin, member, and viewer roles, scoped per site.

🎯 Built for teams that manage infrastructure
---------------------------------------------

-   **IT operations**: Network architecture and physical topology, current after every scan, across every site.
-   **MSPs**: Per-client documentation with read-only portals. No logins required.
-   **Security & compliance**: Segmentation validation and audit-ready documentation for NIS2, ISO 27001, HIPAA, and CMMC.
-   **Platform & DevOps**: Service dependencies and workload placement without APM instrumentation.

Use cases: compliance, multi-site networks, shadow IT discovery, plant & OT networks, handover & onboarding.

📋 Editions and Licensing
-------------------------

Every edition runs on your own infrastructure, so discovery data, topology and credentials stay inside your network.

-   **Community Edition (AGPL-3.0):** free and open source. AGPL-3.0 requires source disclosure for network services and copyleft compliance.
-   **Commercial Edition (Self-Hosted Standard, Self-Hosted Plus, Enterprise):** a commercial license for organizations that can't meet AGPL-3.0's terms or need more networks and seats. Adds Confluence export, invoice billing, procurement documents and support. Self-Hosted Plus adds multiple organizations, and Plus and Enterprise add offline license keys for air-gapped networks.

**Compare editions and get a commercial license**, or email licensing@scanopy.net.

Prefer not to run it yourself? Scanopy Cloud runs the same engine as a hosted service.

🚀 Quick Start for Self Hosting
-------------------------------

**Docker Compose**

curl -O https://raw.githubusercontent.com/scanopy/scanopy/refs/heads/main/docker-compose.yml
docker compose up -d

**Proxmox**

Use this helper script to create a Scanopy LXC.

**Unraid**

Available as an Unraid community app.

* * *

Access the UI at `http://<your-server-ip>:60072`, create your account, and wait for the first discovery to complete.

Have a commercial license? See Installing a Self-Hosted Server.

For detailed setup options and configuration, see the Installation Guide.

📚 Documentation + API
----------------------

**scanopy.net/docs**

🚀 Demo
-------

**demo.scanopy.net**. Hosted demo app with a sample dataset. Try the full UI without installing anything.

🤝 Contributing
---------------

We welcome contributions! See our contributing guide for details.

Great first contributions:

-   Adding service definitions
-   Translating Scanopy into your language

💬 Community & Support
----------------------

-   **Discord**: Join our Discord for help and discussions
-   **Issues**: Report bugs or request features
-   **Discussions**: GitHub Discussions

* * *

**Translations powered by Weblate**

**Built with ❤️ in NYC**
