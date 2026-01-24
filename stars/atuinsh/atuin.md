---
project: atuin
stars: 28030
description: ✨ Magical shell history
url: https://github.com/atuinsh/atuin
---

_magical shell history_

* * *

English | 简体中文

Atuin replaces your existing shell history with a SQLite database, and records additional context for your commands. Additionally, it provides optional and _fully encrypted_ synchronisation of your history between machines, via an Atuin server.

_exit code, duration, time and command shown_

As well as the search UI, it can do things like this:

```
# search for all successful `make` commands, recorded after 3pm yesterday
atuin search --exit 0 --after "yesterday 3pm" make
```

You may use either the server I host, or host your own! Or just don't use sync at all. As all history sync is encrypted, I couldn't access your data even if I wanted to. And I **really** don't want to.

Features
--------

-   rebind `ctrl-r` and `up` (configurable) to a full screen history search UI
-   store shell history in a sqlite database
-   back up and sync **encrypted** shell history
-   the same history across terminals, across sessions, and across machines
-   log exit code, cwd, hostname, session, command duration, etc
-   calculate statistics such as "most used command"
-   old history file is not replaced
-   quick-jump to previous items with Alt-<num>
-   switch filter modes via ctrl-r; search history just from the current session, directory, or globally
-   enter to execute a command, tab to edit

Documentation
-------------

-   Quickstart
-   Install
-   Setting up sync
-   Import history
-   Basic usage

Supported Shells
----------------

-   zsh
-   bash
-   fish
-   nushell
-   xonsh

Community
---------

### Forum

Atuin has a community forum, please ask here for help and support: https://forum.atuin.sh/

### Discord

Atuin also has a community Discord, available here

Quickstart
==========

This will sign you up for the Atuin Cloud sync server. Everything is end-to-end encrypted, so your secrets are safe!

Read more in the docs for an offline setup, self hosted server, and more.

```
curl --proto '=https' --tlsv1.2 -LsSf https://setup.atuin.sh | sh

atuin register -u <USERNAME> -e <EMAIL>
atuin import auto
atuin sync
```

Then restart your shell!

Note

**For Bash users**: The above sets up `bash-preexec` for necessary hooks, but `bash-preexec` has limitations. For details, please see the Bash section of the shell plugin documentation.

Security
========

If you find any security issues, we'd appreciate it if you could alert ellie@atuin.sh

Contributors
============

Made with contrib.rocks.
