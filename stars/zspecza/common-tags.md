---
project: common-tags
stars: 2028
description: 🔖 Useful template literal tags for dealing with strings in ES2015+
url: https://github.com/zspecza/common-tags
---

🔖 A set of **well-tested**, commonly used template literal tag functions for use in ES2015+.

🌟 Plus some extra goodies for easily making your own tags.

Example
-------

import { html } from 'common-tags';

html\`
  <div id\="user-card"\>
    <h2\>${user.name}</h2\>
  </div\>
\`

Project Status
--------------

Info

Badges

Version

License

Popularity

Testing

Quality

Style

Table of Contents
-----------------

-   Introduction
-   Why You Should Care
-   See Who Is Using `common-tags`
-   Installation
    -   Requirements
    -   Instructions
    -   With unpkg
-   Usage
    -   Imports
    -   Available Tags
        -   `html`
            -   Aliases: `source`, `codeBlock`
        -   `safeHtml`
        -   `oneLine`
        -   `oneLineTrim`
        -   `stripIndent`
        -   `stripIndents`
        -   `inlineLists`
        -   `oneLineInlineLists`
        -   `commaLists`
        -   `commaListsOr`
        -   `commaListsAnd`
        -   `oneLineCommaLists`
        -   `oneLineCommaListsOr`
        -   `oneLineCommaListsAnd`
        -   `id`
-   Advanced Usage
    -   Tail Processing
    -   Using Tags on Regular String Literals
    -   Type Definitions
    -   Make Your Own Template Tag
        -   Where It All Starts: createTag
        -   The Anatomy of a Transformer
        -   Plugin Transformers
        -   Plugin Pipeline
        -   Returning Other Values from a Transformer
        -   List of Built-in Transformers
            -   `trimResultTransformer([side])`
            -   `stripIndentTransformer([type='initial'])`
            -   `replaceResultTransformer(replaceWhat, replaceWith)`
            -   `replaceSubstitutionTransformer(replaceWhat, replaceWith)`
            -   `replaceStringTransformer(replaceWhat, replaceWith)`
            -   `inlineArrayTransformer(opts)`
            -   `splitStringTransformer(splitBy)`
-   How to Contribute
-   License
-   Other ES2015 Template Tag Modules

Introduction
------------

`common-tags` initially started out as two template tags I'd always find myself writing - one for stripping indents, and one for trimming multiline strings down to a single line. In its prime, I was an avid user of CoffeeScript, which had this behaviour by default as part of its block strings feature. I also started out programming in Ruby, which has a similar mechanism called Heredocs.

Over time, I found myself needing a few more template tags to cover edge cases - ones that supported including arrays, or ones that helped to render out tiny bits of HTML not large enough to deserve their own file or an entire template engine. So I packaged all of these up into this module.

As more features were proposed, and I found myself needing a way to override the default settings to cover even more edge cases, I realized that my initial implementation wouldn't be easy to scale.

So I re-wrote this module on top of a core architecture that makes use of transformer plugins which can be composed, imported independently and re-used.

Why You Should Care
-------------------

Tagged templates in ES2015 are a welcome feature. But, they have their downsides. One such downside is that they preserve all whitespace by default - which makes multiline strings in source code look terrible.

Source code is not just for computers to interpret. Humans have to read it too 😁. If you care at all about how neat your source code is, or come from a CoffeeScript background and miss the block string syntax, then you will love `common-tags`, as it was initially intended to bring this feature "back" to JS since its initial commit.

`common-tags` also exposes a means of composing pipelines of dynamic transformer plugins. As someone with a little experience writing tagged templates, I can admit that it is often the case that one tag might need to do the same thing as another tag before doing any further processing; for example - a typical tag that renders out HTML could strip initial indents first, then worry about handling character escapes. Both steps could easily be useful as their own separate template tags, but there isn't an immediately obvious way of composing the two together for maximum re-use. `common-tags` offers not one, but two ways of doing this.

Furthermore, I try to keep this project as transparently stable and updated as frequently as I possibly can. As you may have already seen by the project status table, `common-tags` is linted, well tested, tests are well covered, tests pass on both Unix and Windows operating systems, the popularity bandwidth is easily referenced and dependency health is in plain sight 😄. `common-tags` is also already used in production on a number of proprietary sites and dependent projects, and contributions are always welcome, as are suggestions.

See Who Is Using `common-tags`
------------------------------

-   **Slack** (ref)
-   **Discord** (ref)
-   **CircleCI** (ref)
-   **Confluent** (ref)
-   **Tessel** (ref)
-   **Ember.js** (ref)
-   **Angular** (ref)
-   **Prettier** (ref)
-   **Apollo** (ref)
-   **Workbox** (ref)
-   **Gatsby** (ref)
-   **Storybook** (ref)
-   **Cypress** (ref)
-   **stylelint** (ref)
-   **pnpm** (ref)
-   **jss** (ref)
-   **BitMidi** (ref)

Installation
------------

### Requirements

The official recommendation for running `common-tags` is as follows:

-   Node.js v5.0.0 or higher
-   In order to use `common-tags`, your environment will also need to support ES2015 tagged templates (pssst… check Babel out)
-   You might also want to polyfill some features if you plan on supporting older browsers: `Array.prototype.includes`

It might work with below versions of Node, but this is not a guarantee.

### Instructions

`common-tags` is a Node module. So, as long as you have Node.js and NPM installed, installing `common-tags` is as simple as running this in a terminal at the root of your project:

npm install common-tags

### With unpkg

`common-tags` is also available at unpkg. Just put this code in your HTML:

<script src\="https://unpkg.com/common-tags"\></script\>

This will make the library available under a global variable `commonTags`.

Usage
-----

### Imports

Like all modules, `common-tags` begins with an `import`. In fact, `common-tags` supports two styles of import:

**Named imports:**

import {stripIndent} from 'common-tags'

**Direct module imports:**

_(Useful if your bundler doesn't support tree shaking but you still want to only include modules you need)._

import stripIndent from 'common-tags/lib/stripIndent'

### Available Tags

`common-tags` exports a bunch of wonderful pre-cooked template tags for your eager consumption. They are as follows:

#### `html`

##### Aliases: `source`, `codeBlock`

You'll often find that you might want to include an array in a template. Typically, doing something like `${array.join(', ')}` would work - but what if you're printing a list of items in an HTML template and want to maintain the indentation? You'd have to count the spaces manually and include them in the `.join()` call - which is a bit _ugly_ for my taste. This tag properly indents arrays, as well as newline characters in string substitutions, by converting them to an array split by newline and re-using the same array inclusion logic:

import {html} from 'common-tags'
let fruits \= \['apple', 'orange', 'watermelon'\]
html\`
  <div class\="list"\>
    <ul\>
      ${fruits.map(fruit \=> \`<li>${fruit}</li>\`)}
      ${'<li>kiwi</li>\\n<li>guava</li>'}
    </ul\>
  </div\>
\`

Outputs:

<div class\="list"\>
  <ul\>
    <li\>apple</li\>
    <li\>orange</li\>
    <li\>watermelon</li\>
    <li\>kiwi</li\>
    <li\>guava</li\>
  </ul\>
</div\>

#### `safeHtml`

A tag very similar to `html` but it does safe HTML escaping for strings coming from substitutions. When combined with regular `html` tag, you can do basic HTML templating that is safe from XSS (Cross-Site Scripting) attacks.

import {html, safeHtml} from 'common-tags'
let userMessages \= \['hi', 'what are you up to?', '<script>alert("something evil")</script>'\]
html\`
  <div class\="chat-list"\>
    <ul\>
      ${userMessages.map(message \=> safeHtml\`<li\>${message}</li\>\`)}
    </ul\>
  </div\>
\`

Outputs:

<div class\="chat-list"\>
  <ul\>
    <li\>hi</li\>
    <li\>what are you up to?</li\>
    <li\>&lt;script&gt;alert(&quot;something evil&quot;)&lt;/script&gt;</li\>
  </ul\>
</div\>

#### `oneLine`

Allows you to keep your single-line strings under 80 characters without resorting to crazy string concatenation.

import {oneLine} from 'common-tags'

oneLine\`
  foo
  bar
  baz
\`
// "foo bar baz"

#### `oneLineTrim`

Allows you to keep your single-line strings under 80 characters while trimming the new lines:

import {oneLineTrim} from 'common-tags'

oneLineTrim\`
  https://news.com/article
  ?utm\_source=designernews.co
\`
// https://news.com/article?utm\_source=designernews.co

#### `stripIndent`

If you want to strip the initial indentation from the beginning of each line in a multiline string:

import {stripIndent} from 'common-tags'

stripIndent\`
  This is a multi-line string.
  You'll ${verb} that it is indented.
  We don't want to output this indentation.
    But we do want to keep this line indented.
\`
// This is a multi-line string.
// You'll notice that it is indented.
// We don't want to output this indentation.
//   But we do want to keep this line indented.

Important note: this tag will not indent multiline strings coming from the substitutions. If you want that behavior, use the `html` tag (aliases: `source`, `codeBlock`).

#### `stripIndents`

If you want to strip _all_ of the indentation from the beginning of each line in a multiline string:

import {stripIndents} from 'common-tags'

stripIndents\`
  This is a multi-line string.
  You'll ${verb} that it is indented.
  We don't want to output this indentation.
    We don't want to keep this line indented either.
\`
// This is a multi-line string.
// You'll notice that it is indented.
// We don't want to output this indentation.
// We don't want to keep this line indented either.

#### `inlineLists`

Allows you to inline an array substitution as a list:

import {inlineLists} from 'common-tags'

inlineLists\`
  I like ${\['apples', 'bananas', 'watermelons'\]}
  They're good!
\`
// I like apples bananas watermelons
// They're good!

#### `oneLineInlineLists`

Allows you to inline an array substitution as a list, rendered out on a single line:

import {oneLineInlineLists} from 'common-tags'

oneLineInlineLists\`
  I like ${\['apples', 'bananas', 'watermelons'\]}
  They're good!
\`
// I like apples bananas watermelons They're good!

#### `commaLists`

Allows you to inline an array substitution as a comma-separated list:

import {commaLists} from 'common-tags'

commaLists\`
  I like ${\['apples', 'bananas', 'watermelons'\]}
  They're good!
\`
// I like apples, bananas, watermelons
// They're good!

#### `commaListsOr`

Allows you to inline an array substitution as a comma-separated list, the last of which is preceded by the word "or":

import {commaListsOr} from 'common-tags'

commaListsOr\`
  I like ${\['apples', 'bananas', 'watermelons'\]}
  They're good!
\`
// I like apples, bananas or watermelons
// They're good!

#### `commaListsAnd`

Allows you to inline an array substitution as a comma-separated list, the last of which is preceded by the word "and":

import {commaListsAnd} from 'common-tags'

commaListsAnd\`
  I like ${\['apples', 'bananas', 'watermelons'\]}
  They're good!
\`
// I like apples, bananas and watermelons
// They're good!

#### `oneLineCommaLists`

Allows you to inline an array substitution as a comma-separated list, and is rendered out on to a single line:

import {oneLineCommaLists} from 'common-tags'

oneLineCommaLists\`
  I like ${\['apples', 'bananas', 'watermelons'\]}
  They're good!
\`
// I like apples, bananas, watermelons They're good!

#### `oneLineCommaListsOr`

Allows you to inline an array substitution as a comma-separated list, the last of which is preceded by the word "or", and is rendered out on to a single line:

import {oneLineCommaListsOr} from 'common-tags'

oneLineCommaListsOr\`
  I like ${\['apples', 'bananas', 'watermelons'\]}
  They're good!
\`
// I like apples, bananas or watermelons They're good!

#### `oneLineCommaListsAnd`

Allows you to inline an array substitution as a comma-separated list, the last of which is preceded by the word "and", and is rendered out on to a single line:

import {oneLineCommaListsAnd} from 'common-tags'

oneLineCommaListsAnd\`
  I like ${\['apples', 'bananas', 'watermelons'\]}
  They're good!
\`
// I like apples, bananas and watermelons They're good!

#### `id`

A no-op tag that might come in useful in some scenarios, e.g. mocking.

import {id} from 'common-tags'

id\`hello ${'world'}\`
// hello world

Advanced Usage
--------------

### Tail Processing

It's possible to pass the output of a tagged template to another template tag in pure ES2015+:

import {oneLine} from 'common-tags'

oneLine\`
  ${String.raw\`
    foo
    bar\\nbaz
  \`}
\`
// "foo bar\\nbaz"

We can make this neater. Every tag `common-tags` exports can delay execution if it receives a function as its first argument. This function is assumed to be a template tag, and is called via an intermediary tagging process before the result is passed back to our tag. Use it like so (this code is equivalent to the previous code block):

import {oneLine} from 'common-tags'

oneLine(String.raw)\`
  foo
  bar\\nbaz
\`
// "foo bar\\nbaz"

### Using Tags on Regular String Literals

Sometimes you might want to use a tag on a normal string (e.g. for stripping the indentation). For that purpose just call a tag as a function with the passed string:

import {stripIndent} from 'common-tags'

stripIndent("  foo\\n    bar")
// "foo\\n  bar"

### Type Definitions

There are third-party type definitions for `common-tags` on npm. Just install them like so:

npm install @types/common-tags

Please note that these type definitions are not officially maintained by the authors of `common-tags` - they are maintained by the TypeScript community.

### Make Your Own Template Tag

`common-tags` exposes an interface that allows you to painlessly create your own template tags.

#### Where It All Starts: createTag

`common-tags` exports a `createTag` function. This function is the foundation of `common-tags`. The concept of the function works on the premise that transformations occur on a template either when the template is finished being processed (`onEndResult`), or when the tag encounters a string (`onString`) or a substitution (`onSubstitution`). Any tag produced by this function supports tail processing.

The easiest tag to create is a tag that does nothing:

import {createTag} from 'common-tags'

const doNothing \= createTag()

doNothing\`foo bar\`
// 'foo bar'

#### The Anatomy of a Transformer

`createTag` receives either an array or argument list of `transformers`. A `transformer` is just a plain object with three optional methods - `getInitialContext`, `onString`, `onSubstitution` and `onEndResult` - it looks like this:

{
  getInitialContext () {
    // optional. Called before everything else.
    // The result of this hook will be passed to other hooks as \`context\`.
    // If omitted, \`context\` will be an empty object.
  },
  onString (str, context) {
    // optional. Called when the tag encounters a string.
    // (a string is whatever's not inside "${}" in your template literal)
    // \`str\` is the value of the current string
  },
  onSubstitution (substitution, resultSoFar, context) {
    // optional. Called when the tag encounters a substitution.
    // (a substitution is whatever's inside "${}" in your template literal)
    // \`substitution\` is the value of the current substitution
    // \`resultSoFar\` is the end result up to the point of this substitution
  },
  onEndResult (endResult, context) {
    // optional. Called when all substitutions have been parsed
    // \`endResult\` is the final value.
  }
}

#### Plugin Transformers

You can wrap a transformer in a function that receives arguments in order to create a dynamic plugin:

const substitutionReplacer \= (oldValue, newValue) \=> ({
  onSubstitution(substitution, resultSoFar) {
    if (substitution \=== oldValue) {
      return newValue
    }
    return substitution
  }
})

const replaceFizzWithBuzz \= createTag(substitutionReplacer('fizz', 'buzz'))

replaceFizzWithBuzz\`foo bar ${"fizz"}\`
// "foo bar buzz"

#### Plugin Pipeline

You can pass a list of transformers, and `createTag` will call them on your tag in the order they are specified:

// note: passing these as an array also works
const replace \= createTag(
  substitutionReplacer('fizz', 'buzz'),
  substitutionReplacer('foo', 'bar')
)

replace\`${"foo"} ${"fizz"}\`
// "bar buzz"

When multiple transformers are passed to `createTag`, they will be iterated three times - first, all transformer `onString` methods will be called. Once they are done processing, `onSubstitution` methods will be called. Finally, all transformer `onEndResult` methods will be called.

#### Returning Other Values from a Transformer

All transformers get an additional context argument. You can use it to calculate the value you need:

const listSubs \= {
  getInitialContext() {
    return { strings: \[\], subs: \[\] }
  },
  onString(str, context) {
    context.strings.push(str)
    return str
  },
  onSubstitution(sub, res, context) {
    context.subs.push({ sub, precededBy: res })
    return sub
  },
  onEndResult(res, context) {
    return context
  }
}

const toJSON \= {
  onEndResult(res) {
    return JSON.stringify(res, null, 2)
  }
}

const log \= {
  onEndResult(res) {
    console.log(res)
    return res
  }
}

const process \= createTag(\[listSubs, toJSON, log\])

process\`
  foo ${'bar'}
  fizz ${'buzz'}
\`
// {
//  "strings": \[
//    "\\n  foo ",
//    "\\n  foo bar\\n  fizz ",
//    "\\n" 
//  \],
//  "subs": \[
//    {
//      "sub": "bar",
//      "precededBy": "\\n  foo "
//    },
//    {
//      "sub": "buzz",
//      "precededBy": "\\n  foo bar\\n  fizz "
//    }
//  \]
// }

#### List of Built-in Transformers

Since `common-tags` is built on the foundation of this createTag function, it comes with its own set of built-in transformers:

##### `trimResultTransformer([side])`

Trims the whitespace surrounding the end result. Accepts an optional `side` (can be `"start"` or `"end"` or alternatively `"left"` or `"right"`) that when supplied, will only trim whitespace from that side of the string.

##### `stripIndentTransformer([type='initial'])`

Strips the indents from the end result. Offers two types: `all`, which removes all indentation from each line, and `initial`, which removes the shortest indent level from each line. Defaults to `initial`.

##### `replaceResultTransformer(replaceWhat, replaceWith)`

Replaces a value or pattern in the end result with a new value. `replaceWhat` can be a string or a regular expression, `replaceWith` is the new value.

##### `replaceSubstitutionTransformer(replaceWhat, replaceWith)`

Replaces the result of all substitutions (results of calling `${ ... }`) with a new value. Same as for `replaceResultTransformer`, `replaceWhat` can be a string or regular expression and `replaceWith` is the new value.

##### `replaceStringTransformer(replaceWhat, replaceWith)`

Replaces the result of all strings (what's not in `${ ... }`) with a new value. Same as for `replaceResultTransformer`, `replaceWhat` can be a string or regular expression and `replaceWith` is the new value.

##### `inlineArrayTransformer(opts)`

Converts any array substitutions into a string that represents a list. Accepts an options object:

opts \= {
  separator: ',', // what to separate each item with (always followed by a space)
  conjunction: 'and', // replace the last separator with this value
  serial: true // should the separator be included before the conjunction? As in the case of serial/oxford commas
}

##### `splitStringTransformer(splitBy)`

Splits a string substitution into an array by the provided `splitBy` substring, **only** if the string contains the `splitBy` substring.

How to Contribute
-----------------

Please see the Contribution Guidelines.

License
-------

MIT. See license.md.

Other ES2015 Template Tag Modules
---------------------------------

If `common-tags` doesn't quite fit your bill, and you just can't seem to find what you're looking for - perhaps these might be of use to you?

-   tage - make functions work as template tags too
-   is-tagged - Check whether a function call is initiated by a tagged template string or invoked in a regular way
-   es6-template-strings - Compile and resolve template strings notation as specified in ES6
-   t7 - A light-weight virtual-dom template library
-   html-template-tag - ES6 Tagged Template for compiling HTML template strings.
-   clean-tagged-string - A simple utility function to clean ES6 template strings.
-   multiline-tag - Tags for template strings making them behave like coffee multiline strings
-   deindent - ES6 template string helper for deindentation.
-   heredoc-tag - Heredoc helpers for ES2015 template strings
-   regx - Tagged template string regular expression compiler.
-   regexr - Provides an ES6 template tag function that makes it easy to compose regexes out of template strings without double-escaped hell.
-   url-escape-tag - A template tag for escaping url parameters based on ES2015 tagged templates.
-   shell-escape-tag - An ES6+ template tag which escapes parameters for interpolation into shell commands.
-   sql-tags - ES6 tagged template string functions for SQL statements.
-   sql-tag - A template tag for writing elegant sql strings.
-   sequelize-sql-tag - A sequelize plugin for sql-tag
-   pg-sql-tag - A pg plugin for sql-tag
-   sql-template-strings - ES6 tagged template strings for prepared statements with mysql and postgres
-   sql-composer - Composable SQL template strings for Node.js
-   pg-template-tag - ECMAScript 6 (2015) template tag function to write queries for node-postgres.
-   digraph-tag - ES6 string template tag for quickly generating directed graph data
-   es2015-i18n-tag - ES2015 template literal tag for i18n and l10n translation and localization
