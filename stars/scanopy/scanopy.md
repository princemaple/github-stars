---
project: scanopy
stars: 4759
description: Network diagrams that update themselves
url: https://github.com/scanopy/scanopy
---

Scanopy
=======

**Network documentation that updates itself.**

Scanopy scans your network, discovers hosts and services, and generates a live topology diagram that stays current automatically. One daemon, no per-device agents, no manual upkeep.

  
  
  
  

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
-   **MSPs**: Manage multiple client networks with your team

📋 Licensing
------------

**Self-hosted (AGPL-3.0):** Free for all use. Requires source disclosure for network services and copyleft compliance.  
**Self-hosted (Commercial license):** For those who cannot comply with AGPL-3.0 terms. Contact licensing@scanopy.net  
**Hosted Solution:** **Scanopy Cloud** subscription for zero infrastructure management

🚀 Quick Start for Self Hosting
-------------------------------

**Docker Compose**

curl -O https://raw.githubusercontent.com/scanopy/scanopy/refs/heads/main/docker-compose.yml
docker compose up -d

**Proxmox**

Use this helper script to create a Scanopy LXC.

**Unraid**

Available as an Unraid community app.

> 💡 **Prefer not to self-host?** Get a free trial of Scanopy Cloud

* * *

Access the UI at `http://<your-server-ip>:60072`, create your account, and wait for the first discovery to complete.

For detailed setup options and configuration, see the Installation Guide.

📚 Documentation + API
----------------------

**scanopy.net/docs**

🚀 Demo
-------

**demo.scanopy.net**

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
