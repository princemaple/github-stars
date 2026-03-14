---
project: meeseeks
stars: 324
description: An Elixir library for parsing and extracting data from HTML and XML with CSS or XPath selectors.
url: https://github.com/mischov/meeseeks
---

Meeseeks
========

Meeseeks is an Elixir library for parsing and extracting data from HTML and XML with CSS or XPath selectors.

import Meeseeks.CSS

html \= HTTPoison.get!("https://news.ycombinator.com/").body

for story <- Meeseeks.all(html, css("tr.athing")) do
  title \= Meeseeks.one(story, css(".title a"))

  %{
    title: Meeseeks.text(title),
    url: Meeseeks.attr(title, "href")
  }
end
#=> \[%{title: "...", url: "..."}, %{title: "...", url: "..."}, ...\]

Features
--------

-   Friendly API
-   Browser-grade HTML5 parser
-   Permissive XML parser
-   CSS and XPath selectors
-   Supports custom selectors
-   Helpers to extract data from selections

Compatibility
-------------

Meeseeks is tested with a a minimum combination of Elixir 1.16.0 and Erlang/OTP 26.0 and a maximum combination of Elixir 1.18.0 and Erlang/OTP 27.0.

Installation
------------

Meeseeks depends on the Rust library `html5ever` via `meeseeks_html5ever`, but because `meeseeks_html5ever` provides pre-compiled NIFs via `rustler_precompiled` **you do not need to have Rust installed** to use Meeseeks.

To install Meeseeks, add it to your `mix.exs`:

defp deps do
  \[
    {:meeseeks, "~> 0.18.0"}
  \]
end

Then run `mix deps.get`.

### Force Compilation

If you need to force compilation of the Rust NIF for some reason, see the instructions here.

Getting Started
---------------

### Parse

Start by parsing a source (HTML/XML string or `Meeseeks.TupleTree`) into a `Meeseeks.Document` so that it can be queried.

`Meeseeks.parse/1` parses the source as HTML, but `Meeseeks.parse/2` accepts a second argument of either `:html`, `:xml`, or `:tuple_tree` that specifies how the source is parsed.

document \= Meeseeks.parse("<div id=main><p>1</p><p>2</p><p>3</p></div>")
#=> #Meeseeks.Document<{...}>

The selection functions accept an unparsed source, parsing it as HTML, but parsing is expensive so parse ahead of time when running multiple selections on the same document.

### Select

Next, use one of Meeseeks's selection functions - `fetch_all`, `all`, `fetch_one`, or `one` - to search for nodes.

All these functions accept a queryable (a source, a document, or a `Meeseeks.Result`), one or more `Meeseeks.Selector`s, and optionally an initial context.

`all` returns a (possibly empty) list of results representing every node matching one of the provided selectors, while `one` returns a result representing the first node to match a selector (depth-first) or nil if there is no match.

`fetch_all` and `fetch_one` work like `all` and `one` respectively, but wrap the result in `{:ok, ...}` if there is a match or return `{:error, %Meeseeks.Error{type: :select, reason: :no_match}}` if there is not.

To generate selectors, use the `css` macro provided by `Meeseeks.CSS` or the `xpath` macro provided by `Meeseeks.XPath`.

import Meeseeks.CSS
result \= Meeseeks.one(document, css("#main p"))
#=> #Meeseeks.Result<{ <p>1</p> }>

import Meeseeks.XPath
result \= Meeseeks.one(document, xpath("//\*\[@id='main'\]//p"))
#=> #Meeseeks.Result<{ <p>1</p> }>

### Extract

Retrieve information from the `Meeseeks.Result` with an extractor.

The included extractors are `attr`, `attrs`, `data`, `dataset`, `html`, `own_text`, `tag`, `text`, `tree`.

Meeseeks.tag(result)
#=> "p"
Meeseeks.text(result)
#=> "1"
Meeseeks.tree(result)
#=> {"p", \[\], \["1"\]}

The extractors `html` and `tree` work on `Meeseeks.Document`s in addition to `Meeseeks.Result`s.

Meeseeks.html(document)
#=> "<html><head></head><body><div id=\\"main\\"><p>1</p><p>2</p><p>3</p></div></body></html>"

Guides
------

-   Meeseeks vs. Floki
-   CSS Selectors
-   XPath Selectors
-   Custom Selectors
-   Deployment

Contributing
------------

If you are interested in contributing please read the contribution guidelines.

License
-------

Meeseeks is licensed under the MIT license.
