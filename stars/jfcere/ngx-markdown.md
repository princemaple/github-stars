---
project: ngx-markdown
stars: 1167
description: Angular markdown component/directive/pipe/service to parse static, dynamic or remote content to HTML with syntax highlight and more...
url: https://github.com/jfcere/ngx-markdown
---

  

ngx-markdown
============

ngx-markdown is an Angular library that combines...

-   Marked to parse markdown to HTML
-   Prism.js for language syntax highlight
-   Emoji-Toolkit for emoji support
-   KaTeX for math expression rendering
-   Mermaid for diagrams and charts visualization
-   Clipboard.js to copy code blocks to clipboard

Demo available @ https://jfcere.github.io/ngx-markdown  
StackBlitz available @ https://stackblitz.com/edit/ngx-markdown

### Table of contents

-   Installation
-   Configuration
-   Usage
-   Renderer
-   Syntax highlight
-   Demo application
-   AoT compilation
-   Road map
-   Contribution
-   Support Development

Installation
------------

### ngx-markdown

To add ngx-markdown along with the required marked library to your `package.json` use the following commands.

npm install ngx-markdown marked@^17.0.0 --save

### Syntax highlight

> 🔔 Syntax highlight is **optional**, skip this step if you are not planning to use it

To add Prism.js library to your `package.json` use the following command.

npm install prismjs@^1.30.0 --save

To activate Prism.js syntax highlight you will need to include...

-   prism.js core library - `node_modules/prismjs/prism.js` file
-   a highlight css theme - from `node_modules/prismjs/themes` directory
-   desired code language syntax files - from `node_modules/prismjs/components` directory

_Additional themes can be found by browsing the web such as Prism-Themes or Mokokai for example._

If you are using Angular CLI you can follow the `angular.json` example below...

"styles": \[
  "styles.css",
+ "node\_modules/prismjs/themes/prism-okaidia.css"
\],
"scripts": \[
+ "node\_modules/prismjs/prism.js",
+ "node\_modules/prismjs/components/prism-csharp.min.js", # c-sharp language syntax
+ "node\_modules/prismjs/components/prism-css.min.js" # css language syntax
\]

#### Line Numbers plugin

To use the line numbers plugin that shows line numbers in code blocks, in addition to Prism.js configuration files, you will need to include the following files from `prismjs/plugins/line-numbers` directory to your application:

-   CSS styling for line numbers - `prism-line-numbers.css`
-   line numbers plugin script - `prism-line-numbers.js`

If you are using Angular CLI you can follow the `angular.json` example below...

"styles": \[
  "src/styles.css",
  "node\_modules/prismjs/themes/prism-okaidia.css",
+ "node\_modules/prismjs/plugins/line-numbers/prism-line-numbers.css"
\],
"scripts": \[
  "node\_modules/prismjs/prism.js",
  "node\_modules/prismjs/components/prism-csharp.min.js",
  "node\_modules/prismjs/components/prism-css.min.js",
+ "node\_modules/prismjs/plugins/line-numbers/prism-line-numbers.js"
\]

Using `markdown` component and/or directive, you will be able to use the `lineNumbers` property to activate the plugin. The property can be used in combination with either `data` for variable binding, `src` for remote content or using transclusion for static markdown.

Additionally, you can use `start` input property to specify the offset number for the first display line.

<markdown
  lineNumbers
  \[start\]\="5"
  \[src\]\="path/to/file.js"\>
</markdown\>

#### Line Highlight plugin

To use the line highlight plugin that highlights specific lines and/or line ranges in code blocks, in addition to Prism.js configuration files, you will need to include the following files from `prismjs/plugins/line-highlight` directory to your application:

-   CSS styling for line highlight - `prism-line-highlight.css`
-   line highlight plugin script - `prism-line-highlight.js`

If you are using Angular CLI you can follow the `angular.json` example below...

"styles": \[
  "src/styles.css",
  "node\_modules/prismjs/themes/prism-okaidia.css",
+ "node\_modules/prismjs/plugins/line-highlight/prism-line-highlight.css"
\],
"scripts": \[
  "node\_modules/prismjs/prism.js",
  "node\_modules/prismjs/components/prism-csharp.min.js",
  "node\_modules/prismjs/components/prism-css.min.js",
+ "node\_modules/prismjs/plugins/line-highlight/prism-line-highlight.js"
\]

Using `markdown` component and/or directive, you will be able to use the `lineHighlight` property to activate the plugin. The property can be used in combination with either `data` for variable binding, `src` for remote content or using transclusion for static markdown.

Use `line` input property to specify the line(s) to highlight and optionally there is a `lineOffset` property to specify the starting line of code your snippet represents.

<markdown
  lineHighlight
  \[line\]\="'6, 10-16'"
  \[lineOffset\]\="5"
  \[src\]\="path/to/file.js"\>
</markdown\>

#### Command Line Plugin

To use the command line plugin that displays a command line with a prompt and, optionally, the output/response from the commands, you will need to include the following files from `prismjs/plugins/command-line` directory to your application:

-   CSS styling for command line - `prism-command-line.css`
-   command line plugin script - `prism-command-line.js`

If you are using Angular CLI you can follow the `angular.json` example below...

"styles": \[
  "src/styles.css",
  "node\_modules/prismjs/themes/prism-okaidia.css",
+ "node\_modules/prismjs/plugins/command-line/prism-command-line.css"
\],
"scripts": \[
  "node\_modules/prismjs/prism.js",
  "node\_modules/prismjs/components/prism-csharp.min.js",
  "node\_modules/prismjs/components/prism-css.min.js",
+ "node\_modules/prismjs/plugins/command-line/prism-command-line.js"
\]

Using `markdown` component and/or directive, you will be able to use the `commandLine` property to activate the plugin. The property can be used in combination with either `data` for variable binding, `src` for remote content or using transclusion for static markdown.

For a server command line, specify the user and host names using the `user` and `host` input properties. The resulting prompt displays a `#` for the root user and `$` for all other users. For any other command line, such as a Windows prompt, you may specify the entire prompt using the `prompt` input property.

You may also specify the lines to be presented as output (no prompt and no highlighting) through the `output` property in the following simple format:

-   A single number refers to the line with that number
-   Ranges are denoted by two numbers, separated with a hyphen (-)
-   Multiple line numbers or ranges are separated by commas
-   Whitespace is allowed anywhere and will be stripped off

<markdown
  commandLine
  \[user\]\="'chris'"
  \[host\]\="'remotehost'"
  \[output\]\="'2, 4-8'"
  \[src\]\="'path/to/file.bash'"\>
</markdown\>

Optionally, to automatically present some lines as output without providing the line numbers, you can prefix those lines with any string and specify the prefix using the `filterOutput` input property. For example, `[filterOutput]="'(out)'"` will treat lines beginning with `(out)` as output and remove the prefix.

<markdown
  commandLine
  \[prompt\]\="'PS C:\\Users\\Chris>'"
  \[filterOutput\]\="'(out)'"\>
  \`\`\`powershell
  Get-Date
  (out)
  (out)Sunday, November 7, 2021 8:19:21 PM
  (out)
  \`​\`\`
</markdown\>

### Emoji support

> 🔔 Emoji support is **optional**, skip this step if you are not planning to use it

To add Emoji-Toolkit library to your `package.json` use the following command.

npm install emoji-toolkit@^10.0.0 --save

To activate Emoji-Toolkit for emoji suppport you will need to include...

-   Emoji-Toolkit library - `node_modules/emoji-toolkit/lib/js/joypixels.min.js`

If you are using Angular CLI you can follow the `angular.json` example below...

"scripts": \[
+ "node\_modules/emoji-toolkit/lib/js/joypixels.min.js",
\]

#### Emoji plugin

Using `markdown` component and/or directive, you will be able to use the `emoji` property to activate Emoji-Toolkit plugin that converts emoji shortnames such as `:heart:` to native unicode emojis.

<markdown emoji\>
  I :heart: ngx-markdown
</markdown\>

> 📘 You can refer to this Emoji Cheat Sheet for a complete list of _shortnames_.

### Math rendering

> 🔔 Math rendering is **optional**, skip this step if you are not planning to use it

To add KaTeX library to your `package.json` use the following command.

npm install katex@^0.16.0 --save

To activate KaTeX math rendering you will need to include...

-   KaTex JavaScript library - `node_modules/katex/dist/katex.min.js` file
-   KaTex Auto-Render extension - `node_modules/katex/dist/contrib/auto-render.min.js,` file
-   KaTex CSS customization - `node_modules/katex/dist/katex.min.css` file

If you are using Angular CLI you can follow the `angular.json` example below...

"styles": \[
  "styles.css",
+ "node\_modules/katex/dist/katex.min.css"
\],
"scripts": \[
+ "node\_modules/katex/dist/katex.min.js",
+ "node\_modules/katex/dist/contrib/auto-render.min.js",
\]

#### KaTeX plugin

Using `markdown` component and/or directive, you will be able to use the `katex` property to activate KaTeX plugin that renders mathematical expression to HTML.

<markdown
  katex
  \[src\]\="path/to/file.md"\>
</markdown\>

Optionally, you can use `katexOptions` property to specify both the KaTeX options and the KaTeX Auto-Render options.

import { KatexOptions } from 'ngx-markdown';

public options: KatexOptions \= {
  displayMode: true,
  throwOnError: false,
  errorColor: '#cc0000',
  delimiters: \[...\],
  ...
};

<markdown
  katex
  \[katexOptions\]\="options"
  \[src\]\="path/to/file.md"\>
</markdown\>

> 📘 Follow official KaTeX options and KaTeX Auto-Render options documentation for more details on the available options.

### Diagrams tool

> 🔔 Diagram support is **optional**, skip this step if you are not planning to use it

To add Mermaid library to your `package.json` use the following command.

npm install mermaid@^11.0.0 --save

To activate Mermaid diagramming and charting tool you will need to include...

-   Mermaid JavaScript library - `node_modules/mermaid/dist/mermaid.min.js` file

If you are using Angular CLI you can follow the `angular.json` example below...

"scripts": \[
+ "node\_modules/mermaid/dist/mermaid.min.js",
\]

#### Mermaid plugin

Using `markdown` component and/or directive, you will be able to use the `mermaid` property to activate Mermaid plugin that renders Markdown-inspired text definitions to create and modify diagrams dynamically.

<markdown
  mermaid
  \[src\]\="path/to/file.md"\>
</markdown\>

#### Global configuration

You can provide a global configuration for mermaid configuration options to use across your application with the `mermaidOptions` in the `MarkdownModuleConfig` either with `provideMarkdown` provide-function for standalone components or `MarkdownModule.forRoot()` for module configuration.

##### Using the `provideMarkdown` function

provideMarkdown({
  mermaidOptions: {
    provide: MERMAID\_OPTIONS,
    useValue: {
      darkMode: true,
      look: 'handDrawn',
      ...
    },
  },
}),

##### Using the `MarkdownModule` import

MarkdownModule.forRoot({
  mermaidOptions: {
    provide: MERMAID\_OPTIONS,
    useValue: {
      darkMode: true,
      look: 'handDrawn',
      ...
    },
  },
}),

#### Component configuration

Additionally, you can specify mermaid configuration options on component directly using `mermaidOptions` property.

import { MermaidAPI } from 'ngx-markdown';

public options: MermaidAPI.MermaidConfig \= {
  darkMode: true,
  look: 'handDrawn',
  ...
};

<markdown
  mermaid
  \[mermaidOptions\]\="options"
  \[src\]\="'path/to/file.md'"\>
</markdown\>

> 📘 Follow official Mermaid documentation for more details on diagrams and charts syntax.

### Copy-to-clipboard

> 🔔 Copy-to-clipboard support is **optional**, skip this step if you are not planning to use it

To add Clipboard library to your `package.json` use the following command.

npm install clipboard@^2.0.11 --save

To activate Clipboard allowing copy-to-clipboard you will need to include...

-   Clipboard JavaScript library - `node_modules/clipboard/dist/clipboard.min.js` file

If you are using Angular CLI you can follow the `angular.json` example below...

"scripts": \[
+ "node\_modules/clipboard/dist/clipboard.min.js",
\]

#### Clipboard plugin

Using `markdown` component and/or directive, you will be able to use the `clipboard` property to activate Clipboard plugin that enable copy-to-clipboard for code block from a single click.

<markdown
  clipboard
  \[src\]\="path/to/file.md"\>
</markdown\>

#### Default button

The `clipboard` plugin provide an unstyled default button with a default behavior out of the box if no alternative is used.

#### Customize button toolbar

The clipboard button is placed inside a wrapper element that can be customize using the `.markdown-clipboard-toolbar` CSS selector in your global `styles.css/scss` file.

This allows to override the default positionning of the clipboard button and play with the visibility of the button using the `.hover` CSS selector that is applied on the toolbar when the mouse cursor enters and leaves the code block element.

#### Customize default button

To customize the default button styling, use the `.markdown-clipboard-button` CSS selector in your global `styles.css/scss` file. You can also customized the "copied" state happening after the button is clicked using the `.copied` CSS selector.

#### Using global configuration

You can provide a custom component to use globaly across your application with the `clipboardOptions` in the `MarkdownModuleConfig` either with `provideMarkdown` provide-function for standalone components or `MarkdownModule.forRoot()` for module configuration.

##### Using the `provideMarkdown` function

provideMarkdown({
  clipboardOptions: {
    provide: CLIPBOARD\_OPTIONS,
    useValue: {
      buttonComponent: ClipboardButtonComponent,
    },
  },
})

##### Using the `MarkdownModule` import

MarkdownModule.forRoot({
  clipboardOptions: {
    provide: CLIPBOARD\_OPTIONS,
    useValue: {
      buttonComponent: ClipboardButtonComponent,
    },
  },
}),

#### Using a component

You can also provide your custom component using the `clipboardButtonComponent` input property when using the `clipboard` directive.

import { Component } from '@angular/core';

@Component({
  selector: 'app-clipboard-button',
  template: \`<button (click)="onClick()">Copy</button>\`,
})
export class ClipboardButtonComponent {
  onClick() {
    alert('Copied to clipboard!');
  }
}

import { ClipboardButtonComponent } from './clipboard-button-component';

@Component({ ... })
export class ExampleComponent {
  readonly clipboardButton \= ClipboardButtonComponent;
}

<markdown 
  clipboard 
  \[clipboardButtonComponent\]\="clipboardButton"\>
</markdown\>

#### Using ng-template

Alternatively, the `clipboard` directive can be used in conjonction with `ng-template` to provide a custom button implementation via the `clipboardButtonTemplate` input property on the `markdown` component.

<ng-template #buttonTemplate\>
  <button (click)\="onCopyToClipboard()"\>...</button\>
</ng-template\>

<markdown 
  clipboard 
  \[clipboardButtonTemplate\]\="buttonTemplate"\>
</markdown\>

> 📘 Refer to the ngx-markdown clipboard plugin demo for live examples.

Configuration
-------------

The ngx-markdown library can be used either with the standalone components or with modules configuration. Please follow the configuration section that matches your application.

### Standalone components

Use the `provideMarkdown` provide-function in your application configuration `ApplicationConfig` to be able to provide the `MarkdownComponent` and `MarkdownPipe` to your standalone components and/or inject the `MarkdownService`.

import { NgModule } from '@angular/core';
+ import { provideMarkdown } from 'ngx-markdown';

export const appConfig: ApplicationConfig = {
  providers: \[
+   provideMarkdown(),
  \],
};

### Modules configuration

You must import `MarkdownModule` inside your main application module (usually named AppModule) with `forRoot` to be able to use the `markdown` component, directive, pipe and/or `MarkdownService`.

import { NgModule } from '@angular/core';
+ import { MarkdownModule } from 'ngx-markdown';
import { AppComponent } from './app.component';

@NgModule({
  imports: \[
+   MarkdownModule.forRoot(),
  \],
  declarations: \[AppComponent\],
  bootstrap: \[AppComponent\],
})
export class AppModule { }

Use `forChild` when importing `MarkdownModule` into other application modules to allow you to use the same parser configuration across your application.

import { NgModule } from '@angular/core';
+ import { MarkdownModule } from 'ngx-markdown';
import { HomeComponent } from './home.component';

@NgModule({
  imports: \[
+   MarkdownModule.forChild(),
  \],
  declarations: \[HomeComponent\],
})
export class HomeModule { }

### Remote file configuration

If you want to use the `[src]` attribute to directly load a remote file, in order to keep only one instance of `HttpClient` and avoid issues with interceptors, you also have to provide `HttpClient`:

##### Using the `provideMarkdown` function

providers: \[
+  provideHttpClient(),
+  provideMarkdown({ loader: HttpClient }),
\],

##### Using the `MarkdownModule` import

imports: \[
+  HttpClientModule,
+  MarkdownModule.forRoot({ loader: HttpClient }),
\],

#### Sanitization

**Sanitization is enabled by default** and uses Angular’s `DomSanitizer` with `SecurityContext.HTML` to prevent XSS vulnerabilities. It can be disabled by changing the `SecurityContext` level using the `sanitize` property when configuring the `MarkdownModule`.

##### Using the `provideMarkdown` function

import { SecurityContext } from '@angular/core';
import { SANITIZE } from 'ngx-markdown';

// enable default sanitization
provideMarkdown()

// disable sanitization
provideMarkdown({
  sanitize: {
    provide: SANITIZE,
    useValue: SecurityContext.NONE
  },
})

##### Using the `MarkdownModule` import

import { SecurityContext } from '@angular/core';
import { SANITIZE } from 'ngx-markdown';

// enable default sanitization
MarkdownModule.forRoot()

// disable sanitization
MarkdownModule.forRoot({
  sanitize: {
    provide: SANITIZE,
    useValue: SecurityContext.NONE
  },
})

Because Angular's sanitizer offers limited flexibility, you can use any external library for sanitization such as DOMPurify by providing a custom sanitizer function using the `SANITIZE` provider token.

import DOMPurify from 'dompurify';
import { SANITIZE } from 'ngx-markdown';

// sanitize function using an external library
function sanitizeHtml(html: string): string {
  DOMPurify.setConfig({ ... });
  return DOMPurify.sanitize(html);
}

// provide a sanitize function
provideMarkdown({
  sanitize: {
    provide: SANITIZE,
    useValue: sanitizeHtml,
  },
})

##### Using the `MarkdownModule` import

import DOMPurify from 'dompurify';
import { SANITIZE } from 'ngx-markdown';

// sanitize function using an external library
function sanitizeHtml(html: string): string {
  DOMPurify.setConfig({ ... });
  return DOMPurify.sanitize(html);
}

// provide a sanitize function
MarkdownModule.forRoot({
  sanitize: {
    provide: SANITIZE,
    useValue: sanitizeHtml,
  },
})

> 📘 Follow Angular DomSanitizer documentation for more information on sanitization and security contexts.

You can bypass sanitization using the markdown component, directive or pipe using the `disableSanitizer` option as follow:

<!-- disable sanitizer using markdown component -->
<markdown
  \[data\]\="markdown"
  \[disableSanitizer\]\="true"\>
</markdown\>

<!-- disable sanitizer using markdown directive -->
<div markdown
  \[data\]\="markdown"
  \[disableSanitizer\]\="true"\>
</div\>

<!-- disable sanitizer using markdown pipe -->
<div \[innerHTML\]\="markdown | markdown : { disableSanitizer: true } | async"\></div\>

#### MarkedOptions

Optionally, markdown parsing can be configured using MarkedOptions that can be provided with the `MARKED_OPTIONS` injection token via the `markedOptions` property of the `forRoot` method of `MarkdownModule`.

##### Using the `provideMarkdown` function

// imports
import { MARKED\_OPTIONS, provideMarkdown } from 'ngx-markdown';

// using default options
provideMarkdown(),

// using specific options with ValueProvider and passing HttpClient
provideMarkdown({
  markedOptions: {
    provide: MARKED\_OPTIONS,
    useValue: {
      gfm: true,
      breaks: false,
      pedantic: false,
    },
  },
}),

##### Using the `MarkdownModule` import

// imports
import { MarkdownModule, MARKED\_OPTIONS } from 'ngx-markdown';

// using default options
MarkdownModule.forRoot(),

// using specific options with ValueProvider and passing HttpClient
MarkdownModule.forRoot({
  loader: HttpClient, // optional, only if you use \[src\] attribute
  markedOptions: {
    provide: MARKED\_OPTIONS,
    useValue: {
      gfm: true,
      breaks: false,
      pedantic: false,
    },
  },
}),

#### MarkedOptions.renderer

`MarkedOptions` also exposes the `renderer` property which allows you to override token rendering for your whole application.

The example uses a factory function and override the default blockquote token rendering by adding a CSS class for custom styling when using Bootstrap CSS:

import { Parser } from 'marked';
import { MARKED\_OPTIONS, MarkedOptions, MarkedRenderer } from 'ngx-markdown';

// function that returns \`MarkedOptions\` with renderer override
export function markedOptionsFactory(): MarkedOptions {
  const renderer \= new MarkedRenderer();

  renderer.blockquote \= ({ tokens }) \=> {
    return '<blockquote class="blockquote"><p>' + Parser.parse(tokens) + '</p></blockquote>';
  };

  return {
    renderer: renderer,
    gfm: true,
    breaks: false,
    pedantic: false,
  };
}

##### Using the `provideMarkdown` function

// using specific option with FactoryProvider
provideMarkdown({
  markedOptions: {
    provide: MARKED\_OPTIONS,
    useFactory: markedOptionsFactory,
  },
}),

##### Using the `MarkdownModule` import

// using specific option with FactoryProvider
MarkdownModule.forRoot({
  markedOptions: {
    provide: MARKED\_OPTIONS,
    useFactory: markedOptionsFactory,
  },
}),

### Marked extensions

When configuring the `MarkdownModule`, you can provide marked extensions using the `MARKED_EXTENSION` injection token via the `markedExtensions` property, which accepts an array of providers and supports Angular dependency injection.

##### Using the `provideMarkdown` function

import { gfmHeadingId } from 'marked-gfm-heading-id';

providemarkdown({
  markedExtensions: \[
    {
      provide: MARKED\_EXTENSIONS,
      useFactory: gfmHeadingId,
      multi: true,
    },
    {
      provide: MARKED\_EXTENSIONS,
      useFactory: myExtensionFactory,
      deps: \[SomeService\],
      multi: true,
    },
  \],
}),

##### Using the `MarkdownModule` import

import { gfmHeadingId } from 'marked-gfm-heading-id';

MarkdownModule.forRoot({
  markedExtensions: \[
    {
      provide: MARKED\_EXTENSIONS,
      useFactory: gfmHeadingId,
      multi: true,
    },
    {
      provide: MARKED\_EXTENSIONS,
      useFactory: myExtensionFactory,
      deps: \[SomeService\],
      multi: true,
    },
  \],
}),

Usage
-----

`ngx-markdown` provides different approaches to help you parse markdown to your application depending on your needs.

> 💡 As of Angular 6, the template compiler strips whitespace by default. Use `ngPreserveWhitespaces` directive to preserve whitespaces such as newlines in order for the markdown-formatted content to render as intended.  
> https://angular.io/api/core/Component#preserveWhitespaces

### Component

You can use `markdown` component to either parse static markdown directly from your HTML markup, load the content from a remote URL using `src` property or bind a variable to your component using `data` property. You can get a hook on load complete using `load` output event property, on loading error using `error` output event property or when parsing is completed using `ready` output event property.

<!-- static markdown -->
<markdown ngPreserveWhitespaces\>
  # Markdown
</markdown\>

<!-- loaded from remote url -->
<markdown
  \[src\]\="'path/to/file.md'"
  (load)\="onLoad($event)"
  (error)\="onError($event)"\>
</markdown\>

<!-- variable binding -->
<markdown
  \[data\]\="markdown"
  (ready)\="onReady()"\>
</markdown\>

<!-- inline parser, omitting rendering top-level paragraph -->
<markdown
  \[data\]\="markdown"
  \[inline\]\="true"\>
</markdown\>

### Directive

The same way the component works, you can use `markdown` directive to accomplish the same thing.

<!-- static markdown -->
<div markdown ngPreserveWhitespaces\>
  # Markdown
</div\>

<!-- loaded from remote url -->
<div markdown
  \[src\]\="'path/to/file.md'"
  (load)\="onLoad($event)"
  (error)\="onError($event)"\>
</div\>

<!-- variable binding -->
<div markdown
  \[data\]\="markdown"
  (ready)\="onReady()"\>
</div\>

<!-- inline parser, omitting rendering top-level paragraph -->
<div markdown
  \[data\]\="markdown"
  \[inline\]\="true"\>
</div\>

### Pipe

Using `markdown` pipe to transform markdown to HTML allow you to chain pipe transformations and will update the DOM when value changes. It is important to note that, because the `marked` parsing method returns a `Promise`, it requires the use of the `async` pipe.

<!-- chain \`language\` pipe with \`markdown\` pipe to convert typescriptMarkdown variable content -->
<div \[innerHTML\]\="typescriptMarkdown | language : 'typescript' | markdown | async"\></div\>

The `markdown` pipe allow you to use all the same plugins as the component by providing the options parameters.

<!-- provide options parameters to activate plugins or for configuration -->
<div \[innerHTML\]\="typescriptMarkdown | language : 'typescript' | markdown : { emoji: true, inline: true } | async"\></div\>

This is the `MarkdownPipeOptions` parameters interface, those options are the same as the ones available for the `markdown` component:

export interface MarkdownPipeOptions {
  decodeHtml?: boolean;
  inline?: boolean;
  emoji?: boolean;
  katex?: boolean;
  katexOptions?: KatexOptions;
  mermaid?: boolean;
  mermaidOptions?: MermaidAPI.MermaidConfig;
  markedOptions?: MarkedOptions;
  disableSanitizer?: boolean;
}

### Service

You can use `MarkdownService` to have access to markdown parsing, rendering and syntax highlight methods.

import { Component, OnInit } from '@angular/core';
import { MarkdownService } from 'ngx-markdown';

@Component({ ... })
export class ExampleComponent implements OnInit {
  constructor(private markdownService: MarkdownService) { }

  ngOnInit() {
    // outputs: <p>I am using <strong>markdown</strong>.</p>
    console.log(this.markdownService.parse('I am using \_\_markdown\_\_.'));
  }
}

Renderer
--------

Tokens can be rendered in a custom manner by either...

-   providing the `renderer` property with the `MarkedOptions` when importing `MarkdownModule.forRoot()` into your main application module (see Configuration section)
-   using `MarkdownService` exposed `renderer`

Here is an example of overriding the default heading token rendering through `MarkdownService` by adding an embedded anchor tag like on GitHub:

import { Component, OnInit } from '@angular/core';
import { Parser } from 'marked';
import { MarkdownService } from 'ngx-markdown';

@Component({
  selector: 'app-example',
  template: '<markdown># Heading</markdown>',
})
export class ExampleComponent implements OnInit {
  constructor(private markdownService: MarkdownService) { }

  ngOnInit() {
    this.markdownService.renderer.heading \= ({ tokens, depth }) \=> {
      const text \= Parser.parseInline(tokens);
      const escapedText \= text.toLowerCase().replace(/\[^\\w\]+/g, '-');
      return '<h' + depth + '>' +
               '<a name="' + escapedText + '" class="anchor" href="#' + escapedText + '">' +
                 '<span class="header-link"></span>' +
               '</a>' + text +
             '</h' + depth + '>';
    };
  }
}

This code will output the following HTML:

<h1\>
  <a name\="heading" class\="anchor" href\="#heading"\>
    <span class\="header-link"\></span\>
  </a\>
  Heading
</h1\>

> 📘 Follow official marked.renderer documentation for the list of tokens that can be overriden.

Re-render Markdown
------------------

In some situations, you might need to re-render markdown after making changes. If you've updated the text this would be done automatically, however if the changes are internal to the library such as rendering options, you will need to inform the `MarkdownService` that it needs to update.

To do so, inject the `MarkdownService` and call the `reload()` function as shown below.

import { MarkdownService } from 'ngx-markdown';

constructor(
  private markdownService: MarkdownService,
) { }

update() {
  this.markdownService.reload();
}

> 📘 Refer to the ngx-markdown re-render demo for a live example.

Syntax highlight
----------------

When using static markdown you are responsible to provide the code block with related language.

<markdown ngPreserveWhitespaces>
+  \`\`\`typescript
    const myProp: string = 'value';
+  \`\`\`
</markdown>

When using remote URL ngx-markdown will use the file extension to automatically resolve the code language.

<!-- will use html highlights -->
<markdown \[src\]\="'path/to/file.html'"\></markdown\>

<!-- will use php highlights -->
<markdown \[src\]\="'path/to/file.php'"\></markdown\>

When using variable binding you can optionally use `language` pipe to specify the language of the variable content (default value is markdown when pipe is not used).

<markdown \[data\]\="markdown | language : 'typescript'"\></markdown\>

Demo application
----------------

A demo is available @ https://jfcere.github.io/ngx-markdown and its source code can be found inside the `demo` directory.

The following commands will clone the repository, install npm dependencies and serve the application @ http://localhost:4200

git clone https://github.com/jfcere/ngx-markdown.git
npm install
npm start

AoT compilation
---------------

Building with AoT is part of the CI and is tested every time a commit occurs so you don't have to worry at all.

Road map
--------

Here is the list of tasks that will be done on this library in the near future ...

-   Add a FAQ section to the README.md
-   Improve flexibily for some options

Contribution
------------

Contributions are always welcome, just make sure that ...

-   Your code style matches with the rest of the project
-   Unit tests pass
-   Linter passes

Support Development
-------------------

The use of this library is totally free and no donation is required.

As the owner and primary maintainer of this project, I am putting a lot of time and effort beside my job, my family and my private time to bring the best support I can by answering questions, addressing issues and improving the library to provide more and more features over time.

If this project has been useful, that it helped you or your business to save precious time, don't hesitate to give it a star and to consider a donation to support its maintenance and future development.

License
-------

Licensed under MIT.
