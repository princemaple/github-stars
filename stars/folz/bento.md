---
project: bento
stars: 101
description: :bento: A fast, correct, pure-Elixir library for reading and writing Bencoded metainfo (.torrent) files.
url: https://github.com/folz/bento
---

Bento
=====

Bento is a new Bencoding library for Elixir focusing on incredibly fast **speed** without sacrificing **simplicity**, **completeness**, or **correctness**.

It takes inspiration from Poison, a pure-Elixir JSON library, and uses several techniques found there to achieve this speed:

-   Extensive sub-binary matching.
-   A hand-rolled **parser** using several techniques known to benefit HiPE for native compilation.
-   IO list encoding.
-   **Single-pass** decoding.

Additionally, and unlike some other Elixir bencoding libraries, Bento will also reject all malformed input. This guarantees you're working with a well-formed bencoded file.

Preliminary benchmarking shows that Bento performs over 2x faster when encoding, and at least as fast when decoding, compared to other existing Elixir libraries.

Documentation
-------------

Documentation is available on Hexdocs.

Installation
------------

Bento is available in Hex. The package can be installed by:

1.  Add bento to your list of dependencies in `mix.exs`:

{:bento, "~> 1.0"}

1.  Then, update your dependencies.

$ mix do deps.get + deps.compile

Usage
-----

Encoding an Elixir data type:

iex\> Bento.encode(\[1, "two", \[3\]\])
{:ok, "li1e3:twoli3eee"}
iex\> Bento.encode!(%{"foo" \=> \["bar", "baz"\], "qux" \=> "norf"})
"d3:fool3:bar3:baze3:qux4:norfe"

Decoding a bencoded string:

iex\> Bento.decode("li1e3:twoli3eee")
{:ok, \[1, "two", \[3\]\]}
iex\> Bento.decode!("d3:fool3:bar3:baze3:qux4:norfe")
%{"foo" \=> \["bar", "baz"\], "qux" \=> "norf"}

Bento is also metainfo-aware and comes with a `*.torrent` decoder out of the box:

iex\> File.read!("./test/\_data/ubuntu-14.04.4-desktop-amd64.iso.torrent") |> Bento.torrent!()
%Bento.Metainfo.Torrent{
  info: %Bento.Metainfo.SingleFile{
    length: 1069547520,
    md5sum: nil,
    "piece length": 524288,
    pieces: <<109, 235, 143, 234, 36, 25, 142, 36, 20, 3, 227, 227, 134, 136,
      205, 130, 176, 104, 192, 33, 45, 230, 152, 2, 239, 131, 240, 217, 180,
      251, 153, 170, 31, 127, 175, 166, 9, 254, 133, 8, 42, 229, 43, 139, 86,
      ...\>>,
    private: 0,
    name: "ubuntu-14.04.4-desktop-amd64.iso"
  },
  announce: "http://torrent.ubuntu.com:6969/announce",
  "announce-list": \[
    \["http://torrent.ubuntu.com:6969/announce"\],
    \["http://ipv6.torrent.ubuntu.com:6969/announce"\]
  \],
  "creation date": ~U\[2016-02-18 20:12:51Z\],
  comment: "Ubuntu CD releases.ubuntu.com",
  "created by": nil,
  encoding: nil
}

In addition to parsing torrents via `Bento.torrent!/1`, It's also available decoding any bencoded data into any struct you choose, like so:

defmodule Name do
  defstruct \[:family, :given\]
end

iex\> Bento.decode!("d6:family4:Folz5:given6:Rodneye", as: %Name{})
%Name{family: "Folz", given: "Rodney"}

Benchmarking
------------

$ MIX\_ENV=bench mix bench

We currently benchmark against: Bento (this project), bencode, Bencodex, and bencoder.

We are aware of, but unable to benchmark against: exbencode (build errors), and elixir\_bencode (module name conflicts with Bencode).

PRs that add libraries to the benchmarks are greatly appreciated!

License
-------

See LICENSE.
