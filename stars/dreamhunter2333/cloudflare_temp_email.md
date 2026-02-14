---
project: cloudflare_temp_email
stars: 6058
description: CloudFlare free temp domain email 免费收发 临时域名邮箱 支持附件 IMAP SMTP TelegramBot
url: https://github.com/dreamhunter2333/cloudflare_temp_email
---

Cloudflare 临时邮箱 - 免费搭建临时邮件服务
============================

🇨🇳 中文文档 | 🇺🇸 English Document

> 本项目仅供学习和个人用途，请勿将其用于任何违法行为，否则后果自负。

**🎉 一个功能完整的临时邮箱服务！**

-   🆓 **完全免费** - 基于 Cloudflare 免费服务构建，零成本运行
-   ⚡ **高性能** - Rust WASM 邮件解析，响应速度极快
-   🎨 **现代化界面** - 响应式设计，支持多语言，操作简便
-   🔐 **地址密码** - 支持为邮箱地址设置独立密码，增强安全性 (通过 `ENABLE_ADDRESS_PASSWORD` 启用)

📚 部署文档 - 快速开始
--------------

📖 部署文档 | 🚀 Github Action 部署文档

📝 更新日志
-------

查看 CHANGELOG 了解最新更新内容。

🎯 在线体验
-------

立即体验 → https://mail.awsl.uk/

📊 服务状态监控（点击收缩/展开）

Backend

Frontend

⭐ Star History（点击收缩/展开） 📖 目录（点击收缩/展开）

-   Cloudflare 临时邮箱 - 免费搭建临时邮件服务
    -   📚 部署文档 - 快速开始
    -   📝 更新日志
    -   🎯 在线体验
    -   ✨ 核心功能
        -   📧 邮件处理
        -   👥 用户管理
        -   🔧 管理功能
        -   🌐 多语言与界面
        -   🤖 集成与扩展
    -   🏗️ 技术架构
        -   🏛️ 系统架构
        -   🛠️ 技术栈
        -   📦 主要组件
    -   🌟 加入社区

✨ 核心功能
------

✨ 核心功能详情（点击收缩/展开）

### 📧 邮件处理

-   使用 `rust wasm` 解析邮件，解析速度快，几乎所有邮件都能解析，node 的解析模块解析邮件失败的邮件，rust wasm 也能解析成功
-   **AI 邮件识别** - 使用 Cloudflare Workers AI 自动提取邮件中的验证码、认证链接、服务链接等重要信息
-   支持发送邮件，支持 `DKIM` 验证
-   支持 `SMTP` 和 `Resend` 等多种发送方式
-   增加查看 `附件` 功能，支持附件图片显示
-   支持 S3 附件存储和删除功能
-   垃圾邮件检测和黑白名单配置
-   邮件转发功能，支持全局转发地址

### 👥 用户管理

-   使用 `凭证` 重新登录之前的邮箱
-   添加完整的用户注册登录功能，可绑定邮箱地址，绑定后可自动获取邮箱JWT凭证切换不同邮箱
-   支持 `OAuth2` 第三方登录（Github、Authentik 等）
-   支持 `Passkey` 无密码登录
-   用户角色管理，支持多角色域名和前缀配置
-   用户收件箱查看，支持地址和关键词过滤

### 🔧 管理功能

-   完整的 admin 控制台
-   `admin` 后台创建无前缀邮箱
-   admin 用户管理页面，增加用户地址查看功能
-   定时清理功能，支持多种清理策略
-   获取自定义名字的邮箱，`admin` 可配置黑名单
-   增加访问密码，可作为私人站点

### 🌐 多语言与界面

-   前后台均支持多语言
-   现代化 UI 设计，支持响应式布局
-   支持 Google Ads 集成
-   使用 shadow DOM 防止样式污染
-   支持 URL JWT 参数自动登录

### 🤖 集成与扩展

-   完整的 `Telegram Bot` 支持，以及 `Telegram` 推送，Telegram Bot 小程序
-   添加 `SMTP proxy server`，支持 `SMTP` 发送邮件，`IMAP` 查看邮件
-   Webhook 支持，消息推送集成
-   支持 `CF Turnstile` 人机验证
-   限流配置，防止滥用

🏗️ 技术架构
--------

🏗️ 技术架构详情（点击收缩/展开）

### 🏛️ 系统架构

-   **数据库**: Cloudflare D1 作为主数据库
-   **前端部署**: 使用 Cloudflare Pages 部署前端
-   **后端部署**: 使用 Cloudflare Workers 部署后端
-   **邮件转发**: 使用 Cloudflare Email Routing

### 🛠️ 技术栈

-   **前端**: Vue 3 + Vite + TypeScript
-   **后端**: TypeScript + Cloudflare Workers
-   **邮件解析**: Rust WASM (mail-parser-wasm)
-   **数据库**: Cloudflare D1 (SQLite)
-   **存储**: Cloudflare KV + R2 (可选 S3)
-   **代理服务**: Python SMTP/IMAP Proxy Server

### 📦 主要组件

-   **Worker**: 核心后端服务
-   **Frontend**: Vue 3 用户界面
-   **Mail Parser WASM**: Rust 邮件解析模块
-   **SMTP Proxy Server**: Python 邮件代理服务
-   **Pages Functions**: Cloudflare Pages 中间件
-   **Documentation**: VitePress 文档站点

### 提醒

-   在Resend添加域名记录时，如果您域名解析服务商正在托管您的3级域名a.b.com，请删除Resend生成的默认name中二级域名前缀b，否则将会添加a.b.b.com，导致验证失败。添加记录后，可通过

nslookup -qt="mx" a.b.com 1.1.1.1

进行验证。

🌟 加入社区
-------

-   Telegram
