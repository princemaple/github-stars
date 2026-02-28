---
project: freegeoip
stars: 4937
description: IP geolocation web server
url: https://github.com/fiorix/freegeoip
---

freegeoip
=========

**NOTE:** as of April 2018 this repository is no longer active. Please visit https://github.com/apilayer/freegeoip/ for the current version.

* * *

This is the source code of the freegeoip software. It contains both the web server that empowers freegeoip.net, and a package for the Go programming language that enables any web server to support IP geolocation with a simple and clean API.

See http://en.wikipedia.org/wiki/Geolocation for details about geolocation.

Developers looking for the Go API can skip to the Package freegeoip section below.

Running
-------

This section is for people who desire to run the freegeoip web server on their own infrastructure. The easiest and most generic way of doing this is by using Docker. All examples below use Docker.

### Docker

#### Install Docker

Docker has install instructions for many platforms, including

-   Ubuntu
-   CentOS
-   Mac

#### Run the API in a container

docker run --restart=always -p 8080:8080 -d fiorix/freegeoip

#### Test

curl localhost:8080/json/1.2.3.4
# => {"ip":"1.2.3.4","country\_code":"US","country\_name":"United States", # ...

### Other Linux, OS X, FreeBSD, and Windows

There are pre-compiled binaries available.

### Production configuration

For production workloads you may want to use different configuration for the freegeoip web server, for example:

-   Enabling the "internal server" for collecting metrics and profiling/tracing the freegeoip web server on demand
-   Monitoring the internal server using Prometheus, or exporting your metrics to New Relic
-   Serving the freegeoip API over HTTPS (TLS) using your own certificates, or provisioned automatically using LetsEncrypt.org
-   Configuring HSTS to restrict your browser clients to always use HTTPS
-   Configuring the read and write timeouts to avoid stale clients consuming server resources
-   Configuring the freegeoip web server to read the client IP (for logs, etc) from the X-Forwarded-For header when running behind a reverse proxy
-   Configuring CORS to restrict access to your API to specific domains
-   Configuring a specific endpoint path prefix other than the default "/" (thus /json, /xml, /csv) to serve the API alongside other APIs on the same host
-   Optimizing your round trips by enabling TCP Fast Open on your OS and the freegeoip web server
-   Setting up usage limits (quotas) for your clients (per client IP) based on requests per time interval; we support various backends such as in-memory map (for single instance), or redis or memcache for distributed deployments
-   Serve the default GeoLite2 City free database that is downloaded and updated automatically in background on a configurable schedule, or
-   Serve the commercial GeoIP2 City database from MaxMind, either as a local file that you provide and update periodically (so the server can reload it), or configured to be downloaded periodically using your API key

See the Server Options section below for more information on configuring the server.

For automation, check out the freegeoip chef cookbook or the (legacy) Ansible Playbook for Ubuntu 14.04 LTS.

### Server Options

To see all the available options, use the `-help` option:

docker run --rm -it fiorix/freegeoip -help

If you're using LetsEncrypt.org to provision your TLS certificates, you have to listen for HTTPS on port 443. Following is an example of the server listening on 3 different ports: metrics + pprof (8888), http (80), and https (443):

docker run -p 8888:8888 -p 80:8080 -p 443:8443 -d fiorix/freegeoip \\
	-internal-server=:8888 \\
	-http=:8080 \\
	-https=:8443 \\
	-hsts=max-age=31536000 \\
	-letsencrypt \\
	-letsencrypt-hosts=myfancydomain.io

You can configure the freegeiop web server via command line flags or environment variables. The names of environment variables are the same for command line flags, but prefixed with FREEGEOIP, all upperscase, separated by underscores. If you want to use environment variables instead:

$ cat prod.env
FREEGEOIP\_INTERNAL\_SERVER=:8888
FREEGEOIP\_HTTP=:8080
FREEGEOIP\_HTTPS=:8443
FREEGEOIP\_HSTS=max-age=31536000
FREEGEOIP\_LETSENCRYPT=true
FREEGEOIP\_LETSENCRYPT\_HOSTS=myfancydomain.io

$ docker run --env-file=prod.env -p 8888:8888 -p 80:8080 -p 443:8443 -d fiorix/freegeoip

By default, HTTP/2 is enabled over HTTPS. You can disable by passing the `-http2=false` flag.

Also, the Docker image of freegeoip does not provide the web page from freegeiop.net, it only provides the API. If you want to serve that page, you can pass the `-public=/var/www` parameter in the command line. You can also tell Docker to mount that directory as a volume on the host machine and have it serve your own page, using Docker's `-v` parameter.

If the freegeoip web server is running behind a reverse proxy or load balancer, you have to run it passing the `-use-x-forwarded-for` parameter and provide the `X-Forwarded-For` HTTP header in all requests. This is for the freegeoip web server be able to log the client IP, and to perform geolocation lookups when an IP is not provided to the API, e.g. `/json/` (uses client IP) vs `/json/1.2.3.4`.

Database
--------

The current implementation uses the free GeoLite2 City database from MaxMind.

In the past we had databases from other providers, and at some point even our own database comprised of data from different sources. This means it might change in the future.

If you have purchased the commercial database from MaxMind, you can point the freegeoip web server or (Go API, for dev) to the URL containing the file, or local file, and the server will use it.

In case of files on disk, you can replace the file with a newer version and the freegeoip web server will reload it automatically in background. If instead of a file you use a URL (the default), we periodically check the URL in background to see if there's a new database version available, then download the reload it automatically.

All responses from the freegeiop API contain the date that the database was downloaded in the X-Database-Date HTTP header.

API
---

The freegeoip API is served by endpoints that encode the response in different formats.

Example:

curl freegeoip.net/json/

Returns the geolocation information of your own IP address, the source IP address of the connection.

You can pass a different IP or hostname. For example, to lookup the geolocation of `github.com` the server resolves the name first, then uses the first IP address available, which might be IPv4 or IPv6:

curl freegeoip.net/json/github.com

Same semantics are available for the `/xml/{ip}` and `/csv/{ip}` endpoints.

JSON responses can be encoded as JSONP, by adding the `callback` parameter:

curl freegeoip.net/json/?callback=foobar

The callback parameter is ignored on all other endpoints.

Metrics and profiling
---------------------

The freegeoip web server can provide metrics about its usage, and also supports runtime profiling and tracing.

Both are disabled by default, but can be enabled by passing the `-internal-server` parameter in the command line. Metrics are generated for Prometheus and can be queried at `/metrics` even with curl.

HTTP pprof is available at `/debug/pprof` and the examples from the pprof package documentation should work on the freegeiop web server.

Package freegeoip
-----------------

The freegeoip package for the Go programming language provides two APIs:

-   A database API that requires zero maintenance of the IP database;
-   A geolocation `http.Handler` that can be used/served by any http server.

tl;dr if all you want is code then see the `example_test.go` file.

Otherwise check out the godoc reference.

### Features

-   Zero maintenance

The DB object alone can download an IP database file from the internet and service lookups to your program right away. It will auto-update the file in background and always magically work.

-   DevOps friendly

If you do care about the database and have the commercial version of the MaxMind database, you can update the database file with your program running and the DB object will load it in background. You can focus on your stuff.

-   Extensible

Besides the database part, the package provides an `http.Handler` object that you can add to your HTTP server to service IP geolocation lookups with the same simplistic API of freegeoip.net. There's also an interface for crafting your own HTTP responses encoded in any format.

### Install

Download the package:

```
go get -d github.com/fiorix/freegeoip/...
```

Install the web server:

```
go install github.com/fiorix/freegeoip/cmd/freegeoip
```

Test coverage is quite good, and test code may help you find the stuff you need.
