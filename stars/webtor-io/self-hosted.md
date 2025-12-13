---
project: self-hosted
stars: 500
description: Self-hosted version of webtor.io implemented as an all-in-one Docker image
url: https://github.com/webtor-io/self-hosted
---

Webtor, self-hosted
===================

This is the self-hosted version of webtor.io, implemented as an all-in-one Docker image.

Features
--------

-   **Direct Download Link (DDL):** Select any file inside a torrent and download it directly.
-   **Instant Video and Audio Streaming:** Choose a video or audio file inside a torrent and start streaming immediately without needing to download it first.  
    **Supported Formats:**
    -   **Video:** `avi`, `mkv`, `mp4`, `webm`, `m4v`, `ts`, `vob`
    -   **Audio:** `mp3`, `wav`, `ogg`, `flac`, `m4a`
-   **Download Entire Torrent as a ZIP Archive:** Download your torrent as a ZIP archive on-the-fly while preserving the original directory structure, without requiring a torrent client.
-   **Personal Library:** Organize your own collection by adding torrents to your account. Movies and series will be detected automatically!
-   **Stremio integration** Just install the addon using the link from profile and start watching your library on TV with Stremio.
-   **Developer-friendly** With the SDK you can provide your users with the ability to watch torrent-videos online on your website.

Quick Setup
-----------

1.  Install Docker.
2.  Start your Webtor instance with the following command:
    
    docker run -d -p 8080:8080 -v data:/data -v pgdata:/pgdata --name webtor --restart=always ghcr.io/webtor-io/self-hosted:latest
    
3.  Access the UI at http://localhost:8080.
4.  You're all set!

You can run your Webtor instance on ElfHosted!

Setting a Custom Domain
-----------------------

If you plan to access your instance from a different host or domain, set the `DOMAIN` environment variable like this:

docker run -e DOMAIN=https://example.com -d -p 8080:8080 -v data:/data -v pgdata:/pgdata --name webtor --restart=always ghcr.io/webtor-io/self-hosted:latest

Setting Custom Port
-------------------

docker run -e DOMAIN=http://localhost:8085 -d -p 8085:8080 -v data:/data -v pgdata:/pgdata --name webtor --restart=always ghcr.io/webtor-io/self-hosted:latest

Configuring the Autocleaner
---------------------------

Webtor automatically cleans old data when there is insufficient space on the device. You can configure this behavior using the following variables:

CLEANER\_FREE=35%
CLEANER\_KEEP\_FREE=25%

-   `CLEANER_FREE` specifies how much space to clean when triggered.
-   `CLEANER_KEEP_FREE` sets the threshold at which cleaning starts.

Both variables can be defined as percentages or as byte values (e.g., `10G` or `100M`).

Configuring Database
--------------------

By default Webtor uses an embedded PostgreSQL database. You can configure the database connection using the following environment variables:

-   **USE\_LOCALPG** - use built-in postgres (default: true)
-   **PG\_HOST** - host for postgres (default: localhost)
-   **PG\_PORT** - port for postgres (default: 5432)
-   **PG\_USER** - user for postgres (default: app)
-   **PG\_PASSWORD** - password for postgres (default: app)
-   **PG\_DATABASE** - database for postgres (default: app)

Configuring content enrichment
------------------------------

-   **OMDB\_API\_KEY** - key for OMDB API
-   **KINOPOISK\_UNOFFICIAL\_API\_KEY** - key for KinoPoisk Unofficial API

Configring Stremio Addon Access
-------------------------------

-   **STREMIO\_ADDON\_USER\_AGENT** - user agent to use for stremio addon
-   **STREMIO\_ADDON\_PROXY** - proxy to use for stremio addon (like socks5://user:pass@host:port)

Configuring Transcoding
-----------------------

-   **DISABLE\_VIDEO\_TRANSCODING** - disables video transcoding (default: false)

Disable UI Features
-------------------

-   **DISABLE\_WEBDAV** - disables WebDAV interface (default: false)
-   **DISABLE\_EMBED** - disables embeds support (default: false)

Other Custom Variables
----------------------

-   **WAIT\_FOR\_VPN** - waits for VPN to start (in case you are using Gluetun) (default: false)
-   **REQUEST\_URL\_MAPPINGS** - custom mappings for request urls
