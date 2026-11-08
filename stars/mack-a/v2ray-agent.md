---
project: v2ray-agent
stars: 22305
description: Xray、Tuic、hysteria2、sing-box 八合一一键脚本
url: https://github.com/mack-a/v2ray-agent
---

v2ray-agent
===========

-   感谢 JetBrains 提供的非商业开源软件开发授权

基于 Bash 的 Xray-core / sing-box 安装与管理脚本，支持普通主机部署和 Docker Reality 独立部署。

功能
--

-   **多核心支持:** 支持 Xray-core 和 sing-box，可按需安装单核心或组合使用.
-   **多协议支持:** 支持 VLESS（TLS、Reality、XHTTP）、VMess、Trojan、Hysteria2、Tuic、NaiveProxy、AnyTLS，以及独立 SOCKS5 入站.
-   **TLS 与 Reality:** TLS 协议可通过 acme.sh 自动申请和续订证书；Reality 支持无域名部署.
-   **易于管理:** 提供菜单管理用户、端口、配置、核心版本、日志和证书，并支持二维码及客户端节点信息输出.
-   **订阅支持:** 生成和管理订阅链接，支持远程订阅配置.
-   **分流管理:** 提供 WARP/WireGuard（IPv4/IPv6）、IPv6、SOCKS5、DNS、VMess+WS、SNI 反向代理等分流能力，可用于流媒体等场景.
-   **网络策略管理:** 支持 Hysteria2 端口跳跃、域名黑名单和 BT/P2P 下载限制.
-   **Docker Reality:** 无需域名即可通过 Docker 部署 VLESS-Reality，支持 Vision、XHTTP 或同时启用两种模式，并提供交互式和命令行参数模式.
-   **更多内容请访问官方网站、备用、X**

环境要求
----

-   **脚本版:** Linux、root 权限，支持 CentOS、Debian、Ubuntu 和 Alpine；支持 amd64/x86\_64、arm64/aarch64.
-   **Docker Reality:** Linux、root 或 sudo 权限，以及正在运行的 Docker；脚本可在交互模式下提示安装 Docker.

快速开始
----

### 安装脚本版

```
wget -P /root -N --no-check-certificate "https://raw.githubusercontent.com/mack-a/v2ray-agent/master/install.sh" && chmod 700 /root/install.sh && /root/install.sh
```

### 使用

安装后，运行以下命令可再次打开管理菜单:

```
vasma
```

### 安装Docker版

```
wget -P /root -N --no-check-certificate "https://raw.githubusercontent.com/mack-a/v2ray-agent/master/shell/docker_reality.sh" && chmod 700 /root/docker_reality.sh && /root/docker_reality.sh
```

### 使用

-   Docker Reality 使用说明

安装后，运行以下命令可再次打开管理菜单:

```
vasmad
```

文档和指南
-----

-   SOCKS5 入站与分流出站：简明教程
    
-   八合一脚本从入门到精通
    
-   脚本快速搭建教程
    
-   脚本使用注意事项
    
-   脚本异常处理
    
-   VPS选购攻略
    
-   垃圾VPS大救星，hysteria2最新协议一键搭建
    
-   RackNerd低价 联通AS4837套餐，年付10美起
    
-   搬瓦工优质套餐推荐
    
-   DMIT优质套餐推荐
    

社区与支持
-----

-   **Telegram:** 频道 | 群组
-   **网站:** 官网 | 备用
-   **反馈:** 提交 issue
-   **X:** 链接

捐赠
--

感谢您对开源项目的关注和支持。如果您觉得这个项目对您有帮助，欢迎通过以下方式进行捐赠。

-   购买VPS捐赠
-   通过虚拟币向我捐赠

许可证
---

本项根据 AGPL-3.0 许可证 授权.
