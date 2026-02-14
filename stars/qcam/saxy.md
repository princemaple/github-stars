---
project: saxy
stars: 294
description: Fast SAX parser and encoder for XML in Elixir
url: https://github.com/qcam/saxy
---

Saxy
====

Saxy (Sá xị) is an XML SAX parser and encoder in Elixir that focuses on speed, usability and standard compliance.

Comply with Extensible Markup Language (XML) 1.0 (Fifth Edition).

Features highlight
------------------

-   An incredibly fast XML 1.0 SAX parser.
-   An extremely fast XML encoder.
-   Native support for streaming parsing large XML files.
-   Parse XML documents into simple DOM format.
-   Support quick returning in event handlers.

Installation
------------

Add `:saxy` to your `mix.exs`.

def deps() do
  \[
    {:saxy, "~> 1.6"}
  \]
end

Overview
--------

Full documentation is available on HexDocs.

If you never work with a SAX parser before, please check out this guide.

### SAX parser

A SAX event handler implementation is required before starting parsing.

defmodule MyEventHandler do
  @behaviour Saxy.Handler

  def handle\_event(:start\_document, prolog, state) do
    IO.inspect("Start parsing document")
    {:ok, \[{:start\_document, prolog} | state\]}
  end

  def handle\_event(:end\_document, \_data, state) do
    IO.inspect("Finish parsing document")
    {:ok, \[{:end\_document} | state\]}
  end

  def handle\_event(:start\_element, {name, attributes}, state) do
    IO.inspect("Start parsing element #{name} with attributes #{inspect(attributes)}")
    {:ok, \[{:start\_element, name, attributes} | state\]}
  end

  def handle\_event(:end\_element, name, state) do
    IO.inspect("Finish parsing element #{name}")
    {:ok, \[{:end\_element, name} | state\]}
  end

  def handle\_event(:characters, chars, state) do
    IO.inspect("Receive characters #{chars}")
    {:ok, \[{:characters, chars} | state\]}
  end

  def handle\_event(:cdata, cdata, state) do
    IO.inspect("Receive CData #{cdata}")
    {:ok, \[{:cdata, cdata} | state\]}
  end
end

Then start parsing XML documents with:

iex\> xml \= "<?xml version='1.0' ?><foo bar='value'></foo>"
iex\> Saxy.parse\_string(xml, MyEventHandler, \[\])
{:ok,
 \[{:end\_document},
  {:end\_element, "foo"},
  {:start\_element, "foo", \[{"bar", "value"}\]},
  {:start\_document, \[version: "1.0"\]}\]}

### Streaming parsing

Saxy also accepts file stream as the input:

stream \= File.stream!("/path/to/file")

Saxy.parse\_stream(stream, MyEventHandler, initial\_state)

It even supports parsing a normal stream.

stream \= File.stream!("/path/to/file") |> Stream.filter(&(&1 != "\\n"))

Saxy.parse\_stream(stream, MyEventHandler, initial\_state)

### Partial parsing

Saxy can parse an XML document partially. This feature is useful when the document cannot be turned into a stream e.g receiving over socket.

{:ok, partial} \= Partial.new(MyEventHandler, initial\_state)
{:cont, partial} \= Partial.parse(partial, "<foo>")
{:cont, partial} \= Partial.parse(partial, "<bar></bar>")
{:cont, partial} \= Partial.parse(partial, "</foo>")
{:ok, state} \= Partial.terminate(partial)

### Simple DOM format exporting

Sometimes it will be convenient to just export the XML document into simple DOM format, which is a 3-element tuple including the tag name, attributes, and a list of its children.

`Saxy.SimpleForm` module has this nicely supported:

Saxy.SimpleForm.parse\_string(data)

{"menu", \[\],
 \[
   {"movie",
    \[{"id", "tt0120338"}, {"url", "https://www.imdb.com/title/tt0120338/"}\],
    \[{"name", \[\], \["Titanic"\]}, {"characters", \[\], \["Jack &amp; Rose"\]}\]},
   {"movie",
    \[{"id", "tt0109830"}, {"url", "https://www.imdb.com/title/tt0109830/"}\],
    \[
      {"name", \[\], \["Forest Gump"\]},
      {"characters", \[\], \["Forest &amp; Jenny"\]}
    \]}
 \]}

### XML builder

Saxy offers two APIs to build simple form and encode XML document.

Use `Saxy.XML` to build and compose XML simple form, then `Saxy.encode!/2` to encode the built element into XML binary.

iex\> import Saxy.XML
iex\> element \= element("person", \[gender: "female"\], "Alice")
{"person", \[{"gender", "female"}\], \[{:characters, "Alice"}\]}
iex\> Saxy.encode!(element, \[\])
"<?xml version=\\"1.0\\"?><person gender=\\"female\\"\>Alice</person>"

See `Saxy.XML` for more XML building APIs.

Saxy also provides `Saxy.Builder` protocol to help composing structs into simple form.

defmodule Person do
  @derive {Saxy.Builder, name: "person", attributes: \[:gender\], children: \[:name\]}

  defstruct \[:gender, :name\]
end

iex\> jack \= %Person{gender: :male, name: "Jack"}
iex\> john \= %Person{gender: :male, name: "John"}
iex\> import Saxy.XML
iex\> root \= element("people", \[\], \[jack, john\])
iex\> Saxy.encode!(root, \[\])
"<?xml version=\\"1.0\\"?><people><person gender=\\"male\\"\>Jack</person><person gender=\\"male\\"\>John</person></people>"

FAQs with Saxy/XMLs
-------------------

### Saxy sounds cool! But I just wanted to quickly convert some XMLs into maps/JSON...

Saxy does not have offer XML to maps conversion, because many awesome people already made it happen 💪:

-   https://github.com/bennyhat/xml\_json
-   https://github.com/xinz/sax\_map

Alternatively, this pull request could serve as a good reference if you want to implement your own map-based handler.

### Does Saxy work with XPath?

Saxy in its core is a SAX parser, therefore Saxy does not, and likely will not, offer any XPath functionality.

SweetXml is a wonderful library to work with XPath. However, `:xmerl`, the library used by SweetXml, is not always memory efficient and speedy. You can combine the best of both sides with Saxmerl, which is a Saxy extension converting XML documents into SweetXml compatible format. Please check that library out for more information.

### Saxy! Where did the name come from?

Sa Xi, pronounced like `sa-see`, is an awesome soft drink made by Chuong Duong.

Benchmarking
------------

Note that benchmarking XML parsers is difficult and highly depends on the complexity of the documents being parsed. Event I try hard to make the benchmarking suite fair but it's hard to avoid biases when choosing the documents to benchmark against.

Therefore the conclusion in this section is only for reference purpose. Please feel free to benchmark against your target documents. The benchmark suite can be found in bench/.

A rule of thumb is that we should compare apple to apple. Some XML parsers target only specific types of XML. Therefore some indicators are provided in the test suite to let know of the fairness of the benchmark results.

Some quick and biased conclusions from the benchmark suite:

-   For SAX parser, Saxy is usually 1.4 times faster than Erlsom. With deeply nested documents, Saxy is noticeably faster (4 times faster).
-   For XML builder and encoding, Saxy is usually 10 to 30 times faster than XML Builder. With deeply nested documents, it could be 180 times faster.
-   Saxy significantly uses less memory than XML Builder (4 times to 25 times).
-   Saxy significantly uses less memory than Xmerl, Erlsom and Exomler (1.4 times 10 times).

Limitations
-----------

-   No XSD supported.
-   No DTD supported, when Saxy encounters a `<!DOCTYPE`, it skips that.
-   Only support UTF-8 encoding.

Contributing
------------

If you have any issues or ideas, feel free to write to https://github.com/qcam/saxy/issues.

To start developing:

1.  Fork the repository.
2.  Write your code and related tests.
3.  Create a pull request at https://github.com/qcam/saxy/pulls.

Copyright and License
---------------------

Copyright (c) 2018 Cẩm Huỳnh

This software is licensed under the MIT license.
