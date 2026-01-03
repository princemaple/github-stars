---
project: expostal
stars: 100
description: Elixir binding for Libpostal - a library for parsing/normalizing street addresses around the world. Powered by statistical NLP and open geo data.
url: https://github.com/SweetIQ/expostal
---

expostal
========

Elixir binding for Libpostal - a library for parsing/normalizing street addresses around the world. Powered by statistical NLP and open geo data.

Tutorial on how to write Elixir/Erlang NIF: http://cs.mcgill.ca/~mxia3/2017/06/18/tutorial-extending-elixir-with-c-using-NIF/

Installation
------------

The package can be installed by adding `expostal` to your list of dependencies in `mix.exs`:

def deps do
  \[{:expostal, "~> 0.2.0"}\]
end

### Dependencies

Depends on system-wide installation of libpostal.

Usage
-----

Parsing an address:

```
iex> Expostal.parse_address("615 Rene Levesque Ouest, Montreal, QC, Canada")

%{city: "montreal", country: "canada", house_number: "615",
  road: "rene levesque ouest", state: "qc"}

```

Expanding an address:

```
iex> Expostal.expand_address("781 Franklin Ave Crown Hts Brooklyn NY")

["781 franklin avenue crown heights brooklyn new york",
  "781 franklin avenue crown heights brooklyn ny"]
```

Documentation
-------------

View the docs on https://hexdocs.pm/expostal, or generate the docs locally with `mix docs`.
