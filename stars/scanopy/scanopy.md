---
project: scanopy
stars: 2501
description: Clean network diagrams. One-time setup, zero upkeep.
url: https://github.com/scanopy/scanopy
---

Scanopy
=======

**Clean network diagrams. One-time setup, zero upkeep.**

Scanopy scans your network, identifies hosts and services, and generates an interactive visualization showing how everything connects, letting you easily create and maintain network documentation.

  
  
  
  

> 💡 **Prefer not to self-host?** Get a free trial of Scanopy Cloud

✨ Key Features
--------------

-   **Automatic Discovery**: Scans networks to identify hosts, services, and their relationships
-   **200+ Service Definitions**: Auto-detects databases, web servers, containers, network infrastructure, monitoring tools, and enterprise applications
-   **Interactive Topology**: Generates visual network diagrams with extensive customization options
-   **Distributed Scanning**: Deploy daemons across network segments to map complex topologies
-   **Docker Integration**: Discovers containerized services automatically
-   **Organization Management**: Multi-user support with role-based permissions
-   **Scheduled Discovery**: Automated scanning to keep documentation current

🎯 Perfect For
--------------

-   **Home Lab Enthusiasts**: Document your ever-growing infrastructure
-   **IT Professionals**: Maintain accurate network inventory without manual spreadsheets
-   **System Administrators**: Visualize complex multi-VLAN environments
-   **DevOps Teams**: Map containerized services and their dependencies
-   **MSPs**: Manage multiple client networks with separate organizations

🚀 Quick Start
--------------

**Docker Compose**

curl -O https://raw.githubusercontent.com/scanopy/scanopy/refs/heads/main/docker-compose.yml
docker compose up -d

**Proxmox**

Use this helper script to create a Scanopy LXC.

**Unraid**

Available as an Unraid community app.

* * *

Access the UI at `http://<your-server-ip>:60072`, create your account, and wait for the first discovery to complete.

For detailed setup options and configuration, see the Installation Guide.

📚 Documentation
----------------

Full documentation at **scanopy.net/docs**

🖼️ Examples
------------

**scanopy.net/showcase**

📋 Licensing
------------

**Self-hosted (AGPL-3.0):** Free for all use. Requires source disclosure for network services and copyleft compliance.  
**Self-hosted (Commercial license):** For those who cannot comply with AGPL-3.0 terms. Contact licensing@scanopy.net  
**Hosted Solution:** Scanopy Cloud subscription for zero infrastructure management

🤝 Contributing
---------------

We welcome contributions! See our contributing guide for details.

Great first contribution: adding service definitions

💬 Community & Support
----------------------

-   **Discord**: Join our Discord for help and discussions
-   **Issues**: Report bugs or request features
-   **Discussions**: GitHub Discussions

* * *

**Built with ❤️ in NYC**
