---
project: html_sanitize_ex
stars: 275
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

**NOTE:** The one thing missing at this moment is _**support for styles**_. To add this, we have to implement a Scrubber for CSS, to prevent nasty CSS hacks using `<style>` tags and attributes.

Otherwise `html_sanitize_ex` is a full-featured HTML sanitizer.

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

```
text = "<a href=\"javascript:alert('XSS');\">text here</a>"
HtmlSanitizeEx.strip_tags(text)
# => "text here"
```

Or allow certain basic HTML elements to remain:

```
text = "<h1>Hello <script>World!</script></h1>"
HtmlSanitizeEx.basic_html(text)
# => "<h1>Hello World!</h1>"
```

There are built-in scrubbers that cover common use cases, but you can also easily define custom scrubbers (see the next section).

The following default scrubbing options exist:

```
HtmlSanitizeEx.basic_html(html)
HtmlSanitizeEx.html5(html)
HtmlSanitizeEx.markdown_html(html)
HtmlSanitizeEx.strip_tags(html)
```

There is also one scrubber primarily used for testing:

```
HtmlSanitizeEx.noscrub(html)
```

Before using a built-in scrubber, you should verify that it functions in the way you expect. The built-in scrubbers are located in /lib/html\_sanitize\_ex/scrubber

Custom Scrubbers
----------------

A custom scrubber has the advantage of allowing you to support only the minimum functionality needed for your use case.

With a custom scrubber, you define which tags, attributes, and uri schemes (e.g. `https`, `mailto`, `javascript`, etc.) are allowed. Anything not allowed can then be stripped out.

There are also utility functions to remove CDATA sections and comments which you will generally include.

Here is an example of a custom scrubber which allows only `p`, `h1`, and `a` tags, and restricts the `href` attribute to only the `https` and `mailto` URI schemes. It also removes CDATA sections and comments.

Note that the scrubber should include `Meta.strip_everything_not_covered()` at the end.

defmodule MyProject.MyScrubber do
  require HtmlSanitizeEx.Scrubber.Meta
  alias HtmlSanitizeEx.Scrubber.Meta

  Meta.remove\_cdata\_sections\_before\_scrub()
  Meta.strip\_comments()

  Meta.allow\_tag\_with\_these\_attributes("p", \[\])
  Meta.allow\_tag\_with\_these\_attributes("h1", \[\])
  Meta.allow\_tag\_with\_uri\_attributes("a", \["href"\], \["https", "mailto"\])

  Meta.strip\_everything\_not\_covered()
end

Then, you can use the scrubber in your project by giving it as the second argument to `Scrubber.scrub/2`:

defmodule MyProject.MyModule do
  alias HtmlSanitizeEx.Scrubber
  alias MyProject.MyScrubber

  def sanitize\_html(html) do
    Scrubber.scrub(html, MyScrubber)
  end
end

A great way to make a custom scrubber is to use one the of built-in scrubbers closest to your use case as a template. The built in scrubbers are located in /lib/html\_sanitize\_ex/scrubber

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
