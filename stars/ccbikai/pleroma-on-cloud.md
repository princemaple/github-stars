---
project: pleroma-on-cloud
stars: 11
description: 在云平台(Koyeb/Render/Northflank/Zeabur/Fly.io)使用 Docker 部署运行 Pleroma。
---

Pleroma On Cloud
================

在云平台使用 Docker 部署运行 Pleroma。

* * *

支持特性
----

1.  支持 Soapbox-FE 前端
2.  支持 Smoji 表情包
3.  禁止搜索引擎索引外站内容，可自己修改 `static/robots.txt` 自定义
4.  支持自定义 static 内容，文件放入 `static` 目录即可。比如 `favicon.ico`

> 部分平台链接含有 Aff, 介意勿点。 如果其他平台测试通过，欢迎告知我来补充

支持部署平台
------

-   Koyeb
-   Render
-   Northflank
-   Zeabur
-   Fly.io

支持数据库平台
-------

-   Aiven
-   Neon

文件存储
----

只支持 S3, 本地存储重启后会丢失，推荐使用 Backblaze B2(套Cloudflare) 或者 Cloudflare R2 都可以做到 10G 存储和无限流量。

使用方式
----

1.  Fork 此项目到你 Github
    
2.  到云平台注册账号，关联你 Github
    
3.  开始部署此项目，**注意修改环境变量** 为你自己的域名和数据库地址
    
    INSTANCE\_NAME\=Pleroma # 实例英文名称
    DOMAIN\=miantiao.me # 实例域名
    DB\_HOST\=pleroma.aivencloud.com # 数据库主机地址
    DB\_PORT\=28404 # 数据库端口
    DB\_NAME\=pleroma # 数据库名称
    DB\_USER\=avnadmin # 数据库用户名
    DB\_PASS\=AVNS\_password # 数据库密码
    
4.  使用云平台的 Console/Shell 功能，注册你的管理员账号（Zeabur 不支持此功能建议本地/其他平台部署创建账号后再部署到 Zeabur）
    
    `./bin/pleroma_ctl user new fakeadmin admin@test.net --admin`
    
5.  云平台绑定域名，管理员账号登录，进入后台配置实例信息（文件存储，Email通知等等）
    
    -   管理界面路径是 `/pleroma/admin/#/`
    -   修改前端为 soapbox 方法：在 Settings - Frontend - Primary 中，修改 Name 为 `soapbox` Reference 为 `static`
    -   不建议加入 Relay, 中继信息大多无用还占用数据库，你只需要关注感兴趣的用户就行
6.  搜索 `@chi@miantiao.me` 并关注（非必须，建议关注），开始嘟嘟
    

演示
--

https://miantiao.me/@chi

致谢
--

1.  https://github.com/angristan/docker-pleroma

* * *