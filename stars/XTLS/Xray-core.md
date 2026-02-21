---
project: Xray-core
stars: 35233
description: Xray, Penetrates Everything. Also the best v2ray-core. Where the magic happens. An open platform for various uses.
url: https://github.com/XTLS/Xray-core
---

Project X
=========

Project X originates from XTLS protocol, providing a set of network tools such as Xray-core and REALITY.

README is open, so feel free to submit your project here.

Sponsors
--------

**Sponsor Xray-core**

Donation & NFTs
---------------

### Collect a Project X NFT to support the development of Project X!

-   **TRX(Tron)/USDT/USDC: `TNrDh5VSfwd4RPrwsohr6poyNTfFefNYan`**
-   **TON: `UQApeV-u2gm43aC1uP76xAC1m6vCylstaN1gpfBmre_5IyTH`**
-   **BTC: `1JpqcziZZuqv3QQJhZGNGBVdCBrGgkL6cT`**
-   **XMR: `4ABHQZ3yJZkBnLoqiKvb3f8eqUnX4iMPb6wdant5ZLGQELctcerceSGEfJnoCk6nnyRZm73wrwSgvZ2WmjYLng6R7sR67nq`**
-   **SOL/USDT/USDC: `3x5NuXHzB5APG6vRinPZcsUv5ukWUY1tBGRSJiEJWtZa`**
-   **ETH/USDT/USDC: `0xDc3Fe44F0f25D13CACb1C4896CD0D321df3146Ee`**
-   **Project X NFT: https://opensea.io/item/ethereum/0x5ee362866001613093361eb8569d59c4141b76d1/1**
-   **VLESS NFT: https://opensea.io/collection/vless**
-   **REALITY NFT: https://opensea.io/item/ethereum/0x5ee362866001613093361eb8569d59c4141b76d1/2**
-   **Related links: VLESS Post-Quantum Encryption, XHTTP: Beyond REALITY, Announcement of NFTs by Project X**

License
-------

Mozilla Public License Version 2.0

Documentation
-------------

Project X Official Website

Telegram
--------

Project X

Project X Channel

Project VLESS (Русский)

Project XHTTP (Persian)

Installation
------------

-   Linux Script
    -   XTLS/Xray-install (**Official**)
    -   tempest (supports `systemd` and OpenRC; Linux-only)
-   Docker
    -   ghcr.io/xtls/xray-core (**Official**)
    -   teddysun/xray
    -   wulabing/xray\_docker
-   Web Panel
    -   Remnawave
    -   3X-UI
    -   PasarGuard
    -   Xray-UI
    -   X-Panel
    -   Marzban
    -   Hiddify
    -   TX-UI
-   One Click
    -   Xray-REALITY, xray-reality, reality-ezpz
    -   Xray\_bash\_onekey, XTool, VPainLess
    -   v2ray-agent, Xray\_onekey, ProxySU
-   Magisk
    -   NetProxy-Magisk
    -   Xray4Magisk
    -   Xray\_For\_Magisk
-   Homebrew
    -   `brew install xray`

Usage
-----

-   Example
    -   VLESS-XTLS-uTLS-REALITY
    -   VLESS-TCP-XTLS-Vision
    -   All-in-One-fallbacks-Nginx
-   Xray-examples
    -   XTLS/Xray-examples
    -   chika0801/Xray-examples
    -   lxhao61/integrated-examples
-   Tutorial
    -   XTLS Vision
    -   REALITY (English)
    -   XTLS-Iran-Reality (English)
    -   Xray REALITY with 'steal oneself' (English)
    -   Xray with WireGuard inbound (English)

GUI Clients
-----------

-   OpenWrt
    -   PassWall, PassWall 2
    -   ShadowSocksR Plus+
    -   luci-app-xray (openwrt-xray)
-   Asuswrt-Merlin
    -   XRAYUI
    -   fancyss
-   Windows
    -   v2rayN
    -   Furious
    -   Invisible Man - Xray
    -   AnyPortal
-   Android
    -   v2rayNG
    -   X-flutter
    -   SaeedDev94/Xray
    -   SimpleXray
    -   AnyPortal
    -   NetProxy-Magisk
-   iOS & macOS arm64 & tvOS
    -   Happ | Happ RU | Happ tvOS
    -   Streisand
    -   OneXray
-   macOS arm64 & x64
    -   Happ | Happ RU
    -   V2rayU
    -   V2RayXS
    -   Furious
    -   OneXray
    -   GoXRay
    -   AnyPortal
    -   v2rayN
-   Linux
    -   v2rayA
    -   Furious
    -   GorzRay
    -   GoXRay
    -   AnyPortal
    -   v2rayN

Others that support VLESS, XTLS, REALITY, XUDP, PLUX...
-------------------------------------------------------

-   iOS & macOS arm64 & tvOS
    -   Shadowrocket
    -   Loon
    -   Egern
    -   Quantumult X
-   Xray Tools
    -   xray-knife
    -   xray-checker
-   Xray Wrapper
    -   XTLS/libXray
    -   xtls-sdk
    -   xtlsapi
    -   AndroidLibXrayLite
    -   Xray-core-python
    -   xray-api
-   XrayR
    -   XrayR-release
    -   XrayR-V2Board
-   Cores
    -   Amnezia VPN
    -   mihomo
    -   sing-box

Contributing
------------

Code of Conduct

Credits
-------

-   Xray-core v1.0.0 was forked from v2fly-core 9a03cc5, and we have made & accumulated a huge number of enhancements over time, check the release notes for each version.
-   For third-party projects used in Xray-core, check your local or the latest go.mod.

One-line Compilation
--------------------

### Windows (PowerShell)

$env:CGO\_ENABLED\=0
go build \-o xray.exe \-trimpath \-buildvcs\=false \-ldflags\="\-s -w -buildid=" \-v ./main

### Linux / macOS

CGO\_ENABLED=0 go build -o xray -trimpath -buildvcs=false -ldflags="\-s -w -buildid=" -v ./main

### Reproducible Releases

Make sure that you are using the same Go version, and remember to set the git commit id (7 bytes):

CGO\_ENABLED=0 go build -o xray -trimpath -buildvcs=false -gcflags="all=-l=4" -ldflags="\-X github.com/xtls/xray-core/core.build=REPLACE -s -w -buildid=" -v ./main

If you are compiling a 32-bit MIPS/MIPSLE target, use this command instead:

CGO\_ENABLED=0 go build -o xray -trimpath -buildvcs=false -gcflags="\-l=4" -ldflags="\-X github.com/xtls/xray-core/core.build=REPLACE -s -w -buildid=" -v ./main

Stargazers over time
--------------------
