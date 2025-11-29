---
project: caddy-waf
stars: 670
description: Caddy WAF (Regex Rules, IP and DNS filtering, Rate Limiting, GeoIP, Tor, Anomaly Detection)
url: https://github.com/fabriziosalmi/caddy-waf
---

🛡️ Caddy WAF Middleware
========================

A robust, highly customizable, and feature-rich **Web Application Firewall (WAF)** middleware for the Caddy web server. This middleware provides **advanced protection** against a comprehensive range of web-based threats, seamlessly integrating with Caddy and offering flexible configuration options to secure your applications effectively.

🛡️ Core Protections
--------------------

-   **Regex-Based Filtering:** Deep URL, data & header inspection using powerful regex rules.
-   **Blacklisting:** Blocks malicious IPs, domains & optionally TOR exit nodes.
-   **Geo-Blocking:** Restricts access by country using GeoIP.
-   **Rate Limiting:** Prevents abuse via customizable IP request limits.
-   **Anomaly Scoring:** Dynamically blocks requests based on cumulative rule matches.
-   **Multi-Phase Inspection:** Analyzes traffic throughout the request lifecycle.
-   **Sensitive Data Redaction:** Removes private info from logs.
-   **Custom Response Handling:** Tailored responses for blocked requests.
-   **Detailed Monitoring:** JSON endpoint for performance tracking & analysis.
-   **Dynamic Config Reloads:** Seamless updates without restarts.
-   **File Watchers:** Automatic reloads on rule/blacklist changes.
-   **Observability:** Seamless integration with ELK stack and Prometheus.
-   **Rules generator**: powered by custom GPT, try it here

_Simple at a glance UI :)_

🚀 Quick Start
--------------

curl -fsSL -H "Pragma: no-cache" https://raw.githubusercontent.com/fabriziosalmi/caddy-waf/refs/heads/main/install.sh | bash

**Example Output:**

```
2025/01/29 13:50:49.791 INFO    Provisioning WAF middleware     {"log_level": "info", "log_path": "debug.json", "log_json": true, "anomaly_threshold": 10}
2025/01/29 12:50:49.918 INFO    http.handlers.waf       Tor exit nodes updated  {"count": 1093}
2025/01/29 13:50:49.918 INFO    WAF middleware version  {"version": "v0.0.0-20250128221917-c99e875aaf7c"}
2025/01/29 13:50:49.918 INFO    Rate limit configuration        {"requests": 100, "window": 10, "cleanup_interval": 300, "paths": ["/api/v1/.*", "/admin/.*"], "match_all_paths": false}
2025/01/29 13:50:49.918 WARN    GeoIP database not found. Country blocking/whitelisting will be disabled        {"path": "GeoLite2-Country.mmdb"}
2025/01/29 13:50:50.359 INFO    IP blacklist loaded     {"path": "ip_blacklist.txt", "valid_entries": 223770, "invalid_entries": 0, "total_lines": 223770}
2025/01/29 13:50:50.489 INFO    DNS blacklist loaded    {"path": "dns_blacklist.txt", "valid_entries": 854479, "total_lines": 854479}
2025/01/29 13:50:50.490 INFO    WAF rules loaded successfully   {"total_rules": 33, "rule_counts": "Phase 1: 17 rules, Phase 2: 16 rules, Phase 3: 0 rules, Phase 4: 0 rules, "}
2025/01/29 13:50:50.490 INFO    WAF middleware provisioned successfully
```

📑 Table of Contents
--------------------

1.  🚀 Installation
2.  🛠️ Basic Configuration
3.  📚 Full Documentation
4.  📜 License
5.  🙏 Contributing

* * *

🚀 Installation
---------------

# Step 1: Clone the caddy-waf repository from GitHub
git clone https://github.com/fabriziosalmi/caddy-waf.git

# Step 2: Navigate into the caddy-waf directory
cd caddy-waf

# Step 3: Clean up and update the go.mod file
go mod tidy

# Step 4: Fetch and install the required Go modules
go get github.com/caddyserver/caddy/v2
go get github.com/caddyserver/caddy/v2/caddyconfig/caddyfile
go get github.com/caddyserver/caddy/v2/caddyconfig/httpcaddyfile
go get github.com/caddyserver/caddy/v2/modules/caddyhttp
go get github.com/oschwald/maxminddb-golang
go get github.com/fsnotify/fsnotify
go get -v github.com/fabriziosalmi/caddy-waf
go mod tidy

# Step 5: Download the GeoLite2 Country database (required for country blocking/whitelisting)
wget https://git.io/GeoLite2-Country.mmdb

# Step 6: Build Caddy with the caddy-waf module
xcaddy build --with github.com/fabriziosalmi/caddy-waf=./

# Step 7: Fix Caddyfile format
caddy fmt --overwrite

# Step 8: Run the compiled Caddy server
./caddy run

* * *

🛠️ Basic Configuration
-----------------------

Here's a minimal Caddyfile example to get started:

{
    auto\_https off
    admin localhost:2019
}

:8080 {
    log {
        output stdout
        format console
        level INFO
    }

    handle {
        header -Server
    }

    route {
        # WAF Plugin runs on all requests first
        waf {
            metrics\_endpoint /waf\_metrics
            rule\_file rules.json
            ip\_blacklist\_file ip\_blacklist.txt
            dns\_blacklist\_file dns\_blacklist.txt
        }

        # Match the waf metrics endpoint specifically and stop processing
        @wafmetrics path /waf\_metrics
        handle @wafmetrics {
            # Do not respond here so it goes to the WAF plugin
        }

        # All other requests, respond with "Hello World"
        handle {
            respond "Hello world!" 200
        }
    }
}

**For more detailed configuration options, rules format, and usage instructions, please refer to the Full Documentation.**

* * *

📚 Full Documentation
---------------------

For complete documentation, including configuration options, rule format details, protected attack types, testing strategies, and more, please refer to the `/docs` directory in this repository.

### 📑 Table of Contents

1.  **Installation** - _Instructions for installing the Caddy WAF middleware._
2.  **Configuration Options** - _Detailed explanation of all available configuration settings._
3.  **Rules Format (`rules.json`)** - _A comprehensive guide to defining custom rules using the JSON format._
4.  **Blacklist Formats** - _Documentation of the formats used for defining IP and DNS blacklists._
5.  **Rate Limiting** - _How to configure rate limiting, including parameters and usage._
6.  **Country Blocking and Whitelisting** - _Details on how to configure country-based blocking and whitelisting._
7.  **Protected Attack Types** - _An overview of the wide range of web-based threats that the Caddy WAF is designed to protect against._
8.  **Dynamic Updates** - _How to dynamically update the WAF rules and other settings without downtime._
9.  **Metrics** - _Details about the WAF's metrics endpoint and the different metrics collected._
10.  **Prometheus Metrics** - _Instructions on how to expose WAF metrics using the Prometheus format._
11.  **ELK Observability** - _Instructions on how to configure caddy-waf ELK stack observability._
12.  **Rule/Blacklist Population Scripts** - _Documentation on the provided scripts to automatically fetch, update and generate rules and blacklists._
13.  **Testing** - _Guidance on how to test the WAF's effectiveness using the provided testing tools._
14.  **Docker Support** - _Instructions on how to build and run the WAF using Docker._

* * *

📜 License
----------

This project is licensed under the **AGPLv3 License**.

* * *

Others projects
---------------

If You like my projects, you may also like these ones:

-   patterns Automated OWASP CRS and Bad Bot Detection for Nginx, Apache, Traefik and HaProxy
-   blacklists Hourly updated domains blacklist 🚫
-   proxmox-vm-autoscale Automatically scale virtual machines resources on Proxmox hosts
-   UglyFeed Retrieve, aggregate, filter, evaluate, rewrite and serve RSS feeds using Large Language Models for fun, research and learning purposes
-   proxmox-lxc-autoscale Automatically scale LXC containers resources on Proxmox hosts
-   DevGPT Code togheter, right now! GPT powered code assistant to build project in minutes
-   websites-monitor Websites monitoring via GitHub Actions (expiration, security, performances, privacy, SEO)
-   caddy-mib Track and ban client IPs generating repetitive errors on Caddy
-   zonecontrol Cloudflare Zones Settings Automation using GitHub Actions
-   lws linux (containers) web services
-   cf-box cf-box is a set of Python tools to play with API and multiple Cloudflare accounts.
-   limits Automated rate limits implementation for web servers
-   dnscontrol-actions Automate DNS updates and rollbacks across multiple providers using DNSControl and GitHub Actions
-   proxmox-lxc-autoscale-ml Automatically scale the LXC containers resources on Proxmox hosts with AI
-   csv-anonymizer CSV fuzzer/anonymizer
-   iamnotacoder AI code generation and improvement

🙏 Contributing
---------------

Contributions are highly welcome! Feel free to open an issue or submit a pull request.
