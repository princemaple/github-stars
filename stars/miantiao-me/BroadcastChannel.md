---
project: BroadcastChannel
stars: 1913
description: Turn your Telegram Channel into a MicroBlog.
url: https://github.com/miantiao-me/BroadcastChannel
---

BroadcastChannel
================

**Turn your Telegram Channel into a MicroBlog.**

* * *

English | 简体中文

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

### Platform

1.  Cloudflare
2.  Netlify
3.  Vercel

BroadcastChannel supports deployment on serverless platforms like Cloudflare, Netlify, Vercel that support Node.js SSR, or on a VPS. For detailed tutorials, see Deploy your Astro site.

🧱 Tech Stack
-------------

-   Framework: Astro
-   CMS: Telegram Channels
-   Template: Sepia

🏗️ Deployment
--------------

### Docker

1.  `docker pull ghcr.io/miantiao-me/broadcastchannel:main`
2.  `docker run -d --name broadcastchannel -p 4321:4321 -e CHANNEL=miantiao_me ghcr.io/miantiao-me/broadcastchannel:main`

### Serverless

1.  Fork this project to your GitHub
2.  Create a project on Cloudflare/Netlify/Vercel
3.  Select the `BroadcastChannel` project and the `Astro` framework
4.  Configure the environment variable `CHANNEL` with your channel name. This is the minimal configuration, for more configurations see the options below
5.  Save and deploy
6.  Bind a domain (optional).
7.  Update code, refer to the official GitHub documentation Syncing a fork branch from the web UI.

⚒️ Configuration
----------------

#\# Telegram Channel Username, must be configured. The string of characters following t.me/
CHANNEL\=miantiao\_me

#\# Language and timezone settings, language options see \[dayjs\](https://github.com/iamkun/dayjs/tree/dev/src/locale)
LOCALE\=en
TIMEZONE\=America/New\_York

#\# Social media usernames
TELEGRAM\=miantiao-me
TWITTER\=miantiao-me
GITHUB\=miantiao-me
MASTODON\=mastodon.social/@Mastodon
BLUESKY\=bsky.app

#\# The following two social media need to be URLs
DISCORD\=https://DISCORD.com
PODCAST\=https://PODCAST.com

#\# Header and footer code injection, supports HTML
FOOTER\_INJECT\=FOOTER\_INJECT
HEADER\_INJECT\=HEADER\_INJECT

#\# SEO configuration options, can prevent search engines from indexing content
NO\_FOLLOW\=false
NO\_INDEX\=false

#\# Hide Telegram channel description
HIDE\_DESCRIPTION\=false

#\# Sentry configuration options, collect server-side errors
SENTRY\_AUTH\_TOKEN\=SENTRY\_AUTH\_TOKEN
SENTRY\_DSN\=SENTRY\_DSN
SENTRY\_PROJECT\=SENTRY\_PROJECT

#\# Telegram host name and static resource proxy, not recommended to modify
HOST\=telegram.dog
STATIC\_PROXY\=

#\# Enable Google Site Search
GOOGLE\_SEARCH\_SITE\=memo.miantiao.me

#\# Enable tags page, separate tags with commas
TAGS\=tag1,tag2,tag3

#\# Show comments
COMMENTS\=true

#\# List of links in the Links page, Separate using commas and semicolons
LINKS\=Title1,URL1;Title2,URL3;Title3,URL3;

#\# Sidebar Navigation Item, Separate using commas and semicolons
NAVS\=Title1,URL1;Title2,URL3;Title3,URL3;

#\# Enable RSS beautify
RSS\_BEAUTIFY\=true

🙋🏻 FAQs
---------

1.  Why is the content empty after deployment?
    -   Check if the channel is public, it must be public
    -   The channel username is a string, not a number
    -   Turn off the "Restricting Saving Content" setting in the channel
    -   Redeploy after modifying environment variables
    -   Telegram blocks public display of some sensitive channels, you can verify by visiting `https://t.me/s/channelusername`.

☕ Sponsor
---------

1.  Follow me on Telegram
2.  Follow me on 𝕏
3.  Sponsor me on GitHub
