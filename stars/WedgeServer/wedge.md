---
project: wedge
stars: 239
description: Fast, cross-platform HTTP/2 web server with automatic HTTPS
url: https://github.com/WedgeServer/wedge
---

Wedge is a general-purpose HTTP/2 web server that serves HTTPS by default.

**Wedge is a fork of Caddy**, with sponsor headers removed. The project is unofficial.

As a result of issue #2, references to Caddy in this documentation are being changed to reference the name "Wedge" instead.

\---

Wedge is fast, easy to use, and makes you more productive.

Available for Windows, Mac, Linux, BSD, Solaris, and Android.

Building Wedge
--------------

```
go get github.com/WedgeServer/builds
go get github.com/WedgeServer/wedge/caddy
```

Then `cd` to `wedge/caddy` and `go run build.go`.

Menu
----

-   Features
-   Install
-   Quick Start
-   Running in Production
-   Contributing
-   About the Project

Features
--------

-   **Easy configuration** with the configuration file
-   **Automatic HTTPS** on by default (via Let's Encrypt)
-   **HTTP/2** by default
-   **Virtual hosting** so multiple sites just work
-   Experimental **QUIC support** for those that like speed
-   TLS session ticket **key rotation** for more secure connections
-   **Extensible with plugins** because a convenient web server is a helpful one
-   **Runs anywhere** with **no external dependencies** (not even libc)

Install
-------

Follow the instructions above for building from source. Binaries will be available soon.

Quick Start
-----------

To serve static files from the current working directory, run:

```
wedge
```

The default port is 2015, so open your browser to http://localhost:2015.

### Go from 0 to HTTPS in 5 seconds

If the binary has permission to bind to low ports and your domain name's DNS records point to the machine you're on:

```
wedge -host example.com
```

This command serves static files from the current directory over HTTPS. Certificates are automatically obtained and renewed for you!

### Customizing your site

To customize how your site is served, create a file named Wedgefile by your site and paste this into it:

```
localhost

push
browse
websocket /echo cat
ext    .html
log    /var/log/access.log
proxy  /api 127.0.0.1:7005
header /api Access-Control-Allow-Origin *
```

When you run `wedge` in that directory, it will automatically find and use that Wedgefile.

This simple file enables server push (via Link headers), allows directory browsing (for folders without an index file), hosts a WebSocket echo server at /echo, serves clean URLs, logs requests to an access log, proxies all API requests to a backend on port 7005, and adds the coveted `Access-Control-Allow-Origin: *` header for all responses from the API.

Wow! Wedge can do a lot with just a few lines.

### Doing more with Wedge

It is possible to host multiple sites and customise the web server using the configuration file.

Sites with qualifying hostnames are served over HTTPS by default.

Wedge has a command line interface. Run `caddy -h` to view basic help.

Running in Production
---------------------

Wedge is production-ready if you find it to be a good fit for your site and workflow.

**Running as root:** We advise against this. You can still listen on ports < 1024 on Linux using setcap like so: `sudo setcap cap_net_bind_service=+ep ./caddy`

How you choose to run Wedge is up to you. Many users are satisfied with `nohup wedge &`. Others use `screen`. Users who need Wedge to come back up after reboots either do so in the script that caused the reboot, add a command to an init script, or configure a service with their OS.

If you have questions or concerns about Wedge' underlying crypto implementations, consult Go's crypto packages, starting with their documentation, then issues, then the code itself; as Wedge uses mainly those libraries.

Contributing
------------

Please see our contributing guidelines for instructions.

We use GitHub issues and pull requests only for discussing bug reports and the development of specific changes.

Thanks for making Wedge -- and the Web -- better!

About the Project
-----------------

Wedge was created following the announcement that sponsor headers would be added to HTTP responses, and official binaries would no longer be able to be used for commercial purposes.

See the HackerNews post.
