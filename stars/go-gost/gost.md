---
project: gost
stars: 6722
description: GO Simple Tunnel - a simple tunnel written in golang
url: https://github.com/go-gost/gost
---

GO Simple Tunnel
================

### GO语言实现的安全隧道

功能特性
----

-   多端口监听
-   多级转发链
-   多协议支持
-   TCP/UDP端口转发
-   反向代理和隧道
-   TCP/UDP透明代理
-   DNS解析和代理
-   TUN/TAP设备与TUN2SOCKS
-   负载均衡
-   路由控制
-   准入控制
-   限速限流
-   插件系统
-   Prometheus监控指标
-   动态配置
-   Web API
-   GUI/WebUI

概览
--

GOST作为隧道有三种主要使用方式。

### 正向代理

作为代理服务访问网络，可以组合使用多种协议组成转发链进行转发。

### 端口转发

将一个服务的端口映射到另外一个服务的端口，同样可以组合使用多种协议组成转发链进行转发。

### 反向代理

利用隧道和内网穿透将内网服务暴露到公网访问。

下载安装
----

### 二进制文件

https://github.com/go-gost/gost/releases

### 安装脚本

# 安装最新版本 \[https://github.com/go-gost/gost/releases\](https://github.com/go-gost/gost/releases)
bash <(curl -fsSL https://github.com/go-gost/gost/raw/master/install.sh) --install

# 选择要安装的版本
bash <(curl -fsSL https://github.com/go-gost/gost/raw/master/install.sh)

### 源码编译

```
git clone https://github.com/go-gost/gost.git
cd gost/cmd/gost
go build
```

### Docker

```
docker run --rm gogost/gost -V
```

工具
--

### GUI

go-gost/gostctl

### WebUI

go-gost/gost-ui

### Shadowsocks Android插件

hamid-nazari/ShadowsocksGostPlugin

帮助与支持
-----

Wiki站点：https://gost.run

YouTube: https://www.youtube.com/@gost-tunnel

Telegram：https://t.me/gogost

Google讨论组：https://groups.google.com/d/forum/go-gost

旧版入口：v2.gost.run
