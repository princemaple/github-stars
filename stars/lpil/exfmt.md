---
project: exfmt
stars: 430
description: 🌸 An opinionated Elixir source code formatter
url: https://github.com/lpil/exfmt
---

exfmt 🌸
========

This tool has been deprecated
-----------------------------

With the new formatter in Elixir v1.6 there is no need for this formatter any more. Thanks for checking out exfmt, it's been fun. :)

Intro
-----

> `exfmt` is in alpha. If you run into any problems, please report them.
> 
> **The format produced by exfmt will change significantly before the 1.0.0 release.** If this will cause problems for you, please refrain from using exfmt during the alpha- and beta-test periods.

`exfmt` is inspired by Aaron VonderHaar's elm-format, and aims to format Elixir source code largely according to the standards defined in Aleksei Magusev's Elixir Style Guide.

\# exfmt takes any Elixir code...

defmodule MyApp, do: (
    use( SomeLib )
    def run( data ), do: {
      :ok,
      data
   }
)

\# and rewrites it in a clean and idiomatic style:

defmodule MyApp do
  use SomeLib

  def run(data) do
    {:ok, data}
  end
end

The benefits of `exfmt`:

-   It makes code **easier to write**, because you never have to worry about minor formatting concerns while powering out new code.
-   It makes code **easier to read**, because there are no longer distracting minor stylistic differences between different code bases. As such, your brain can map more efficiently from source to mental model.
-   It makes code **easier to maintain**, because you can no longer have diffs related only to formatting; every diff necessarily involves a material change.
-   It **saves your team time** debating how to format things, because there is a standard tool that formats everything the same way.
-   It **saves you time** because you don't have to nitpick over formatting details of your code.

Contents
--------

-   Usage
-   Installation
-   Editor Integration
    -   Atom
    -   Vim
    -   VS Code
-   Development

Usage
-----

mix exfmt path/to/file.ex

### Command line options

-   `--check` - Check if file is formatted, sets exit status to 1 if false.
-   `--stdin` - Read from STDIN instead of a file.
-   `--unsafe` - Disable the semantics check that verifies that `exmft` has not altered the semantic meaning of the input file.

Installation
------------

`exfmt` makes use of Elixir compiler features coming in Elixir v1.6.0 and as a result can only be run with Elixir v1.6-dev off the Elixir master branch, which you will need to download and compile yourself. Use with earlier versions may work without crashing, but the output format will be incorrect.

An easier method of installation will be available when Elixir v1.6.0 is released. Or sooner, perhaps!

Editor integration
------------------

### Atom

Atom users can install Ron Green's exfmt-atom package.

### Vim

Vim users can use exfmt with Steve Dignam's Neoformat.

Once installed the following config will enable formatting of the current Elixir buffer using `:Neoformat`. For further instructions, please reference the Neoformat documentation.

let g:neoformat\_elixir\_exfmt \= {
  \\ 'exe': 'mix',
  \\ 'args': \['exfmt', '\--stdin'\],
  \\ 'stdin': 1
  \\ }

let g:neoformat\_enabled\_elixir \= \['exfmt'\]

### Visual Studio Code

VSCode users can use exfmt with James Hrisho's vscode-exfmt package.
