---
project: mua
stars: 13
description: SMTP client in Elixir
url: https://github.com/ruslandoga/mua
---

Mua
===

Minimal SMTP client (aka Mail user agent).

Can be used with Bamboo and Swoosh.

### Features

-   Direct messaging (no relays)
-   Indirect messaging (relays)
-   Minimal API
-   Processless

Installation
------------

defp deps do
  \[
    {:mua, "~> 0.2.0"}
  \]
end

Usage
-----

This demo will use Mailpit:

$ docker run -d --rm -p 1025:1025 -p 8025:8025 -e "MP\_SMTP\_AUTH\_ACCEPT\_ANY=1" -e "MP\_SMTP\_AUTH\_ALLOW\_INSECURE=1" --name mailpit axllent/mailpit
$ open http://localhost:8025

High-level API:

message \= """
Date: Mon, 25 Dec 2023 06:52:15 +0000\\r
From: Mua <mua@github.com>\\r
Subject: README\\r
To: Mr Receiver <receiver1@mailpit.example>\\r
CC: Ms Receiver <receiver2@mailpit.example>\\r
\\r
like and subscribe
"""

{:ok, \_receipt} \=
  Mua.easy\_send(
    \_host \= "localhost",
    \_mail\_from \= "mua@github.com",
    \_rcpt\_to \= \["receiver1@mailpit.example", "receiver2@mailpit.example"\],
    message,
    port: 1025,
    auth: \[username: "username", password: "password"\]
  )

Low-level API:

{:ok, socket, \_banner} \= Mua.connect(:tcp, "localhost", \_port \= 1025)
{:ok, extensions} \= Mua.ehlo(socket, \_sending\_domain \= "github.com")

{:ok, socket} \=
  if "STARTTLS" in extensions do
    Mua.starttls(socket, "localhost")
  else
    {:ok, socket}
  end

:plain \= Mua.pick\_auth\_method(extensions)
:ok \= Mua.auth(socket, :plain, username: "username", password: "password")

:ok \= Mua.mail\_from(socket, "mua@github.com")
:ok \= Mua.rcpt\_to(socket, "receiver@mailpit.example")

message \=
  """
  Date: Mon, 25 Dec 2023 06:52:15 +0000\\r
  From: Mua <mua@github.com>\\r
  Subject: How was your day?\\r
  To: Mr Receiver <receiver@mailpit.example>\\r
  \\r
  Mine was fine.
  """

{:ok, \_receipt} \= Mua.data(socket, message)
:ok \= Mua.close(socket)
