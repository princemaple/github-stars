---
project: databasus
stars: 3757
description: Databases backup tool (PostgreSQL, MySQL, MongoDB)
url: https://github.com/databasus/databasus
---

### Backup tool for PostgreSQL, MySQL and MongoDB

Databasus is a free, open source and self-hosted tool to backup databases. Make backups with different storages (S3, Google Drive, FTP, etc.) and notifications about progress (Slack, Discord, Telegram, etc.). Previously known as Postgresus (see migration guide).

  

Features • Installation • Usage • License • Contributing

**🌐 Databasus website**

* * *

✨ Features
----------

### 💾 **Supported databases**

-   **PostgreSQL**: 12, 13, 14, 15, 16, 17 and 18
-   **MySQL**: 5.7, 8 and 9
-   **MariaDB**: 10 and 11
-   **MongoDB**: 4, 5, 6, 7 and 8

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

### 🔒 **Enterprise-grade security** (docs)

-   **AES-256-GCM encryption**: Enterprise-grade protection for backup files
-   **Zero-trust storage**: Backups are encrypted and remain useless to attackers, so you can safely store them in shared storage like S3, Azure Blob Storage, etc.
-   **Encryption for secrets**: Any sensitive data is encrypted and never exposed, even in logs or error messages
-   **Read-only user**: Databasus uses a read-only user by default for backups and never stores anything that can modify your data

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

Databasus works seamlessly with both self-hosted PostgreSQL and cloud-managed databases:

-   **Cloud support**: AWS RDS, Google Cloud SQL, Azure Database for PostgreSQL
-   **Self-hosted**: Any PostgreSQL instance you manage yourself
-   **Why no PITR support?**: Cloud providers already offer native PITR, and external PITR backups cannot be restored to managed cloud databases — making them impractical for cloud-hosted PostgreSQL
-   **Practical granularity**: Hourly and daily backups are sufficient for 99% of projects without the operational complexity of WAL archiving

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

You have three ways to install Databasus: automated script (recommended), simple Docker run, or Docker Compose setup.

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
6.  **Add notifications** (optional): Configure email, Telegram, Slack, or webhook notifications
7.  **Save and start**: Databasus will validate settings and begin the backup schedule

### 🔑 Resetting password (docs)

If you need to reset the password, you can use the built-in password reset command:

docker exec -it databasus ./main --new-password="YourNewSecurePassword123" --email="admin"

Replace `admin` with the actual email address of the user whose password you want to reset.

* * *

📝 License
----------

This project is licensed under the Apache 2.0 License - see the LICENSE file for details

* * *

🤝 Contributing
---------------

Contributions are welcome! Read the contributing guide for more details, priorities and rules. If you want to contribute but don't know where to start, message me on Telegram @rostislav\_dugin

\--

📖 Migration guide
------------------

Databasus is the new name for Postgresus. You can stay with latest version of Postgresus if you wish. If you want to migrate - follow installation steps for Databasus itself.

Just renaming an image is not enough as Postgresus and Databasus use different data folders and internal database naming.

You can put a new Databasus image with updated volume near the old Postgresus and run it (stop Postgresus before):

```
services:
  databasus:
    container_name: databasus
    image: databasus/databasus:latest
    ports:
      - "4005:4005"
    volumes:
      - ./databasus-data:/databasus-data
    restart: unless-stopped
```

Then manually move databases from Postgresus to Databasus.

### Why was Postgresus renamed to Databasus?

It was an important step for the project to grow. Actually, there are a couple of reasons:

1.  Postgresus is no longer a little tool that just adds UI for pg\_dump for little projects. It became a tool both for individual users, DevOps, DBAs, teams, companies and even large enterprises. Tens of thousands of users use Postgresus every day. Postgresus grew into a reliable backup management tool. Initial positioning is no longer suitable: the project is not just a UI wrapper, it's a solid backup management system now (despite it's still easy to use).
    
2.  New databases are supported: although the primary focus is PostgreSQL (with 100% support in the most efficient way) and always will be, Databasus added support for MySQL, MariaDB and MongoDB. Later more databases will be supported.
    
3.  Trademark issue: "postgres" is a trademark of PostgreSQL Inc. and cannot be used in the project name. So for safety and legal reasons, we had to rename the project.
