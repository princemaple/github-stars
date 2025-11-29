---
project: dockmon
stars: 929
description: DockMon - Modern Docker container monitoring with auto-restart and alerts
url: https://github.com/darthnorse/dockmon
---

DockMon
=======

A comprehensive Docker container monitoring and management platform with real-time monitoring, intelligent auto-restart, multi-channel alerting, and complete event logging.

Key Features
------------

-   **Multi-Host Monitoring** - Monitor containers across unlimited Docker hosts (local and remote)
-   **Real-Time Dashboard** - Drag-and-drop customizable widgets with WebSocket updates
-   **Real-Time Statistics** - Live CPU, memory, network metrics
-   **Real-Time Container Logs** - View logs from multiple containers simultaneously with live updates
-   **Event Viewer** - Comprehensive audit trail with filtering, search, and real-time updates
-   **Intelligent Auto-Restart** - Per-container auto-restart with configurable retry logic
-   **Advanced Alerting** - Discord, Slack, Telegram, Pushover, Gotify, SMTP with customizable templates
-   **Container Tagging** - Automatic tag derivation from Docker labels with user-defined tags
-   **Bulk Operations** - Start, stop, restart multiple containers simultaneously with progress tracking
-   **Container Deployments** - Deploy containers to local and remote hosts. Supports Docker Run style deployments as well as Docker Compose, including the ability to create templates for repeated deployments
-   **Automatic Updates** - Detect and execute container image updates on schedule
-   **HTTP/HTTPS Health Checks** - Custom endpoint monitoring with auto-restart on failure
-   **Blackout Windows** - Schedule maintenance periods to suppress alerts
-   **Secure by Design** - Session-based auth, rate limiting, mTLS for remote hosts, Alpine Linux base

Documentation
-------------

-   **Complete User Guide** - Full documentation
-   **Quick Start** - Get started in 5 minutes
-   **Installation** - Docker, unRAID, Synology, QNAP
-   **Configuration** - Alerts, notifications, settings
-   **Security** - Best practices and mTLS setup
-   **Remote Monitoring** - Monitor remote Docker hosts
-   **Event Viewer** - Comprehensive audit trail with filtering
-   **Container Logs** - Real-time multi-container log viewer
-   **API Reference** - REST and WebSocket APIs
-   **FAQ** - Frequently asked questions
-   **Troubleshooting** - Common issues

Support & Community
-------------------

-   **Discord Server** - Join the community, get help, share tips
-   **Report Issues** - Found a bug?
-   **Discussions** - Ask questions, share ideas
-   **Wiki** - Complete documentation
-   **Star on GitHub** - Show your support!
-   **Buy Me A Coffee** - Support the project

Technology Stack
----------------

### Backend

-   **Python 3.13** with FastAPI and async/await
-   **Alpine Linux 3.x** container base (reduced attack surface)
-   **OpenSSL 3.x** for modern cryptography
-   **SQLAlchemy 2.0** with Alembic migrations
-   **Go 1.23** stats service for real-time metrics streaming

### Frontend

-   **React 18.3** with TypeScript (strict mode, zero `any`)
-   **Vite** for fast development builds
-   **TanStack Table** for data tables
-   **React Grid Layout** for dashboard customization
-   **Tailwind CSS** for styling

### Infrastructure

-   **Multi-stage Docker build** - Go stats + React frontend + Python backend
-   **Supervisor** for process management
-   **Nginx** reverse proxy with SSL/TLS
-   **WebSocket** for real-time updates
-   **Health checks** for all services

Upgrading from v1 to v2
-----------------------

### Breaking Changes

-   **Alert Rules**: Old alert rules must be recreated using the new alert system
-   **mTLS Certificates**: Regenerate certificates due to Alpine's stricter OpenSSL 3.x requirements
-   **Database Schema**: Automatic one-time migration from v1.1.3 to v2.0.0

### Data Preserved

-   ✅ Hosts and their configurations
-   ✅ Containers and container history
-   ✅ Event logs and audit trail
-   ✅ User accounts and preferences

### Post-Upgrade Steps

1.  Regenerate mTLS certificates for remote hosts (see mTLS Setup Guide)
2.  Recreate alert rules using the new alert system
3.  Verify host connections after upgrade

See the Migration Guide for detailed instructions.

Contributing
------------

Contributions are welcome! **No CLA required** - just submit a PR!

-   Report bugs via GitHub Issues
-   Suggest features in Discussions
-   Improve documentation (edit the Wiki)
-   Submit pull requests (see Contributing Guide)

By contributing, you agree your contributions are licensed under the same BSL 1.1 terms as the project.

Development
-----------

Want to contribute code or run DockMon in development mode?

See Development Setup for:

-   Local development environment setup
-   Architecture overview
-   Running tests
-   Building from source

License
-------

**Business Source License 1.1** - see LICENSE file for full details.

### What this means:

✅ **You can use DockMon:**

-   For internal use in your company (any size)
-   For personal projects
-   To monitor your clients' infrastructure as part of consulting/MSP services
-   Fork, modify, and customize for your own use
-   Contribute improvements back to the project

❌ **You cannot:**

-   Offer DockMon as a SaaS product to third parties
-   Embed DockMon in a commercial monitoring platform sold to others
-   Provide DockMon hosting as a standalone commercial service

### Future Open Source:

After 2 years (Change Date: 2027-01-01), each version automatically converts to **Apache License 2.0**, becoming fully permissive open source with explicit patent grants.

### Commercial Licensing:

Need to use DockMon in a way not permitted by BSL? Contact us for commercial licensing:

-   Open an Issue
-   Describe your use case
-   We'll work with you on licensing terms

### Why BSL?

BSL protects the project from direct commercial competition while remaining contributor-friendly:

-   **No CLAs required** - standard GitHub workflow
-   **Eventually becomes open source** - builds community trust
-   **Allows all legitimate uses** - only blocks competitive SaaS offerings
-   Used successfully by Sentry, CockroachDB, MariaDB, and other major projects

Author
------

Created by darthnorse

Acknowledgments
---------------

This project has been developed with **vibe coding** and **AI assistance** using Claude Code. The codebase includes clean, well-documented code with proper error handling, comprehensive testing considerations, modern async/await patterns, robust database design, and production-ready deployment configurations.

* * *

**If DockMon helps you, please consider giving it a star or supporting the project!**

Documentation • Issues • Discussions
