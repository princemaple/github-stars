---
project: codepagex
stars: 119
description: Elixir string encoding conversion - like iconv but pure Elixir
url: https://github.com/tallakt/codepagex
---

Codepagex
=========

Codepagex is an elixir library to convert between string encodings to and from utf-8. Like iconv, but written in pure Elixir.

All the encodings are fetched from unicode.org tables and conversion functions are generated from these at compile time.

Note on the unicode built in module
-----------------------------------

Note that the Erlang built in `:unicode` module has some provisions for converting between utf-8 and latin1 code sets. If that is all you need, you should consider not using `codepagex` but rather rely on this simpler alternative.

Compared to this functionality `codepagex` provides:

-   More codepage mapping options
-   The ability to handle illegal encoding with custom logic
-   A simpler interface

But please remember that `codepagex` is comparatively a lot more complex, making extensive use of macro programming.

Examples
--------

The package is assumed to be interfaced using only the `Codepagex` module.

    iex\> from\_string("æøåÆØÅ", :iso\_8859\_1)
    {:ok, <<230, 248, 229, 198, 216, 197\>>}

    iex\> to\_string(<<230, 248, 229, 198, 216, 197\>>, :iso\_8859\_1)
    {:ok, "æøåÆØÅ"}

    iex\> from\_string!("æøåÆØÅ", :iso\_8859\_1)
    <<230, 248, 229, 198, 216, 197\>>

    iex\> to\_string!(<<230, 248, 229, 198, 216, 197\>>, :iso\_8859\_1)
    "æøåÆØÅ"

When there are invalid byte sequences in a String or encoded binary, the functions will not succeed. If you still want to handle these strings, you may specify a function to handle these circumstances. Eg:

    iex\> from\_string("Hello æøå!", :ascii, replace\_nonexistent("\_"))
    {:ok, "Hello \_\_\_!", 3}

    iex\> iso \= "Hello æøå!" |> from\_string!(:iso\_8859\_1)
    iex\> to\_string!(iso, :ascii, use\_utf\_replacement())
    "Hello ���!"

Encodings
---------

A full list of encodings is found by running `encoding_list/1`.

The encodings are best supplied as an atom, or else the string is converted to atom for you (but with a somewhat less efficient function lookup). Eg:

    iex\> from\_string("æøå", "ISO8859/8859-9")
    {:ok, <<230, 248, 229\>>}

    iex\> from\_string("æøå", :"ISO8859/8859-9")
    {:ok, <<230, 248, 229\>>}

For some encodings, an alias is set up for easier dispatch. The list of aliases is found by running `aliases/1`. The code looks like:

    iex\> from\_string!("Hello æøåÆØÅ!", :iso\_8859\_1)
    <<72, 101, 108, 108, 111, 32, 230, 248, 229, 198, 216, 197, 33\>>

Encoding selection
------------------

By default all ISO-8859 encodings and ASCII is included. There are a few more available, and these must be specified in the `config/config.exs` file. The specified files are then compiled. Adding many encodings may affect compilation times, in particular for the largest ones.

To specify the encodings to use, add the following lines to your `config/config.exs` and recompile:

    use Mix.Config
    config :codepagex, :encodings, \[:ascii\]

This will add only the ASCII encoding, as specified by it's shorthand alias. Any number of encodings may be specified like this in the list. The list may contain strings, atoms or regular expressions that match either an alias or a full encoding name, eg:

    use Mix.Config
    config :codepagex, :encodings, \[
      :ascii,           \# by alias name
      ~r\[iso8859\]i,     \# by a regex matching the full name
      "ETSI/GSM0338",   \# by the full name as a string
      :"MISC/CP856"     \# by a full name as an atom
    \]

After modifying the encodings list in the configuration, always make sure to run the following or the encodings you specified will not be compiled in:

mix deps.compile codepagex --force

This is necessary due to the fact that `Codepagex`'s configuration changes are not picked up automatically when it's a dependency in another project. Credit for the find goes to @michalmuskala here: https://elixirforum.com/t/sharing-with-the-community-text-transcoding-libraries/17962/2

The encodings that are known to require very long compile times are:

-   VENDORS/MISC/KPS9566
-   VENDORS/MICSFT/WINDOWS/CP932
-   VENDORS/MICSFT/WINDOWS/CP936
-   VENDORS/MICSFT/WINDOWS/CP949
-   VENDORS/MICSFT/WINDOWS/CP950

TODO
----

-   A few encodings are not yet supported for different reasons. In particular the asian and arab ones with left-right and up-down variations.
-   Test Elixir function specs
-   Benchmarking vs `iconv` native libraries
-   Support for iolists
-   when converting sections of a string that are unchanged, return the original input. Consider using iolists to return the values so that chunks may be saved continuously
-   lazy converter to get n characters / codepoints
-   function to drop n characters and take n characters (and slice?)
