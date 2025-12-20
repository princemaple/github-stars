---
project: postgresus
stars: 3325
description: PostgreSQL backup tool
url: https://github.com/RostislavDugin/postgresus
---

### PostgreSQL backup

Free, open source and self-hosted solution for automated PostgreSQL backups. With multiple storage options and notifications

Features • Installation • Usage • License • Contributing

**🌐 Postgresus website**

* * *

✨ Features
----------

### 🔄 **Scheduled backups**

-   **Flexible scheduling**: hourly, daily, weekly, monthly or cron
-   **Precise timing**: run backups at specific times (e.g., 4 AM during low traffic)
-   **Smart compression**: 4-8x space savings with balanced compression (~20% overhead)

### 🗄️ **Multiple storage destinations** (view supported)

-   **Local storage**: Keep backups on your VPS/server
-   **Cloud storage**: S3, Cloudflare R2, Google Drive, NAS, Dropbox, SFTP, Rclone and more
-   **Secure**: All data stays under your control

### 📱 **Smart notifications** (view supported)

-   **Multiple channels**: Email, Telegram, Slack, Discord, webhooks
-   **Real-time updates**: Success and failure notifications
-   **Team integration**: Perfect for DevOps workflows

### 🐘 **PostgreSQL support**

-   **Multiple versions**: PostgreSQL 12, 13, 14, 15, 16, 17 and 18
-   **SSL support**: Secure connections available
-   **Easy restoration**: One-click restore from any backup

### 🔒 **Enterprise-grade security** (docs)

-   **AES-256-GCM encryption**: Enterprise-grade protection for backup files
-   **Zero-trust storage**: Backups are encrypted and they are useless to attackers, so you can keep them in shared storages like S3, Azure Blob Storage, etc.
-   **Encryption for secrets**: Any sensitive data is encrypted and never exposed, even in logs or error messages
-   **Read-only user**: Postgresus uses by default a read-only user for backups and never stores anything that can change your data

### 👥 **Suitable for teams** (docs)

-   **Workspaces**: Group databases, notifiers and storages for different projects or teams
-   **Access management**: Control who can view or manage specific databases with role-based permissions
-   **Audit logs**: Track all system activities and changes made by users
-   **User roles**: Assign viewer, member, admin or owner roles within workspaces

### 🎨 **UX-Friendly**

-   **Designer-polished UI**: Clean, intuitive interface crafted with attention to detail
-   **Dark & light themes**: Choose the look that suits your workflow
-   **Mobile adaptive**: Check your backups from anywhere on any device

### ☁️ **Works with self-hosted & cloud databases**

Postgresus works seamlessly with both self-hosted PostgreSQL and cloud-managed databases:

-   **Cloud support**: AWS RDS, Google Cloud SQL, Azure Database for PostgreSQL
-   **Self-hosted**: Any PostgreSQL instance you manage yourself
-   **Why no PITR?**: Cloud providers already offer native PITR, and external PITR backups cannot be restored to managed cloud databases — making them impractical for cloud-hosted PostgreSQL
-   **Practical granularity**: Hourly and daily backups are sufficient for 99% of projects without the operational complexity of WAL archiving

### 🐳 **Self-hosted & secure**

-   **Docker-based**: Easy deployment and management
-   **Privacy-first**: All your data stays on your infrastructure
-   **Open source**: Apache 2.0 licensed, inspect every line of code

### 📦 Installation (docs)

You have several ways to install Postgresus:

-   Script (recommended)
-   Simple Docker run
-   Docker Compose setup

* * *

📦 Installation
---------------

You have three ways to install Postgresus: automated script (recommended), simple Docker run, or Docker Compose setup.

### Option 1: Automated installation script (recommended, Linux only)

The installation script will:

-   ✅ Install Docker with Docker Compose (if not already installed)
-   ✅ Set up Postgresus
-   ✅ Configure automatic startup on system reboot

sudo apt-get install -y curl && \\
sudo curl -sSL https://raw.githubusercontent.com/RostislavDugin/postgresus/refs/heads/main/install-postgresus.sh \\
| sudo bash

### Option 2: Simple Docker run

The easiest way to run Postgresus with embedded PostgreSQL:

docker run -d \\
  --name postgresus \\
  -p 4005:4005 \\
  -v ./postgresus-data:/postgresus-data \\
  --restart unless-stopped \\
  rostislavdugin/postgresus:latest

This single command will:

-   ✅ Start Postgresus
-   ✅ Store all data in `./postgresus-data` directory
-   ✅ Automatically restart on system reboot

### Option 3: Docker Compose setup

Create a `docker-compose.yml` file with the following configuration:

services:
  postgresus:
    container\_name: postgresus
    image: rostislavdugin/postgresus:latest
    ports:
      - "4005:4005"
    volumes:
      - ./postgresus-data:/postgresus-data
    restart: unless-stopped

Then run:

docker compose up -d

### Option 4: Kubernetes with Helm

For Kubernetes deployments, install directly from the OCI registry.

**With ClusterIP + port-forward (development/testing):**

helm install postgresus oci://ghcr.io/rostislavdugin/charts/postgresus \\
  -n postgresus --create-namespace

kubectl port-forward svc/postgresus-service 4005:4005 -n postgresus
# Access at http://localhost:4005

**With LoadBalancer (cloud environments):**

helm install postgresus oci://ghcr.io/rostislavdugin/charts/postgresus \\
  -n postgresus --create-namespace \\
  --set service.type=LoadBalancer

kubectl get svc postgresus-service -n postgresus
# Access at http://<EXTERNAL-IP>:4005

**With Ingress (domain-based access):**

helm install postgresus oci://ghcr.io/rostislavdugin/charts/postgresus \\
  -n postgresus --create-namespace \\
  --set ingress.enabled=true \\
  --set ingress.hosts\[0\].host=backup.example.com

For more options (NodePort, TLS, HTTPRoute for Gateway API), see the Helm chart README.

* * *

🚀 Usage
--------

1.  **Access the dashboard**: Navigate to `http://localhost:4005`
2.  **Add first DB for backup**: Click "New Database" and follow the setup wizard
3.  **Configure schedule**: Choose from hourly, daily, weekly, monthly or cron intervals
4.  **Set database connection**: Enter your PostgreSQL credentials and connection details
5.  **Choose storage**: Select where to store your backups (local, S3, Google Drive, etc.)
6.  **Add notifications** (optional): Configure email, Telegram, Slack, or webhook notifications
7.  **Save and start**: Postgresus will validate settings and begin the backup schedule

### 🔑 Resetting password (docs)

If you need to reset the password, you can use the built-in password reset command:

docker exec -it postgresus ./main --new-password="YourNewSecurePassword123" --email="admin"

Replace `admin` with the actual email address of the user whose password you want to reset.

* * *

📝 License
----------

This project is licensed under the Apache 2.0 License - see the LICENSE file for details

* * *

🤝 Contributing
---------------

Contributions are welcome! Read contributing guide for more details, priorities and rules are specified there. If you want to contribute, but don't know what and how - message me on Telegram @rostislav\_dugin
