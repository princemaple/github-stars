---
project: coturn
stars: 13489
description: coturn TURN server project
url: https://github.com/coturn/coturn
---

Docker Hub | GitHub Container Registry | Quay.io

Coturn TURN server
==================

coturn is a free open source implementation of TURN and STUN Server. The TURN Server is a VoIP media traffic NAT traversal server and gateway.

Installing / Getting started
----------------------------

Linux distros may have a version of coturn which you can install by

```
apt install coturn
turnserver --log-file stdout
```

Or run coturn using docker container:

```
docker run -d -p 3478:3478 -p 3478:3478/udp -p 5349:5349 -p 5349:5349/udp -p 49152-65535:49152-65535/udp coturn/coturn
```

See more details about using docker container Docker Readme

Developing
----------

### Dependencies

coturn requires following dependencies to be installed first

-   libevent2

Optional

-   openssl (to support TLS and DTLS, authorized STUN and TURN)
-   libmicrohttp and prometheus-client-c (prometheus interface)
-   MariaDB/MySQL (user database)
-   Hiredis (user database, monitoring)
-   SQLite (user database)
-   PostgreSQL (user database)

### Building

git clone git@github.com:coturn/coturn.git
cd coturn
./configure
make

Features
--------

STUN specs:

-   RFC 3489 - "classic" STUN
-   RFC 5389 - base "new" STUN specs
-   RFC 5769 - test vectors for STUN protocol testing
-   RFC 5780 - NAT behavior discovery support
-   RFC 7443 - ALPN support for STUN & TURN
-   RFC 7635 - oAuth third-party TURN/STUN authorization

TURN specs:

-   RFC 5766 - base TURN specs
-   RFC 6062 - TCP relaying TURN extension
-   RFC 6156 - IPv6 extension for TURN
-   RFC 7443 - ALPN support for STUN & TURN
-   RFC 7635 - oAuth third-party TURN/STUN authorization
-   RFC 8016 - Mobility with Traversal Using Relays around NAT (TURN)
-   DTLS support (http://tools.ietf.org/html/draft-petithuguenin-tram-turn-dtls-00)
-   TURN REST API (http://tools.ietf.org/html/draft-uberti-behave-turn-rest-00)
-   Origin field in TURN (Multi-tenant TURN Server) (https://tools.ietf.org/html/draft-ietf-tram-stun-origin-06)
-   TURN Bandwidth draft specs (http://tools.ietf.org/html/draft-thomson-tram-turn-bandwidth-01)
-   TURN-bis (with dual allocation) draft specs (http://tools.ietf.org/html/draft-ietf-tram-turnbis-04)

ICE and related specs:

-   RFC 5245 - ICE
-   RFC 5768 – ICE–SIP
-   RFC 6336 – ICE–IANA Registry
-   RFC 6544 – ICE–TCP
-   RFC 5928 - TURN Resolution Mechanism

The implementation fully supports the following client-to-TURN-server protocols:

-   UDP (per RFC 5766)
-   TCP (per RFC 5766 and RFC 6062)
-   TLS (per RFC 5766 and RFC 6062): including TLS1.3; ECDHE is supported.
-   DTLS1.0 and DTLS1.2 (http://tools.ietf.org/html/draft-petithuguenin-tram-turn-dtls-00)
-   SCTP (experimental implementation).

Relay protocols:

-   UDP (per RFC 5766)
-   TCP (per RFC 6062)

User databases (for user repository, with passwords or keys, if authentication is required):

-   SQLite
-   MariaDB/MySQL
-   PostgreSQL
-   Redis
-   MongoDB

Management interfaces:

-   telnet cli
-   HTTPS interface

Monitoring:

-   Redis can be used for status and statistics storage and notification
-   prometheus interface (unavailable on apt package)

Message integrity digest algorithms:

-   HMAC-SHA1, with MD5-hashed keys (as required by STUN and TURN standards)

TURN authentication mechanisms:

-   'classic' long-term credentials mechanism;
-   TURN REST API (a modification of the long-term mechanism, for time-limited secret-based authentication, for WebRTC applications: http://tools.ietf.org/html/draft-uberti-behave-turn-rest-00);
-   experimental third-party oAuth-based client authorization option;

Performance and Load Balancing:

When used as a part of an ICE solution, for VoIP connectivity, this TURN server can handle thousands simultaneous calls per CPU (when TURN protocol is used) or tens of thousands calls when only STUN protocol is used. For virtually unlimited scalability a load balancing scheme can be used. The load balancing can be implemented with the following tools (either one or a combination of them):

-   DNS SRV based load balancing;
-   built-in 300 ALTERNATE-SERVER mechanism (requires 300 response support by the TURN client);
-   network load-balancer server.

Traffic bandwidth limitation and congestion avoidance algorithms implemented.

Target platforms:

-   Linux (Debian, Ubuntu, Mint, CentOS, Fedora, Redhat, Amazon Linux, Arch Linux, OpenSUSE)
-   BSD (FreeBSD, NetBSD, OpenBSD, DragonFlyBSD)
-   Solaris 11
-   Mac OS X
-   Cygwin (for non-production R&D purposes)
-   Windows (native with, e.g., MSVC toolchain)

This project can be successfully used on other `*NIX` platforms, too, but that is not officially supported.

The implementation is supposed to be simple, easy to install and configure. The project focuses on performance, scalability and simplicity. The aim is to provide an enterprise-grade TURN solution.

To achieve high performance and scalability, the TURN server is implemented with the following features:

-   High-performance industrial-strength Network IO engine libevent2 is used
-   Configurable multi-threading model implemented to allow full usage of available CPU resources (if OS allows multi-threading)
-   Multiple listening and relay addresses can be configured
-   Efficient memory model used
-   The TURN project code can be used in a custom proprietary networking environment. In the TURN server code, an abstract networking API is used. Only couple files in the project have to be re-written to plug-in the TURN server into a proprietary environment. With this project, only implementation for standard UNIX Networking/IO API is provided, but the user can implement any other environment. The TURN server code was originally developed for a high-performance proprietary corporate environment, then adopted for UNIX Networking API
-   The TURN server works as a user space process, without imposing any special requirements on the system

Links
-----

-   Project homepage: https://coturn.github.io/
-   Repository: https://github.com/coturn/coturn/
-   Issue tracker: https://github.com/coturn/coturn/issues
-   Google group: https://groups.google.com/forum/#!forum/turn-server-project-rfc5766-turn-server
