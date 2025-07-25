---
project: acorn
stars: 11019
description: A small, fast, JavaScript-based JavaScript parser
url: https://github.com/acornjs/acorn
---

Acorn
=====

A tiny, fast JavaScript parser, written completely in JavaScript.

Community
---------

Acorn is open source software released under an MIT license.

You are welcome to report bugs or create pull requests on github.

Packages
--------

This repository holds three packages:

-   acorn: The main parser
-   acorn-loose: The error-tolerant parser
-   acorn-walk: The syntax tree walker

To build the content of the repository, run `npm install`.

git clone https://github.com/acornjs/acorn.git
cd acorn
npm install

Plugin developments
-------------------

Acorn is designed to support plugins which can, within reasonable bounds, redefine the way the parser works. Plugins can add new token types and new tokenizer contexts (if necessary), and extend methods in the parser object. This is not a clean, elegant API—using it requires an understanding of Acorn's internals, and plugins are likely to break whenever those internals are significantly changed. But still, it is _possible_, in this way, to create parsers for JavaScript dialects without forking all of Acorn. And in principle it is even possible to combine such plugins, so that if you have, for example, a plugin for parsing types and a plugin for parsing JSX-style XML literals, you could load them both and parse code with both JSX tags and types.

A plugin is a function from a parser class to an extended parser class. Plugins can be used by simply applying them to the `Parser` class (or a version of that already extended by another plugin). But because that gets a little awkward, syntactically, when you are using multiple plugins, the static method `Parser.extend` can be called with any number of plugin values as arguments to create a `Parser` class extended by all those plugins. You'll usually want to create such an extended class only once, and then repeatedly call `parse` on it, to avoid needlessly confusing the JavaScript engine's optimizer.

const {Parser} \= require("acorn")

const MyParser \= Parser.extend(
  require("acorn-jsx")(),
  require("acorn-bigint")
)
console.log(MyParser.parse("// Some bigint + JSX code"))

Plugins override methods in their new parser class to implement additional functionality. It is recommended for a plugin package to export its plugin function as its default value or, if it takes configuration parameters, to export a constructor function that creates the plugin function.

This is what a trivial plugin, which adds a bit of code to the `readToken` method, might look like:

module.exports \= function noisyReadToken(Parser) {
  return class extends Parser {
    readToken(code) {
      console.log("Reading a token!")
      super.readToken(code)
    }
  }
}
