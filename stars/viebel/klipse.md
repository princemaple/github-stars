---
project: klipse
stars: 3135
description: Klipse is a JavaScript plugin for embedding interactive code snippets in tech blogs.
url: https://github.com/viebel/klipse
---

Klipse
======

Klipse is a JavaScript plugin for embedding interactive code snippets in tech blogs. See examples at https://blog.klipse.tech/

Technically, Klipse is a small piece of JavaScript code that evaluates code snippets in the browser and it is pluggable on any web page.

If you like this stuff, please consider a (small donation) on Patreon.

Plugin
------

The klipse plugin is a `JavaScript` tag (see details below) that transforms static code snippets of an html page into live and interactive snippets:

1.  **Live**: The code is executed in your browser
2.  **Interactive**: You can modify the code and it is evaluated as you type

The code evaluation is done in the browser: no server is involved at all!

Live demo
=========

With the klipse plugin, the code is evaluated as you type...

Here is a live demo of the embedding of klipse in a web page.

JavaScript

Ruby

PHP

Clojure

Supported languages
===================

-   JavaScript: evaluation is done with the JavaScript function `eval` and pretty printing of the result is done with pretty-format
-   Clojure\[Script\]: evaluation is done with Self-Hosted Clojurescript
-   Ruby: evaluation is done with Opal
-   C++: evaluation is done with JSCPP
-   Python: evaluation is done with Skulpt
-   Python3: evaluation is done with Pyodide
-   Scheme: evaluation is done with BiwasScheme
-   Prolog: evaluation is done with Tau Prolog
-   Common Lisp: evaluation is done with JSCL
-   PHP: evaluation is done with Uniter
-   SQL: evaluation is done with sql.js. See SQL example
-   Lua: evaluation is done with wasm\_lua
-   Go: evaluation is done with Yaegi
-   BrainFuck
-   JSX
-   EcmaScript2017
-   Google Charts: See Interactive Business Report with Google Charts.

The code editing inside the interactive snippets is powered by CodeMirror.

How does it work?
=================

-   JavaScript: A new way of blogging about JavaScript
-   Ruby: A new way of blogging about ruby
-   Clojure\[Script\]: How to klipsify a clojure\[script\] blog post

Integration
===========

In order to integrate the klipse plugin on a blog, library documentation or any other web page, you have to follow 3 simple steps.

1.  Make sure you have `<!DOCTYPE html>` at the top of your html file and `<meta charset="utf-8">` right after your `<head>` (It is required in order to display properly the CodeMirror elements used by Klipse.)
    
2.  Add css and custom configuration somewhere in the page (it could be in the `<head>` or in the `<body>`) **before** the `<script>` element of step #3. The selector keys are per language (see below for a list of supported languages) and the value are the CSS selector of the elements that you want to klipsify.
    

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
        selector\_eval\_js: '.language-klipse-eval-js', // css selector for the html elements you want to klipsify
    };
</script\>

1.  Add the `JavaScript` tag at the **end of the body tag** :

For Clojure:

<script src\="https://storage.googleapis.com/app.klipse.tech/plugin/js/klipse\_plugin.js"\></script\>
</body\>

For other languages:

    <script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>
</body\>

Here is an interactive guide of the klipse snippets.

If you want to host Klipse JavaScript tag from your own server, see Host Klipse Locally.

If you want to use an older version of Klipse, see Use Older Versions.

JavaScript
----------

Here is the full interactive guide of the klipse `JavaScript` snippets.

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
        selector\_eval\_js: '.language-klipse-eval-js', // css selector for the html elements you want to klipsify
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

Here is a jsfiddle with Klipse plugin for JavaScript. And here are detailed explanations about a JavaScript live code editor in a blog post.

Clojure and ClojureScript in a web page
---------------------------------------

> Pay attention: for Clojure interactive snippets, you must use the **non-minified** version of klipse as for the moment, self-host cljs doesn't support advanced compilation!

Here is the full interactive guide of the klipse `clojure` snippets.

You can manipulate the DOM inside KLIPSE: here is a tutorial.

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
        selector: '.language-klipse'// css selector for the html elements you want to klipsify
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin/js/klipse\_plugin.js"\></script\>

ClojureScript project
---------------------

If you want to integrate Klipse inside a Clojurescript project, it is recommended to consume Klipse as a Clojurescript library like any other Clojurescript lib, just like this .

Inside your code you have to require two namespaces and call a function:

(ns my.project
  (:require \[klipse.run.plugin.plugin\] ;; this namespace initializes Klipse. We require it for its side effects
            \[klipse.plugin :as klipse-plugin\]))

(klipse-plugin/init #js {:selector ".language-klipse"
                         :selector\_reagent ".language-reagent"})

Here is an example of a tiny reagent demo project that integrates Klipse as a Clojurescript library.

Python
------

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
        selector\_eval\_python\_client: '.language-klipse-python', // css selector for the html elements you want to klipsify
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

Python3 (numpy, pandas)
-----------------------

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
        selector\_pyodide: '.language-klipse-pyodide', // css selector for the html elements you want to klipsify
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

Ruby
----

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
        selector\_eval\_ruby: '.language-klipse-eval-ruby', // css selector for the html elements you want to klipsify
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

Lua
---

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>
<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/lua.css"\>

<script\>
    window.klipse\_settings \= {
        selector\_lua: '.language-klipse-lua', // css selector for the html elements you want to klipsify
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

Go
--

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
        selector\_golang: '.language-klipse-go, // css selector for the html elements you want to klipsify
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

Scheme
------

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
        selector\_eval\_scheme: '.language-klipse-eval-scheme', // css selector for the html elements you want to klipsify
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

Prolog
------

Prolog code snippets are separated into two kinds:

-   Rules
-   Queries

In the query, you must omit the `?-` characters.

See A new way of blogging about Prolog for a full example and guide.

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>
<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/prolog.css"\>

<script\>
    window.klipse\_settings \= {
        selector\_prolog\_rules: '.language-prolog-rules', // css selector for the html elements that contain prolog rules
        selector\_prolog\_query: '.language-prolog-query', // css selector for the html elements that contain prolog queries
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js?v=7.7.1-a"\></script\>

Common Lisp
-----------

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
        selector\_eval\_clisp: '.language-klipse-eval-clisp', // css selector for the html elements you want to klipsify
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

OCaml
-----

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
 	    selector\_eval\_ocaml: '.language-klipse-ocaml', // selector for ocaml evaluation snippets
	    selector\_transpile\_ocaml: '.language-transpile-ocaml' // selector for ocaml transpilation snippets
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

ReasonML version 3
------------------

> Note: Code Snippets in Reason version 3 will automagically be upgraded to latest Reason version once a new version of Reason is released.

We have 4 kinds of ReasonML snippets:

1.  Code Evaluation
2.  Transpilation to JavaScript
3.  Transpilation to Ocaml
4.  Transpilation from Ocaml

Here is the JavaScript tag that you need to setup for embedding ReasonML snippets on your page:

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
 	     selector\_transpile\_reason\_3: '.language-transpile-reason', // selector for reason transpilation snippets
         selector\_transpile\_reason\_3\_to\_ocaml: '.language-transpile-reason-to-ocaml', // selector for reason transpilation into ocaml snippets
         selector\_eval\_reason\_3: '.language-klipse-reason',  // selector for reason evaluation snippets
         selector\_ocaml\_to\_reason: '.language-klipse-ocaml-to-reason' // selector for ocaml to reason snippets
   };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

ReasonML - Old Syntax(deprecated)
---------------------------------

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
    	 selector\_transpile\_reason: '.language-transpile-reason', // selector for reason transpilation snippets
         selector\_transpile\_reason\_to\_ocaml: '.language-transpile-reason-to-ocaml', // selector for reason transpilation into ocaml snippets
         selector\_eval\_reason: '.language-klipse-reason' // selector for reason evaluation snippets
   };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

SQL
---

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>
<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/sql.css"\>

<script\>
    window.klipse\_settings \= {
     selector\_sql: '.sql',
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

PHP
---

<link rel\="stylesheet" type\="text/css" href\="https://storage.googleapis.com/app.klipse.tech/css/codemirror.css"\>

<script\>
    window.klipse\_settings \= {
        selector\_eval\_php: '.language-klipse-eval-php', // css selector for the html elements you want to klipsify
    };
</script\>
<script src\="https://storage.googleapis.com/app.klipse.tech/plugin\_prod/js/klipse\_plugin.min.js"\></script\>

https
-----

If your site runs under `https`, you need to load the klipse plugin from `https://storage.googleapis.com/app.klipse.tech` instead of `http://app.klipse.tech`.

The reason is that the klipse plugin is hosted on Google Cloud Storage and for the moment SSL is not supported for custom domains.

Configuration
-------------

The klipse plugin is configurable both at the level of the page and at the level of the snippet.

### Page level configuration

Here are the settings for the klipse plugin a page level:

window.klipse\_settings \= {
     eval\_idle\_msec: 20, // idle time in msec before the snippet is evaluated
     selector: '.language-klipse', // selector for Clojure evaluation snippets
     selector\_js: '.language-klipse-js', // selector for Clojure transpilation snippets
     selector\_reagent: '.language-reagent', // selector for reagent snippets
     selector\_google\_charts: '.language-google-charts' // selector for Google charts snippets
     selector\_oblivion: '.language-oblivion' // selector for oblivion snippets
     selector\_eval\_js: '.language-klipse-eval-js', // selector for JavaScript evaluation snippets
     selector\_eval\_ruby: '.language-klipse-eval-ruby', // selector for Ruby evaluation snippets
     selector\_lua: '.language-klipse-lua', // selector for lua evaluation snippets
     selector\_es2017: '.language-klipse-es2017', // selector for EcmaScript 2017 evaluation snippets
     selector\_jsx: '.language-klipse-jsx', // selector for JSX evaluation snippets
     selector\_transpile\_jsx: '.language-transpile-jsx', // selector for JSX transpilation snippets
     selector\_render\_jsx: '.language-render-jsx', // selector for JSX rendering snippets
     selector\_react: '.language-react', // selector for React snippets
     selector\_eval\_php: '.language-klipse-eval-php', // selector for PHP evaluation snippets
     selector\_eval\_markdown: '.language-klipse-markdown', // selector for Markdown transpilation snippets
     selector\_render\_hiccup: '.render-hiccup', // selector for Hiccup rendering snippets
     selector\_transpile\_hiccup: '.transpile-hiccup', // selector for Hiccup transpiling snippets
     selector\_eval\_lambdaway: '.language-klipse-lambdaway', // selector for lambdaway transpilation snippets
     selector\_eval\_python\_client: '.language-klipse-python', // selector for Python evaluation snippets
     selector\_eval\_cpp: '.language-klipse-cpp', // selector for cpp evaluation
     selector\_eval\_html: '.language-klipse-html', // selector for Html evaluation snippets
     selector\_sql: '.language-klipse-sql', // selector for sqlite evaluation snippets
     selector\_eval\_scheme: '.language-klipse-scheme', // selector for Scheme evaluation snippets
     selector\_brainfuck: '.language-klipse-brainfuck', // selector for Brainfuck snippets
     selector\_eval\_ocaml: '.language-klipse-ocaml', // selector for Ocaml evaluation snippets
     selector\_transpile\_ocaml: '.language-transpile-ocaml', // selector for Ocaml transpilation snippets
     selector\_transpile\_reason\_3: '.language-transpile-reason', // selector for Reason transpilation snippets
     selector\_transpile\_reason\_3\_to\_ocaml: '.language-transpile-reason-to-ocaml', // selector for Reason transpilation into ocaml snippets
     selector\_eval\_reason\_3: '.language-klipse-reason', // selector for Reason evaluation snippets
     selector\_ocaml\_to\_reason: '.language-klipse-ocaml-to-reason' // selector for Ocaml to reason snippets
     cached\_ns\_root: '/my-root', // the root of Clojure cached namespace, default: https://viebel.github.io/cljs-analysis-cache/cache/
     clojure\_cached\_macro\_ns\_regexp: /reagent.\*/, // the regexp for Clojure macro namespaces that are cached
     clojure\_cached\_ns\_regexp: /reagent.\*/, // the regexp for clojure namespaces that are cached
     codemirror\_root: '/my-codemirror-root', // the root of Codemirror files
     scripts\_root: '/my-scripts-root', // the root of scripts files (e.g pretty\_format.js, opal.js ...)
     re\_evaluate\_all\_snippets\_on\_change: false, // Whether all snippets should be reevaluated when any one snippet is edited, since snippets might depend on each other
     editor\_type: 'code-mirror', //the type of the editor for Klipse results (the element where the evaluation of the snippet is displayed). Allowed values:
                                 // "code-mirror": The input editor is codemirror. The output editor is codemirror
                                 // "html": The input editor is codemirror. The output editor is html
                                 // "dom": The input editor is plain text. The output editor is plain text

};

Additionally, you can configure CodeMirror input (snippet source code) and output (snippet evaluation) by setting `codemirror_options_in` and `codemirror_options_out`:

Currently, we support all the settings CodeMirror Configuration settings and part of the Addons settings: `matchBrackets` and `autoCloseBrackets`.

For instance, you can modify the `indentUnit`, `lineWrapping`, `lineNumbers` and `autoCloseBrackets` like this:

window.klipse\_settings \= {
    codemirror\_options\_in: {
        indentUnit: 8,
        lineWrapping: true,
        lineNumbers: true,
        autoCloseBrackets: true
    },
    codemirror\_options\_out: {
        lineWrapping: true,
        lineNumbers: true
    }
}

#### Clojure only

-   `print_length`: (default 1000) max number of items in collections to display - useful to prevent browser stuck when evaluating infinite sequences like `(range)`
-   `beautify_strings`: (default false) when evaluation result is a string - display the "interior" of the string without escaping the quotes.

### Snippet level configuration

The following attributes can be added to the DOM element of the snippet:

-   `data-eval-idle-msec`: (default 20) idle time in msec before the snippet is evaluated
-   `data-loop-msec`: (default `undefined`) the code is run in a loop every `data-loop-msec` msec
-   `data-preamble`: (default `""`) A string containing Clojurescript source code that should be run before the contents of this snippet, eg "(reset! canvas-id :canvas-2)". Useful for hiding implementation details from readers in blog posts, like e.g. setting a `canvas-id` atom to `:canvas-2`, or for performing any other setup operations that need to be done on a per-snippet basis
-   `data-editor-type`: (default `"code-mirror"`) the type of the editor for the klipse result (the element where the evaluation of the snippet is displayed). Allowed values: \*\* "code-mirror": The input editor is codemirror. The output editor is codemirror \*\* "html": The input editor is codemirror. The output editor is html \*\* "dom": The input editor is plain text. The output editor is plain text

### JavaScript only

-   `data-external-libs`: comma separated list of JavaScript libraries to load before snippet evaluation
-   `data-async-code`: (default `false`) when `true`, asynchronous calls to `console.log` append their result to the result cell

#### Clojure only

Here is a live demo of the different snippet level configuration options.

The following data attributes are supported on a klipse snippet DOM element:

-   `data-static-fns`: (default `false`) set to true for using static dispatch
-   `data-external-libs`: comma separated list of github repositories to resolve dependencies: you need to provide the full list of dependencies (including the dependencies of dependencies recursively). See for instance Lambda Calculus with clojure and Klipse
-   `data-print-length`: (default 1000) max number of items in collections to display - useful to prevent browser stuck when evaluating infinite sequences like `(range)`
-   `data-beautify-strings`: (default false) when evaluation result is a string - display the "interior" of the string without escaping the quotes.
-   `data-verbose`: (default false) passed to bootstrapped `eval` and `compile` `:verbose` opts
-   `data-max-eval-duration`: (default 1000) max number of milliseconds the snippet code is allowed to run synchronously before being interrupted.
-   `data-compile-display-guard`: (default false) when true, display the anti-starvation code inside result of compilation

Styling
-------

The Klipse plugin can be easily styled with CSS, which can be applied both to the Klipse plugin's own elements, and to the CodeMirror editor's elements. Much of the styling you'll apply will be to CodeMirror, as it contains all the CSS classes to style the code itself. Surrounding CodeMirror is the Klipse plugin, the styles of which control the plugin's borders, and the executed code's output.

DOM elements
------------

Each klipse snippet is associated with 4 HTML elements:

1.  The klipse snippet itself: it has the class `klipse-snippet`.
2.  The result: it has the class `klipse-result`.
3.  A container: it has the class `klipse-container` and is accessible inside the klipse snippet through the global variable `klipse_container` (the global variable is dynamically bound to the correct klipse container).
4.  A separator: it has the class `klipse-separator`.

### Changing the style of CodeMirror

You can change the theme of the CodeMirror editor simply by modifying its CSS. If you don't want to create your own theme, Farhad Gayour has an awesome list of ready-made themes you can select from. Have a look at the different themes by selecting them from the drop-down. Once you've found one you like, head to the theme repo to copy the CSS, paste it into a CSS file, and link to it from the HTML page containing your Klipse plugin.

### Changing the style of the Klipse plugin

To change the style of the Klipse plugin's borders and the console output, you'll need to add a few extra style rules to your CSS file. These are:

-   `.CodeMirror` - modify the plugin's borders and CodeMirror's containing `div`
-   `.CodeMirror:last-child::before` - modify the console's title (i.e. the bit that says _Output:_)
-   `.CodeMirror:last-child` - modify the console area (i.e. the area beneath _Output:_)

You can see an example of styling Klipse in `demos/styling`. And here is a live demo

Interactive slides with Klipse
------------------------------

You can build interactive slides by integrating Klipse with Reveal.js using this template for reveal.js and Klipse.

Klipse Community
----------------

Here are a couple of examples of blogs using the klipse plugin:

-   Clojure: Procedural Dungeon Generation: A Drunkard's Walk in ClojureScript
-   Python: Drawing fractals with a turtle
-   Clojure: Island Generator
-   ClojureScript transpiled: blog.ducky.io - More about protocols in ClojureScript
-   Ruby: jessewaites.com - interactive ruby snippets
-   Clojure: z.caudate.me - live documentation with klipse
-   Ruby, Javascript, Clojure: blog.klipse.tech
-   Prolog: A new way of blogging about Prolog
-   Clojure documentation: Anonymous functions in clojure
-   JavaScript: Untangled.io - Advanced ES6 destructuring techniques with live examples
-   Clojure: Klipse for Kids: A fun way to learn computer programming
-   JavaScript Immutable.js: An Introduction with examples written for humans
-   Clojure: Yet another scheme dialect written in Clojure and ClojureScript
-   JavaScript: Try Partial Lenses with KLIPSE
-   JavaScript: Clause.js, a JavaScript contract system, documentation created with klipse
-   Clojure: Reagent deep dive part 1 2 3 4
-   ClojureScript: Visualising Bézier Curves
-   Clojure: core.async fun tutorial
-   ClojureScript: reagent and reframe playground
-   JavaScript: chai unit tests playground
-   Clojure: polynomial macro
-   Prolog: A scientific paper with interactive code snippets: \[Continuous Reasoning for Managing Next-Gen Distributed Applications\] (http://eptcs.web.cse.unsw.edu.au/paper.cgi?ICLP2020.22.pdf)

Ask us any question about the klipse plugin (integration, feature requests...) on

Access the CodeMirror editors programmatically
----------------------------------------------

Each code snippet is wrapped into a CodeMirror editor.

The CodeMirror editors are accessible via the JavaScript global variable: `klipse_editors`. This is an array that contains the CodeMirror editors wrapping the original code snippets. For instance, you can modify the content of the code snippet `i` by calling: `klipse_editors[i].setValue('let a = 1');`

Here is a jsfiddle that shows it in action.

The evaluation of each snippet is also wrapped into a CodeMirror editor. The CodeMirror editors that wrapped results are accessible via the JavaScript global variable: `klipse_results`. This is an array that contains the CodeMirror editors wrapping the results of the evaluation of the code snippets. For instance, you can read the content of the code snippet `i` by calling: `klipse_results[i].getValue();`

Here is a jsfiddle that shows it in action.

Use older versions
------------------

Since version `6.8.0`, Klipse is published on npm. Therefore you can access the klipse files of a specific version from unpkg - a cdn for stuff that is published to `npm`.

For instance, The urls are for the version `6.8.0` are:

-   JavaScript minified: https://unpkg.com/klipse@6.8.0/dist/klipse\_plugin.min.js
-   JavaScript non-minified: https://unpkg.com/klipse@6.8.0/dist/klipse\_plugin.min.js
-   Css: https://unpkg.com/klipse@6.8.0/dist/codemirror.css

Host Klipse locally
-------------------

You can download klipse with `npm` or `bower`.

In order to serve Klipse from your own server, you have to:

1.  Include in your page all the assets that you need from the `dist` folder: `codemirror.css`, `klipse_plugin.js` or `klipse_plugin.min.js`, `javascript.inc.js` (CodeMirror JavaScript addon), `pretty_format.js` (JavaScript beautifier)
2.  set `klipse_settings.no_dynamic_scripts=true;`

If you need more assets that are usually dynamically loaded by klipse, please download them manually.

Klipse App - Clojure Web Repl
-----------------------------

Here is the information about the Klipse app

The Web REPL is live at http://app.klipse.tech

Here is the manual for the KLIPSE web repl.

Languages supported in the REPL: `Clojure` and `ClojureScript`.

License
=======

If you like this stuff, please consider a (small donation) on Patreon.

See the LICENSE file for license rights and limitations (GNU General Public License v3.0).
