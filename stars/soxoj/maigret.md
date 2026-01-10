---
project: maigret
stars: 18672
description: 🕵️‍♂️ Collect a dossier on a person by username from thousands of sites
url: https://github.com/soxoj/maigret
---

Maigret
=======

_The Commissioner Jules Maigret is a fictional French police detective, created by Georges Simenon. His investigation method is based on understanding the personality of different people and their interactions._

**👉👉👉 Online Telegram bot**

About
-----

**Maigret** collects a dossier on a person **by username only**, checking for accounts on a huge number of sites and gathering all the available information from web pages. No API keys are required. Maigret is an easy-to-use and powerful fork of Sherlock.

Currently supports more than 3000 sites (full list), search is launched against 500 popular sites in descending order of popularity by default. Also supported checking Tor sites, I2P sites, and domains (via DNS resolving).

Powered By Maigret
------------------

These are professional tools for social media content analysis and OSINT investigations that use Maigret (banners are clickable).

Main features
-------------

-   Profile page parsing, extraction of personal info, links to other profiles, etc.
-   Recursive search by new usernames and other IDs found
-   Search by tags (site categories, countries)
-   Censorship and captcha detection
-   Requests retries

See the full description of Maigret features in the documentation.

Installation
------------

‼️ Maigret is available online via official Telegram bot. Consider using it if you don't want to install anything.

### Windows

Standalone EXE-binaries for Windows are located in Releases section of GitHub repository.

Video guide on how to run it: https://youtu.be/qIgwTZOmMmM.

### Installation in Cloud Shells

You can launch Maigret using cloud shells and Jupyter notebooks. Press one of the buttons below and follow the instructions to launch it in your browser.

### Local installation

Maigret can be installed using pip, Docker, or simply can be launched from the cloned repo.

**NOTE**: Python 3.10 or higher and pip is required, **Python 3.11 is recommended.**

# install from pypi
pip3 install maigret

# usage
maigret username

### Cloning a repository

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

Usage examples
--------------

# make HTML, PDF, and Xmind8 reports
maigret user --html
maigret user --pdf
maigret user --xmind #Output not compatible with xmind 2022+

# search on sites marked with tags photo & dating
maigret user --tags photo,dating

# search on sites marked with tag us
maigret user --tags us

# search for three usernames on all available sites
maigret user1 user2 user3 -a

Use `maigret --help` to get full options description. Also options are documented.

### Web interface

You can run Maigret with a web interface, where you can view the graph with results and download reports of all formats on a single page.

Web Interface Screenshots

Instructions:

1.  Run Maigret with the `--web` flag and specify the port number.

maigret --web 5000

1.  Open http://127.0.0.1:5000 in your browser and enter one or more usernames to make a search.
    
2.  Wait a bit for the search to complete and view the graph with results, the table with all accounts found, and download reports of all formats.
    

Contributing
------------

Maigret has open-source code, so you may contribute your own sites by adding them to `data.json` file, or bring changes to it's code!

For more information about development and contribution, please read the development documentation.

Demo with page parsing and recursive username search
----------------------------------------------------

### Video (asciinema)

### Reports

PDF report, HTML report

Full console output

Disclaimer
----------

**This tool is intended for educational and lawful purposes only.** The developers do not endorse or encourage any illegal activities or misuse of this tool. Regulations regarding the collection and use of personal data vary by country and region, including but not limited to GDPR in the EU, CCPA in the USA, and similar laws worldwide.

It is your sole responsibility to ensure that your use of this tool complies with all applicable laws and regulations in your jurisdiction. Any illegal use of this tool is strictly prohibited, and you are fully accountable for your actions.

The authors and developers of this tool bear no responsibility for any misuse or unlawful activities conducted by its users.

Feedback
--------

If you have any questions, suggestions, or feedback, please feel free to open an issue, create a GitHub discussion, or contact the author directly via Telegram.

SOWEL classification
--------------------

This tool uses the following OSINT techniques:

-   SOTL-2.2. Search For Accounts On Other Platforms
-   SOTL-6.1. Check Logins Reuse To Find Another Account
-   SOTL-6.2. Check Nicknames Reuse To Find Another Account

License
-------

MIT © Maigret  
MIT © Sherlock Project  
Original Creator of Sherlock Project - Siddharth Dushantha
