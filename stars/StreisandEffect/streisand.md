---
project: streisand
stars: 23707
description: Streisand sets up a new server running your choice of WireGuard, OpenConnect, OpenSSH, OpenVPN, Shadowsocks, sslh, Stunnel, or a Tor bridge. It also generates custom instructions for all of these services. At the end of the run you are given an HTML file with instructions that can be shared with friends, family members, and fellow activists.
url: https://github.com/StreisandEffect/streisand
---

Streisand
=========

* * *

English, Français, 简体中文, Русский | Mirror

* * *

Streisand
=========

**Silence censorship. Automate the effect.**

The Internet can be a little unfair. It's way too easy for ISPs, telecoms, politicians, and corporations to block access to the sites and information that you care about. But breaking through these restrictions is _tough_. Or is it?

If you have an account with a cloud computing provider, Streisand can set up a new node with many censorship-resistant VPN services nearly automatically. You'll need a little experience with a Unix command-line. (But without Streisand, it could take days for a skilled Unix administrator to configure these services securely!) At the end, you'll have a private website with software and instructions.

Here's what **a sample Streisand server** looks like.

There's a list of supported cloud providers; experts may be able to use Streisand to install on many other cloud providers.

VPN services
------------

One type of tool that people use to avoid network censorship is a Virtual Private Network (VPN). There are many kinds of VPNs.

Not all network censorship is alike; in some places, it changes from day to day. Streisand provides many different VPN services to try. (You don't have to install them all, though.)

Some Streisand services include add-ons for further censorship and throttling resistance:

-   OpenSSH
    -   Tinyproxy may be used as an HTTP proxy.
-   OpenConnect / Cisco AnyConnect
    -   This protocol is widely used by multi-national corporations, and might not be blocked.
-   OpenVPN
    -   Stunnel add-on available.
-   Shadowsocks,
    -   The V2ray-plugin is installed to provide robust traffic evasion on hostile networks (especially those implementing quality of service (QOS) throttling).
-   A private Tor bridge relay
    -   Obfsproxy with obfs4 available as an add-on.
-   WireGuard, a modern high-performance protocol.

See also:

-   A more technical list of features
-   A more technical list of services

Cloud providers
---------------

-   Amazon Web Services (AWS)
-   Microsoft Azure
-   Digital Ocean
-   Google Compute Engine (GCE)
-   Linode
-   Rackspace

#### Other providers

We recommend using one of the above providers. If you are an expert and can set up a _fresh Ubuntu 16.04 server_ elsewhere, there are "localhost" and "existing remote server" installation methods. For more information, see the advanced installation instructions.

Installation
------------

You need command-line access to a Unix system. You can use Linux, BSD, or macOS; on Windows 10, the Windows Subsystem for Linux (WSL) counts as Linux.

Once you're ready, see the full installation instructions.

Things we want to do better
---------------------------

Aside from a good deal of cleanup, we could really use:

-   Easier setup.
-   Faster adoption of new censorship-avoidance tools

We're looking for help with both.

If there is something that you think Streisand should do, or if you find a bug in its documentation or execution, please file a report on the Issue Tracker.

Core Contributors
-----------------

-   Jay Carlson (@nopdotcom)
-   Nick Clarke (@nickolasclarke)
-   Joshua Lund (@jlund)
-   Ali Makki (@alimakki)
-   Daniel McCarney (@cpu)
-   Corban Raun (@CorbanR)

Acknowledgements
----------------

Jason A. Donenfeld deserves a lot of credit for being brave enough to reimagine what a modern VPN should look like and for coming up with something as good as WireGuard. He has our sincere thanks for all of his patient help and high-quality feedback.

We are grateful to Trevor Smith for his massive contributions. He suggested the Gateway approach, provided tons of invaluable feedback, made _everything_ look better, and developed the HTML template that served as the inspiration to take things to the next level before Streisand's public release.

Huge thanks to Paul Wouters of The Libreswan Project for his generous help troubleshooting the L2TP/IPsec setup.

Starcadian's 'Sunset Blood' album was played on repeat approximately 300 times during the first few months of work on the project in early 2014.
