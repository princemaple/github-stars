---
project: erldns
stars: 468
description: DNS server, in Erlang.
url: https://github.com/dnsimple/erldns
---

Erlang DNS Server
=================

Serve DNS authoritative responses... with Erlang.

This application consists of three main subsystems:

-   `m:erldns_zones` The system responsible for loading and caching zone data.
    
-   `m:erldns_pipeline` The system responsible for processing incoming DNS queries, including resolution and any extension thereof.
    
-   `m:erldns_listeners` The system responsible for listening for incoming DNS queries. The system is designed to be able to listen on multiple ports and interfaces and supports both UDP and TCP, Unix network stack optimisations, and high parallelism.
    

There is also an Admin API for querying the current zone cache and for basic control.

Instrumentation
---------------

Telemetry is used to instrument the code.

All events are divided in the following namespaces:

-   `[erldns, pipeline | _]` are triggered by the `m:erldns_pipeline` subsystem.
-   `[erldns, request | _]` are triggered by the `m:erldns_listeners` subsystem.

Getting started
---------------

You can use this application as a standalone service or embedded into your OTP application. In both cases, you'll need to: configure it, and load zones.

### Zones

Zones are loaded from JSON files in the `priv/zones/` directory. The path is configured in `erldns.config` using the `zones.path` setting. For more details about zone file format and configuration, see `priv/zones/ZONES`.

### Configuration

An example configuration file can be found in `erldns.example.config`. For more details, see the subsystems and the admin API documentation.

To get started, copy it into your own `erldns.config` and modify as needed.

Building
--------

To build:

make

To start fresh:

make fresh
make

Running
-------

### Launch directly

overmind start

### To get an interactive Erlang REPL

rebar3 shell

### Build a distribution with and run the release

rebar3 release
\_build/default/rel/erldns/bin/erldns foreground

Usage
-----

### DNS Queries

Here are some queries to try:

dig -p 8053 @127.0.0.1 example.com a
dig -p 8053 @127.0.0.1 example.com cname
dig -p 8053 @127.0.0.1 example.com ns
dig -p 8053 @127.0.0.1 example.com mx
dig -p 8053 @127.0.0.1 example.com txt
dig -p 8053 @127.0.0.1 example.com sshfp
dig -p 8053 @127.0.0.1 example.com soa
dig -p 8053 @127.0.0.1 example.com naptr
dig -p 8053 @127.0.0.1 -x 127.0.0.1 ptr

### Admin API

The Admin API provides a RESTful HTTP interface for managing zones at runtime. By default, it listens on port `8083`.

# List all zones
curl http://localhost:8083/

# Get zone details
curl http://localhost:8083/zones/example.com

# Get specific records
curl "http://localhost:8083/zones/example.com/records/example.com?type=A"

For complete documentation including authentication, TLS configuration, and extensibility options, see the Admin API documentation.

Performance
-----------

If you want to perform some benchmarks, see the benchmarking guide.

AXFR Support
------------

AXFR zone transfers are not currently implemented. The current implementation (`m:erldns_axfr`) is a stub.

Tests
-----

To run automated tests:

make test

This runs the following:

-   erlfmt
-   Elvis linter
-   xref
-   dialyzer
-   ExDoc
-   Common Tests
-   Coverage
