---
project: litestream
stars: 14352
description: Streaming replication for SQLite.
url: https://github.com/benbjohnson/litestream
---

Litestream
==========

Litestream is a standalone disaster recovery tool for SQLite. It runs as a background process and safely replicates changes incrementally to another file or S3. Litestream only communicates with SQLite through the SQLite API so it will not corrupt your database.

If you need support or have ideas for improving Litestream, please visit GitHub Issues. Please visit the Litestream web site for installation instructions and documentation.

If you find this project interesting, please consider starring the project on GitHub.

Source database changes
-----------------------

When Litestream begins replicating a database, it creates an internal `_litestream_lock` table in the source SQLite database. This is expected and safe to leave in place. Litestream uses the table to acquire SQLite's write lock while coordinating synchronization around WAL checkpoints. The writes occur in transactions that are rolled back, so Litestream does not leave rows in the table.

The table is part of the source database, not a separate table in the replica destination. Because the source schema is backed up, restored databases also contain it. Its creation changes the source database schema and can change its page count or bytes, so a database under Litestream should not be expected to remain byte-identical to its pre-Litestream state.

Do not drop `_litestream_lock` while Litestream is running. Synchronization around a checkpoint can fail until Litestream reinitializes the database. Restarting Litestream recreates the missing table automatically.

Contributing
------------

We welcome bug reports, fixes, and patches! Please see our Contributing Guide for details on how to contribute.

Security
--------

Please do not open a public issue for security vulnerabilities. Report them privately through GitHub's private vulnerability reporting, which keeps the report visible only to you and the maintainers until a fix is released. See our Security Policy for what to include and what to expect.

Acknowledgements
----------------

I want to give special thanks to individuals who invest much of their time and energy into the project to help make it better:

-   Thanks to Cory LaNou for giving early feedback and testing when Litestream was still pre-release.
-   Thanks to Michael Lynch for digging into issues and contributing to the documentation.
-   Thanks to Kurt Mackey for feedback and testing.
-   Thanks to Sam Weston for figuring out how to run Litestream on Kubernetes and writing up the docs for it.
-   Thanks to Rafael & Jungle Boogie for helping to get OpenBSD release builds working.
-   Thanks to Simon Gottschlag, Marin,Victor Björklund, Jonathan Beri Yuri, Nathan Probst, Yann Coleu, and Nicholas Grilly for frequent feedback, testing, & support.

Huge thanks to fly.io for their support and for contributing credits for testing and development!
