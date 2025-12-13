---
project: pig
stars: 171
description: PostgreSQL Extension Package Manager
url: https://github.com/pgsty/pig
---

PIG - Postgres Install Genius
=============================

**pig** is an open-source PostgreSQL (& Extension) Package Manager for mainstream (EL/Debian/Ubuntu) Linux.

Install PostgreSQL 13 ~ 18 along with 473 extensions on (`amd64` / `arm64`) with native OS package manager

Also check the **PGEXT.CLOUD** to get details about the package manager, repository and extension catalog.

* * *

Get Started
-----------

Install the `pig` package first, (you can also use the `apt` / `yum` or just copy the binary)

curl -fsSL https://repo.pigsty.io/pig | bash

Then it's ready to use, assume you want to install the `pg_duckdb` extension:

$ pig repo add pigsty pgdg -u       # add pgdg & pigsty repo, then update repo cache
$ pig ext install pg18              # install PostgreSQL 18 kernels with native PGDG packages
$ pig ext install pg\_duckdb -v 18   # install the pg\_duckdb extension (for current pg18)

That's it, All set! Check the advanced usage for details and the full list 430+ available extensions.

* * *

Installation
------------

The `pig` util is a standalone go binary with no dependencies. You can install with the script:

curl -fsSL https://repo.pigsty.io/pig | bash   # cloudflare default
curl -fsSL https://repo.pigsty.cc/pig | bash   # mainland china mirror

Or just download and extract the binary, or use the `apt/dnf` package manager:

For Ubuntu 22.04 / 24.04 & Debian 12 / 13 or any compatible platforms:

sudo tee /etc/apt/sources.list.d/pigsty.list \> /dev/null <<EOF
deb \[trusted=yes\] https://repo.pigsty.io/apt/infra generic main 
EOF
sudo apt update; sudo apt install -y pig

For EL 8 / 9 / 10 and compatible platforms:

sudo tee /etc/yum.repos.d/pigsty.repo \> /dev/null <<\-'EOF'
\[pigsty-infra\]
name=Pigsty Infra for $basearch
baseurl=https://repo.pigsty.io/yum/infra/$basearch
enabled = 1
gpgcheck = 0
module\_hotfixes=1
EOF
sudo yum makecache; sudo yum install -y pig

> For mainland china user: consider replace the `repo.pigsty.io` with `repo.pigsty.cc`

`pig` has self-update feature, you can update pig itself to the latest version with:

pig update                  # self-update to the latest version
pig update -v 0.7.4         # self-update to the specific version
pig ext reload              # update extension catalog metadata only

* * *

Advanced Usage
--------------

**Environment Status**

pig status                    # show os & pg & pig status
pig repo status               # show upstream repo status
pig ext  status               # show pg extensions status 

**Extension Management**

pig ext list    \[query\]       # list & search extension      
pig ext info    \[ext...\]      # get information of a specific extension
pig ext status  \[-v\]          # show installed extension and pg status
pig ext add     \[ext...\]      # install extension for current pg version
pig ext rm      \[ext...\]      # remove extension for current pg version
pig ext update  \[ext...\]      # update extension to the latest version
pig ext import  \[ext...\]      # download extension to local repo
pig ext link    \[ext...\]      # link postgres installation to path
pig ext upgrade               # fetch the latest extension catalog

**Repo Management**

pig repo list                    # available repo list
pig repo info   \[repo|module...\] # show repo info
pig repo status                  # show current repo status
pig repo add    \[repo|module...\] # add repo and modules
pig repo set    \[repo|module...\] # overwrite & update after add
pig repo rm     \[repo|module...\] # remove repo & modules
pig repo update                  # update repo pkg cache
pig repo create                  # create repo on current system
pig repo boot                    # boot repo from offline package
pig repo cache                   # cache repo as offline package

**Build Management**

pig build repo                   # init build repo (=repo set -ru)
pig build tool  \[mini|full|...\]  # init build toolset
pig build proxy \[id@host:port \]  # init build proxy (optional)
pig build rust                   # init rustc cargo
pig build pgrx  \[-v 0.16.1\]      # init pgrx
pig build spec                   # init build spec repo
pig build get   \[all|std|..\]     # get ext code tarball with prefixes
pig build dep   \[extname...\]     # install extension build deps
pig build ext   \[extname...\]     # build extension
pig build pkg   \[extname...\]     # get+dep+ext, build extension in one-pass

**Radical Repo Admin**

The default `pig repo add pigsty pgdg` will add the `PGDG` repo and `PIGSTY` repo to your system. While the following command will backup & wipe your existing repo and add all require repo to your system.

pig repo add all --ru        # This will OVERWRITE all existing repo with node,pgdg,pigsty repo
pig repo set                 # = pig repo add all --update --remove

There's a brutal version of repo add: `repo set`, which will overwrite you existing repo (`-ru`) by default.

And you can recover you old repos at `/etc/apt/backup` or `/etc/yum.repos.d/backup`.

**Install PostgreSQL**

You can also install PostgreSQL kernel packages with

pig ext install postgresql -v 18 # install PostgreSQL 18 kernels
pig ext install pg17             # install PostgreSQL 17 kernels (all except test/devel)
pig ext install pg16-mini        # install PostgreSQL 16 kernels with minimal packages
pig ext install pg15 -y          # install PostgreSQL 15 kernels with auto-confirm
pig ext install pg14=14.3        # install PostgreSQL 14 kernels with an specific minor version
pig ext install pg13=13.10       # install PostgreSQL 13 kernels

You can link the installed PostgreSQL to the system path with:

pig ext link 17               # create /usr/pgsql -> /usr/pgsql-17 or /usr/lib/postgresql/17 and put its bin dir in your PATH
. /etc/profile.d/pgsql.sh     # reload the path and take effect immediately

You can also use other package aliases, it will translate to corresponding package on your OS distro and the `$v` will be replaced with the active or given pg version number, such as `17`, `16`, etc...

pgsql:        "postgresql$v postgresql$v-server postgresql$v-libs postgresql$v-contrib postgresql$v-plperl postgresql$v-plpython3 postgresql$v-pltcl postgresql$v-llvmjit"
pg18:         "postgresql18 postgresql18-server postgresql18-libs postgresql18-contrib postgresql18-plperl postgresql18-plpython3 postgresql18-pltcl postgresql18-llvmjit"
pg17-client:  "postgresql17"
pg17-server:  "postgresql17-server postgresql17-libs postgresql17-contrib"
pg17-devel:   "postgresql17-devel"
pg17-basic:   "pg\_repack\_17\* wal2json\_17\* pgvector\_17\*"
pg16-mini:    "postgresql16 postgresql16-server postgresql16-libs postgresql16-contrib"
pg15-full:    "postgresql15 postgresql15-server postgresql15-libs postgresql15-contrib postgresql15-plperl postgresql15-plpython3 postgresql15-pltcl postgresql15-llvmjit postgresql15-test postgresql15-devel"
pg14-main:    "postgresql14 postgresql14-server postgresql14-libs postgresql14-contrib postgresql14-plperl postgresql14-plpython3 postgresql14-pltcl postgresql14-llvmjit pg\_repack\_14\* wal2json\_14\* pgvector\_14\*"
pg13-core:    "postgresql13 postgresql13-server postgresql13-libs postgresql13-contrib postgresql13-plperl postgresql13-plpython3 postgresql13-pltcl postgresql13-llvmjit"

More Alias

Take el for examples:

"postgresql":          "postgresql$v\*",
"pgsql-common":        "patroni patroni-etcd pgbouncer pgbackrest pg\_exporter pgbackrest\_exporter vip-manager",
"patroni":             "patroni patroni-etcd",
"pgbouncer":           "pgbouncer",
"pgbackrest":          "pgbackrest",
"pg\_exporter":         "pg\_exporter",
"pgbackrest\_exporter": "pgbackrest\_exporter",
"vip-manager":         "vip-manager",
"pgbadger":            "pgbadger",
"pg\_activity":         "pg\_activity",
"pg\_filedump":         "pg\_filedump",
"pgxnclient":          "pgxnclient",
"pgformatter":         "pgformatter",
"pgcopydb":            "pgcopydb",
"pgloader":            "pgloader",
"pg\_timetable":        "pg\_timetable",
"timescaledb-utils":   "timescaledb-tools timescaledb-event-streamer",
"ivorysql":            "ivorysql5",
"wiltondb":            "wiltondb",
"polardb":             "PolarDB",
"orioledb":            "orioledb\_17 oriolepg\_17",
"openhalodb":          "openhalodb",
"percona-core":        "percona-postgresql18,percona-postgresql18-server,percona-postgresql18-contrib,percona-postgresql18-plperl,percona-postgresql18-plpython3,percona-postgresql18-pltcl,percona-pg\_tde18",
"percona-main":        "percona-postgresql18,percona-postgresql18-server,percona-postgresql18-contrib,percona-postgresql18-plperl,percona-postgresql18-plpython3,percona-postgresql18-pltcl,percona-pg\_tde18,percona-postgis35\_18,percona-postgis35\_18-client,percona-postgis35\_18-utils,percona-pgvector\_18,percona-wal2json18,percona-pg\_repack18,percona-pgaudit18,percona-pgaudit18\_set\_user,percona-pg\_stat\_monitor18,percona-pg\_gather",
"ferretdb":            "ferretdb2",
"duckdb":              "duckdb",
"etcd":                "etcd",
"haproxy":             "haproxy",
"pig":                 "pig",
"vray":                "vray",
"juicefs":             "juicefs",
"restic":              "restic",
"rclone":              "rclone",
"genai-toolbox":       "genai-toolbox",

**Install for another PG**

`pig` will use the default postgres installation in your active `PATH`, but you can install extension for a specific installation with `-v` (when using the PGDG convention), or passing any `pg_config` path for custom installation.

pig ext install pg\_duckdb -v 17     # install the extension for pg17
pig ext install pg\_duckdb -p /usr/lib/postgresql/16/bin/pg\_config    # specify a pg16 pg\_config  

**Install a specific Version**

You can also install PostgreSQL kernel packages with:

pig ext install pgvector=0.8.0 # install pgvector 0.8.0
pig ext install pg16=16.5      # install PostgreSQL 16 with a specific minor version

> Beware the **APT** repo may only have the latest minor version for its software (and require the full version string)

**Search Extension**

You can perform fuzzy search on extension name, description, and category.

$ pig ext ls olap

found 13 extensions matching 'olap':
Name            State  Version  Cate  Flags   License       Repo     PGVer  Package                     Description
----            -----  -------  ----  ------  -------       ------   -----  ------------                ---------------------
citus           avail  13.2.0   OLAP  -dsl--  AGPL-3.0      PIGSTY   14-17  postgresql-17-citus         Distributed PostgreSQL as an extension
citus\_columnar  avail  13.2.0   OLAP  -ds---  AGPL-3.0      PIGSTY   14-17  postgresql-17-citus         Citus columnar storage engine
columnar        n/a    1.1.2    OLAP  -ds---  AGPL-3.0      PIGSTY   13-16  postgresql-17-hydra         Hydra Columnar extension
pg\_analytics    avail  0.3.7    OLAP  -ds-t-  PostgreSQL    PIGSTY   14-17  postgresql-17-pg-analytics  Postgres for analytics, powered by DuckDB
pg\_duckdb       added  1.1.0    OLAP  -dsl--  MIT           PIGSTY   14-18  postgresql-17-pg-duckdb     DuckDB Embedded in Postgres
pg\_mooncake     added  0.2.0    OLAP  -d----  MIT           PIGSTY   14-18  postgresql-17-pg-mooncake   Columnstore Table in Postgres
duckdb\_fdw      avail  1.1.2    OLAP  -ds--r  MIT           PIGSTY   13-17  postgresql-17-duckdb-fdw    DuckDB Foreign Data Wrapper
pg\_parquet      avail  0.5.1    OLAP  -dslt-  PostgreSQL    PIGSTY   14-18  postgresql-17-pg-parquet    copy data between Postgres and Parquet
pg\_fkpart       avail  1.7.0    OLAP  -d----  GPL-2.0       PIGSTY   13-17  postgresql-17-pg-fkpart     Table partitioning by foreign key utility
pg\_partman      avail  5.3.1    OLAP  -ds---  PostgreSQL    PGDG     13-18  postgresql-17-partman       Extension to manage partitioned tables by time or ID
plproxy         avail  2.11.0   OLAP  -ds---  BSD 0-Clause  PGDG     13-18  postgresql-17-plproxy       Database partitioning implemented as procedural language
pg\_strom        n/a    6.0      OLAP  -ds--x  PostgreSQL             n/a                                PG-Strom - big-data processing acceleration using GPU and NVME
tablefunc       added  1.0      OLAP  -ds-tx  PostgreSQL    CONTRIB  13-18  postgresql-17               functions that manipulate whole tables, including crosstab

(13 Rows) (State: added|avail|n/a, Flags: b = HasBin, d = HasDDL, s = HasLib, l = NeedLoad, t = Trusted, r = Relocatable, x = Unknown)

You can use the `-v 16` or `-p /path/to/pg_config` to find extension availability for other PostgreSQL installation.

**Print Extension Summary**

You can get extension metadata with `pig ext info` subcommand:

$ pig ext info pg\_duckdb
╭────────────────────────────────────────────────────────────────────────────╮
│ pg\_duckdb                                                                  │
├────────────────────────────────────────────────────────────────────────────┤
│ DuckDB Embedded in Postgres                                                │
├────────────────────────────────────────────────────────────────────────────┤
│ Extension : pg\_duckdb                                                      │
│ Package   : pg\_duckdb                                                      │
│ Lead Ext  : pg\_duckdb                                                      │
│ Category  : OLAP                                                           │
│ State     : available                                                      │
│ Version   : 1.1.0                                                          │
│ License   : MIT                                                            │
│ Website   : https://github.com/duckdb/pg\_duckdb                            │
│ Details   : https://pgext.cloud/e/pg\_duckdb                                │
├────────────────────────────────────────────────────────────────────────────┤
│ Extension Properties                                                       │
├────────────────────────────────────────────────────────────────────────────┤
│ PostgreSQL Ver │  Available on: 18, 17, 16, 15, 14                         │
│ Contrib :  No  │  Lead Ext :  Yes │  Has Binary :  No                      │
│ CREATE  :  Yes │  CREATE EXTENSION pg\_duckdb;                              │
│ DYLOAD  :  Yes │  SET shared\_preload\_libraries = 'pg\_duckdb'               │
│ TRUST   :  No  │  require database superuser to install                    │
│ Reloc   :  No  │  Schemas: \[\]                                              │
│ Depend  :  No  │                                                           │
├────────────────────────────────────────────────────────────────────────────┤
│ Required By                                                                │
├────────────────────────────────────────────────────────────────────────────┤
│ - pg\_mooncake                                                              │
├────────────────────────────────────────────────────────────────────────────┤
│ See Also                                                                   │
├────────────────────────────────────────────────────────────────────────────┤
│ pg\_mooncake, duckdb\_fdw, pg\_analytics, columnar, citus, citus\_columnar     │
├────────────────────────────────────────────────────────────────────────────┤
│ RPM Package                                                                │
├────────────────────────────────────────────────────────────────────────────┤
│ Repository     │  PIGSTY                                                   │
│ Package        │  pg\_duckdb\_$v\*                                            │
│ Version        │  1.1.0                                                    │
│ Availability   │  18, 17, 16, 15, 14                                       │
├────────────────────────────────────────────────────────────────────────────┤
│ DEB Package                                                                │
├────────────────────────────────────────────────────────────────────────────┤
│ Repository     │  PIGSTY                                                   │
│ Package        │  postgresql-$v\-pg-duckdb                                  │
│ Version        │  1.1.0                                                    │
│ Availability   │  18, 17, 16, 15, 14                                       │
├────────────────────────────────────────────────────────────────────────────┤
│ Source: pg\_duckdb-1.1.0.tar.gz                                             │
├────────────────────────────────────────────────────────────────────────────┤
│ Additional Comments                                                        │
├────────────────────────────────────────────────────────────────────────────┤
│ conflict with duckdb\_fdw                                                   │
╰────────────────────────────────────────────────────────────────────────────╯

**List Repo**

You can list all available repo / module (repo collection) with `pig repo list`:

$ pig repo list

os\_environment: {code: d13, arch: amd64, type: deb, major: 13}
repo\_upstream:  # Available Repo: 15
  - { name: pigsty-local   ,description: 'Pigsty Local'       ,module: local    ,releases: \[11,12,13,20,22,24\] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'http://${admin\_ip}/pigsty ./' }
  - { name: pigsty-pgsql   ,description: 'Pigsty PgSQL'       ,module: pgsql    ,releases: \[11,12,13,20,22,24\] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'https://repo.pigsty.io/apt/pgsql/${distro\_codename} ${distro\_codename} main' }
  - { name: pigsty-infra   ,description: 'Pigsty Infra'       ,module: infra    ,releases: \[11,12,13,20,22,24\] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'https://repo.pigsty.io/apt/infra/ generic main' }
  - { name: docker-ce      ,description: 'Docker'             ,module: infra    ,releases: \[11,12,13,20,22,24\] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'https://download.docker.com/linux/${distro\_name} ${distro\_codename} stable' }
  - { name: base           ,description: 'Debian Basic'       ,module: node     ,releases: \[11,12,13         \] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'http://deb.debian.org/debian/ ${distro\_codename} main non-free-firmware' }
  - { name: updates        ,description: 'Debian Updates'     ,module: node     ,releases: \[11,12,13         \] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'http://deb.debian.org/debian/ ${distro\_codename}-updates main non-free-firmware' }
  - { name: security       ,description: 'Debian Security'    ,module: node     ,releases: \[11,12,13         \] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'http://security.debian.org/debian-security ${distro\_codename}-security main non-free-firmware' }
  - { name: pgdg           ,description: 'PGDG'               ,module: pgsql    ,releases: \[11,12,13,22,24   \] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'http://apt.postgresql.org/pub/repos/apt/ ${distro\_codename}-pgdg main' }
  - { name: pgdg-beta      ,description: 'PGDG Beta'          ,module: beta     ,releases: \[11,12,13,22,24   \] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'http://apt.postgresql.org/pub/repos/apt/ ${distro\_codename}-pgdg-testing main 19' }
  - { name: groonga        ,description: 'Groonga Debian'     ,module: groonga  ,releases: \[11,12,13         \] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'https://packages.groonga.org/debian/ ${distro\_codename} main' }
  - { name: grafana        ,description: 'Grafana'            ,module: grafana  ,releases: \[11,12,13,20,22,24\] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'https://apt.grafana.com stable main' }
  - { name: kubernetes     ,description: 'Kubernetes'         ,module: kube     ,releases: \[11,12,13,20,22,24\] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'https://pkgs.k8s.io/core:/stable:/v1.33/deb/ /' }
  - { name: gitlab-ee      ,description: 'Gitlab EE'          ,module: gitlab   ,releases: \[11,12,13,20,22,24\] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'https://packages.gitlab.com/gitlab/gitlab-ee/${distro\_name}/ ${distro\_codename} main' }
  - { name: gitlab-ce      ,description: 'Gitlab CE'          ,module: gitlab   ,releases: \[11,12,13,20,22,24\] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'https://packages.gitlab.com/gitlab/gitlab-ce/${distro\_name}/ ${distro\_codename} main' }
  - { name: clickhouse     ,description: 'ClickHouse'         ,module: click    ,releases: \[11,12,13,20,22,24\] ,arch: \[x86\_64, aarch64\]  ,baseurl: 'https://packages.clickhouse.com/deb/ stable main' }
repo\_modules:   # Available Modules: 20
  - all       : pigsty-infra, pigsty-pgsql, pgdg, base, updates, extras, epel, centos-sclo, centos-sclo-rh, baseos, appstream, powertools, crb, security, backports
  - pigsty    : pigsty-infra, pigsty-pgsql
  - pgdg      : pgdg
  - node      : base, updates, extras, epel, centos-sclo, centos-sclo-rh, baseos, appstream, powertools, crb, security, backports
  - infra     : pigsty-infra, nginx, docker-ce
  - pgsql     : pigsty-pgsql, pgdg-common, pgdg-el8fix, pgdg-el9fix, pgdg13, pgdg14, pgdg15, pgdg16, pgdg17, pgdg18, pgdg
  - extra     : pgdg-extras, pgdg13-nonfree, pgdg14-nonfree, pgdg15-nonfree, pgdg16-nonfree, pgdg17-nonfree, timescaledb, citus
  - mssql     : wiltondb
  - mysql     : mysql
  - kube      : kubernetes
  - grafana   : grafana
  - beta      : pgdg19-beta, pgdg-beta
  - click     : clickhouse
  - gitlab    : gitlab-ee, gitlab-ce
  - groonga   : groonga
  - haproxy   : haproxyd, haproxyu
  - local     : pigsty-local
  - mongo     : mongo
  - percona   : percona
  - redis     : redis

**Pigsty Management**

The **pig** can also be used as a cli tool for Pigsty — the battery-include free PostgreSQL RDS. Which brings HA, PITR, Monitoring, IaC, and all the extensions to your PostgreSQL cluster.

pig sty init     # install pigsty to ~/pigsty 
pig sty boot     # install ansible and other pre-deps 
pig sty conf     # auto-generate pigsty.yml config file
pig sty install  # run the install.yml playbook

You can use the `pig sty` subcommand to bootstrap pigsty on current node.

**Usage in Docker**

The pig cli is intended to be used on standard linux environment, but you can also use it inside container:

FROM debian:13
USER root
WORKDIR /root/
CMD \["/bin/bash"\]

RUN apt update && apt install -y ca-certificates curl && curl https://repo.pigsty.io/pig | bash
RUN pig repo set && pig install -y -v 18 pgsql pg\_duckdb timescaledb postgis pgvector

**Build Extension**

You can even build rpm / deb directly with `pig build` subcommand:

You can prepare an extension building environment with docker & pig easily:

Building RPM/DEB with pig

FROM debian:13
USER root
WORKDIR /root/
CMD \["/bin/bash"\]

RUN apt update && apt install -y ca-certificates vim ncdu wget curl rsync unzip && \\
    curl https://repo.pigsty.io/pig | bash -s && pig repo add --remove && apt clean
RUN pig repo set && pig build tool && pig build spec && pig build rust && pig build pgrx -v 0.16.1

docker build -t d13:latest .
docker run --name=d13 -d -it d13:latest /bin/bash
docker exec -it d13 /bin/bash

Then building an extension such as timescaledb is as simple as:

$ pig build pkg timescaledb  # now you can build extension with pig!

* * *

Compatibility
-------------

`pig` runs on: RHEL 8/9/10, Ubuntu 22.04/24.04, and Debian 12/13 and compatible OS

Code

Distribution

`x86_64`

`aarch64`

**el10**

RHEL 10 / Rocky10 / Alma10 / ...

PG 18 - 13

PG 18 - 13

**el9**

RHEL 9 / Rocky9 / Alma9 / ...

PG 18 - 13

PG 18 - 13

**el8**

RHEL 8 / Rocky8 / Alma8 / ...

PG 18 - 13

PG 18 - 13

**u24**

Ubuntu 24.04 (`noble`)

PG 18 - 13

PG 18 - 13

**u22**

Ubuntu 22.04 (`jammy`)

PG 18 - 13

PG 18 - 13

**d13**

Debian 13 (`trixie`)

PG 18 - 13

PG 18 - 13

**d12**

Debian 12 (`bookworm`)

PG 18 - 13

PG 18 - 13

* * *

About
-----
