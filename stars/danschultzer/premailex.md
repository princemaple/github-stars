---
project: premailex
stars: 177
description: Preflight for your HTML emails - inline styling and plain text.
url: https://github.com/danschultzer/premailex
---

Premailex
=========

Preflight for your HTML emails. Adds inline styling, and converts HTML to plain text.

Features
--------

-   Add inline CSS properties from `<style>`
-   Add inline CSS properties from external `<link>` stylesheets
-   Transform HTML to plain text

Installation
------------

def deps do
  \[
    \# ...
    {:premailex, "~> 0.3.20"},

    \# Optional, but recommended for SSL validation with :httpc
    {:certifi, "~> 2.4"},
    {:ssl\_verify\_fun, "~> 1.1"},
    \# ...
  \]
end

Run `mix deps.get` to install it.

Getting started
---------------

Transform an HTML string to text:

Premailex.to\_text(html)

Add inline styles based on styles defined in `<head>`:

Premailex.to\_inline\_css(html)

Example with Swoosh
-------------------

def welcome(user) do
  new()
  |> to({user.name, user.email})
  |> from({"Dr B Banner", "hulk.smash@example.com"})
  |> subject("Hello, Avengers!")
  |> render\_body("welcome.html", %{username: user.username})
  |> premail()
end

defp premail(email) do
  html \= Premailex.to\_inline\_css(email.html\_body)
  text \= Premailex.to\_text(email.html\_body)

  email
  |> html\_body(html)
  |> text\_body(text)
end

Example with Bamboo
-------------------

def welcome\_email do
  new\_email
  |> subject("Email subject")
  |> to("test@example.com")
  |> from("test@example.com")
  |> put\_text\_layout(false)
  |> render("email.html")
  |> premail()
end

defp premail(email) do
  html \= Premailex.to\_inline\_css(email.html\_body)
  text \= Premailex.to\_text(email.html\_body)

  email
  |> html\_body(html)
  |> text\_body(text)
end

HTML parser
-----------

By default, premailex uses `Floki` to parse HTML, but you can exchange it for any HTML parser you prefer. `Meeseeks` is supported with the `Premailex.HTMLParser.Meeseeks` module. To use it, add the following to `config.exs`:

config :premailex, html\_parser: Premailex.HTMLParser.Meeseeks

LICENSE
-------

(The MIT License)

Copyright (c) 2017 Dan Schultzer & the Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
