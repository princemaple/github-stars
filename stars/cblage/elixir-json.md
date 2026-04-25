---
project: elixir-json
stars: 219
description: Native JSON library for Elixir
url: https://github.com/cblage/elixir-json
---

Elixir JSON
===========

This library provides a natively implemented JSON encoder and decoder for Elixir.

You can find the package in hex.pm and the documentation in hexdocs.pm.

All contributions are welcome!

Installing
==========

Simply add `{:json, "~> 1.4"}` to your project's `mix.exs` and run `mix deps.get`.

Usage
=====

Encoding an Elixir type

  @doc "
	JSON encode an Elixir list
  "	
  list \= \[key: "this will be a value"\]
  is\_list(list)
  \# true
  list\[:key\]
  \# "this will be a value"
  {status, result} \= JSON.encode(list)
  \# {:ok, "{\\"key\\":\\"this will be a value\\"}"}
  String.length(result)
  \# 41

Decoding a list from a string that contains JSON

  @doc "
	JSON decode a string into an Elixir list
  "
  json\_input \= "{\\"key\\":\\"this will be a value\\"}"
  {status, list} \= JSON.decode(json\_input)
	{:ok, %{"key" \=> "this will be a value"}}
  list\[:key\]
  \# nil
  list\["key"\]
  \# "this will be a value"

At any time, you can turn on verbose logging for this library only. To do so, head to config file of your application and add below lines:

use Mix.Config

config :logger, level: :debug

config :json, log\_level: :debug

Note that, changing only `:logger` level to `:info`, `:warn` or `:error` will silent `:json` too.

License
=======

The Elixir JSON library is available under the BSD 3-Clause aka "BSD New" license
