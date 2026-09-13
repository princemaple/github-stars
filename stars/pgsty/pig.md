---
project: pig
stars: 204
description: PostgreSQL Extension Package Manager
url: https://github.com/pgsty/pig
---

PIG
===

**PIG** is a self-contained PostgreSQL package manager and operations CLI. It resolves PostgreSQL kernels and extensions to native APT/DNF packages, manages package repositories, builds extension packages, and provides selected PostgreSQL and Pigsty workflows.

-   Website: https://pig.pgsty.com/
-   Documentation: https://pig.pgsty.com/docs/
-   Design records: https://pig.pgsty.com/design/
-   Release notes: https://pig.pgsty.com/release/
-   Extension catalog: https://pigsty.io/ext/

The website is the canonical documentation source. This repository keeps source code, tests, packaging metadata, and only the short project entry point you are reading now.

Install
-------

On a supported RPM or DEB Linux distribution:

curl -fsSL https://repo.pigsty.io/pig | bash

For mainland China:

curl -fsSL https://repo.pigsty.cc/pig | bash

Release RPM, DEB, Linux, and macOS archives are available from GitHub Releases. See the current installation guide for package names, checksums, upgrades, and removal.

Quick start
-----------

pig repo set                        # configure PostgreSQL package repositories
pig install pg18                    # install PostgreSQL 18 packages
pig ext list duck                   # search the extension catalog
pig install pg\_duckdb vector        # install extension packages
pig status                          # inspect the current host

PIG installs host packages. Extension-specific preload, restart, `CREATE EXTENSION`, and SQL upgrade steps remain the operator's responsibility. Follow the extension's own documentation and the PIG getting-started guide.

Command families
----------------

Command

Purpose

Reference

`pig repo`

Configure and inspect APT/DNF repositories

repo

`pig ext`

Search and manage PostgreSQL extension packages

ext

`pig build`

Build PostgreSQL extensions from source

build

`pig install`

Install translated aliases or native package names

commands

`pig sty`

Initialize and operate a Pigsty controller

sty

`pig inventory`

Inspect, edit, validate, and exchange Pigsty Inventory

inventory

`pig do`

Run bounded Pigsty administrative playbooks

do

`pig pg`

Operate a local PostgreSQL instance

pg

`pig pt`

Run Patronictl transparently with local helpers

pt

`pig pe`

Inspect and reload pg\_exporter

pe

`pig pb`

Run pgBackRest backup and restore primitives

pb

`pig pitr`

Run the orchestrated PITR workflow

pitr

Run `pig help COMMAND` for the command's embedded help. Use the linked website pages for the maintained bilingual reference and the Design Records for the reasoning behind major contracts.

Development
-----------

PIG is written in Go. Read AGENTS.md before changing the Cobra command layer.

go test ./...
go vet ./...
make build
make docs-check                    # validate the sibling pig.pgsty.com checkout

Keep Cobra entry points in `cmd/`, concrete command behavior in `cli/*`, and shared foundations in `internal/*`. Do not add a local `docs/` tree: current documentation and design history belong in the dedicated `pig.pgsty.com` repository. Override `DOCS_DIR` when that checkout is not at `../pig.pgsty.com`.

License
-------

Copyright 2018-2026 Ruohang Feng. Licensed under the Apache License 2.0.
