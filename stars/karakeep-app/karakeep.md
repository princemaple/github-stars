---
project: karakeep
stars: 21703
description: A self-hostable bookmark-everything app (links, notes and images) with AI-based automatic tagging and full text search
url: https://github.com/karakeep-app/karakeep
---

Karakeep (previously Hoarder) is a self-hostable bookmark-everything app with a touch of AI for the data hoarders out there.

Features
--------

-   🔗 Bookmark links, take simple notes and store images and pdfs.
-   ⬇️ Automatic fetching for link titles, descriptions and images.
-   📋 Sort your bookmarks into lists.
-   👥 Collaborate with others on the same list.
-   🔎 Full text search of all the content stored.
-   ✨ AI-based (aka chatgpt) automatic tagging and summarization. With supports for local models using ollama!
-   🤖 Rule-based engine for customized management.
-   🎆 OCR for extracting text from images.
-   🔖 Chrome plugin and Firefox addon for quick bookmarking.
-   📱 An iOS app, and an Android app.
-   📰 Auto hoarding from RSS feeds.
-   🔌 REST API and multiple clients.
-   🌐 Multi-language support.
-   🖍️ Mark and store highlights from your hoarded content.
-   🗄️ Full page archival (using monolith) to protect against link rot.
-   ▶️ Auto video archiving using yt-dlp.
-   ☑️ Bulk actions support.
-   🔐 SSO support.
-   🌙 Dark mode support.
-   💾 Self-hosting first.
-   ⬇️ Bookmark importers from Chrome, Pocket, Linkwarden, Omnivore, Tab Session Manager.
-   🔄 Automatic sync with browser bookmarks via floccus.
-   \[Planned\] Offline reading on mobile, semantic search across bookmarks, ...

**⚠️ This app is under heavy development.**

Documentation
-------------

-   Installation
-   Configuration
-   Screenshots
-   Security Considerations
-   Development

Demo
----

You can access the demo at https://try.karakeep.app. Login with the following creds:

```
email: demo@karakeep.app
password: demodemo
```

The demo is seeded with some content, but it's in read-only mode to prevent abuse.

About the name
--------------

The name Karakeep is inspired by the Arabic word "كراكيب" (karakeeb), a colloquial term commonly used to refer to miscellaneous clutter, odds and ends, or items that may seem disorganized but often hold personal value or hidden usefulness. It evokes the image of a messy drawer or forgotten box, full of stuff you can't quite throw away—because somehow, it matters (or more likely, because you're a hoarder!).

Stack
-----

-   NextJS for the web app. Using app router.
-   Drizzle for the database and its migrations.
-   NextAuth for authentication.
-   tRPC for client->server communication.
-   Puppeteer for crawling the bookmarks.
-   OpenAI because AI is so hot right now.
-   Meilisearch for the full content search.

Why did I build it?
-------------------

I browse reddit, twitter and hackernews a lot from my phone. I frequently find interesting stuff (articles, tools, etc) that I'd like to bookmark and read later when I'm in front of a laptop. Typical read-it-later apps usecase. Initially, I was using Pocket for that. Then I got into self-hosting and I wanted to self-host this usecase. I used memos for those quick notes and I loved it but it was lacking some features that I found important for that usecase such as link previews and automatic tagging (more on that in the next section).

I'm a systems engineer in my day job (and have been for the past 7 years). I didn't want to get too detached from the web development world. I decided to build this app as a way to keep my hand dirty with web development, and at the same time, build something that I care about and use every day.

Alternatives
------------

-   memos: I love memos. I have it running on my home server and it's one of my most used self-hosted apps. It doesn't, however, archive or preview the links shared in it. It's just that I dump a lot of links there and I'd have loved if I'd be able to figure which link is that by just looking at my timeline. Also, given the variety of things I dump there, I'd have loved if it does some sort of automatic tagging for what I save there. This is exactly the usecase that I'm trying to tackle with Karakeep.
-   mymind: Mymind is the closest alternative to this project and from where I drew a lot of inspirations. It's a commercial product though.
-   raindrop: A polished open source bookmark manager that supports links, images and files. It's not self-hostable though.
-   Bookmark managers (mostly focused on bookmarking links):
    -   Pocket: Pocket is what hooked me into the whole idea of read-it-later apps. I used it a lot. However, I recently got into home-labbing and became obsessed with the idea of running my services in my home server. Karakeep is meant to be a self-hosting first app.
    -   Linkwarden: An open-source self-hostable bookmark manager that I ran for a bit in my homelab. It's focused mostly on links and supports collaborative collections.
    -   Omnivore: Omnivore is pretty cool open source read-it-later app. Unfortunately, it's heavily dependent on google cloud infra which makes self-hosting it quite hard. They published a blog post on how to run a minimal omnivore but it was lacking a lot of stuff. Self-hosting doesn't really seem to be a high priority for them, and that's something I care about, so I decided to build an alternative.
    -   Wallabag: Wallabag is a well-established open source read-it-later app written in php and I think it's the common recommendation on reddit for such apps. To be honest, I didn't give it a real shot, and the UI just felt a bit dated for my liking. Honestly, it's probably much more stable and feature complete than this app, but where's the fun in that?
    -   Shiori: Shiori is meant to be an open source pocket clone written in Go. It ticks all the marks but doesn't have my super sophisticated AI-based tagging. (JK, I only found about it after I decided to build my own app, so here we are 🤷).

Translations
------------

Karakeep uses Weblate for managing translations. If you want to help translate Karakeep, you can do so here.

Support
-------

If you're enjoying using Karakeep, drop a ⭐️ on the repo!

License
-------

Karakeep is licensed under AGPL-3.0 and owned by Localhost Labs Ltd.

Star History
------------
