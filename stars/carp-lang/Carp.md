---
project: Carp
stars: 5758
description: A statically typed lisp, without a GC, for real-time applications.
url: https://github.com/carp-lang/Carp
---

Carp
====

We now have an official Discord server (invite) - future discussions about the language will most likely happen there, come join!

_WARNING! This is a research project and a lot of information here might become outdated and misleading without any explanation. Don't use it for anything important just yet!_

_Version 0.5.5 of the language is out!_

About
-----

Carp is a programming language designed to work well for interactive and performance sensitive use cases like games, sound synthesis and visualizations.

The key features of Carp are the following:

-   Automatic and deterministic memory management (no garbage collector or VM)
-   Inferred static types for great speed and reliability
-   Ownership tracking enables a functional programming style while still using mutation of cache-friendly data structures under the hood
-   No hidden performance penalties – allocation and copying are explicit
-   Straightforward integration with existing C code
-   Lisp macros, compile time scripting and a helpful REPL

Learn more
----------

-   The Compiler Manual - how to install and use the compiler
-   Carp Language Guide - syntax and semantics of the language
-   Core Docs - documentation for our standard library

A Very Small Example
--------------------

(load-and-use SDL)

(defn tick \[state\]
  (+ state 10))

(defn draw \[app rend state\]
  (bg rend &(rgb (/ @state 2) (/ @state 3) (/ @state 4))))

(defn main \[\]
  (let \[app (SDLApp.create "The Minimalistic Color Generator" 400 300)
        state 0\]
    (SDLApp.run-with-callbacks &app SDLApp.quit-on-esc tick draw state)))

For instructions on how to run Carp code, see this document.

For more examples, check out the examples directory.

Maintainers
-----------

-   Erik Svedäng
-   Veit Heller
-   Jorge Acereda
-   Scott Olsen
-   Tim Dévé

Contributing
------------

Thanks to all the awesome people who have contributed to Carp over the years!

We are always looking for more help – check out the contributing guide to get started.

License
-------

Copyright 2016 - 2021 Erik Svedäng

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

```
http://www.apache.org/licenses/LICENSE-2.0
```

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

The regular expression implementation as found in src/carp\_regex.h are Copyright (C) 1994-2017 Lua.org, PUC-Rio under the terms of the MIT license. Details can be found in the License file LUA\_LICENSE.
