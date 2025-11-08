---
project: drawnix-seedream
stars: 252
description: Drawnix whiteboard application - open source collaborative drawing tool with mind maps, flowcharts, and free drawing capabilities
url: https://github.com/joeseesun/drawnix-seedream
---

开源白板工具（SaaS），一体化白板，包含思维导图、流程图、自由画等  

-------------------------------------

All in one 白板，思维导图、流程图、自由画等

  

_English README_

特性
--

-   💯 免费 + 开源
-   ⚒️ 思维导图、流程图
-   🖌 画笔
-   😀 插入图片
-   🚀 基于插件机制
-   🖼️ 📃 导出为 PNG, JSON(`.drawnix`)
-   💾 自动保存（浏览器缓存）
-   ⚡ 编辑特性：撤销、重做、复制、粘贴等
-   🌌 无限画布：缩放、滚动
-   🎨 主题模式
-   📱 移动设备适配
-   📈 支持 mermaid 语法转流程图
-   ✨ 支持 markdown 文本转思维导图（新支持 🔥🔥🔥）

关于名称
----

_**Drawnix**_ ，源于绘画( _**Draw**_ )与凤凰( _**Phoenix**_ )的灵感交织。

凤凰象征着生生不息的创造力，而 _Draw_ 代表着人类最原始的表达方式。在这里，每一次创作都是一次艺术的涅槃，每一笔绘画都是灵感的重生。

创意如同凤凰，浴火方能重生，而 _**Drawnix**_ 要做技术与创意之火的守护者。

_Draw Beyond, Rise Above._

与 Plait 画图框架
------------

_Drawnix_ 的定位是一个开箱即用、开源、免费的工具产品，它的底层是 _Plait_ 框架，_Plait_ 是我司开源的一款画图框架，代表着公司在知识库产品(PingCode Wiki)上的重要技术沉淀。

Drawnix 是插件架构，与前面说到开源工具比技术架构更复杂一些，但是插件架构也有优势，比如能够支持多种 UI 框架（_Angular、React_），能够集成不同富文本框架（当前仅支持 _Slate_ 框架），在开发上可以很好的实现业务的分层，开发各种细粒度的可复用插件，可以扩展更多的画板的应用场景。

仓储结构
----

```
drawnix/
├── apps/
│   ├── web                   # drawnix.com
│   │    └── index.html       # HTML
├── dist/                     # 构建产物
├── packages/
│   └── drawnix/              # 白板应用
│   └── react-board/          # 白板 React 视图层
│   └── react-text/           # 文本渲染模块
├── package.json
├── ...
└── README.md
└── README_en.md

```

应用
--

_https://drawnix.com_ 是 _drawnix_ 的最小化应用。

近期会高频迭代 drawnix.com，直到发布 _Dawn（破晓）_ 版本。

开发
--

```
npm install

npm run start
```

Docker
------

```
docker pull pubuzhixing/drawnix:latest
```

依赖
--

-   plait - 开源画图框架
-   slate - 富文本编辑器框架
-   floating-ui - 一个超级好用的创建弹出层基础库

贡献
--

欢迎任何形式的贡献：

-   提 Bug
    
-   贡献代码
    

感谢支持
----

特别感谢公司对开源项目的大力支持，也感谢为本项目贡献代码、提供建议的朋友。

License
-------

MIT License
