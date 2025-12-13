---
project: FastSend
stars: 1207
description: FastSend 是一个基于 WebRTC 技术的点对点文件传输工具，支持快速的目录同步和文件传输。通过浏览器即可实现安全、高效的文件共享。
url: https://github.com/ShouChenICU/FastSend
---

FastSend 文件快传 🚀
================

📖 项目介绍
-------

FastSend 是一个基于 WebRTC 技术的点对点文件传输工具，支持快速的目录同步和文件传输。通过浏览器即可实现安全、高效的文件共享。

🌐 在线体验：fastsend.ing

✨ 特性
----

-   🔒 点对点加密传输，确保数据安全
-   📁 支持文件和文件夹传输
-   🚀 局域网自动优化，传输更快
-   🎯 简单易用的界面设计
-   🌍 支持中英文界面
-   📲 支持PWA轻量安装

🛠️ 技术栈
-------

-   WebRTC
-   Vue.js
-   Nuxt3
-   TypeScript
-   Modern File System API

📦 安装与构建
--------

# 安装依赖
yarn install

# 构建项目
yarn build

🚀 使用方法
-------

# 启动服务
node .output/server/index.mjs

Important

目录传输和同步需要 `HTTPS` 以及浏览器支持，一般新版本的桌面浏览器都支持

本项目自身的 HTTPS 配置方式（测试环境）请参考：

-   置顶 Issue
-   Nuxt 部署教程（英文）

FastSend 不建议直接以 HTTPS 形式进行生产环境部署，而应当位于反向代理服务器之后，请参考：

-   Nginx
-   Apache httpd
-   Caddy
-   Windows IIS

🐳 Docker 和 Docker Compose
--------------------------

### 使用 Docker Hub 发行版

docker run -d --name fastsend -p 3000:3000 shouchenicu/fastsend:0.6.0

Caution

`shouchenicu/fastsend` 是此项目在 Docker Hub 上的 **唯一** 官方镜像！

当前已发现 12 个第三方镜像，其中5个1的下载使用量高于官方镜像。请注意甄别，风险自负！

### Docker 构建

docker build -t fastsend .
docker run -d --name fastsend -p 3000:3000 fastsend

### Docker Compose

将项目拉取到本地，然后运行：

docker-compose up -d

访问 `http://localhost:3000` 即可使用。

💡 使用提示
-------

1.  确保浏览器启用了 WebRTC 功能
2.  如需传输文件夹或同步目录，请确保浏览器支持现代文件系统 API 并已启用 HTTPS 传输
3.  在同一局域网内传输速度最快
4.  建议在网络状态良好时使用，部分网络环境可能会阻止 P2P / WebRTC 正确建立连接，从而导致传输失败

👨‍💻 作者
--------

**ShouChen**

-   博客: shouchen.blog
-   X: @ShouChen\_

🤝 贡献
-----

欢迎提交 Issue 和 Pull Request！

📝 开源协议
-------

本项目基于 MIT 协议开源。

⭐ 支持项目
------

如果这个项目对你有帮助，欢迎给一个 star 支持一下！

* * *

Footnotes
---------

1.  比如 `niliaerith/fastsend` ↩
