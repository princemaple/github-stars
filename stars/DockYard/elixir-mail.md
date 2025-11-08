---
project: elixir-mail
stars: 477
description: Build composable mail messages
url: https://github.com/DockYard/elixir-mail
---

Mail
====

An RFC2822 implementation in Elixir, built for composability.

**Mail is built and maintained by DockYard, contact us for expert Elixir and Phoenix consulting**.

Installation
------------

def deps do
  \[
    \# Get from hex
    {:mail, "~> 0.4"},

    \# Or use the latest from master
    {:mail, github: "DockYard/elixir-mail"}
  \]
end

Building
--------

You can quickly build an RFC2822 spec compliant message.

#### Single-Part

message \=
  Mail.build()
  |> Mail.put\_text("A great message")
  |> Mail.put\_to("bob@example.com")
  |> Mail.put\_from("me@example.com")
  |> Mail.put\_subject("Open me")

#### Multi-Part

message \=
  Mail.build\_multipart()
  |> Mail.put\_text("Hello there!")
  |> Mail.put\_html("<h1>Hello there!</h1>")
  |> Mail.put\_attachment("path/to/README.md")
  |> Mail.put\_attachment({"README.md", file\_data})

Rendering
---------

After you have built your message you can render it:

rendered\_message \= Mail.render(message)

Parsing
-------

If you'd like to parse an already rendered message back into a data model:

%Mail.Message{} \= message \= Mail.parse(rendered\_message)

There are more functions described in the docs

Authors
-------

-   Brian Cardarella

We are very thankful for the many contributors

Versioning
----------

This library follows Semantic Versioning

Looking for help with your Elixir project?
------------------------------------------

At DockYard we are ready to help you build your next Elixir project. We have a unique expertise in Elixir and Phoenix development that is unmatched. Get in touch!

At DockYard we love Elixir! You can read our Elixir blog posts or come visit us at The Boston Elixir Meetup that we organize.

Want to help?
-------------

Please do! We are always looking to improve this library. Please see our Contribution Guidelines on how to properly submit issues and pull requests.

Legal
-----

DockYard, Inc. © 2015

@dockyard

Licensed under the MIT license
