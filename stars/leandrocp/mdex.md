---
project: mdex
stars: 425
description: Markdown for Elixir. Fast, Extensible, Phoenix-native. AI-ready. Built on top of comrak, ammonia, and lumis.
url: https://github.com/leandrocp/mdex
---

MDEx
====

  

Fast and Extensible Markdown for Elixir.

Features
--------

-   Fast
-   Compliant with the CommonMark spec
-   Plugins
-   Formats:
    -   Markdown (CommonMark)
    -   HTML
    -   Phoenix HEEx
    -   JSON
    -   XML
    -   Quill Delta
-   Floki-like Document AST
-   Req-like Document pipeline API
-   GitHub Flavored Markdown
-   GitLab Flavored Markdown
-   Discord Flavored Markdown (Partial)
-   Wiki-style links
-   Phoenix HEEx components and expressions
-   Streaming incomplete fragments
-   Emoji shortcodes
-   Built-in Syntax Highlighting with Lumis or Syntect
-   Code Block Decorators
-   HTML sanitization
-   ~MD Sigil for Markdown, HTML, HEEx, JSON, XML, and Quill Delta

Plugins
-------

-   mdex\_gfm - Enable GitHub Flavored Markdown (GFM)
-   mdex\_mermaid - Render Mermaid diagrams in code blocks
-   mdex\_katex - Render math formulas using KaTeX
-   mdex\_video\_embed - Privacy-respecting video embeds from code blocks
-   mdex\_custom\_heading\_id - Custom heading IDs for markdown headings
-   mdex\_mermex - Render Mermaid diagrams server-side using Mermex (Rust NIF)

Installation
------------

Add `:mdex` dependency:

def deps do
  \[
    {:mdex, "~> 0.12"}
  \]
end

Or use Igniter:

mix igniter.install mdex

Usage
-----

#### Convert to HTML

iex\> MDEx.to\_html!("# Hello :smile:", extension: \[shortcodes: true\])
"<h1>Hello 😄</h1>"

#### Syntax Highlighting

Syntax highlight code blocks using either Lumis or Syntect, for example to use Lumis:

def deps do
  \[
    {:mdex, "~> 0.12"},
    {:lumis, "~> 0.1"}
  \]
end

config :mdex\_native, syntax\_highlighter: :lumis

#### GitHub Flavored Markdown (GFM)

_Using the `:html_multi_themes` syntax highlighting formatter is not required but you get light/dark using it._

Mix.install(\[
  {:mdex\_gfm, "~> 0.1"}
\])

markdown \= """
\- \[x\] Set up project
\- \[ \] Write docs
\`\`\`elixir
spawn(fn -> send(current, {self(), 1 + 2}) end)
\`\`\`
"""

MDEx.new(
  markdown: markdown,
  syntax\_highlight: \[
    engine: :lumis,
    opts: \[
      formatter: {:html\_multi\_themes,
        themes: \[light: "github\_light", dark: "github\_dark"\],
        default\_theme: "light-dark()"}
    \]
  \]
)
|> MDExGFM.attach()
|> MDEx.to\_html!()

#### Sigils

iex\> import MDEx.Sigil
iex\> ~MD\[\# Hello :smile:\]HTML
"<h1>Hello 😄</h1>"

iex\> import MDEx.Sigil
iex\> assigns \= %{project: "MDEx"}
iex\> ~MD\[\# {@project}\]HEEX
%Phoenix.LiveView.Rendered{...}

iex\> import MDEx.Sigil
iex\> ~MD\[\# Hello :smile:\]
#MDEx.Document(3 nodes)<
├── 1 \[heading\] level: 1, setext: false
│   ├── 2 \[text\] literal: "Hello "
│   └── 3 \[short\_code\] code: "smile", emoji: "😄"
\>

#### Streaming

iex\> MDEx.new(streaming: true)
...\> |> MDEx.Document.put\_markdown("\*\*Install")
...\> |> MDEx.to\_html!()
"<p><strong>Install</strong></p>"

Examples and Guides
-------------------

In docs you can find Livebook examples covering options and usage, and Guides for more info.

Foundation
----------

The library is built on top of:

-   comrak - a fast Rust port of GitHub's CommonMark parser
-   ammonia for HTML Sanitization
-   lumis for Syntax Highlighting

Used By
-------

-   00
-   Algora
-   Ash AI
-   BeaconCMS
-   BeamLens Web
-   Bonfire
-   Canada Navigator
-   Conpipe
-   Exmeralda
-   Hexpm
-   Jido
-   Loomkin
-   Phoenix SEO
-   Phoenix Storybook
-   Plural Console
-   Prosody
-   Reposit
-   Sagents Live Debugger
-   Sayfa
-   Tableau
-   Teiserver
-   TermUI
-   Tuist
-   Valentine
-   Wraft
-   And more...

_Are you using MDEx and want to list your project here? Please send a PR!_

Sponsors
--------

💜 **Support MDEx Development**

If you or your company find MDEx useful, please consider sponsoring its development.

➡️ **GitHub Sponsors**

Your support helps maintain and improve MDEx for the entire Elixir community!

**Current and previous sponsors**

Motivation
----------

MDEx was born out of the necessity of parsing CommonMark files, to parse hundreds of files quickly, and to be easily extensible by consumers of the library.

-   earmark is extensible but can't parse all kinds of documents and is slow to convert hundreds of markdowns.
-   md is very extensible but the doc says "If one needs to perfectly parse the common markdown, Md is probably not the correct choice" and CommonMark was a requirement to parse many existing files.
-   markdown is not precompiled and has not received updates in a while.
-   cmark is a fast CommonMark parser but it requires compiling the C library, is hard to extend, and was archived on Apr 2024.

Comparison
----------

Feature

MDEx

Earmark

md

cmark

Active

✅

✅

✅

❌

Pure Elixir

⚠️¹

✅

✅

❌

Extensible

✅

✅

✅

❌

Syntax Highlighting

✅

❌

❌

❌

Code Block Decorators

✅

❌

❌

❌

Streaming (fragments)

✅

❌

❌

❌

Phoenix HEEx components

✅

❌

❌

❌

AST

✅

✅

✅

❌

AST to Markdown

✅

⚠️²

❌

❌

To HTML

✅

✅

✅

✅

To JSON

✅

❌

❌

❌

To XML

✅

❌

❌

✅

To Manpage

❌

❌

❌

✅

To LaTeX

❌

❌

❌

✅

To Quill Delta

✅

❌

❌

❌

Emoji

✅

❌

❌

❌

GFM³

✅

✅

❌

❌

GLFM⁴

✅

❌

❌

❌

Discord⁵

⚠️⁶

❌

❌

❌

1.  MDEx depends on mdex\_native which uses Rustler
2.  Possible with earmark\_reversal
3.  GitHub Flavored Markdown
4.  GitLab Flavored Markdown
5.  Discord Flavored Markdown
6.  Partial support

Benchmark
---------

A benchmark is available to compare existing libs:

```
Name              ips        average  deviation         median         99th %
mdex          8983.16       0.111 ms     ±6.52%       0.110 ms       0.144 ms
md             461.00        2.17 ms     ±2.64%        2.16 ms        2.35 ms
earmark        110.47        9.05 ms     ±3.17%        9.02 ms       10.01 ms

Comparison:
mdex          8983.16
md             461.00 - 19.49x slower +2.06 ms
earmark        110.47 - 81.32x slower +8.94 ms

Memory usage statistics:

Name            average  deviation         median         99th %
mdex         0.00184 MB     ±0.00%     0.00184 MB     0.00184 MB
md              6.45 MB     ±0.00%        6.45 MB        6.45 MB
earmark         5.09 MB     ±0.00%        5.09 MB        5.09 MB

Comparison:
mdex         0.00184 MB
md              6.45 MB - 3506.37x memory usage +6.45 MB
earmark         5.09 MB - 2770.15x memory usage +5.09 MB
```

The most performance gain is using the `~MD` sigil to compile the Markdown instead of parsing it at runtime, prefer using it when possible.

To finish, a friendly reminder that all libs have their own strengths and trade-offs so use the one that better suits your needs.

Acknowledgements
----------------

-   comrak crate for all the heavy work on parsing Markdown and rendering HTML
-   Floki for the AST
-   Req for the pipeline API
-   Logo based on markdown-mark
