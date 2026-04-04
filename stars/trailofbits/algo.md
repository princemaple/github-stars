---
project: algo
stars: 30328
description: Set up a personal VPN in the cloud
url: https://github.com/trailofbits/algo
---

Algo VPN
========

Algo VPN is a set of Ansible scripts that simplify the setup of a personal WireGuard and IPsec VPN. It uses the most secure defaults available and works with common cloud providers.

See our release announcement for more information.

Features
--------

-   Supports only IKEv2 with strong crypto (AES-GCM, SHA2, and P-256) for iOS, MacOS, and Linux
-   Supports WireGuard for all of the above, in addition to Android and Windows 11
-   Generates .conf files and QR codes for iOS, macOS, Android, and Windows WireGuard clients
-   Generates Apple profiles to auto-configure iOS and macOS devices for IPsec - no client software required
-   Includes helper scripts to add, remove, and manage users
-   Blocks ads with a local DNS resolver (optional)
-   Sets up limited SSH users for tunneling traffic (optional)
-   Privacy-focused with minimal logging, automatic log rotation, and configurable privacy enhancements
-   Based on Ubuntu 22.04 LTS with automatic security updates
-   Installs to DigitalOcean, Amazon Lightsail, Amazon EC2, Vultr, Microsoft Azure, Google Compute Engine, Scaleway, OpenStack, CloudStack, Hetzner Cloud, Linode, or your own Ubuntu server (for advanced users)

Anti-features
-------------

-   Does not support legacy cipher suites or protocols like L2TP, IKEv1, or RSA
-   Does not install Tor, OpenVPN, or other risky servers
-   Does not depend on the security of TLS
-   Does not claim to provide anonymity or censorship avoidance
-   Does not claim to protect you from the FSB, MSS, DGSE, or FSM

Deploy the Algo Server
----------------------

The easiest way to get an Algo server running is to run it on your local system or from Google Cloud Shell and let it set up a _new_ virtual machine in the cloud for you.

1.  **Setup an account on a cloud hosting provider.** Algo supports DigitalOcean (most user friendly), Amazon Lightsail, Amazon EC2, Vultr, Microsoft Azure, Google Compute Engine, Scaleway, DreamCompute, Linode, other OpenStack-based cloud hosting, CloudStack-based cloud hosting, or Hetzner Cloud.
    
2.  **Get a copy of Algo.** The Algo scripts will be run from your local system. There are two ways to get a copy:
    
    -   Download the ZIP file. Unzip the file to create a directory named `algo-master` containing the Algo scripts.
        
    -   Use `git clone` to create a directory named `algo` containing the Algo scripts:
        
        git clone https://github.com/trailofbits/algo.git
        
3.  **Set your configuration options.** Open `config.cfg` in your favorite text editor. Specify the users you want to create in the `users` list. Create a unique user for each device you plan to connect to your VPN. You should also review the other options before deployment, as changing your mind about them later may require you to deploy a brand new server.
    
4.  **Start the deployment.** Return to your terminal. In the Algo directory, run the appropriate script for your platform:
    
    **macOS/Linux:**
    
    ./algo
    
    **Windows:**
    
    .\\algo.ps1
    
    The first time you run the script, it will automatically install the required Python environment (Python 3.11+). On subsequent runs, it starts immediately and works on all platforms (macOS, Linux, Windows via WSL). The Windows PowerShell script automatically uses WSL when needed, since Ansible requires a Unix-like environment. There are several optional features available, none of which are required for a fully functional VPN server. These optional features are described in the deployment documentation.
    

That's it! You can now set up clients to connect to your VPN. Proceed to Configure the VPN Clients below.

```
    "#                          Congratulations!                            #"
    "#                     Your Algo server is running.                     #"
    "#    Config files and certificates are in the ./configs/ directory.    #"
    "#              Go to https://whoer.net/ after connecting               #"
    "#        and ensure that all your traffic passes through the VPN.      #"
    "#                     Local DNS resolver 172.16.0.1                    #"
    "#        The p12 and SSH keys password for new users is XXXXXXXX       #"
    "#        The CA key password is XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX       #"
    "#      Shell access: ssh -F configs/<server_ip>/ssh_config <hostname>  #"
```

Configure the VPN Clients
-------------------------

Certificates and configuration files that users will need are placed in the `configs` directory. Make sure to secure these files since many contain private keys. All files are saved under a subdirectory named with the IP address of your new Algo VPN server.

**Important for IPsec users**: If you want to add or delete users later, you must select `yes` at the `Do you want to retain the keys (PKI)?` prompt during the server deployment. This preserves the certificate authority needed for user management.

### Apple

WireGuard is used to provide VPN services on Apple devices. Algo generates a WireGuard configuration file, `wireguard/<username>.conf`, and a QR code, `wireguard/<username>.png`, for each user defined in `config.cfg`.

On iOS, install the WireGuard app from the iOS App Store. Then, use the WireGuard app to scan the QR code or AirDrop the configuration file to the device.

On macOS, install the WireGuard app from the Mac App Store. WireGuard will appear in the menu bar once you run the app. Click on the WireGuard icon, choose **Import tunnel(s) from file...**, then select the appropriate WireGuard configuration file.

On either iOS or macOS, you can enable "Connect on Demand" and/or exclude certain trusted Wi-Fi networks (such as your home or work) by editing the tunnel configuration in the WireGuard app. (Algo can't do this automatically for you.)

If you prefer to use the built-in IPsec VPN on Apple devices, or need "Connect on Demand" or excluded Wi-Fi networks automatically configured, see the Apple IPsec client setup guide for detailed configuration instructions.

### Android

WireGuard is used to provide VPN services on Android. Install the WireGuard VPN Client. Import the corresponding `wireguard/<name>.conf` file to your device, then set up a new connection with it. See the Android setup guide for detailed installation and configuration instructions.

### Windows

WireGuard is used to provide VPN services on Windows. Algo generates a WireGuard configuration file, `wireguard/<username>.conf`, for each user defined in `config.cfg`.

Install the WireGuard VPN Client. Import the generated `wireguard/<username>.conf` file to your device, then set up a new connection with it. See the Windows setup instructions for more detailed walkthrough and troubleshooting.

### Linux

Linux clients can use either WireGuard or IPsec:

WireGuard: WireGuard works great with Linux clients. See the Linux WireGuard setup guide for step-by-step instructions on configuring WireGuard on Ubuntu and other distributions.

IPsec: For strongSwan IPsec clients (including OpenWrt, Ubuntu Server, and other distributions), see the Linux IPsec setup guide for detailed configuration instructions.

### OpenWrt

For OpenWrt routers using WireGuard, see the OpenWrt WireGuard setup guide for router-specific configuration instructions.

### Other Devices

For devices not covered above or manual configuration, you'll need specific certificate and configuration files. The files you need depend on your device platform and VPN protocol (WireGuard or IPsec).

-   ipsec/manual/cacert.pem: CA Certificate
-   ipsec/manual/.p12: User Certificate and Private Key (in PKCS#12 format)
-   ipsec/manual/.conf: strongSwan client configuration
-   ipsec/manual/.secrets: strongSwan client configuration
-   ipsec/apple/.mobileconfig: Apple Profile
-   wireguard/.conf: WireGuard configuration profile
-   wireguard/.png: WireGuard configuration QR code

Setup an SSH Tunnel
-------------------

If you turned on the optional SSH tunneling role, local user accounts will be created for each user in `config.cfg`, and SSH authorized\_key files for them will be in the `configs` directory (user.pem). SSH user accounts do not have shell access, cannot authenticate with a password, and only have limited tunneling options (e.g., `ssh -N` is required). This ensures that SSH users have the least access required to set up a tunnel and can perform no other actions on the Algo server.

Use the example command below to start an SSH tunnel by replacing `<user>` and `<ip>` with your own. Once the tunnel is set up, you can configure a browser or other application to use 127.0.0.1:1080 as a SOCKS proxy to route traffic through the Algo server:

ssh -D 127.0.0.1:1080 -f -q -C -N <user\>@algo -i configs/<ip\>/ssh-tunnel/<user\>.pem -F configs/<ip\>/ssh\_config

SSH into Algo Server
--------------------

Your Algo server is configured for key-only SSH access for administrative purposes. Open the Terminal app, `cd` into the `algo-master` directory where you originally downloaded Algo, and then use the command listed on the success message:

```
ssh -F configs/<ip>/ssh_config <hostname>
```

where `<ip>` is the IP address of your Algo server. If you find yourself regularly logging into the server, it will be useful to load your Algo SSH key automatically. Add the following snippet to the bottom of `~/.bash_profile` to add it to your shell environment permanently:

```
ssh-add ~/.ssh/algo > /dev/null 2>&1
```

Alternatively, you can choose to include the generated configuration for any Algo servers created into your SSH config. Edit the file `~/.ssh/config` to include this directive at the top:

```
Include <algodirectory>/configs/*/ssh_config
```

where `<algodirectory>` is the directory where you cloned Algo.

Adding or Removing Users
------------------------

Algo makes it easy to add or remove users from your VPN server after initial deployment.

For IPsec users: You must have selected `yes` at the `Do you want to retain the keys (PKI)?` prompt during the initial server deployment. This preserves the certificate authority needed for user management. You should also save the p12 and CA key passwords shown during deployment, as they're only displayed once.

To add or remove users, first edit the `users` list in your `config.cfg` file. Add new usernames or remove existing ones as needed. Then navigate to the algo directory in your terminal and run:

**macOS/Linux:**

./algo update-users

**Windows:**

.\\algo.ps1 update-users

After the process completes, new configuration files will be generated in the `configs` directory for any new users. The Algo VPN server will be updated to contain only the users listed in the `config.cfg` file. Removed users will no longer be able to connect, and new users will have fresh certificates and configuration files ready for use.

Privacy and Logging
-------------------

Algo takes a pragmatic approach to privacy. By default, we minimize logging while maintaining enough information for security and troubleshooting.

What IS logged by default:

-   System security events (failed SSH attempts, firewall blocks, system updates)
-   Kernel messages and boot diagnostics (with reduced verbosity)
-   WireGuard client state (visible via `sudo wg` - shows last endpoint and handshake time)
-   Basic service status (service starts/stops/errors)
-   All logs automatically rotate and delete after 7 days

Privacy is controlled by two main settings in `config.cfg`:

-   `strongswan_log_level: -1` - Controls StrongSwan connection logging (-1 = disabled, 2 = debug)
-   `privacy_enhancements_enabled: true` - Master switch for log rotation, history clearing, log filtering, and cleanup

To enable full debugging when troubleshooting, set both `strongswan_log_level: 2` and `privacy_enhancements_enabled: false`. This will capture detailed connection logs and disable all privacy features. Remember to revert these changes after debugging.

After deployment, verify your privacy settings:

ssh -F configs/<server\_ip\>/ssh\_config <hostname\>
sudo /usr/local/bin/privacy-monitor.sh

Perfect privacy is impossible with any VPN solution. Your cloud provider sees and logs network traffic metadata regardless of your server configuration. And of course, your ISP knows you're connecting to a VPN server, even if they can't see what you're doing through it.

For the highest level of privacy, treat your Algo servers as disposable. Spin up a new instance when you need it, use it for your specific purpose, then destroy it completely. The ephemeral nature of cloud infrastructure can be a privacy feature if you use it intentionally.

Additional Documentation
------------------------

-   FAQ
-   Troubleshooting
-   How Algo uses Firewalls

### Setup Instructions for Specific Cloud Providers

-   Configure Amazon EC2
-   Configure Azure
-   Configure DigitalOcean
-   Configure Google Cloud Platform
-   Configure Vultr
-   Configure CloudStack
-   Configure Hetzner Cloud

### Install and Deploy from Common Platforms

-   Deploy from macOS
-   Deploy from Windows
-   Deploy from Google Cloud Shell
-   Deploy from a Docker container

### Setup VPN Clients to Connect to the Server

-   Setup Windows clients
-   Setup Android clients
-   Setup Linux clients with Ansible
-   Setup Ubuntu clients to use WireGuard
-   Setup Linux clients to use IPsec
-   Setup Apple devices to use IPsec
-   Setup Macs running macOS 10.13 or older to use WireGuard

### Advanced Deployment

-   Deploy to your own Ubuntu server, and road warrior setup
-   Deploy from Ansible non-interactively
-   Deploy onto a cloud server at time of creation with shell script or cloud-init
-   Deploy to an unsupported cloud provider

If you've read all the documentation and have further questions, create a new discussion.

Endorsements
------------

> I've been ranting about the sorry state of VPN svcs for so long, probably about time to give a proper talk on the subject. TL;DR: use Algo.

\-- Kenn White

> Before picking a VPN provider/app, make sure you do some research https://research.csiro.au/ng/wp-content/uploads/sites/106/2016/08/paper-1.pdf ... – or consider Algo

\-- The Register

> Algo is really easy and secure.

\-- the grugq

> I played around with Algo VPN, a set of scripts that let you set up a VPN in the cloud in very little time, even if you don’t know much about development. I’ve got to say that I was quite impressed with Trail of Bits’ approach.

\-- Romain Dillet for TechCrunch

> If you’re uncomfortable shelling out the cash to an anonymous, random VPN provider, this is the best solution.

\-- Thorin Klosowski for Lifehacker

Contributing
------------

See our Development Guide for information on:

-   Setting up your development environment
-   Using prek hooks for code quality
-   Running tests and linters
-   Contributing code via pull requests

Support Algo VPN
----------------

All donations support continued development. Thanks!

-   We accept donations via PayPal and Patreon.
-   Use our referral code when you sign up to Digital Ocean for a $10 credit.
-   We also accept and appreciate contributions of new code and bugfixes via Github Pull Requests.

Algo is licensed and distributed under the AGPLv3. If you want to distribute a closed-source modification or service based on Algo, then please consider purchasing an exception . As with the methods above, this will help support continued development.
