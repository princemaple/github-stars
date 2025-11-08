---
project: duplicati
stars: 13410
description: Store securely encrypted backups in the cloud!
url: https://github.com/duplicati/duplicati
---

Duplicati
=========

**English** | 中文 | 日本語

Store securely encrypted backups on cloud storage services!

Duplicati is a free, open-source backup client that securely stores encrypted, incremental, and compressed backups on cloud storage services and remote file servers. It supports:

   _Amazon S3, IDrive e2, Backblaze (B2), Box, Dropbox, FTP, Google Cloud and Drive, MEGA, Microsoft Azure and OneDrive, Rackspace Cloud Files, OpenStack Storage (Swift), Storj DCS, SSH (SFTP), WebDAV, Tencent Cloud Object Storage (COS), Aliyun OSS, and more!_

Duplicati is licensed under the MIT license and is available for Windows, macOS, and Linux.

Download
========

Click here to download the latest Duplicati release.

The beta release will automatically notify you of updates and allows you to upgrade with a single click (or command in the terminal). For even more bleeding edge access, check the latest releases or choose another update channel in the UI or on the commandline.

All releases are GPG-signed with the public key 3DAC703D. The latest signature file and ASCII signature file are available on the Duplicati download page.

Support
=======

Duplicati is supported by an active community and you can reach them via our forum.

We also provide a comprehensive Duplicati manual, which you can contribute to.

Features
========

-   Duplicati uses AES-256 encryption (or GNU Privacy Guard) to secure all data before uploading.
-   Only initial backup is with full contents, all additional backups are differential to save bandwidth and storage
-   Built-in scheduler ensures backups stay up-to-date automatically.
-   An integrated updater notifies you of new releases.
-   Encrypted backups can be transferred to destinations like FTP, WebDAV, SSH (SFTP), Amazon S3, and more.
-   Flexible backup options: back up folders, specific file types (e.g., documents or images), or use custom filters.
-   Available as a user-friendly application or a command-line tool.
-   Supports backing up open or locked files using Volume Snapshot Service (VSS) on Windows or Logical Volume Manager (LVM) on Linux.
-   Advanced options for filters, deletion rules, transfer settings, bandwidth limits, and more.

Why Use Duplicati?
==================

Keep your data safe, store it remotely, and back it up regularly! Many backup solutions fail to meet these essential requirements, but Duplicati excels at all three:

-   **Keep your data safe:** Duplicati uses strong encryption to ensure your data remains private. With a secure password, your backup files are safer on a public web server than unencrypted files at home.
-   **Store your backup remotely:** Protect your data from local disasters like fires by storing backups on remote servers. Duplicati supports incremental backups, making it efficient to use distant storage destinations.
-   **Backup regularly:** Outdated backups are as good as no backups. Duplicati's built-in scheduler ensures your backups are always current. It also uses compression and incremental backups to save storage and bandwidth.

Contributing
============

Reporting Bugs
--------------

We use GitHub for bug tracking. Please search existing issues before creating a new one: https://github.com/duplicati/duplicati/issues.

Contributing Translations
-------------------------

Want to help translate Duplicati? Contributions are welcome on Transifex: https://explore.transifex.com/duplicati/duplicati/.

Contributing Code
-----------------

Instructions for setting up your development environment and building Duplicati are available in the documentation. Pull requests for bug fixes or improvements are highly appreciated.

Looking for something to work on? Check out minor change issues or UI-related issues.

Thank you to all our contributors:

Backers
-------

Thank you to all our backers! 🙏

Sponsors
--------

A special thanks to our sponsors for supporting this open-source project:
