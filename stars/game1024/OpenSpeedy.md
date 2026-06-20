---
project: OpenSpeedy
stars: 16236
description: 🎮 An open-source game speed modifier.
url: https://github.com/game1024/OpenSpeedy
---

OpenSpeedy
==========

最好用的开源游戏变速器

  
  
  
  

🌐 English | Deutsch | Français | 日本語 | 한국어 | 中文

🚀 特性
=====

-   快捷变速
-   现代化UI
-   同时可以支持x86和x64平台进程
-   无内核侵入性，Ring3层Hook，不破坏系统内核

💾 安装
=====

📦 **方式1: Winget**

# 安装命令如下
winget install openspeedy

# 打开一个新的终端，运行openspeedy
openspeedy

📥 **方式2: 手动下载**

访问 安装页面 下载最新版本

💻 操作系统要求
=========

-   OS: Windows10 以上
-   平台：x86（32位） 和 x64 （64位）

📝 使用说明
=======

1.  启动 OpenSpeedy
2.  运行需要变速的目标游戏

1.  勾选游戏进程，在 OpenSpeedy 界面中调整速度倍率

1.  即刻生效，对比效果如下

2026-06-20.20-40-21.mp4

🔧 技术原理
=======

编译环境要求：

-   Node.js 18+
-   Rust
-   CMake
-   Visual Studio（含 C++ 桌面开发工作负载）

编译命令：

npm run tauri dev

OpenSpeedy 通过 Hook 以下 Windows 系统时间函数来实现游戏速度调整：

函数名

所属库

功能

Sleep

user32.dll

线程休眠

SetTimer

user32.dll

创建基于消息的计时器

timeGetTime

winmm.dll

获取系统启动后经过的毫秒数

GetTickCount

kernel32.dll

获取系统启动后经过的毫秒数

GetTickCount64

kernel32.dll

获取系统启动后经过的毫秒数(64位)

QueryPerformanceCounter

kernel32.dll

高精度性能计数器

GetSystemTimeAsFileTime

kernel32.dll

获取系统时间

GetSystemTimePreciseAsFileTime

kernel32.dll

获取高精度系统时间

⚠️ 注意事项
=======

-   本工具仅供学习和研究使用
-   部分在线游戏可能有反作弊系统，使用本工具可能导致账号被封禁
-   过度加速可能导致游戏物理引擎异常或崩溃
-   不建议在竞技类在线游戏中使用
-   开源产品不带数字签名，可能被杀毒软件误报

🔄 反馈
=====

如果在使用过程中遇到任何问题，欢迎通过以下方式反馈：

-   FAQ - 先查看wiki定位常见问题
-   GitHub Issues - 提交问题报告, 网盘类问题请勿提issue, 我不支持, 谢谢合作～🙏

📜 开源协议
=======

OpenSpeedy 遵循 GPL v3 许可证。

🙏 鸣谢
=====

OpenSpeedy使用到以下项目的源码，感谢开源社区的力量，如果OpenSpeedy对你有帮助，欢迎Star!

-   minhook: 用于API Hook
-   tauri: GUI

免责声明: OpenSpeedy 仅用于教育和研究目的。用户应自行承担使用本软件的所有风险和责任。作者不对因使用本软件导致的任何损失或法律责任负责。
