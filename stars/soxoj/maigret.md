---
project: maigret
stars: 19509
description: 🕵️‍♂️ Collect a dossier on a person by username from 3000+ sites
url: https://github.com/soxoj/maigret
---

Maigret
=======

  

  

**Maigret** collects a dossier on a person **by username only**, checking for accounts on a huge number of sites and gathering all the available information from web pages. No API keys required.

Contents
--------

-   In one minute
-   Main features
-   Demo
-   Installation
-   Usage
-   Contributing
-   Commercial Use
-   About

In one minute
-------------

Ensure you have Python 3.10 or higher.

pip install maigret
maigret YOUR\_USERNAME

No install? Try the Telegram bot or a Cloud Shell.

Want a web UI? See how to launch it.

See also: Quick start.

Main features
-------------

-   Supports 3,000+ sites (see full list). A default run checks the 500 highest-ranked sites by traffic; pass `-a` to scan everything, or `--tags` to narrow by category/country.
-   Embeddable in Python projects — import `maigret` and run searches programmatically (see library usage).
-   Extracts all available information about the account owner from profile pages and site APIs, including links to other accounts.
-   Performs recursive search using discovered usernames and other IDs.
-   Allows filtering by tags (site categories, countries).
-   Detects and partially bypasses blocks, censorship, and CAPTCHA.
-   Fetches an auto-updated site database from GitHub each run (once per 24 hours), and falls back to the built-in database if offline.
-   Works with Tor and I2P websites; able to check domains.
-   Ships with a web interface for browsing results as a graph and downloading reports in every format from a single page.

For the complete feature list, see the features documentation.

### Used by

Professional OSINT and social-media analysis tools built on Maigret:

Demo
----

### Video

### Reports

PDF report, HTML report

Full console output

Installation
------------

Already ran the In one minute steps? You're set. Below are alternative methods.

Don't want to install anything? Use the Telegram bot.

### Windows

Download a standalone EXE from Releases. Video guide: https://youtu.be/qIgwTZOmMmM.

### Cloud Shells

Run Maigret in the browser via cloud shells or Jupyter notebooks:

### Local installation (pip)

# install from pypi
pip3 install maigret

# usage
maigret username

### From source

# or clone and install manually
git clone https://github.com/soxoj/maigret && cd maigret

# build and install
pip3 install .

# usage
maigret username

### Docker

# official image
docker pull soxoj/maigret

# usage
docker run -v /mydir:/app/reports soxoj/maigret:latest username --html

# manual build
docker build -t maigret .

### Troubleshooting

Build errors? See the troubleshooting guide.

Usage
-----

### Examples

# make HTML, PDF, and Xmind8 reports
maigret user --html
maigret user --pdf
maigret user --xmind #Output not compatible with xmind 2022+

# machine-readable exports
maigret user --json ndjson   # newline-delimited JSON (also: --json simple)
maigret user --csv
maigret user --txt
maigret user --graph         # interactive D3 graph (HTML)

# search on sites marked with tags photo & dating
maigret user --tags photo,dating

# search on sites marked with tag us
maigret user --tags us

# search for three usernames on all available sites
maigret user1 user2 user3 -a

Run `maigret --help` for all options. Docs: CLI options, more examples. Running into 403s or timeouts? See TROUBLESHOOTING.md.

### Web interface

Maigret has a built-in web UI with a results graph and downloadable reports.

Web Interface Screenshots

maigret --web 5000

Open http://127.0.0.1:5000, enter a username, and view results.

### Python library

**Maigret can be embedded in your own Python projects.** The CLI is a thin wrapper around an async function you can call directly — build custom pipelines, feed results into your own tooling, or run it inside a larger OSINT workflow.

See the full library usage guide for a working example, async patterns, and how to filter sites by tag.

### Useful CLI flags

-   `--parse URL` — parse a profile page, extract IDs/usernames, and use them to kick off a recursive search.
-   `--permute` — generate likely username variants from two or more inputs (e.g. `john doe` → `johndoe`, `j.doe`, …) and search for all of them.
-   `--self-check [--auto-disable]` — verify `usernameClaimed` / `usernameUnclaimed` pairs against live sites for maintainers auditing the database.

### Tor / I2P / proxies

Maigret can route checks through a proxy, Tor, or I2P — useful for `.onion` / `.i2p` sites and for bypassing WAFs that block datacenter IPs.

# any HTTP/SOCKS proxy
maigret user --proxy socks5://127.0.0.1:1080

# Tor (default gateway socks5://127.0.0.1:9050)
maigret user --tor-proxy socks5://127.0.0.1:9050

# I2P (default gateway http://127.0.0.1:4444)
maigret user --i2p-proxy http://127.0.0.1:4444

Start your Tor / I2P daemon before running the command — Maigret does not manage these gateways.

Contributing
------------

Add or fix new sites surgically in `data.json` (no `json.load`/`json.dump`), then run `./utils/update_site_data.py` to regenerate `sites.md` and the database metadata, and open a pull request. For more details, see the CONTRIBUTING guide and development docs. Release history: CHANGELOG.md.

Commercial Use
--------------

The open-source Maigret is MIT-licensed and free for commercial use without restriction — but site checks break over time and need active maintenance.

For serious commercial use — with a **daily-updated site database** or a **username-check API** — reach out: 📧 maigret@soxoj.com

-   Private site database — 5 000+ sites, updated daily (separate from the public open-source database)
-   Username check API — integrate Maigret into your product

About
-----

### Disclaimer

**For educational and lawful purposes only.** You are responsible for complying with all applicable laws (GDPR, CCPA, etc.) in your jurisdiction. The authors bear no responsibility for misuse.

### Feedback

Open an issue · GitHub Discussions · Telegram

### SOWEL classification

OSINT techniques used:

-   SOTL-2.2. Search For Accounts On Other Platforms
-   SOTL-6.1. Check Logins Reuse To Find Another Account
-   SOTL-6.2. Check Nicknames Reuse To Find Another Account

### License

MIT © Maigret
