---
project: obligator
stars: 798
description: Simple and opinionated OpenID Connect server designed for self-hosters
url: https://github.com/lastlogin-net/obligator
---

Introduction
============

obligator is a relatively simple and opinionated OpenID Connect (OIDC) Provider (OP) server designed for self-hosters.

Hacker News discussion here.

Motivation
==========

There are lots of great open source OIDC servers out there (see comparison). I made obligator because I needed a specific combination of features I didn't find in any of the others. Here's a brief list. See the feature explanation section for more detailed information.

-   Simple to deploy and manage. Static executable and either flat-file or sqlite storage
-   Support for anonymous OAuth2 client auth
-   Authenticate to multiple domains at once
-   Passwordless email login
-   Configurable at runtime with an API
-   Support for forward auth
-   Support for trusted headers
-   Support for upstream social login providers (GitLab, GitHub, Google, etc)

Design
======

The overarching philosophy of obligator is that identities are built on email. Email isn't perfect, but it's the globally unique federated identity we have that works today.

Thus the purpose of obligator is to validate that a user controls an email address as simply as possible, and communicate that to the application the user is attempting to log in to. Validation can either be done directly through SMTP, or delegated to upstream OIDC (and some plain OAuth2) providers.

Running it
==========

You can initialize obligator with a config file by passing the `-config` option with a JSON file matching the following format:

{
  "oauth2\_providers": \[
    {
      "id": "google",
      "name": "Google",
      "uri": "https://accounts.google.com",
      "client\_id": "<google oauth2 client\_id>",
      "client\_secret": "<google oauth2 client\_secret>",
      "openid\_connect": true
    },
    {
      "id": "lastlogin",
      "name": "LastLogin",
      "uri": "https://lastlogin.net",
      "client\_id": "https://example.com",
      "client\_secret": "",
      "openid\_connect": true
    }
  \],
  "smtp": {
    "server": "smtp.fastmail.com",
    "username": "<smtp-username>",
    "password": "<smtp-password>",
    "port": 587,
    "sender": "auth@example.com",
    "sender\_name": "Example"
  }
}

If you're already using docker, it's the easiest way to get started with obligator:

```
mkdir obligator_docker/
cp obligator_storage.json obligator_docker/

docker run --user $(id -u):$(id -g) --rm -it -v $PWD/obligator_docker:/data -v $PWD/obligator_docker:/api -p 1616:1616 anderspitman/obligator:latest -storage-dir /data -api-socket-dir /api -root-uri example.com -port 1616
```

You can also download static executables for various platforms from the releases page.

Using the API
=============

Currently the API is only offered through unix sockets. This reduces the chance that it accidentally gets exposed, which is important because it's not authenticated in any way.

There's not any documentation, and the API is in flux, so refer to the source code for usage.

Here's an example assuming you ran the docker command above:

```
curl --unix-socket obligator_docker/obligator_api.sock dummy-domain/oauth2-providers
```

See here for more info on using curl over unix sockets.

Support
=======

Community support is provided on the IndieBits forums.

Feature explanation
===================

Anonymous OAuth2 auth
---------------------

Normally in OAuth2 (and therefore OIDC), an app (client) is required to pre-register with the provider. This can create a lot of friction, especially if you're self-hosting an open source application. App developers are forced to either share a single client ID for all their users (and share their `client secret`, which essentially makes it pointless), or each user must separately register their instance.

Instead, obligator takes essentially the approach described here. Any OAuth2 client can anonymously authenticate with an obligator instance, with the `client_id` equal to the domain of the client, and `client_secret` left blank. Security is maintained through the following means:

-   Only approved email addresses are permitted unless `public: true` is set in the config.
-   The `client_id` URI must be a prefix of the `redirect_uri`, and the `client_id` is displayed to the user when consenting to the login. This guarantees that the user approves the ID token to be sent to the domain shown. Note that this can actually be more secure than pre-registration. There have been attacks in the past where users were tricked into authorizing apps because the pre-registered information looked convincing. By forcing the user to decide whether they trust the actual domain where the ID token will be sent, and not displaying any sort of logo which can be faked, security is improved.

Note that some servers implement OIDC Dynamic Client Registration, which is an official specification to accomplish some of the same goals as anonymous auth. When an initial access token is not required (notably the case with Ory), this can result in a very similar experience from the user perspective. The main problem is that client apps must support dynamic client registration, and many don't. Anonymous auth does not require any special features on the client side.

Multi-domain authentication
---------------------------

Have you ever noticed when you login to Gmail on a new computer that you're also automatically logged in to YouTube? How does this work when Gmail is on google.com and youtube.com doesn't have any access to the cookies or localstorage of google.com?

The answer is that when you log in on accounts.google.com, it makes a quick redirect to youtube.com with a URL parameter to also set up the cookies there. I also want this functionality for all the domains protected by my OIDC server so I'm building it into obligator.

Passwordless email login
------------------------

In line with the philosophy above, email reigns supreme in obligator. Since passwords are relatively difficult to use securely, the way to add an email identity is to send a confirmation code to the email address.

Demo
====

There's a public instance of obligator running at https://lastlogin.net (discovery doc at https://lastlogin.net/.well-known/openid-configuration). You can use it with any OIDC client. Just set the `client_id` to a prefix of the `redirect_uri` the client application uses when making the authorization request. I like to use https://openidconnect.net/ for ad-hoc testing, like so:

1.  Click on "Configuration" on the right side
2.  Enter the discovery document URL, ie https://lastlogin.net/.well-known/openid-configuration for LastLogin
3.  Click "Use Discovery Document". It should populate most of the fields
4.  Set the `client_id` to https://openidconnect.net/. This is a prefix of the `redirect_uri` that openidconnect.net uses, which is https://openidconnect.net/callback
5.  You can leave the `client_secret` as it is or remove it.
6.  Click "Save", then "Start" to begin the flow.

The official OpenID conformance suite is also excellent for testing OIDC servers.

Comparison is the thief of joy
==============================

Software is rarely about right vs wrong, but rather tradeoffs. This table is intended to help compare tradeoffs of different servers. It's also very incomplete and probably incorrect in many cases. If you have a correction, please submit an issue or leave a comment on the Google sheet here which is where it's generated from.

It's generated using the excellent https://tabletomarkdown.com

obligator

Portier

Rauthy

Authelia

Authentik

KeyCloak

Vouch

oauth2-proxy

Dex

Ory Stack

Zitadel

Casdoor

Kanidm

Simple

✅

✅

✅

✅

❌

❌

❓

❓

❓

❌

❌

❓

❓

Anonymous auth

✅

✅

✅

❌

❌

❌

❌

❌

❌

❌

❌

❌

❌

Multi-domain auth

✅ (planned)

❓

❓

❌

❌

❌

❌

❌

❓

❌

❓

❓

❌

Passwordless email login

✅

✅

❌

❌

❌

❌

❌

❌

❌

✅

❌

❓

❌

HTTP API

✅

❓

✅

❌

✅

✅

❌

❌

✅

✅

✅

❓

✅

Forward auth

✅

❓

✅

✅

✅

✅

✅

✅

❓

✅

❓

❓

❌

Trusted header auth

✅ (planned)

❓

✅

✅

✅

❌

❌

❌

❓

✅

❓

❓

✅

Upstream OIDC/OAuth2

✅

❌ (partial)

✅

❌

✅

✅

✅

✅

✅

✅

✅

❓

❌

SAML

❌

❌

❓

❌

✅

✅

❌

❌

✅

Needs coding

✅

❓

❌

LDAP

❌

❌

❓

✅

✅

✅

❌

❌

✅

Needs coding

✅

❓

✅

MFA

❌

❓

✅

✅

✅

✅

❌

❌

❓

✅

✅

❓

✅

Standalone reverse proxy

❌

❌

❓

❌

✅

✅

❌

✅

❌

✅

❓

❓

❌

Admin GUI

❌

❌

✅

✅

✅

✅

❌

❌

❓

✅

✅

❓

❌

Dyanmic client registration

✅

❌

✅

❌

❌

❓

❌

❌

❌

✅

❌

❓

❌

Passkey support

❌

❓

✅

❓

❓

❓

❓

❓

❓

❓

❓

❓

✅

Vanity

Language

Go

Rust

Rust

Go

Python

Java

Go

Go

Go

Go

Go

Go

Rust

Dependencies

5

21

73

49

54

❓

16

36

36

58

81

68

116

Lines of code

~5600

~9500

~59000

~148000

~247000

~869000

~5500

~54000

~63500

~330000

~603000

~113000

~239000

Lines of code were calculated using tokei, and last updated on 2024-04-21.

Ory is calculated using Hydra + Oathkeeper + Kratos, per this
