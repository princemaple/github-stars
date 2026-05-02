---
project: lark
stars: 5868
description: Lark is a parsing toolkit for Python, built with a focus on ergonomics, performance and modularity.
url: https://github.com/lark-parser/lark
---

Lark - a parsing toolkit for Python
===================================

Lark is a parsing toolkit for Python, built with a focus on ergonomics, performance and modularity.

Lark can parse all context-free languages. To put it simply, it means that it is capable of parsing almost any programming language out there, and to some degree most natural languages too.

**Who is it for?**

-   **Beginners**: Lark is very friendly for experimentation. It can parse any grammar you throw at it, no matter how complicated or ambiguous, and do so efficiently. It also constructs an annotated parse-tree for you, using only the grammar and an input, and it gives you convenient and flexible tools to process that parse-tree.
    
-   **Experts**: Lark implements both Earley(SPPF) and LALR(1), and several different lexers, so you can trade-off power and speed, according to your requirements. It also provides a variety of sophisticated features and utilities.
    

**What can it do?**

-   Parse all context-free grammars, and handle any ambiguity gracefully
-   Build an annotated parse-tree automagically, no construction code required.
-   Provide first-rate performance in terms of both Big-O complexity and measured run-time (considering that this is Python ;)
-   Run on every Python interpreter (it's pure-python)
-   Generate a stand-alone parser (for LALR(1) grammars)

And many more features. Read ahead and find out!

Most importantly, Lark will save you time and prevent you from getting parsing headaches.

### Quick links

-   Documentation @readthedocs
-   Cheatsheet (PDF)
-   Online IDE
-   Tutorial for writing a JSON parser.
-   Blog post: How to write a DSL with Lark
-   Gitter chat

### Install Lark

```
$ pip install lark --upgrade
```

Lark has no dependencies.

### Syntax Highlighting

Lark provides syntax highlighting for its grammar files (\*.lark):

-   Sublime Text & TextMate
-   vscode
-   Intellij & PyCharm
-   Vim
-   Atom

### Clones

These are implementations of Lark in other languages. They accept Lark grammars, and provide similar utilities.

-   Lerche (Julia) - an unofficial clone, written entirely in Julia.
-   Lark.js (Javascript) - a port of the stand-alone LALR(1) parser generator to Javascsript.

### Hello World

Here is a little program to parse "Hello, World!" (Or any other similar phrase):

from lark import Lark

l \= Lark('''start: WORD "," WORD "!"
            %import common.WORD   // imports from terminal library
            %ignore " "           // Disregard spaces in text
         ''')

print( l.parse("Hello, World!") )

And the output is:

Tree(start, \[Token(WORD, 'Hello'), Token(WORD, 'World')\])

Notice punctuation doesn't appear in the resulting tree. It's automatically filtered away by Lark.

### Fruit flies like bananas

Lark is great at handling ambiguity. Here is the result of parsing the phrase "fruit flies like bananas":

Read the code here, and see more examples here.

List of main features
---------------------

-   Builds a parse-tree (AST) automagically, based on the structure of the grammar
-   **Earley** parser
    -   Can parse all context-free grammars
    -   Full support for ambiguous grammars
-   **LALR(1)** parser
    -   Fast and light, competitive with PLY
    -   Can generate a stand-alone parser (read more)
-   **EBNF** grammar
-   **Unicode** fully supported
-   Automatic line & column tracking
-   Interactive parser for advanced parsing flows and debugging
-   Grammar composition - Import terminals and rules from other grammars
-   Standard library of terminals (strings, numbers, names, etc.)
-   Import grammars from Nearley.js (read more)
-   Extensive test suite
-   Type annotations (MyPy support)
-   And much more!

See the full list of features here

### Comparison to other libraries

#### Performance comparison

Lark is fast and light (lower is better)

Check out the JSON tutorial for more details on how the comparison was made.

For thorough 3rd-party benchmarks, checkout the Python Parsing Benchmarks repo.

#### Feature comparison

Library

Algorithm

Grammar

Builds tree?

Supports ambiguity?

Can handle every CFG?

Line/Column tracking

Generates Stand-alone

**Lark**

Earley/LALR(1)

EBNF

Yes!

Yes!

Yes!

Yes!

Yes! (LALR only)

PLY

LALR(1)

BNF

No

No

No

No

No

PyParsing

PEG

Combinators

No

No

No\*

No

No

Parsley

PEG

EBNF

No

No

No\*

No

No

Parsimonious

PEG

EBNF

Yes

No

No\*

No

No

ANTLR

LL(\*)

EBNF

Yes

No

Yes?

Yes

No

(\* _PEGs cannot handle non-deterministic grammars. Also, according to Wikipedia, it remains unanswered whether PEGs can really parse all deterministic CFGs_)

### Projects using Lark

-   Poetry - A utility for dependency management and packaging
-   Vyper - Pythonic Smart Contract Language for the EVM
-   PyQuil - Python library for quantum programming using Quil
-   Preql - An interpreted relational query language that compiles to SQL
-   Hypothesis - Library for property-based testing
-   mappyfile - a MapFile parser for working with MapServer configuration
-   tartiflette - GraphQL server by Dailymotion
-   synapse - an intelligence analysis platform
-   Datacube-core - Open Data Cube analyses continental scale Earth Observation data through time
-   SPFlow - Library for Sum-Product Networks
-   Torchani - Accurate Neural Network Potential on PyTorch
-   Command-Block-Assembly - An assembly language, and C compiler, for Minecraft commands
-   EQL - Event Query Language
-   Fabric-SDK-Py - Hyperledger fabric SDK with Python 3.x
-   required - multi-field validation using docstrings
-   miniwdl - A static analysis toolkit for the Workflow Description Language
-   pytreeview - a lightweight tree-based grammar explorer
-   harmalysis - A language for harmonic analysis and music theory
-   gersemi - A CMake code formatter
-   MistQL - A query language for JSON-like structures
-   Outlines - Structured generation with Large Language Models

Full list

License
-------

Lark uses the MIT license.

(The standalone tool is under MPL2)

Contributors
------------

Lark accepts pull-requests. See How to develop Lark

Big thanks to everyone who contributed so far:

Sponsor
-------

If you like Lark, and want to see us grow, please consider sponsoring us!

Contact the author
------------------

Questions about code are best asked on gitter or in the issues.

For anything else, I can be reached by email at erezshin at gmail com.

\-- Erez
