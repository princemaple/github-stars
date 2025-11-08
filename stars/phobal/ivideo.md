---
project: ivideo
stars: 11872
description: 一个可以观看国内主流视频平台所有视频的客户端（Mac、Windows、Linux） A client that can watch video of domestic(China) mainstream video platform
url: https://github.com/phobal/ivideo
---

### i视频

#### 产品介绍

> 基于 Electron 开发的跨平台客户端版本的视频播放器，该播放器包括国内主流视频平台视频资源，你不用去单独下载各个平台的客户端，只需要使用这一个客户端就能查看所有平台的视频，并且内置了各大视频网站 VIP 资源。

#### 使用方法

1.  下载客户端

-   Mac
-   Windows
-   Linux

1.  选择视频资源

比方说看腾讯视频上的 VIP 才能看的《下一站,别离》

点击进去以后提示需要开通VIP才能看

1.  选择资源播放接口

点击【确定】按钮就可以播放了，如果遇到无法播放的情况，请多换几条线路试试

### 技术栈

-   Electron
-   React
-   Redux

### 如何启动

> node version >= 7.6

1.  clone 项目到本地

git clone https://github.com/phobal/ivideo.git

1.  进入项目 `cd ivideo`
2.  安装依赖 `yarn install`(如果没有的话，请全局安装yarn, `npm i yarn -g`)
3.  打开开发环境 `yarn start`

### 如何编译

-   编译全平台 `yarn package-all`
-   编译当前平台 `yarn package`
-   windows: `yarn package-win`
-   Linux `yarn package-linux`

编译出来的包都放在 `release` 目录下

该项目是基于 electron-react-boilerplate 脚手架 进行创建，感谢 @chentsulin

最后请大家低调使用，祝大家看得舒心
=================

本项目仅作为个人学习用途，如有侵权请联系我删除该仓库
--------------------------
