---
project: BroadcastChannel
stars: 2051
description: Turn your Telegram Channel into a MicroBlog.
url: https://github.com/miantiao-me/BroadcastChannel
---

BroadcastChannel
================

**Turn your Telegram Channel into a MicroBlog.**

* * *

English | 简体中文

**Contents:** Features · Demo · Tech Stack · Deployment · Configuration · Themes · FAQs · Sponsor

✨ Features
----------

-   **Turn your Telegram Channel into a MicroBlog**
-   **SEO friendly** `/sitemap.xml`
-   **0 JS on the browser side**
-   **RSS and RSS JSON** `/rss.xml` `/rss.json`

🪧 Demo
-------

### Real users

-   面条实验室
-   Find Blog👁发现博客
-   Memos 广场 🎪
-   APPDO 数字生活指南
-   85.60×53.98卡粉订阅/提醒
-   新闻在花频道
-   ALL About RSS
-   Charles Chin's Whisper
-   PlayStation 新闻转发
-   Yu's Life
-   Leslie 和朋友们
-   OKHK 分享
-   gledos 的微型博客
-   Steve Studio
-   LiFePO4:沙雕吐槽
-   Hotspot Hourly
-   大河马中文财经新闻分享
-   \_My. Tricks 🎩 Collection
-   小报童专栏精选
-   Fake news
-   miyi23's Geekhub资源分享
-   Magazine｜期刊杂志｜财新周刊
-   Remote Jobs & Cooperation
-   甬哥侃侃侃--频道发布
-   Fugoou.log
-   Bboysoul的博客
-   MakerHunter
-   ChatGPT/AI新闻聚合
-   Abner's memos
-   Appinn Talk
-   小报童优惠与排行榜
-   热干面拌 10 号土豆泥
-   万事屋工程部

### Platform

1.  Cloudflare Workers
2.  Netlify
3.  Vercel

BroadcastChannel supports deployment on serverless platforms like Cloudflare Workers, Netlify, Vercel that support SSR, or on a VPS. Cloudflare Pages SSR is not supported with Astro 6 + @astrojs/cloudflare v13; use Workers for Cloudflare deployments. For detailed tutorials, see Deploy your Astro site.

🧱 Tech Stack
-------------

-   Framework: Astro
-   CMS: Telegram Channels
-   Theme inspiration and CSS compatibility: Bear Blog (independently implemented, with no official affiliation or Bear source files included)
-   Optional theme: Sepia
-   Optional theme inspiration: Terminal
-   Optional theme inspiration: Aria
-   Optional theme visual inspiration: Hacker News by Y Combinator, independently implemented with no official affiliation
-   Optional theme visual inspiration: Telegram public channel previews, independently implemented with no official affiliation with Telegram Messenger Inc.
-   Optional theme visual inspiration: Zed's Agentic Engineering page, independently implemented with no official affiliation with Zed Industries, Inc.

🏗️ Deployment
--------------

### Docker

1.  `docker pull ghcr.io/miantiao-me/broadcastchannel:main`
2.  `docker run -d --name broadcastchannel -p 4321:4321 -e CHANNEL=miantiao_me ghcr.io/miantiao-me/broadcastchannel:main`

### Serverless

1.  Fork this project to your GitHub
2.  Create a project on Cloudflare Workers/Netlify/Vercel/EdgeOne
3.  Select the `BroadcastChannel` project and the `Astro` framework
4.  Configure the environment variable `CHANNEL` with your channel name. This is the minimal configuration; see Configuration for more
5.  Save and deploy
6.  Bind a domain (optional)
7.  Update code, refer to the official GitHub documentation Syncing a fork branch from the web UI

EdgeOne is supported and detected automatically through std-env's `edgeone_pages` provider or the platform-provided `EDGEONE_PROJECT_ID`/`EO_MAKERS` variables. Set `SERVER_ADAPTER` only when you need to override automatic adapter detection.

Cloudflare Workers minimal commands:

pnpm exec wrangler login
SERVER\_ADAPTER=cloudflare\_workers pnpm build
pnpm exec wrangler deploy

Configure `CHANNEL` and other runtime values in the Workers dashboard or with `pnpm exec wrangler secret put CHANNEL`. Cloudflare Pages SSR is not supported with Astro 6 + @astrojs/cloudflare v13. Migrate Pages deployments to Workers.

⚒️ Configuration
----------------

### Minimal

Only `CHANNEL` is required. It is the public Telegram channel username (the string after `t.me/`).

CHANNEL\=miantiao\_me

### Full reference

Optional variables. Also see `.env.example`.

#\# Required
CHANNEL\=miantiao\_me

#\# Language and timezone (Intl/BCP 47 locale, e.g. en or zh-CN)
LOCALE\=en
TIMEZONE\=America/New\_York

#\# Social usernames
TELEGRAM\=miantiao-me
TWITTER\=miantiao-me
GITHUB\=miantiao-me
MASTODON\=mastodon.social/@Mastodon
BLUESKY\=bsky.app

#\# Social URLs (full URLs required)
DISCORD\=https://DISCORD.com
PODCAST\=https://PODCAST.com

#\# Trusted-admin raw HTML injection (header / footer)
HEADER\_INJECT\=
FOOTER\_INJECT\=

#\# SEO
NOFOLLOW\=false
NOINDEX\=false

#\# UI
HIDE\_DESCRIPTION\=false
COMMENTS\=true
REACTIONS\=true
RSS\_BEAUTIFY\=true

#\# Tags, links, and navigation (comma / semicolon separated)
TAGS\=tag1,tag2,tag3
LINKS\=Title1,URL1;Title2,URL2;Title3,URL3;
NAVS\=Title1,URL1;Title2,URL2;Title3,URL3;

#\# Search
GOOGLE\_SEARCH\_SITE\=memo.miantiao.me

#\# Advanced (usually leave as-is)
TELEGRAM\_HOST\=telegram.dog
STATIC\_PROXY\=
# Override automatic adapter detection when needed.
SERVER\_ADAPTER\=
# Append hostname-only proxy targets to the defaults, separated by commas (no protocol, port, or path).
TARGET\_WHITELIST\=a.com,b.com

🎨 Themes
---------

Base is always loaded. Leave `HEADER_INJECT` empty to use Base, or load **exactly one** built-in override:

Theme

Path

Sepia

`/themes/sepia.css`

Aria

`/themes/aria.css`

Terminal Amber

`/themes/terminal-amber.css`

Terminal Green

`/themes/terminal-green.css`

Terminal Cyan

`/themes/terminal-cyan.css`

Terminal Magenta

`/themes/terminal-magenta.css`

HN News

`/themes/hn-news.css`

TG Channel

`/themes/tg-channel.css`

ZAE

`/themes/zae.css`

HEADER\_INJECT\='<link rel="stylesheet" href="/themes/aria.css">'

HN News, TG Channel, and ZAE are fixed-light themes. Do not load `/themes/terminal-base.css` directly; there is no `/themes/terminal.css`.

Full configuration, light/dark behavior, platform dashboard values, custom CSS, and security notes: **THEMES.md**. Theme credits: **NOTICE.md**.

🙋🏻 FAQs
---------

1.  Why is the content empty after deployment?
    -   The channel must be **public**
    -   The channel username is a **string**, not a number
    -   Turn off **Restricting Saving Content** in the channel settings
    -   Redeploy after changing environment variables
    -   Telegram may block public display of some sensitive channels; verify at `https://t.me/s/channelusername`

☕ Sponsor
---------

1.  Follow me on Telegram
2.  Follow me on 𝕏
3.  Sponsor me on GitHub
