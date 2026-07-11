---
project: syslog-ng
stars: 2353
description: syslog-ng is an enhanced log daemon, supporting a wide range of input and output methods: syslog, unstructured text, queueing, SQL & NoSQL.
url: https://github.com/syslog-ng/syslog-ng
---

syslog-ng
=========

syslog-ng is an enhanced log daemon, supporting a wide range of input and output methods: syslog, unstructured text, message queues, databases (SQL and NoSQL alike), and more.

Quickstart
----------

The simplest configuration accepts system logs from /dev/log (from applications or forwarded by systemd) and writes everything to a single file:

```
@version: current
@include "scl.conf"

log {
	source { system(); };
	destination { file("/var/log/syslog"); };
};
```

This one additionally processes logs from the network (TCP/514 by default):

```
@version: current
@include "scl.conf"

log {
	source {
		system();
		network();
	};
	destination { file("/var/log/syslog"); };
};
```

This config is designed for structured/application logging, using local submission via JSON, and outputting in key=value format:

```
@version: current
@include "scl.conf"

log {
	source { system(); };
	destination { file("/var/log/app.log" template("$(format-welf --subkeys .cim.)\n")); };
};
```

To submit a structured log using `logger`, you might run:

$ logger '@cim: {"name1":"value1", "name2":"value2"}'

In which case the resulting message will be:

```
name1=value1 name2=value2
```

For a brief introduction to configuring the syslog-ng application, see the quickstart guide.

Features
--------

-   Receive and send RFC3164 and RFC5424 style syslog messages
-   Receive and send JSON formatted messages
-   Work with any kind of unstructured data
-   Classify and structure logs using built-in parsers (csv-parser(), db-parser(), kv-parser(), etc.)
-   Normalize, crunch, and process logs as they flow through the system
-   Hand over logs for further processing using files, message queues (like AMQP), or databases (like PostgreSQL or MongoDB)
-   Forward logs to big data tools (like Elasticsearch, Apache Kafka, or Apache Hadoop)

### Performance

-   syslog-ng provides performance levels comparable to a large cluster when running on a single node
-   In the simplest use case, it scales up to 600-800k messages per second
-   But classification, parsing, and filtering still produce several tens of thousands of messages per second

### Community

-   syslog-ng is developed by a community of volunteers, the best way to contact us is via our github project page project, our gitter channel or our mailing list.
-   syslog-ng is integrated into almost all Linux distributions and BSDs, it is also incorporated into a number of products, see our powered by syslog-ng page for more details.

### Sponsors

-   Balabit is the original commercial sponsor of the syslog-ng project, and was acquired by One Identity in 2018. One Identity offers a commercial edition for syslog-ng, called the syslog-ng Premium Edition.
-   Axoflow is the company of Balazs Scheidler, the original creator and main developer of syslog-ng.

Feedback
--------

We are really interested to see who uses our software, so if you do use it and you like what you see, please tell us about it. A star on github or an email saying thanks means a lot already, but telling us about your use case, your experience, and things to improve would be much appreciated.

Just send an email to feedback (at) syslog-ng.org.

_Feedback Powers Open Source._

Installation from source
------------------------

Releases and precompiled tarballs are available on GitHub.

To compile from source, the easiest is to use `dbld`, a docker based, self-hosted compile/build/release infrastructure within the source tree. See `dbld/README.md` for more information.

For the brave souls who want to compile syslog-ng from scratch, the usual drill applies:

```
$ ./configure && make && make install
```

The extra effort in contrast with the dbld based build is the need to fetch and install all build dependencies of syslog-ng (of which there are a few).

If you don't have a configure script (because of cloning from git, for example), run

```
./autogen.sh
```

to generate it.

Some of the functionality of syslog-ng is compiled only if the required development libraries are present. The configure script displays a summary of enabled features at the end of its run. For details, see the syslog-ng compiling instructions.

Installation from binaries
--------------------------

Binaries are available in various Linux distributions and contributors maintain packages of the latest and greatest syslog-ng version for various OSes.

### Debian/Ubuntu

Simply invoke the following command as root:

apt install syslog-ng

The latest versions of syslog-ng are available for a wide range of Debian and Ubuntu releases from our APT repository.

The packages and the APT repository are provided "as is" without warranty of any kind, on a best-effort level.

#### Supported distributions

syslog-ng packages are released for the following distribution versions:

Distro version

sources.list component name

Arch

stable

nightly

Ubuntu 26.04

ubuntu-resolute

x86-64

stable

nightly

Ubuntu 26.04

ubuntu-resolute-arm64

arm64

stable

nightly

Ubuntu 25.04

ubuntu-plucky

x86-64

stable

nightly

Ubuntu 25.04

ubuntu-plucky-arm64

arm64

stable

nightly

Ubuntu 24.04

ubuntu-noble

x86-64

stable

nightly

Ubuntu 24.04

ubuntu-noble-arm64

arm64

stable

nightly

Ubuntu 22.04

ubuntu-jammy

x86-64

stable

nightly

Debian 13

debian-trixie

x86-64

stable

nightly

Debian 13

debian-trixie-arm64

arm64

stable

nightly

Debian 12

debian-bookworm

x86-64

stable

nightly

Debian 12

debian-bookworm-arm64

arm64

stable

nightly

Debian 11

debian-bullseye

x86-64

stable

nightly

Debian Unstable

debian-sid

x86-64

stable

nightly

Debian Testing

debian-testing

x86-64

stable

nightly

#### Adding the APT repository

1.  Download and store the release signing key:
    
    wget -qO - https://ose-repo.syslog-ng.com/apt/syslog-ng-ose-pub.asc | sudo apt-key add -
    
    with newer apt (like on Debian 13 - Trixie)
    
    wget -qO - https://ose-repo.syslog-ng.com/apt/syslog-ng-ose-pub.asc | sudo gpg --dearmor -o /etc/apt/keyrings/syslog-ng-ose.gpg
    
2.  Add the repository containing the latest stable build of syslog-ng to your APT sources. For example if you are running Debian 13 on ARM64, you would use `debian-trixie-arm64` (see chart above) NOTE: For X86-64 you do not have to use any postfix, so, for Debian 13 on X86-64, you should simply use `debian-trixie`.
    
    deb \[signed-by\=/etc/apt/keyrings/syslog-ng-ose.gpg\] https://ose-repo.syslog-ng.com/apt/ stable <os\>\-<codename\>\[-<architecture\>\]
    
    on newer OSes (like on Debian 13 - Trixie)
    
    echo "deb \[signed-by=/etc/apt/keyrings/syslog-ng-ose.gpg\] https://ose-repo.syslog-ng.com/apt/ stable <os>-<codename>\[-<architecture>\]" | sudo tee /etc/apt/sources.list.d/syslog-ng-ose.list \> /dev/null
    
3.  Update your repositories with
    
    sudo apt update
    
4.  Now install syslog-ng:
    
    sudo apt install syslog-ng
    

#### Nightly builds

Nightly packages are built and released from the git `develop` branch everyday.

Use `nightly` instead of `stable` in step 2 to use the nightly APT repository. e.g.:

echo "deb https://ose-repo.syslog-ng.com/apt/ nightly ubuntu-noble" | sudo tee -a /etc/apt/sources.list.d/syslog-ng-ose.list

Nightly builds can be used for testing purposes (obtaining new features and bugfixes) at the risk of breakage.

### RHEL

Simply invoke the following command as root:

dnf install syslog-ng

The latest versions of syslog-ng are available for a wide range of RHEL releases from our DNF repository.

The packages and the DNF repository are provided "as is" without warranty of any kind, on a best-effort level.

#### Supported distributions

syslog-ng packages are released for the following distribution versions:

Distro version

sources.list component name

Arch

stable

nightly

RHEL 8

rhel8

x86-64

stable

nightly

RHEL 8

rhel8-arm64

arm64

stable

nightly

RHEL 9

rhel9

x86-64

stable

nightly

RHEL 9

rhel9-arm64

arm64

stable

nightly

RHEL 10

rhel10

x86-64

stable

nightly

RHEL 10

rhel10-arm64

arm64

stable

nightly

#### Adding the DNF repository

1.  Download and install the repository definition:
    
    sudo curl -o /etc/yum.repos.d/syslog-ng-ose-stable.repo https://ose-repo.syslog-ng.com/yum/syslog-ng-ose-stable.repo
    
2.  Refresh repsitory metadata:
    
    sudo dnf makecache
    
3.  Now install syslog-ng:
    
    sudo dnf install syslog-ng
    

#### Nightly builds

Nightly packages are built and released from the git `develop` branch everyday.

Use `nightly` instead of `stable` in step 1 to use the nightly DNF repository. E.g.:

sudo curl -o /etc/yum.repos.d/syslog-ng-ose-nightly.repo https://ose-repo.syslog-ng.com/yum/syslog-ng-ose-nightly.repo

Nightly builds can be used for testing purposes (obtaining new features and bugfixes) at the risk of breakage.

### Arch Linux

pacman -S syslog-ng

### Fedora

syslog-ng is available as a Fedora package that you can install using dnf:

dnf install syslog-ng

You can download packages for the latest versions from here.

For instructions on how to install syslog-ng on RPM distributions, see the blog post Installing latest syslog-ng on RHEL and other RPM distributions.

If you wish to install the latest RPM package that comes from a recent commit in Git for testing purposes, read the blog post, RPM packages from syslog-ng Git HEAD.

### macOS

brew install syslog-ng

### Others

Binaries for other platforms are listed on the official third party page.

Installation from Docker image
------------------------------

Two flavors of the official syslog-ng image are published:

Image

Base

Init model

Tag

`balabit/syslog-ng`

Debian (trixie)

`syslog-ng -F` as PID 1 (entrypoint wrapper)

`latest` / `nightly`

`balabit/syslog-ng-rpm`

AlmaLinux 9

`systemd` as PID 1, syslog-ng as a service

`latest` / `nightly`

Both images include every published syslog-ng module subpackage (Java-based modules excluded to keep the image lean).

### Debian-based image (`balabit/syslog-ng`)

# Latest official release
docker pull balabit/syslog-ng:latest

# Latest developer nightly build
docker pull balabit/syslog-ng:nightly

# Run (syslog-ng is PID 1 — standard docker run is enough)
docker run -d --name syslog-ng \\
    -p 514:514/udp -p 601:601/tcp -p 6514:6514/tcp \\
    balabit/syslog-ng:latest

### AlmaLinux / systemd-based image (`balabit/syslog-ng-rpm`)

The RPM image runs `systemd` as PID 1 and manages `syslog-ng` as a regular systemd service. systemd-in-container needs a writable cgroup hierarchy and a tmpfs `/run`, so the `docker run` invocation is different from the Debian image:

# Latest official release
docker pull balabit/syslog-ng-rpm:latest

# Latest developer nightly build
docker pull balabit/syslog-ng-rpm:nightly

# Run (Linux host with cgroup v2)
docker run -d --name syslog-ng-rpm \\
    --privileged --cgroupns=host \\
    -p 514:514/udp -p 601:601/tcp -p 6514:6514/tcp \\
    balabit/syslog-ng-rpm:latest

# Run (Docker Desktop on macOS / Windows — add explicit tmpfs and cgroup mounts)
docker run -d --name syslog-ng-rpm \\
    --privileged --cgroupns=host \\
    --tmpfs /run --tmpfs /run/lock \\
    -v /sys/fs/cgroup:/sys/fs/cgroup:rw \\
    -e SYSTEMD\_LOG\_TARGET=console \\
    -p 514:514/udp -p 601:601/tcp -p 6514:6514/tcp \\
    balabit/syslog-ng-rpm:latest

# Inspect / control syslog-ng inside the container
docker exec -it syslog-ng-rpm systemctl status syslog-ng
docker exec -it syslog-ng-rpm syslog-ng-ctl stats

> **Note:** `systemd` logs to the journal, not to container stdout. Use `docker exec <container> journalctl -u syslog-ng` to read syslog-ng's startup logs (or set `-e SYSTEMD_LOG_TARGET=console` to route systemd's own messages to stdout for debugging).

For build instructions and additional run examples, see docker/README.md.

Documentation
-------------

For the latest, markdown based version, see the syslog-ng documentation center.  
The official documentation of the earlier versions (3.X) of syslog-ng Open Source Edition provided by One Identity is available here.

Contributing
------------

If you would like to contribute to syslog-ng, to fix a bug or create a new module, the syslog-ng developer pages helps you take the first steps to working with the code base.
