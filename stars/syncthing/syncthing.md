---
project: syncthing
stars: 79708
description: Open Source Continuous File Synchronization
url: https://github.com/syncthing/syncthing
---

* * *

Goals
-----

Syncthing is a **continuous file synchronization program**. It synchronizes files between two or more computers. We strive to fulfill the goals below. The goals are listed in order of importance, the most important ones first. This is the summary version of the goal list - for more commentary, see the full Goals document.

Syncthing should be:

1.  **Safe From Data Loss**
    
    Protecting the user's data is paramount. We take every reasonable precaution to avoid corrupting the user's files.
    
2.  **Secure Against Attackers**
    
    Again, protecting the user's data is paramount. Regardless of our other goals, we must never allow the user's data to be susceptible to eavesdropping or modification by unauthorized parties.
    
3.  **Easy to Use**
    
    Syncthing should be approachable, understandable, and inclusive.
    
4.  **Automatic**
    
    User interaction should be required only when absolutely necessary.
    
5.  **Universally Available**
    
    Syncthing should run on every common computer. We are mindful that the latest technology is not always available to every individual.
    
6.  **For Individuals**
    
    Syncthing is primarily about empowering the individual user with safe, secure, and easy to use file synchronization.
    
7.  **Everything Else**
    
    There are many things we care about that don't make it on to the list. It is fine to optimize for these values, as long as they are not in conflict with the stated goals above.
    

Getting Started
---------------

Take a look at the getting started guide.

There are a few examples for keeping Syncthing running in the background on your system in the etc directory. There are also several GUI implementations for Windows, Mac, and Linux.

Docker
------

To run Syncthing in Docker, see the Docker README.

Getting in Touch
----------------

The first and best point of contact is the Forum. If you've found something that is clearly a bug, feel free to report it in the GitHub issue tracker.

If you believe that you’ve found a Syncthing-related security vulnerability, please report it by emailing security@syncthing.net. Do not report it in the Forum or issue tracker.

Building
--------

Building Syncthing from source is easy. After extracting the source bundle from a release or checking out git, you just need to run `go run build.go` and the binaries are created in `./bin`. There's a guide with more details on the build process.

Signed Releases
---------------

Release binaries are GPG signed with the key available from https://syncthing.net/security/. There is also a built-in automatic upgrade mechanism (disabled in some distribution channels) which uses a compiled in ECDSA signature. macOS and Windows binaries are also code-signed.

Documentation
-------------

Please see the Syncthing documentation site \[source\].

All code is licensed under the MPLv2 License.
