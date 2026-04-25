---
project: html_sanitize_ex
stars: 290
description: HTML sanitizer for Elixir
url: https://github.com/rrrene/html_sanitize_ex
---

HtmlSanitizeEx
==============

`html_sanitize_ex` provides a fast and straightforward HTML Sanitizer written in Elixir which lets you include HTML authored by third-parties in your web application while protecting against XSS.

It is the first Hex package to come out of the elixirstatus.com project, where it will be used to sanitize user announcements from the Elixir community.

What can it do?
---------------

`html_sanitize_ex` parses a given HTML string and, based on the used Scrubber, either completely strips it from HTML tags or sanitizes it by only allowing certain HTML elements and attributes to be present.

Installation
------------

Add html\_sanitize\_ex as a dependency in your `mix.exs` file.

defp deps do
  \[{:html\_sanitize\_ex, "~> 1.4"}\]
end

After adding you are done, run `mix deps.get` in your shell to fetch the new dependency.

The only dependency of `html_sanitize_ex` is `mochiweb` which is used to parse HTML.

Usage
-----

Depending on the scrubber you select, it can strip all tags from the given string:

text \= "<a href=\\"javascript:alert('XSS');\\"\>text here</a>"
HtmlSanitizeEx.strip\_tags(text)
\# => "text here"

Or allow certain basic HTML elements to remain:

text \= "<h1>Hello <script>World!</script></h1>"
HtmlSanitizeEx.basic\_html(text)
\# => "<h1>Hello World!</h1>"

There are built-in scrubbers that cover common use cases, but you can also easily define custom scrubbers (see the next section).

The following default scrubbing options exist:

HtmlSanitizeEx.basic\_html(html)
HtmlSanitizeEx.html5(html)
HtmlSanitizeEx.markdown\_html(html)
HtmlSanitizeEx.strip\_tags(html)

There is also one scrubber primarily used for testing:

HtmlSanitizeEx.noscrub(html)

Before using or extending a built-in scrubber, you should verify that it functions in the way you expect. The built-in scrubbers are located in /lib/html\_sanitize\_ex/scrubber

Custom Scrubbers
----------------

A custom scrubber has the advantage of allowing you to support only the minimum functionality needed for your use case.

With a custom scrubber, you define which tags, attributes, and uri schemes (e.g. `https`, `mailto`, `javascript`, etc.) are allowed. Anything not allowed can then be stripped out.

Here is an example of a custom scrubber which allows only `p`, `h1`, and `a` tags, and restricts the `href` attribute to only the `https` and `mailto` URI schemes. It also removes CDATA sections and comments.

defmodule MyProject.MyScrubber do
  use HtmlSanitizeEx

  allow\_tag\_with\_these\_attributes("p", \[\])
  allow\_tag\_with\_these\_attributes("h1", \[\])

  allow\_tag\_with\_uri\_attributes("a", \["href"\], \["https", "mailto"\])
end

Then, you can use the scrubber in your project by calling `MyProject.MyScrubber.sanitize/1`:

text \= "<h1>Hello <script>World!</script></h1>"
MyProject.MyScrubber.sanitize(text)
\# => "<h1>Hello World!</h1>"

A great way to make a custom scrubber is to use one the of built-in scrubbers closest to your use case as a template.

The built in scrubbers are located in /lib/html\_sanitize\_ex/scrubber

Extending Scrubbers
-------------------

Let's say you love `HtmlSanitizeEx.basic_html/1`, you just need it to also support the `small` tag (for whatever reason).

You can extend any scrubber by using the `:extend` option.

defmodule MyProject.MyScrubber do
  use HtmlSanitizeEx, extend: :basic\_html

  allow\_tag\_with\_these\_attributes("small", \[\])
end

You can extend `:basic_html`, `:html5`, `:markdown_html` and `:strip_tags` to extend built-in functionality and you can also extend any custom scrubber you created:

defmodule MyProject.MyOtherScrubber do
  use HtmlSanitizeEx, extend: MyProject.MyScrubber

  allow\_tag\_with\_these\_attributes("p", \["class"\])
end

The result is a scrubber that works like the built-in BasicHTML scrubber, but also allows `small` tags and `class` attributes on `<p>` tags.

Contributing
------------

1.  Fork it!
2.  Create your feature branch (`git checkout -b my-new-feature`)
3.  Commit your changes (`git commit -am 'Add some feature'`)
4.  Push to the branch (`git push origin my-new-feature`)
5.  Create new Pull Request

Author
------

René Föhring (@rrrene)

License
-------

html\_sanitize\_ex is released under the MIT License. See the LICENSE file for further details.
