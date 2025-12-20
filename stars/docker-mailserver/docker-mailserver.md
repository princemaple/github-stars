---
project: docker-mailserver
stars: 17606
description: Production-ready fullstack but simple mail server (SMTP, IMAP, LDAP, Antispam, Antivirus, etc.) running inside a container.
url: https://github.com/docker-mailserver/docker-mailserver
---

Docker Mailserver
=================

📃 About
--------

A production-ready fullstack but simple containerized mail server (SMTP, IMAP, LDAP, Anti-spam, Anti-virus, etc.).

-   Only configuration files, no SQL database. Keep it simple and versioned. Easy to deploy and upgrade.
-   Originally created by @tomav, this project is now maintained by volunteers since January 2021.

Tip

Be sure to read our documentation. It provides guidance on initial setup of your mail server.

Important

If you have issues, please search through the documentation **for your version** before opening an issue.

The issue tracker is for issues, not for personal support.  
Make sure the version of the documentation matches the image version you're using!

🔗 Links to Useful Resources
----------------------------

1.  FAQ
2.  Usage
3.  Examples
4.  Issues and Contributing
5.  Release Notes
6.  Environment Variables
7.  Updating

📦 Included Services
--------------------

-   Postfix with SMTP or LDAP authentication and support for extension delimiters
-   Dovecot with SASL, IMAP, POP3, LDAP, basic Sieve support and quotas
-   Rspamd
-   Amavis
-   SpamAssassin supporting custom rules
-   ClamAV with automatic updates
-   OpenDKIM & OpenDMARC
-   Fail2ban
-   Fetchmail
-   Getmail6
-   Postscreen
-   Postgrey
-   Support for LetsEncrypt, manual and self-signed certificates
-   A setup script for easy configuration and maintenance
-   SASLauthd with LDAP authentication
-   OAuth2 authentication (_via `XOAUTH2` or `OAUTHBEARER` SASL mechanisms_)
