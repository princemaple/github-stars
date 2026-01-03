---
project: setup-ipsec-vpn
stars: 27203
description: Scripts to build your own IPsec VPN server, with IPsec/L2TP, Cisco IPsec and IKEv2
url: https://github.com/hwdsl2/setup-ipsec-vpn
---

English | 中文 | 日本語

IPsec VPN Server Auto Setup Scripts
===================================

Set up your own IPsec VPN server in just a few minutes, with IPsec/L2TP, Cisco IPsec and IKEv2.

An IPsec VPN encrypts your network traffic, so that nobody between you and the VPN server can eavesdrop on your data as it travels via the Internet. This is especially useful when using unsecured networks, e.g. at coffee shops, airports or hotel rooms.

We will use Libreswan as the IPsec server, and xl2tpd as the L2TP provider.

**» 📖 Book: Privacy Tools in the Age of AI  Build Your Own VPN Server**

Quick start
-----------

First, prepare your Linux server\* with an install of Ubuntu, Debian or CentOS.

Use this one-liner to set up an IPsec VPN server:

wget https://get.vpnsetup.net -O vpn.sh && sudo sh vpn.sh

Your VPN login details will be randomly generated, and displayed when finished.

**Optional:** Install WireGuard and/or OpenVPN on the same server.

See the script in action (terminal recording).

**Note:** This recording is for demo purposes only. VPN credentials in this recording are **NOT** valid.

Click here if you are unable to download.

You may also use `curl` to download:

curl -fsSL https://get.vpnsetup.net -o vpn.sh && sudo sh vpn.sh

Alternative setup URLs:

https://github.com/hwdsl2/setup-ipsec-vpn/raw/master/vpnsetup.sh
https://gitlab.com/hwdsl2/setup-ipsec-vpn/-/raw/master/vpnsetup.sh

If you are unable to download, open vpnsetup.sh, then click the `Raw` button on the right. Press `Ctrl/Cmd+A` to select all, `Ctrl/Cmd+C` to copy, then paste into your favorite editor.

A pre-built Docker image is also available. For other options and client setup, read the sections below.

\* A cloud server, virtual private server (VPS) or dedicated server.

Features
--------

-   Fully automated IPsec VPN server setup, no user input needed
-   Supports IKEv2 with strong and fast ciphers (e.g. AES-GCM)
-   Generates VPN profiles to auto-configure iOS, macOS and Android devices
-   Supports Windows, macOS, iOS, Android, Chrome OS and Linux as VPN clients
-   Includes helper scripts to manage VPN users and certificates

Requirements
------------

A cloud server, virtual private server (VPS) or dedicated server, with an install of:

-   Ubuntu 24.04 or 22.04
-   Debian 13, 12 or 11
-   CentOS Stream 10 or 9
-   Rocky Linux or AlmaLinux
-   Oracle Linux
-   Amazon Linux 2

Other supported Linux distributions.

-   Raspberry Pi OS (Raspbian)
-   Kali Linux
-   Alpine Linux
-   Red Hat Enterprise Linux (RHEL)

This also includes Linux VMs in public clouds, such as DigitalOcean, Vultr, Linode, OVH and Microsoft Azure. Public cloud users can also deploy using user data.

Quick deploy to:

   

**» I want to run my own VPN but don't have a server for that**

For servers with an external firewall (e.g. EC2/GCE), open UDP ports 500 and 4500 for the VPN.

A pre-built Docker image is also available. Advanced users can install on a Raspberry Pi. \[1\] \[2\]

⚠️ **DO NOT** run these scripts on your PC or Mac! They should only be used on a server!

Installation
------------

First, update your server with `sudo apt-get update && sudo apt-get dist-upgrade` (Ubuntu/Debian) or `sudo yum update` and reboot. This is optional, but recommended.

To install the VPN, please choose one of the following options:

**Option 1:** Have the script generate random VPN credentials for you (will be displayed when finished).

wget https://get.vpnsetup.net -O vpn.sh && sudo sh vpn.sh

**Option 2:** Edit the script and provide your own VPN credentials.

wget https://get.vpnsetup.net -O vpn.sh
nano -w vpn.sh
\[Replace with your own values: YOUR\_IPSEC\_PSK, YOUR\_USERNAME and YOUR\_PASSWORD\]
sudo sh vpn.sh

**Note:** A secure IPsec PSK should consist of at least 20 random characters.

**Option 3:** Define your VPN credentials as environment variables.

# All values MUST be placed inside 'single quotes'
# DO NOT use these special characters within values: \\ " '
wget https://get.vpnsetup.net -O vpn.sh
sudo VPN\_IPSEC\_PSK='your\_ipsec\_pre\_shared\_key' \\
VPN\_USER='your\_vpn\_username' \\
VPN\_PASSWORD='your\_vpn\_password' \\
sh vpn.sh

You may optionally install WireGuard and/or OpenVPN on the same server. If your server runs CentOS Stream, Rocky Linux or AlmaLinux, first install OpenVPN/WireGuard, then install the IPsec VPN.

Click here if you are unable to download.

You may also use `curl` to download. For example:

curl -fL https://get.vpnsetup.net -o vpn.sh
sudo sh vpn.sh

Alternative setup URLs:

https://github.com/hwdsl2/setup-ipsec-vpn/raw/master/vpnsetup.sh
https://gitlab.com/hwdsl2/setup-ipsec-vpn/-/raw/master/vpnsetup.sh

If you are unable to download, open vpnsetup.sh, then click the `Raw` button on the right. Press `Ctrl/Cmd+A` to select all, `Ctrl/Cmd+C` to copy, then paste into your favorite editor.

I want to install the older Libreswan version 4.

It is generally recommended to use the latest Libreswan version 5, which is the default version in this project. However, if you want to install the older Libreswan version 4:

wget https://get.vpnsetup.net -O vpn.sh
sudo VPN\_SWAN\_VER=4.15 sh vpn.sh

**Note:** If Libreswan version 5 is already installed, you may need to first Uninstall the VPN before installing Libreswan version 4. Alternatively, download the update script, edit it to specify `SWAN_VER=4.15`, then run the script.

Customize VPN options
---------------------

### Use alternative DNS servers

By default, clients are set to use Google Public DNS when the VPN is active. When installing the VPN, you may optionally specify custom DNS server(s) for all VPN modes. Example:

sudo VPN\_DNS\_SRV1=1.1.1.1 VPN\_DNS\_SRV2=1.0.0.1 sh vpn.sh

Use `VPN_DNS_SRV1` to specify the primary DNS server, and `VPN_DNS_SRV2` to specify the secondary DNS server (optional).

Below is a list of some popular public DNS providers for your reference.

Provider

Primary DNS

Secondary DNS

Notes

Google Public DNS

8.8.8.8

8.8.4.4

Default in this project

Cloudflare

1.1.1.1

1.0.0.1

See also: Cloudflare for families

Quad9

9.9.9.9

149.112.112.112

Blocks malicious domains

OpenDNS

208.67.222.222

208.67.220.220

Blocks phishing domains, configurable.

CleanBrowsing

185.228.168.9

185.228.169.9

Domain filters available

NextDNS

Varies

Varies

Ad blocking, free tier available. Learn more.

Control D

Varies

Varies

Ad blocking, configurable. Learn more.

If you need to change DNS servers after VPN setup, see Advanced usage.

**Note:** If IKEv2 is already set up on the server, the variables above have no effect for IKEv2 mode. In that case, to customize IKEv2 options such as DNS servers, you can first remove IKEv2, then set it up again using `sudo ikev2.sh`.

### Customize IKEv2 options

When installing the VPN, advanced users can optionally customize IKEv2 options.

Option 1: Skip IKEv2 during VPN setup, then set up IKEv2 using custom options.

When installing the VPN, you can skip IKEv2 and only install the IPsec/L2TP and IPsec/XAuth ("Cisco IPsec") modes:

sudo VPN\_SKIP\_IKEV2=yes sh vpn.sh

(Optional) If you want to specify custom DNS server(s) for VPN clients, define `VPN_DNS_SRV1` and optionally `VPN_DNS_SRV2`. See Use alternative DNS servers for details.

After that, run the IKEv2 helper script to set up IKEv2 interactively using custom options:

sudo ikev2.sh

You can customize the following options: VPN server's DNS name, name and validity period of the first client, DNS server for VPN clients and whether to password protect client config files.

**Note:** The `VPN_SKIP_IKEV2` variable has no effect if IKEv2 is already set up on the server. In that case, to customize IKEv2 options, you can first remove IKEv2, then set it up again using `sudo ikev2.sh`.

Option 2: Customize IKEv2 options using environment variables.

When installing the VPN, you can optionally specify a DNS name for the IKEv2 server address. The DNS name must be a fully qualified domain name (FQDN). Example:

sudo VPN\_DNS\_NAME='vpn.example.com' sh vpn.sh

Similarly, you may specify a name for the first IKEv2 client. The default is `vpnclient` if not specified.

sudo VPN\_CLIENT\_NAME='your\_client\_name' sh vpn.sh

By default, clients are set to use Google Public DNS when the VPN is active. You may specify custom DNS server(s) for all VPN modes. Example:

sudo VPN\_DNS\_SRV1=1.1.1.1 VPN\_DNS\_SRV2=1.0.0.1 sh vpn.sh

By default, no password is required when importing IKEv2 client configuration. You can choose to protect client config files using a random password.

sudo VPN\_PROTECT\_CONFIG=yes sh vpn.sh

For reference: List of IKEv1 and IKEv2 parameters.

IKEv1 parameter\*

Default value

Customize (env variable)\*\*

Server address (DNS name)

\-

No, but you can connect using a DNS name

Server address (public IP)

Auto detect

VPN\_PUBLIC\_IP

IPsec pre-shared key

Auto generate

VPN\_IPSEC\_PSK

VPN username

vpnuser

VPN\_USER

VPN password

Auto generate

VPN\_PASSWORD

DNS servers for clients

Google Public DNS

VPN\_DNS\_SRV1, VPN\_DNS\_SRV2

Skip IKEv2 setup

no

VPN\_SKIP\_IKEV2=yes

\* These IKEv1 parameters are for IPsec/L2TP and IPsec/XAuth ("Cisco IPsec") modes.  
\*\* Define these as environment variables when running vpn(setup).sh.

IKEv2 parameter\*

Default value

Customize (env variable)\*\*

Customize (interactive)\*\*\*

Server address (DNS name)

\-

VPN\_DNS\_NAME

✅

Server address (public IP)

Auto detect

VPN\_PUBLIC\_IP

✅

Name of first client

vpnclient

VPN\_CLIENT\_NAME

✅

DNS servers for clients

Google Public DNS

VPN\_DNS\_SRV1, VPN\_DNS\_SRV2

✅

Protect client config files

no

VPN\_PROTECT\_CONFIG=yes

✅

Enable/Disable MOBIKE

Enable if supported

❌

✅

Client cert validity

10 years (120 months)

VPN\_CLIENT\_VALIDITY\*\*\*\*

✅

CA & server cert validity

10 years (120 months)

❌

❌

CA certificate name

IKEv2 VPN CA

❌

❌

Certificate key size

3072 bits

❌

❌

\* These IKEv2 parameters are for IKEv2 mode.  
\*\* Define these as environment variables when running vpn(setup).sh, or when setting up IKEv2 in auto mode (`sudo ikev2.sh --auto`).  
\*\*\* Can be customized during interactive IKEv2 setup (`sudo ikev2.sh`). Refer to option 1 above.  
\*\*\*\* Use `VPN_CLIENT_VALIDITY` to specify the client cert validity period in months. Must be an integer between 1 and 120.

In addition to these parameters, advanced users can also customize VPN subnets during VPN setup.

Next steps
----------

_Read this in other languages: English, 中文, 日本語._

Get your computer or device to use the VPN. Please refer to:

**Configure IKEv2 VPN Clients (recommended)**

**Configure IPsec/L2TP VPN Clients**

**Configure IPsec/XAuth ("Cisco IPsec") VPN Clients**

**Read 📖 VPN book to access extra content.**

Enjoy your very own VPN! ✨🎉🚀✨

Important notes
---------------

**Windows users**: For IPsec/L2TP mode, a one-time registry change is required if the VPN server or client is behind NAT (e.g. home router).

The same VPN account can be used by your multiple devices. However, due to an IPsec/L2TP limitation, if you wish to connect multiple devices from behind the same NAT (e.g. home router), you must use IKEv2 or IPsec/XAuth mode. To view or update VPN user accounts, see Manage VPN users.

For servers with an external firewall (e.g. EC2/GCE), open UDP ports 500 and 4500 for the VPN. Aliyun users, see #433.

Clients are set to use Google Public DNS when the VPN is active. If another DNS provider is preferred, see Advanced usage.

Using kernel support could improve IPsec/L2TP performance. It is available on all supported OS. Ubuntu users should install the `linux-modules-extra-$(uname -r)` package and run `service xl2tpd restart`.

The scripts will backup existing config files before making changes, with `.old-date-time` suffix.

Upgrade Libreswan
-----------------

Use this one-liner to update Libreswan (changelog | announce) on your VPN server.

wget https://get.vpnsetup.net/upg -O vpnup.sh && sudo sh vpnup.sh

Click here if you are unable to download.

You may also use `curl` to download:

curl -fsSL https://get.vpnsetup.net/upg -o vpnup.sh && sudo sh vpnup.sh

Alternative update URLs:

https://github.com/hwdsl2/setup-ipsec-vpn/raw/master/extras/vpnupgrade.sh
https://gitlab.com/hwdsl2/setup-ipsec-vpn/-/raw/master/extras/vpnupgrade.sh

If you are unable to download, open vpnupgrade.sh, then click the `Raw` button on the right. Press `Ctrl/Cmd+A` to select all, `Ctrl/Cmd+C` to copy, then paste into your favorite editor.

The latest supported Libreswan version is `5.3`. Check installed version: `ipsec --version`.

**Note:** `xl2tpd` can be updated using your system's package manager, such as `apt-get` on Ubuntu/Debian.

Manage VPN users
----------------

See Manage VPN users.

-   Manage VPN users using helper scripts
-   View VPN users
-   View or update the IPsec PSK
-   Manually manage VPN users

Advanced usage
--------------

See Advanced usage.

-   Use alternative DNS servers
-   DNS name and server IP changes
-   IKEv2-only VPN
-   Internal VPN IPs and traffic
-   Specify VPN server's public IP
-   Customize VPN subnets
-   Port forwarding to VPN clients
-   Split tunneling
-   Access VPN server's subnet
-   Access VPN clients from server's subnet
-   Modify IPTables rules
-   Deploy Google BBR congestion control

Uninstall the VPN
-----------------

To uninstall IPsec VPN, run the helper script:

**Warning:** This helper script will remove IPsec VPN from your server. All VPN configuration will be **permanently deleted**, and Libreswan and xl2tpd will be removed. This **cannot be undone**!

wget https://get.vpnsetup.net/unst -O unst.sh && sudo bash unst.sh

Click here if you are unable to download.

You may also use `curl` to download:

curl -fsSL https://get.vpnsetup.net/unst -o unst.sh && sudo bash unst.sh

Alternative script URLs:

https://github.com/hwdsl2/setup-ipsec-vpn/raw/master/extras/vpnuninstall.sh
https://gitlab.com/hwdsl2/setup-ipsec-vpn/-/raw/master/extras/vpnuninstall.sh

For more information, see Uninstall the VPN.

Feedback & Questions
--------------------

-   Have a suggestion for this project? Open an Enhancement request. Pull requests are also welcome.
-   If you found a reproducible bug, open a bug report for the IPsec VPN or for the VPN scripts.
-   Got a question? Please first search existing issues and comments in this Gist and on my blog.
-   Ask VPN related questions on the Libreswan or strongSwan mailing list, or read these wikis: \[1\] \[2\] \[3\] \[4\] \[5\].

License
-------

Copyright (C) 2014-2025 Lin Song  
Based on the work of Thomas Sarlandie (Copyright 2012)

  
This work is licensed under the Creative Commons Attribution-ShareAlike 3.0 Unported License  
Attribution required: please include my name in any derivative and let me know how you have improved it!
