---
project: multipart
stars: 53
description: Constructs a multipart message, such an HTTP form data request or multipart email
url: https://github.com/breakroom/multipart
---

Multipart
=========

Constructs a multipart message, such an HTTP form data request or multipart email.

Features
========

-   Follows RFC 2046 and RFC 7578
-   Can stream the request body, reducing memory consumption for large request bodies

Requirements
============

-   Elixir >= 1.16
-   Erlang/OTP >= 26

Installation
------------

Add `multipart` to your list of dependencies in `mix.exs`:

def deps do
  \[
    {:multipart, "~> 0.6"}
  \]
end

Usage
-----

Typically, you'll use `Multipart` to construct the HTTP body and headers, and use those to build a request in an HTTP client such as Finch:

multipart \=
  Multipart.new()
  |> Multipart.add\_part(Part.binary\_body("first body"))
  |> Multipart.add\_part(Part.binary\_body("second body", \[{"content-type", "text/plain"}\]))
  |> Multipart.add\_part(Part.binary\_body("<p>third body</p>", \[{"content-type", "text/html"}\]))

body\_stream \= Multipart.body\_stream(multipart)
content\_length \= Multipart.content\_length(multipart)
content\_type \= Multipart.content\_type(multipart, "multipart/mixed")

headers \= \[{"Content-Type", content\_type}, {"Content-Length", to\_string(content\_length)}\]

Finch.build("POST", "https://example.org/", headers, {:stream, body\_stream})
|> Finch.request(MyFinch)

You can construct a `multipart/form-data` request using the field helpers in `Path`.

multipart \=
  Multipart.new()
  |> Multipart.add\_part(Part.text\_field("field 1 text", :field1))
  |> Multipart.add\_part(Part.file\_field("/tmp/upload.jpg", :image))

body\_stream \= Multipart.body\_stream(multipart)
content\_length \= Multipart.content\_length(multipart)
content\_type \= Multipart.content\_type(multipart, "multipart/form-data")

headers \= \[{"Content-Type", content\_type}, {"Content-Length", to\_string(content\_length)}\]

Finch.build("POST", "https://example.org/", headers, {:stream, body\_stream})
|> Finch.request(MyFinch)
