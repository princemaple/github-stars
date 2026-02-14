---
project: hashids-elixir
stars: 281
description: Stringify your ids
url: https://github.com/alco/hashids-elixir
---

Hashids
=======

Hashids lets you obfuscate numerical identifiers via reversible mapping.

This is a port of Hashids from JavaScript.

Installation
------------

Add Hashids as a dependency to your Mix project:

defp deps do
  \[
    {:hashids, "~> 2.0"}
  \]
end

Usage
-----

Hashids encodes a list of integers into a string (technically, iodata). Some of the encoding parameters can be customized.

s \= Hashids.new(\[
  salt: "123",  \# using a custom salt helps producing unique cipher text
  min\_len: 2,   \# minimum length of the cipher text (1 by default)
\])

cipher1 \= Hashids.encode(s, 129)
#=> "pE6"

cipher2 \= Hashids.encode(s, \[1,2,3,4\])
#=> "4bSwImsd"

\# decode() always returns a list of numbers

Hashids.decode(s, cipher1)
#=> {:ok, \[129\]}

Hashids.decode!(s, cipher2)
#=> \[1, 2, 3, 4\]

It is also possible to customize the character set used for the cipher text by providing a custom alphabet. It has to be at least 16 characters long.

defmodule MyAccessToken do
  @cyrillic\_alphabet "123456789абвгґдеєжзиіїйклмнопрстуфцчшщьюяАБВГҐДЕЄЖЗИІЇЙКЛМНОПРСТУФЦЧШЩЬЮЯ"
  @coder Hashids.new(alphabet: @cyrillic\_alphabet)

  def encode(token\_ids) do
    Hashids.encode(@coder, token\_ids)
  end

  def decode(data) do
    Hashids.decode(@coder, data)
  end
end

data \= MyAccessToken.encode(\[1234, 786, 21, 0\])
#=> "ЦфюєИНаЛ1И"

MyAccessToken.decode(data)
#=> {:ok, \[1234, 786, 21, 0\]}

Migrating from 1.0
------------------

See the changelog.

License
-------

This software is licensed under the MIT license.
