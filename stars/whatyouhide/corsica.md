---
project: corsica
stars: 537
description: Elixir library for dealing with CORS requests. 🏖
url: https://github.com/whatyouhide/corsica
---

Corsica
=======

Corsica is a plug and a DSL for handling CORS requests. Documentation can be found online.

> Photo by Hendrik Cornelissen on Unsplash

_(I had to include a nice pic because, let's be honest, CORS requests aren't the most fun thing in the world, are they?)_

Features
--------

-   Is compliant with the W3C CORS specification
-   Provides both low-level CORS utilities as well as high-level facilities (like a built-in plug and a CORS-focused router)
-   Handles preflight requests like a breeze
-   Never sends any CORS headers if the CORS request is not valid (smaller requests, yay!)

Installation
------------

Add the `:corsica` dependency to your project's `mix.exs`:

defp deps do
  \[
    {:plug, "~> 1.0"},
    {:corsica, "~> 2.0"}
  \]
end

and then run `$ mix deps.get`.

Overview
--------

You can use Corsica both as a plug as well as a router generator. To use it as a plug, just plug it into your plug pipeline:

defmodule MyApp.Endpoint do
  plug Logger
  plug Corsica, origins: "http://foo.com"
  plug MyApp.Router
end

To gain finer control over which resources are CORS-enabled and with what options, you can use the `Corsica.Router` module:

defmodule MyApp.CORS do
  use Corsica.Router,
    origins: \["http://localhost", ~r{^https?://(.\*\\.)?foo\\.com$}\],
    allow\_credentials: true,
    max\_age: 600

  resource "/public/\*", origins: "\*"
  resource "/\*"
end

defmodule MyApp.Endpoint do
  plug Logger
  plug MyApp.CORS
  plug MyApp.Router
end

This is only a brief overview of what Corsica can do. To find out more, head to the online documentation.

### Common issues

Note that Corsica is compliant with the W3C CORS specification, which means CORS response headers are not sent for invalid CORS requests. The documentation goes into more detail about this, but it's worth noting so that the first impression is not that Corsica is doing nothing. One common pitfall is not including CORS request headers in your requests: this makes the request an invalid CORS request, so Corsica won't add any CORS response headers. Be sure to add at least the `Origin` header:

curl localhost:4000 -v -H "Origin: http://foo.com"

There is a dedicated page in the documentation that covers some of the common issues with CORS (and Corsica in part).

Contributing
------------

If you find a bug, something unclear (including in the documentation!) or a behaviour that is not compliant with the latest revision of the official CORS specification, please open an issue on GitHub.

If you want to contribute to code or documentation, fork the repository and then open a Pull Request (how-to). Before opening a Pull Request, make sure all the tests passes by running `$ mix test` in your shell. If you're contributing to documentation, you can preview the generated documentation locally by running:

mix docs

Documentation will be generated in the `doc/` directory.

License
-------

MIT © 2015 Andrea Leopardi, see the license file.
