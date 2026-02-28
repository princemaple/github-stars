---
project: ProxyBridge
stars: 2584
description: Proxifier Alternative to redirect any Windows/MacOS/Linux TCP and UDP traffic to HTTP/Socks5 proxy
url: https://github.com/InterceptSuite/ProxyBridge
---

ProxyBridge
===========

ProxyBridge is a lightweight, open-source universal proxy client (Proxifier alternative) that provides transparent proxy routing for applications on **Windows**, **macOS**, and **Linux**. It redirects TCP and UDP traffic from specific processes through SOCKS5 or HTTP proxies, with the ability to route, block, or allow traffic on a per-application basis. ProxyBridge fully supports both TCP and UDP proxy routing and works at the system level, making it compatible with proxy-unaware applications without requiring any configuration changes.

Tip

**Need advanced traffic analysis?** Check out **InterceptSuite** - our comprehensive MITM proxy for analyzing TLS, TCP, UDP, DTLS traffic. Perfect for security testing, network debugging, and system administration!

Table of Contents
-----------------

-   Features
-   Platform Documentation
-   Screenshots
-   Use Cases
-   License
-   Author
-   Credits

**💖 Support ProxyBridge Development**  
_If you find ProxyBridge useful, consider sponsoring to support ongoing development and new features!_  
  

Features
--------

-   **Cross-platform** - Available for Windows, macOS and Linux
-   **Dual interface** - Feature-rich GUI and powerful CLI for all use cases
-   **Process-based traffic control** - Route, block, or allow traffic for specific applications
-   **Universal compatibility** - Works with proxy-unaware applications
-   **Multiple proxy protocols** - Supports SOCKS5 and HTTP proxies
-   **System-level interception** - Reliable packet capture at kernel/network extension level
-   **No configuration needed** - Applications work without any modifications
-   **Protocol agnostic** - Compatible with TCP and UDP protocols (HTTP/HTTPS, HTTP/3, databases, RDP, SSH, games, DTLS, DNS, etc.)
-   **Traffic blocking** - Block specific applications from accessing the internet or any network (LAN, localhost, etc.)
-   **Flexible rules** - Direct connection, proxy routing, or complete blocking per process
-   **Advanced rule configuration** - Target specific processes, IPs, ports, protocols (TCP/UDP), and hostnames with wildcard support
-   **Process exclusion** - Prevent proxy loops by excluding proxy applications
-   **Import/Export rules** - Share rule configurations across systems with JSON-based import/export

Caution

**Beware of Fake ProxyBridge Downloads**

Multiple **fake ProxyBridge download sources** have been identified. Some of these sources distribute **unwanted binaries** and **malicious software**.

❌ **Do NOT download ProxyBridge from any third-party or unofficial sources.**

✅ **Official ProxyBridge sources (only):**

-   GitHub Repository: https://github.com/InterceptSuite/ProxyBridge/
-   Official Website: https://interceptsuite.com/download/proxybridge

If you prefer not to use prebuilt binaries, you may safely build ProxyBridge yourself by following the **Contribution Guide** and compiling directly from the **official source code**.

ProxyBridge does not communicate with any external servers except the GitHub API for update checks (triggered only on app launch or manual update checks);

Platform Documentation
----------------------

ProxyBridge is available for Windows, macOS, and Linux, with platform-specific implementations:

### 📘 Windows

-   **View Full Windows Documentation**
-   **Technology**: WinDivert for kernel-level packet interception
-   **Installer**: Available from Releases
-   **Requirements**: Windows 10 or later (64-bit), Administrator privileges
-   **GUI**: Avalonia-based modern interface
-   **CLI**: Full-featured command-line tool with rule file support

### 📗 macOS

-   **View Full macOS Documentation**
-   **Technology**: Network Extension framework with transparent proxy
-   **Distribution**: Direct download (.pkg installer) from Releases
-   **Requirements**: macOS 13.0 (Ventura) or later, Apple Silicon (ARM) or Intel
-   **GUI**: Native SwiftUI interface

### 📙 Linux

-   **View Full Linux Documentation**
-   **Technology**: Netfilter NFQUEUE for kernel-level packet interception
-   **Distribution**: TAR.GZ archive or one-command install from Releases
-   **Requirements**: Linux kernel with NFQUEUE support, root privileges (not compatible with WSL1/WSL2)
-   **GUI**: GTK3-based interface (optional)
-   **CLI**: Full-featured command-line tool with rule support
-   **Quick Install**: `curl -Lo deploy.sh https://raw.githubusercontent.com/InterceptSuite/ProxyBridge/refs/heads/master/Linux/deploy.sh && sudo bash deploy.sh`

Screenshots
-----------

### macOS

  
_ProxyBridge GUI - Main Interface_

  
_Proxy Settings Configuration_

  
_Proxy Rules Management_

  
_Add/Edit Proxy Rule_

### Windows

#### GUI

  
_ProxyBridge GUI - Main Interface_

  
_Proxy Settings Configuration_

  
_Proxy Rules Management_

  
_Add/Edit Proxy Rule_

#### CLI

  
_ProxyBridge CLI Interface_

### Linux

#### GUI

  
_ProxyBridge GUI - Main Interface_

  
_Proxy Settings Configuration_

  
_Proxy Rules Management_

  
_Add/Edit Proxy Rule_

#### CLI

  
_ProxyBridge CLI Interface_

Use Cases
---------

-   Redirect proxy-unaware applications (games, desktop apps) through InterceptSuite/Burp Suite for security testing
-   Route specific applications through Tor, SOCKS5 or HTTP proxies
-   Intercept and analyze traffic from applications that don't support proxy configuration
-   Test application behavior under different network conditions
-   Analyze protocols and communication patterns

License
-------

MIT License - See LICENSE file for details

Author
------

Sourav Kalal / InterceptSuite

Credits
-------

**Windows Implementation:** This project is built on top of WinDivert by basil00. WinDivert is a powerful Windows packet capture and manipulation library that makes kernel-level packet interception possible. Special thanks to the WinDivert project for providing such a robust foundation.

Based on the StreamDump example from WinDivert: https://reqrypt.org/samples/streamdump.html

The Windows GUI is built using Avalonia UI - a cross-platform XAML-based UI framework for .NET, enabling a modern and responsive user interface.

**macOS Implementation:** Built using Apple's Network Extension framework for transparent proxy capabilities on macOS.

**Linux Implementation:** Built using Linux Netfilter NFQUEUE for kernel-level packet interception and iptables for traffic redirection. The GUI uses GTK3 for native Linux desktop integration.
