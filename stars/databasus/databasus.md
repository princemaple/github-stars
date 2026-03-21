---
project: databasus
stars: 6110
description: Databases backup tool (PostgreSQL, MySQL, MongoDB)
url: https://github.com/databasus/databasus
---

### Backup tool for PostgreSQL, MySQL and MongoDB

Databasus is a free, open source and self-hosted tool to backup databases (with focus on PostgreSQL). Make backups with different storages (S3, Google Drive, FTP, etc.) and notifications about progress (Slack, Discord, Telegram, etc.)

  

Features • Installation • Usage • License • Contributing

**🌐 Databasus website**

* * *

✨ Features
----------

### 💾 **Supported databases**

-   **PostgreSQL**: 12, 13, 14, 15, 16, 17 and 18
-   **MySQL**: 5.7, 8 and 9
-   **MariaDB**: 10, 11 and 12
-   **MongoDB**: 4, 5, 6, 7 and 8

### 🔄 **Scheduled backups**

-   **Flexible scheduling**: hourly, daily, weekly, monthly or cron
-   **Precise timing**: run backups at specific times (e.g., 4 AM during low traffic)
-   **Smart compression**: 4-8x space savings with balanced compression (~20% overhead)

### 🗑️ **Retention policies**

-   **Time period**: Keep backups for a fixed duration (e.g., 7 days, 3 months, 1 year)
-   **Count**: Keep a fixed number of the most recent backups (e.g., last 30)
-   **GFS (Grandfather-Father-Son)**: Layered retention — keep hourly, daily, weekly, monthly and yearly backups independently for fine-grained long-term history (enterprises requirement)
-   **Size limits**: Set per-backup and total storage size caps to control storage usage

### 🗄️ **Multiple storage destinations** (view supported)

-   **Local storage**: Keep backups on your VPS/server
-   **Cloud storage**: S3, Cloudflare R2, Google Drive, NAS, Dropbox, SFTP, Rclone and more
-   **Secure**: All data stays under your control

### 📱 **Smart notifications** (view supported)

-   **Multiple channels**: Email, Telegram, Slack, Discord, webhooks
-   **Real-time updates**: Success and failure notifications
-   **Team integration**: Perfect for DevOps workflows

### 🔒 **Enterprise-grade security** (docs)

-   **AES-256-GCM encryption**: Enterprise-grade protection for backup files
-   **Zero-trust storage**: Backups are encrypted and remain useless to attackers, so you can safely store them in shared storage like S3, Azure Blob Storage, etc.
-   **Encryption for secrets**: Any sensitive data is encrypted and never exposed, even in logs or error messages
-   **Read-only user**: Databasus uses a read-only user by default for backups and never stores anything that can modify your data

It is also important for Databasus that you are able to decrypt and restore backups from storages (local, S3, etc.) without Databasus itself. To do so, read our guide on how to recover directly from storage. We avoid "vendor lock-in" even to open source tool!

### 👥 **Suitable for teams** (docs)

-   **Workspaces**: Group databases, notifiers and storages for different projects or teams
-   **Access management**: Control who can view or manage specific databases with role-based permissions
-   **Audit logs**: Track all system activities and changes made by users
-   **User roles**: Assign viewer, member, admin or owner roles within workspaces

### 🎨 **UX-Friendly**

-   **Designer-polished UI**: Clean, intuitive interface crafted with attention to detail
-   **Dark & light themes**: Choose the look that suits your workflow
-   **Mobile adaptive**: Check your backups from anywhere on any device

### 🔌 **Connection types**

-   **Remote** — Databasus connects directly to the database over the network (recommended in read-only mode). No agent or additional software required. Works with cloud-managed and self-hosted databases
-   **Agent** — A lightweight Databasus agent (written in Go) runs alongside the database. The agent streams backups directly to Databasus, so the database never needs to be exposed publicly. Supports host-installed databases and Docker containers

### 📦 **Backup types**

-   **Logical** — Native dump of the database in its engine-specific binary format. Compressed and streamed directly to storage with no intermediate files
-   **Physical** — File-level copy of the entire database cluster. Faster backup and restore for large datasets compared to logical dumps (requires agent)
-   **Incremental** — Physical base backup combined with continuous WAL segment archiving. Enables Point-in-Time Recovery (PITR) — restore to any second between backups. Designed for disaster recovery and near-zero data loss requirements (requires agent)

### 🐳 **Self-hosted & secure**

-   **Docker-based**: Easy deployment and management
-   **Privacy-first**: All your data stays on your infrastructure
-   **Open source**: Apache 2.0 licensed, inspect every line of code

### 📦 Installation (docs)

You have four ways to install Databasus:

-   Automated script (recommended)
-   Simple Docker run
-   Docker Compose setup
-   Kubernetes with Helm

* * *

📦 Installation
---------------

You have four ways to install Databasus: automated script (recommended), simple Docker run, or Docker Compose setup.

### Option 1: Automated installation script (recommended, Linux only)

The installation script will:

-   ✅ Install Docker with Docker Compose (if not already installed)
-   ✅ Set up Databasus
-   ✅ Configure automatic startup on system reboot

sudo apt-get install -y curl && \\
sudo curl -sSL https://raw.githubusercontent.com/databasus/databasus/refs/heads/main/install-databasus.sh \\
| sudo bash

### Option 2: Simple Docker run

The easiest way to run Databasus:

docker run -d \\
  --name databasus \\
  -p 4005:4005 \\
  -v ./databasus-data:/databasus-data \\
  --restart unless-stopped \\
  databasus/databasus:latest

This single command will:

-   ✅ Start Databasus
-   ✅ Store all data in `./databasus-data` directory
-   ✅ Automatically restart on system reboot

### Option 3: Docker Compose setup

Create a `docker-compose.yml` file with the following configuration:

services:
  databasus:
    container\_name: databasus
    image: databasus/databasus:latest
    ports:
      - "4005:4005"
    volumes:
      - ./databasus-data:/databasus-data
    restart: unless-stopped

Then run:

docker compose up -d

### Option 4: Kubernetes with Helm

For Kubernetes deployments, install directly from the OCI registry.

**With ClusterIP + port-forward (development/testing):**

helm install databasus oci://ghcr.io/databasus/charts/databasus \\
  -n databasus --create-namespace

kubectl port-forward svc/databasus-service 4005:4005 -n databasus
# Access at http://localhost:4005

**With LoadBalancer (cloud environments):**

helm install databasus oci://ghcr.io/databasus/charts/databasus \\
  -n databasus --create-namespace \\
  --set service.type=LoadBalancer

kubectl get svc databasus-service -n databasus
# Access at http://<EXTERNAL-IP>:4005

**With Ingress (domain-based access):**

helm install databasus oci://ghcr.io/databasus/charts/databasus \\
  -n databasus --create-namespace \\
  --set ingress.enabled=true \\
  --set ingress.hosts\[0\].host=backup.example.com

For more options (NodePort, TLS, HTTPRoute for Gateway API), see the Helm chart README.

* * *

🚀 Usage
--------

1.  **Access the dashboard**: Navigate to `http://localhost:4005`
2.  **Add your first database for backup**: Click "New Database" and follow the setup wizard
3.  **Configure schedule**: Choose from hourly, daily, weekly, monthly or cron intervals
4.  **Set database connection**: Enter your database credentials and connection details
5.  **Choose storage**: Select where to store your backups (local, S3, Google Drive, etc.)
6.  **Configure retention policy**: Choose time period, count or GFS to control how long backups are kept
7.  **Add notifications** (optional): Configure email, Telegram, Slack, or webhook notifications
8.  **Save and start**: Databasus will validate settings and begin the backup schedule

### 🔑 Resetting password (docs)

If you need to reset the password, you can use the built-in password reset command:

docker exec -it databasus ./main --new-password="YourNewSecurePassword123" --email="admin"

Replace `admin` with the actual email address of the user whose password you want to reset.

### 💾 Backuping Databasus itself

After installation, it is also recommended to backup your Databasus itself or, at least, to copy secret key used for encryption (30 seconds is needed). So you are able to restore from your encrypted backups if you lose access to the server with Databasus or it is corrupted.

* * *

📝 License
----------

This project is licensed under the Apache 2.0 License - see the LICENSE file for details

🤝 Contributing
---------------

Contributions are welcome! Read the contributing guide for more details, priorities and rules. If you want to contribute but don't know where to start, message me on Telegram @rostislav\_dugin

Also you can join our large community of developers, DBAs and DevOps engineers on Telegram @databasus\_community.

AI disclaimer
-------------

There have been questions about AI usage in project development in issues and discussions. As the project focuses on security, reliability and production usage, it's important to explain how AI is used in the development process.

First of all, we are proud to say that Databasus has been accepted into both Claude for Open Source by Anthropic and Codex for Open Source by OpenAI in March 2026. For us it is one more signal that the project was recognized as important open-source software and was as critical infrastructure worth supporting independently by two of the world's leading AI companies. Read more at databasus.com/faq.

Despite of this, we have the following rules how AI is used in the development process:

AI is used as a helper for:

-   verification of code quality and searching for vulnerabilities
-   cleaning up and improving documentation, comments and code
-   assistance during development
-   double-checking PRs and commits after human review
-   additional security analysis of PRs via Codex Security

AI is not used for:

-   writing entire code
-   "vibe code" approach
-   code without line-by-line verification by a human
-   code without tests

The project has:

-   solid test coverage (both unit and integration tests)
-   CI/CD pipeline automation with tests and linting to ensure code quality
-   verification by experienced developers with experience in large and secure projects

So AI is just an assistant and a tool for developers to increase productivity and ensure code quality. The work is done by developers.

Moreover, it's important to note that we do not differentiate between bad human code and AI vibe code. There are strict requirements for any code to be merged to keep the codebase maintainable.

Even if code is written manually by a human, it's not guaranteed to be merged. Vibe code is not allowed at all and all such PRs are rejected by default (see contributing guide).

We also draw attention to fast issue resolution and security vulnerability reporting.
