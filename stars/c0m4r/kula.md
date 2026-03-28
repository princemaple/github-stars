---
project: kula
stars: 893
description: Lightweight, self-contained Linux® server monitoring tool
url: https://github.com/c0m4r/kula
---

K U L A
=======

**Lightweight, self-contained Linux® server monitoring tool.**

🌏 Website | 👀 Demo | 🐋 Docker Hub

Zero dependencies. No external databases. Single binary. Just deploy and go.

* * *

📦 What It Does
---------------

Kula collects system metrics every second by reading directly from `/proc` and `/sys`, stores them in a built-in tiered ring-buffer storage engine, and serves them through a real-time Web UI dashboard and a terminal TUI.

Metric

What's Collected

**CPU**

Total usage (user, system, iowait, irq, softirq, steal) + core count

**GPU**

Load, Power consumption, VRAM

**Load**

1 / 5 / 15 min averages, running & total tasks

**Memory**

Total, free, available, used, buffers, cached, shmem

**Swap**

Total, free, used

**Network**

Per-interface throughput (Mbps), packets/s, errors, drops; TCP errors/s, resets/s, established connections; socket counts

**Disks**

Per-device I/O (read/write bytes/s, reads/s, writes/s IOPS); filesystem usage

**System**

Uptime, entropy, clock sync, hostname, logged-in user count

**Processes**

Running, sleeping, blocked, zombie counts

**Self**

Kula's own CPU%, RSS memory, open file descriptors

**Thermal**

CPU, GPU and Disk temperatures

Note: Monitoring NVIDIA GPUs might require additional setup. Check GPU monitoring.

* * *

🪩 How It Works
---------------

```
    ╭──────────────────────────────────────────────╮
    │                  Linux Kernel                │
    │      /proc/stat  /proc/meminfo  /sys/...     │
    ╰───────────────────────┬──────────────────────╯
                            │ Read every 1s
                            ▼
    ╭──────────────────────────────────────────────╮
    │                   Collectors                 │
    │        (CPU, Mem, Net, Disk, System)         │
    ╰───────────────────────┬──────────────────────╯
                            │ Live Data
         ╭──────────────────┼─────────────────────╮
         ▼                  ▼                     ▼
╭─────────────────╮  ╭────────────────╮  ╭─────────────────╮
│ Storage Engine  │  │   Web Server   │  │   TUI Terminal  │
╰───┬─────────┬───╯  ╰──────┬─────────╯  ╰─────────────────╯
    │         │             │
    │         ╰──(History)──┤              ╭───────────────╮
    │                       ╰──(HTTP/WS)─► |   Dashboard   |
    ▼                                      ╰───────────────╯
╭──────────┬──────────┬──────────╮
│  Tier 1  │  Tier 2  │  Tier 3  │
│    1s    │    1m    │    5m    │
│  250 MB  │  150 MB  │  50 MB   │
╰──────────┴──────────┴──────────╯
 Ring-buffer binary files
 with circular overwrites
```

### Storage Engine

Kula is powered by a custom-built, high-performance **ring-buffer** storage system that writes metrics directly into fixed-size binary files. Because the files have a strict maximum capacity, new data seamlessly wraps around to overwrite the oldest entries. On startup, Kula restores the latest-sample cache and reconstructs any pending aggregation buffers so it can resume serving recent data and continue tier rollups after a restart.

To maximize efficiency, Kula employs a multi-tiered architecture that intelligently downsamples older data:

-   **Tier 1** — Raw 1-second samples (default 250 MB)
-   **Tier 2** — 1-minute metrics aggregation (Avg/Min/Max) (default 150 MB)
-   **Tier 3** — 5-minute metrics aggregation (Avg/Min/Max) (default 50 MB)

### HTTP server

The HTTP server on backend exposes a REST API and a WebSocket endpoint for live streaming. Authentication is optional. When enabled, Kula uses Argon2id password hashing, secure session cookies, token-only session validation with sliding expiration, and hashed-at-rest session persistence. Authenticated API access can also use a bearer session token via the `Authorization` header.

### Dashboard

The frontend is a single-page application embedded in the binary. Built on Chart.js with custom SVG gauges, it connects via WebSocket for live updates and falls back to history API for longer time ranges. Features include:

-   Interactive zoom with drag-select (auto-pauses live stream)
-   Focus mode to display only specific charts of interest
-   Configurable Y-axis bounds (Manual limits or Auto-detect)
-   Per-device selectors for Network, Disk I/O, and Thermal monitoring
-   Grid / stacked list layout toggle
-   Alert system for clock sync, low entropy, and system overload
-   Modern aesthetics with light/dark theme support

* * *

💾 Installation
---------------

Kula was built to have everything in one binary file. You can just upload it to your server and not worry about installing anything else because Kula has no dependencies. It just works out of the box! It is a great tool when you need to quickly start real-time monitoring.

Example installation methods for **amd64 (x86\_64)** GNU/Linux.

Check Releases for **ARM** and **RISC-V** packages.

Note: Never thoughtlessly paste commands into the terminal. Even checking the checksum is no substitute for reviewing the code.

### Guided

sh -c "$(curl -fsSL https://raw.githubusercontent.com/c0m4r/kula/refs/heads/main/addons/install.sh)"

### Guided (verify installer)

KULA\_INSTALL=$(mktemp)
curl -o ${KULA\_INSTALL} -fsSL https://kula.ovh/install
echo "c70f6f070a1f93e278f07f7efb7d662a48bc16f43909df7889d8778430dde1b6 ${KULA\_INSTALL}" | sha256sum -c || rm -f ${KULA\_INSTALL}
bash ${KULA\_INSTALL}
rm -f ${KULA\_INSTALL}

### Standalone

wget https://github.com/c0m4r/kula/releases/download/0.13.0/kula-0.13.0-amd64.tar.gz
echo "2ce34692d9bf91b28ac8d540ccf49e48af20d3b0eb6054b778f87cc37ad7a044 kula-0.13.0-amd64.tar.gz" | sha256sum -c || rm -f kula-0.13.0-amd64.tar.gz
tar -xvf kula-0.13.0-amd64.tar.gz
cd kula
./kula

### Docker

Temporary, no persistent storage:

docker run --rm -it --name kula --pid host --network host -v /proc:/proc:ro c0m4r/kula:latest

With persistent storage:

docker run -d --name kula --pid host --network host -v /proc:/proc:ro -v kula\_data:/app/data c0m4r/kula:latest
docker logs -f kula

### Debian / Ubuntu (.deb)

wget https://github.com/c0m4r/kula/releases/download/0.13.0/kula-0.13.0-amd64.deb
echo "090c17401875e817e47fcbe2c11831f14afb9773f73e05a648a49cb69e326a14 kula-0.13.0-amd64.deb" | sha256sum -c || rm -f kula-0.13.0-amd64.deb
sudo dpkg -i kula-0.13.0-amd64.deb
journalctl -f -t kula

### RHEL / Fedora / CentOS / Rocky / Alma (.rpm)

wget https://github.com/c0m4r/kula/releases/download/0.13.0/kula-0.13.0-x86\_64.rpm
echo "86e4b87429b409ceeb478cf542b0401750baf05aa1dbcb76ca4c133865c9ef71 kula-0.13.0-x86\_64.rpm" | sha256sum -c || rm -f kula-0.13.0-x86\_64.rpm
sudo rpm -i kula-0.13.0-x86\_64.rpm
journalctl -f -t kula

### Arch Linux / Manjaro (AUR)

https://aur.archlinux.org/packages/kula

git clone https://aur.archlinux.org/kula.git
cd kula
makepkg -si

### Build from Source

git clone https://github.com/c0m4r/kula.git
cd kula
./addons/build.sh

* * *

💻 Usage
--------

### Quick Start

Starting Kula is as simple as running:

./kula

Dashboard will be available at: http://localhost:27960 (or :8080 if you're using earlier versions)

You can change default port and listen address in `config.yaml` or using environment variables:

export KULA\_LISTEN="127.0.0.1"
export KULA\_PORT="27960"
./kula

### TUI

./kula tui

### Inspect storage

./kula inspect

### Prometheus metrics

See: Prometheus metrics for more info.

### Health endpoints

Kula exposes lightweight liveness endpoints at:

```
http://localhost:27960/health
http://localhost:27960/status
```

Both return:

```
200 OK
kula is healthy
```

### Authentication (Optional)

# Generate password hash
./kula hash-password

# Add the output to config.yaml under web.auth

When authentication is enabled, Kula issues a random session token after login, stores only its hash on disk, and validates requests by token expiry/validity rather than binding sessions to client IP or User-Agent.

### Service Management

Init system files are provided in `addons/init/`:

# systemd
sudo cp addons/init/systemd/kula.service /etc/systemd/system/
sudo systemctl enable --now kula

# OpenRC
sudo cp addons/init/openrc/kula /etc/init.d/
sudo rc-update add kula default

# runit
sudo cp -r addons/init/runit/kula /etc/sv/
sudo ln -s /etc/sv/kula /var/service/

* * *

⚙️ Configuration
----------------

All settings live in `config.yaml`. See `config.example.yaml` for defaults.

* * *

🧰 Development
--------------

# Lint + test suite
./addons/check.sh

# Build
./addonsh.build.sh

# Build dev (Binary size: ~17MB)
CGO\_ENABLED=0 go build -o kula ./cmd/kula/

# Build prod (Binary size: ~12MB, xz: ~4MB)
CGO\_ENABLED=0 go build -trimpath -ldflags="\-s -w" -buildvcs=false -o kula ./cmd/kula/

### Updating Dependencies

To safely update only the Go modules used by Kula to their latest minor/patch versions, and prune any unused dependencies:

./addons/go\_modules\_updates.py
go get -u ./...
go mod tidy

### Testing & Benchmarks

# Run unit tests with race detector
go test -race ./...

# Run the full storage benchmark suite (default: 3s per bench)
./addons/benchmark.sh

# Python scripts formatter and linters
black addons/\*.py
pylint addons/\*.py
mypy --strict addons/\*.py

### Cross-Compile

./addons/build.sh cross    # builds amd64, arm64, riscv64

### Debian / Ubuntu (.deb)

./addons/build\_deb.sh
ls -1 dist/kula-\*.deb

### Arch Linux / Manjaro (AUR)

./addons/build\_aur.sh
cd dist/aur && makepkg -si

### RHEL / Fedora / CentOS / Rocky / Alma (.rpm)

./addons/build\_rpm.sh
ls -1 dist/kula-\*.rpm

### Docker

./addons/docker/build.sh
docker compose -f addons/docker/docker-compose.yml up -d

* * *

🔒 Privacy
----------

Privacy is a core pillar, not an afterthought.

Kula is built for privacy-conscious infrastructure. It is a completely self-contained binary that requires no cloud connection and no third-party APIs. Designed to function perfectly in air-gapped networks, Kula never sends metadata to external servers, never serves advertisements, and requires no user registration. Your monitoring starts and ends on your infrastructure, exactly where it should be.

* * *

📖 License
----------

GNU Affero General Public License v3.0

* * *

🫶 Attributions
---------------

-   Linux® is the registered trademark of Linus Torvalds in the U.S. and other countries.
-   Chart.js library licensed under MIT
-   Inter font by Rasmus Andersson licensed under OFL-1.1
-   Press Start 2P font by CodeMan38 licensed under OFL-1.1
