---
project: netvisor
stars: 2015
description: Automatically discover and visually document network infrastructure.
url: https://github.com/mayanayza/netvisor
---

NetVisor
========

**Automatically discover and visually document network infrastructure.**

NetVisor scans your network, identifies hosts and services, and generates an interactive visualization showing how everything connects, letting you easily create and maintain network documentation.  
  
  
  

> 💡 **Prefer not to self-host, or want to use this for your business?** Get early access to NetVisor Cloud

✨ Key Features
--------------

-   **Automatic Discovery**: Scans networks to identify hosts, services, and their relationships
-   **200+ Service Definitions**: Auto-detects databases, web servers, containers, network infrastructure, monitoring tools, and enterprise applications
-   **Interactive Topology**: Generates visual network diagrams with extensive customization options
-   **Multi-VLAN Support**: Deploy daemons and scan across network segments to map complex topologies
-   **Docker Integration**: Discovers containerized services automatically
-   **Organization Management**: Multi-user support with role-based permissions (Owner, Admin, Member, Visualizer)
-   **Scheduled Discovery**: Automated scanning to keep documentation current
-   **Export & Share**: Download topology diagrams as PNG images

🎯 Perfect For
--------------

-   **Home Lab Enthusiasts**: Document your ever-growing infrastructure
-   **IT Professionals**: Maintain accurate network inventory without manual spreadsheets
-   **System Administrators**: Visualize complex multi-VLAN environments
-   **DevOps Teams**: Map containerized services and their dependencies
-   **MSPs**: Manage multiple client networks with separate organizations

* * *

**Want hosted NetVisor without the setup?** Get early access to our upcoming cloud service at netvisor.io

* * *

📚 Documentation
----------------

-   **Installation Guide** - Detailed setup instructions for all platforms
-   **User Guide** - Complete guide to using NetVisor features
-   **Configuration Reference** - Server, daemon, and environment variables
-   **Architecture Overview** - System design and technology stack

🚀 Quick Start
--------------

### Prerequisites

-   **Server**: Docker and Docker Compose
-   **Daemon** (included in default setup): Docker with host networking, or standalone binary

### Installation

1.  **Start the server** (includes integrated daemon):
    
    **Docker Compose**
    
    curl -O https://raw.githubusercontent.com/mayanayza/netvisor/refs/heads/main/docker-compose.yml && docker compose up -d
    
    **Proxmox**
    
    You can use this helper script to create a NetVisor LXC on your Proxmox host.
    
    **Unraid**
    
    NetVisor is available as an Unraid community app.
    
2.  **Access the UI** at `http://<your-server-ip>:60072`
    
3.  **Create your account** on the registration page
    
4.  **Wait for first discovery** to complete (5-10+ minutes depending on network size)
    

That's it! NetVisor automatically:

-   Creates a default network
-   Starts the integrated daemon
-   Runs initial discovery
-   Schedules daily scans

### Next Steps

-   **View your topology**: Navigate to Topology to see the network diagram
-   **Scan additional VLANs**: Deploy more daemons at **Manage > Daemons** or add subnets to your existing daemon's scan list in **Discover > Scheduled**
-   **Organize your network**: Create groups, consolidate hosts, manage subnets

See the User Guide for detailed feature documentation.

🔍 What Gets Discovered?
------------------------

NetVisor automatically detects **200+ common services** including:

**Infrastructure & Networking**: Pi-hole, AdGuard Home, Unifi Controller, pfSense, OPNsense  
**Virtualization & Containers**: Proxmox, Docker, Kubernetes, Portainer  
**Databases**: PostgreSQL, MySQL/MariaDB, MongoDB, Redis, Microsoft SQL Server  
**Web Servers & Proxies**: Apache, Nginx, Lighttpd, Traefik, Caddy, HAProxy  
**Monitoring & Observability**: Grafana, Prometheus, Zabbix, Netdata, Nagios  
**Storage & File Sharing**: Synology DSM, QNAP, TrueNAS, Nextcloud, Samba, Windows File Server  
**Development & CI/CD**: GitLab, Jenkins, Ansible AWX, GitHub Enterprise, Azure DevOps  
**Communication & Collaboration**: Microsoft Exchange, Asterisk, FreePBX, Rocket.Chat  
**Media & Content**: Plex, Jellyfin, Emby, streaming servers  
**Automation & IoT**: Home Assistant, Node-RED, MQTT brokers

For the complete list, see the service definitions directory.

**Missing a service?** Request it or contribute a definition!

🛠️ Technology Stack
--------------------

-   **Backend**: Rust with Axum web framework
-   **Frontend**: Svelte 5 with SvelteKit
-   **Database**: PostgreSQL 17
-   **Visualization**: @xyflow/svelte for topology rendering
-   **Deployment**: Docker and Docker Compose

See ARCHITECTURE.md for detailed system design.

🤝 Contributing
---------------

We welcome contributions! Whether you're:

-   Adding service definitions (great first contribution!)
-   Reporting bugs
-   Requesting features
-   Submitting pull requests

See our contributing guide for details.

💬 Community & Support
----------------------

-   **Documentation**: You're reading it! Check the User Guide for detailed features
-   **Discord**: Join our Discord for help and discussions
-   **Issues**: Report bugs or request features
-   **Discussions**: GitHub Discussions

📋 FAQ
------

**Can I run NetVisor without Docker?**

The server requires Docker (or manual PostgreSQL + Rust + Node.js setup for development). The daemon is available as a standalone binary for Linux, macOS, and Windows.

**How do I scan multiple VLANs?**

Deploy multiple daemons—one per VLAN you want to scan. Each daemon connects to the server and discovers its local network segment. See Multi-VLAN Setup in the User Guide.

**Is IPv6 supported?**

Not currently. IPv6 support is planned for displaying IPv6 addresses and connectivity testing, but not full subnet scanning. See User Guide FAQ for details.

**How long does discovery take?**

Typically 5-10+ minutes depending on network size, subnet masks, and concurrent scan settings. Monitor progress in **Discover > Sessions**.

**Can I customize the topology layout?**

Yes! Extensive customization options including network filters, service category hiding, Docker grouping, edge type filters, manual node positioning, and subnet resizing. See Topology Visualization.

📄 License
----------

NetVisor is dual-licensed:

-   **Open Source**: AGPL-3.0 - Free for self-hosted, open source use
-   **Commercial**: Commercial licensing available for organizations that need to use NetVisor without AGPL requirements

* * *

**Built with ❤️ in NYC**
