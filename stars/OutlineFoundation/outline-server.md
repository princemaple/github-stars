---
project: outline-server
stars: 6134
description: Outline Server, developed by Jigsaw. The Outline Server is a proxy server that runs a Shadowsocks instance and provides a REST API for access key management.
url: https://github.com/OutlineFoundation/outline-server
---

Outline Server
==============

Outline Server is the component that provides the Shadowsocks service (via outline-ss-server) and a service management API. You can deploy this server directly following simple instructions in this repository, or if you prefer a ready-to-use graphical interface you can use the Outline Manager.

**Components:**

-   **Outline Server** (`src/shadowbox`): The core proxy server that runs and manages outline-ss-server, a Shadowsocks backend. It provides a REST API for access key management.
    
-   **Metrics Server** (`src/metrics_server`): A REST service for optional, anonymous metrics sharing.
    

**Join the Outline Community** by signing up for the IFF Mattermost!

Shadowsocks and Anti-Censorship
-------------------------------

Outline's use of Shadowsocks means it benefits from ongoing improvements that strengthen its resistance against detection and blocking.

**Key Protections:**

-   **AEAD ciphers** are mandatory.
-   **Probing resistance** mitigates detection techniques.
-   **Protection against replayed data.**
-   **Variable packet sizes** to hinder identification.

See Shadowsocks resistance against detection and blocking.

Installation
------------

**Prerequisites**

-   Node LTS (`lts/hydrogen`, version `18.16.0`)
-   NPM (version `9.5.1`)
-   Go 1.21+

1.  **Install dependencies**
    
    npm install
    
2.  **Start the server**
    
    ./task shadowbox:start
    
    Exploring further options:
    
    -   **Refer to the README:** Find additional configuration and usage options in the core server's `README`.
    -   **Learn about the build system:** For in-depth build system information, consult the contributing guide.
3.  **To clean up**
    
    ./task clean
