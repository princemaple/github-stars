---
project: svgtofont
stars: 698
description: Read a set of SVG icons and ouput a TTF/EOT/WOFF/WOFF2/SVG font.
url: https://github.com/jaywcjlove/svgtofont
---

Using my app is also a way to support me:  

* * *

Free Font

Read a set of SVG icons and ouput a TTF/EOT/WOFF/WOFF2/SVG font, Generator of fonts from SVG icons.

Install · Usage · Command · Font Usage · API · options · npm · License

**Features:**

-   Supported font formats: `WOFF2`, `WOFF`, `EOT`, `TTF` and `SVG`.
-   Support SVG Symbol file.
-   Support `React`, `ReactNative`, `Vue` & `TypeScript`.
-   Support `Less`/`Sass`/`Stylus`.
-   Allows to use custom templates (example `css`, `less` and etc).
-   Automatically generate a preview site.

                                ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
                                ┆      Project       ┆
                                ┆   ╭┈┈┈┈┈┈┈┈┈┈┈╮    ┆
╭┈┈┈┈┈┈┈┈╮                      ┆   ┆    svg    ┆┈┈╮ ┆
┆iconfont┆┈┈╮                   ┆   ╰┈┈┈┈┈┈┈┈┈┈┈╯  ┆ ┆
╰┈┈┈┈┈┈┈┈╯  ┆  ╭┈┈┈┈┈┈┈┈┈┈┈┈╮   ┆   ╭┈┈┈┈┈┈┈┈┈┈┈╮  ┆ ┆
            ├┈▶┆download svg┆┈┈▶┆   ┆┈svgtofont┈┆  ┆ ┆
╭┈┈┈┈┈┈┈┈╮  ┆  ╰┈┈┈┈┈┈┈┈┈┈┈┈╯   ┆╭┈┈┆create font┆◀┈╯ ┆
┆icomoon ┆┈┈╯                   ┆┆  ╰┈┈┈┈┈┈┈┈┈┈┈╯    ┆
╰┈┈┈┈┈┈┈┈╯                      ┆┆  ╭┈┈┈┈┈┈┈┈┈┈┈╮    ┆
                                ┆╰┈▶┆ use font  ┆    ┆
                                ┆   ╰┈┈┈┈┈┈┈┈┈┈┈╯    ┆
                                ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯

graph LR;
    A\[iconfont\]-->C\[Download SVG\];
    B\[icomoon\]-->C;
    D\[icongo\]-->C;
    E\[yesicon\]-->C;
    click A "https://www.iconfont.cn" "阿里巴巴矢量图标库" \_blank
    click B "https://icomoon.io" "Pixel Perfect Icon Solutions" \_blank
    click D "https://icongo.github.io" "Include popular icons in your React projects easily icons." \_blank
    click E "https://yesicon.app/" "216,162 High-Quality Vector Icons from Top Design Teams." \_blank
    C .-> ide1
    subgraph ide1 \[Project\]
        svg -->a2\[svgtofont create font\]
        a2 .-> b3\[use font\]
    end

Loading

**Icon Font Created By svgtofont**

-   file-icons File icons in the file tree.
-   uiw-iconfont The premium icon font for @uiwjs Component Library. Support `React` & `TypeScript`.
-   Bootstrap Icons Font Official open source SVG icon library for Bootstrap.
-   test example For a simple test example, run `npm run test` in the root directory to see the results.

Install
-------

npm i svgtofont

Note

This package `v5+` is ESM only: Node 18+ is needed to use it and it must be `import` instead of `require`.

import svgtofont from 'svgtofont';

#### Using With Command

{
  "scripts": {
    "font": "svgtofont --sources ./svg --output ./font --fontName uiw-font"
  },
  "svgtofont": {
    "css": {
      "fontSize": "12px"
    }
  }
}

You can add configuration to package.json. #48

Support for `.svgtofontrc` and more configuration files.

{
  "fontName": "svgtofont",
  "css": true
}

/\*\*
 \* @type {import('svgtofont').SvgToFontOptions}
 \*/
export default {
  fontName: "iconfont",
}

#### Using With Nodejs

Note

This package `v5+` is now pure ESM. Please read this.

import svgtofont from 'svgtofont';
import path from 'node:path';
 
svgtofont({
  src: path.resolve(process.cwd(), 'icon'), // svg path, only searches one level, not recursive
  dist: path.resolve(process.cwd(), 'fonts'), // output path
  fontName: 'svgtofont', // font name
  css: true, // Create CSS files.
}).then(() \=> {
  console.log('done!');
});

Or

import svgtofont from 'svgtofont';
import path from 'node:path';

svgtofont({
  src: path.resolve(process.cwd(), "icon"), // svg path, only searches one level, not recursive
  dist: path.resolve(process.cwd(), "fonts"), // output path
  styleTemplates: path.resolve(rootPath, "styles"), // file templates path (optional)
  fontName: "svgtofont", // font name
  css: true, // Create CSS files.
  startUnicode: 0xea01, // unicode start number
  svgicons2svgfont: {
    fontHeight: 1000,
    normalize: true
  },
  // website = null, no demo html files
  website: {
    title: "svgtofont",
    // Must be a .svg format image.
    logo: path.resolve(process.cwd(), "svg", "git.svg"),
    version: pkg.version,
    meta: {
      description: "Converts SVG fonts to TTF/EOT/WOFF/WOFF2/SVG format.",
      keywords: "svgtofont,TTF,EOT,WOFF,WOFF2,SVG"
    },
    description: \`\`,
    // Add a Github corner to your website
    // Like: https://github.com/uiwjs/react-github-corners
    corners: {
      url: 'https://github.com/jaywcjlove/svgtofont',
      width: 62, // default: 60
      height: 62, // default: 60
      bgColor: '#dc3545' // default: '#151513'
    },
    links: \[
      {
        title: "GitHub",
        url: "https://github.com/jaywcjlove/svgtofont"
      },
      {
        title: "Feedback",
        url: "https://github.com/jaywcjlove/svgtofont/issues"
      },
      {
        title: "Font Class",
        url: "index.html"
      },
      {
        title: "Unicode",
        url: "unicode.html"
      }
    \],
    footerInfo: \`Licensed under MIT. (Yes it's free and <a href="https://github.com/jaywcjlove/svgtofont">open-sourced</a>\`
  }
}).then(() \=> {
  console.log('done!');
});;

API
---

import { createSVG, createTTF, createEOT, createWOFF, createWOFF2, createSvgSymbol, copyTemplate, createHTML } from 'svgtofont/lib/utils';

const options \= { ... };

async function createFont() {
  const unicodeObject \= await createSVG(options); 
  const ttf \= await createTTF(options); // SVG Font => TTF
  await createEOT(options, ttf); // TTF => EOT
  await createWOFF(options, ttf); // TTF => WOFF
  await createWOFF2(options, ttf); // TTF => WOFF2
  await createSvgSymbol(options); // SVG Files => SVG Symbol
}

options
-------

> svgtofont(options)

### config

> Type: `config?: AutoConfOption<SvgToFontOptions>`

By default, settings are automatically loaded from `.svgtofontrc` and `package.json`. You can add configuration to `package.json`. #48

Support for `.svgtofontrc` and more configuration files.

### log

> Type: `Boolean`

A value of `false` disables logging

### logger

> Type: `(msg) => void`

log callback function

### dist

> Type: `String`  
> Default value: `dist` => `fonts`

The output directory.

### outSVGReact

> Type: `Boolean`  
> Default value: `false`

Output `./dist/react/`, SVG generates `react` components.

git/git.svg

// ↓↓↓↓↓↓↓↓↓↓

import React from 'react';
export const Git \= props \=> (
  <svg viewBox\="0 0 20 20" {...props}\><path d\="M2.6 10.59L8.38 4.8l1.69 -." fillRule\="evenodd" /></svg\>
);

### outSVGReactNative

> Type: `Boolean`  
> Default value: `false`

Output `./dist/reactNative/`, SVG generates `reactNative` components.

import { Text } from 'react-native';

const icons \= { "Git": "\_\_GitUnicodeChar\_\_", "Adobe": "\_\_AdobeUnicodeChar\_\_" };

export const RangeIconFont \= props \=> {
  const { name, ...rest } \= props;
  return (<Text style\={{ fontFamily: 'svgtofont', fontSize: 16, color: '#000000', ...rest }}\>
    {icons\[name\]}
  </Text\>);
};

### outSVGVue

> Type: `Boolean`  
> Default value: `false`

Output `./dist/vue/`, SVG generates `vue` components.

git/git.svg

// ↓↓↓↓↓↓↓↓↓↓

import { defineComponent, h } from 'vue';

export const Git \= defineComponent({
  name: 'Git',
  props: {
    class: {
      type: String,
      default: ''
    }
  },
  setup(props, { attrs }) {
    return () \=> h(
      'svg',
      {
        viewBox: '0 0 20 20',
        width: undefined,
        height: undefined,
        class: \`svgtofont ${props.class}\`,
        ...attrs
      },
      \[<path d\="m2.6 10.59l5.78-5.79 1.69 1.7c-0.24 0.85 0.15 1.78 0.93 2.23v5.54c-0.6 0.34-1 0.99-1 1.73a2 2 0 0 0 2 2 2 2 0 0 0 2 -2c0-0.74-0.4-1.39-1-1.73v-4.86l2.07 2.09c-0.07 0.15-0.07 0.32-0.07 0.5a2 2 0 0 0 2 2 2 2 0 0 0 2 -2 2 2 0 0 0 -2 -2c-0.18 0-0.35 0-0.5 0.07l-2.57-2.57c0.26-0.93-0.22-1.95-1.15-2.34-0.43-0.16-0.88-0.2-1.28-0.09l-1.7-1.69 0.79-0.78c0.78-0.79 2.04-0.79 2.82 0l7.99 7.99c0.79 0.78 0.79 2.04 0 2.82l-7.99 7.99c-0.78 0.79-2.04 0.79-2.82 0l-7.99-7.99c-0.79-0.78-0.79-2.04 0-2.82z" fillRule\="evenodd" />\]
    );
  }
});

### outSVGPath

> Type: `Boolean`  
> Default value: `false`

Output `./dist/svgtofont.json`, The content is as follows:

{
  "adobe": \["M14.868 3H23v19L14.868 3zM1 3h8.138L1 22V3zm.182 11.997H13.79l-1.551-3.82H8.447z...."\],
  "git": \["M2.6 10.59L8.38 4.8l1.69 1.7c-.24.85.15 1.78.93 2.23v5.54c-.6.34-1 .99-1..."\],
  "stylelint": \["M129.74 243.648c28-100.109 27.188-100.5.816c2.65..."\]
}

Or you can generate the file separately:

const { generateIconsSource } \= require('svgtofont/src/generate');	
const path \= require('path');	

async function generate () {	
  const outPath \= await generateIconsSource({	
    src: path.resolve(process.cwd(), 'svg'),	
    dist: path.resolve(process.cwd(), 'dist'),	
    fontName: 'svgtofont',	
  });	
}	

generate();

### generateInfoData

> Type: `Boolean`  
> Default value: `false`

Output `./dist/info.json`, The content is as follows:

{
  "adobe": {
    "encodedCode": "\\\\ea01",
    "prefix": "svgtofont",
    "className": "svgtofont-adobe",
    "unicode": "&#59905;"
  },
  ...
}

### src

> Type: `String`  
> Default value: `svg`

output path

### emptyDist

> Type: `String`  
> Default value: `false`

Clear output directory contents

### fontName

> Type: `String`  
> Default value: `iconfont`

The font family name you want.

### styleTemplates

> Type: `String` Default value: `undefined`

The path of the templates, see `src/styles` or `test/templates/styles` to get reference about how to create a template, file names can have the extension .template, like a `filename.scss.template`

### startUnicode

> Type: `Number`  
> Default value: `0xea01`

unicode start number

### getIconUnicode

Get Icon Unicode

getIconUnicode?: (name: string, unicode: string, startUnicode: number) 
      \=> \[string, number\];

### useNameAsUnicode

> Type: `Boolean`  
> Default value: `false`

should the name(file name) be used as unicode? this switch allows for the support of ligatures.

let's say you have an svg with a file name of `add` and you want to use ligatures for it. you would set up your processing as mentioned above and turn on this switch.

{
  ...
  useNameAsUnicode: true
}

while processing, instead of using a single sequential char for the unicode, it uses the file name. using the file name as the unicode allows the following code to work as expected.

.icons {
  font-family: 'your-font-icon-name' !important;
  font-size: 16px;
  font-style: normal;
  \-webkit-font-smoothing: antialiased;
  \-moz-osx-font-smoothing: grayscale;
}

<i class\="icons"\>add</i\>

as you add more svgs and process them into your font you would just use the same pattern.

<i class\="icons"\>add</i\>
<i class\="icons"\>remove</i\>
<i class\="icons"\>edit</i\>

### addLigatures

> Type: `Boolean`  
> Default value: `false`

adds possibility to use name (file name) in addition to codepoints. adds support of ligatures.

let's say you have some svgs and you want to use codepoints but for some of them for example with a file name of `add` you want to use ligatures for it. this option only adds ligatures and still allows for using codepoints as usual. this is in contrary to useNameAsUnicode which basically removes support for codepoints in favour of ligatures.

{
  ...
  addLigatures: true
}

### useCSSVars

> Type: `Boolean`  
> Default value: `false`

consoles whenever {{ cssString }} template outputs unicode characters or css vars

### classNamePrefix

> Type: `String`  
> Default value: font name

Create font class name prefix, default value font name.

### css

> Type: `Boolean|CSSOptions`  
> Default value: `false`

Create CSS/LESS files, default `true`.

type CSSOptions \= {
  /\*\*
   \* Output the css file to the specified directory
   \*/
  output?: string;
  /\*\*
   \* Which files are exported.
   \*/
  include?: RegExp;
  /\*\*
   \* Setting font size.
   \*/
  fontSize?: string | boolean;
  /\*\*
   \* Set the path in the css file
   \* https://github.com/jaywcjlove/svgtofont/issues/48#issuecomment-739547189
   \*/
  cssPath?: string;
  /\*\*
   \* Set file name
   \* https://github.com/jaywcjlove/svgtofont/issues/48#issuecomment-739547189
   \*/
  fileName?: string;
  /\*\*
   \* Ad hoc template variables.
   \*/
  templateVars?: Record<string, any\>;
  /\*\*
   \* When including CSS files in a CSS file,
   \* you can add a timestamp parameter or custom text to the file path to prevent browser caching issues and ensure style updates are applied. @default true
   \* @example \`path/to/iconfont.css?t=1612345678\`
   \*/
  hasTimestamp?: boolean | string;
}

### svgicons2svgfont

This is the setting for svgicons2svgfont

#### svgicons2svgfont.fontName

> Type: `String`  
> Default value: `'iconfont'`

The font family name you want.

#### svgicons2svgfont.fontId

> Type: `String`  
> Default value: the options.fontName value

The font id you want.

#### svgicons2svgfont.fontStyle

> Type: `String`  
> Default value: `''`

The font style you want.

#### svgicons2svgfont.fontWeight

> Type: `String`  
> Default value: `''`

The font weight you want.

#### svgicons2svgfont.fixedWidth

> Type: `Boolean`  
> Default value: `false`

Creates a monospace font of the width of the largest input icon.

#### svgicons2svgfont.centerHorizontally

> Type: `Boolean`  
> Default value: `false`

Calculate the bounds of a glyph and center it horizontally.

#### svgicons2svgfont.normalize

> Type: `Boolean`  
> Default value: `false`

Normalize icons by scaling them to the height of the highest icon.

#### svgicons2svgfont.fontHeight

> Type: `Number`  
> Default value: `MAX(icons.height)`

The outputted font height (defaults to the height of the highest input icon).

#### svgicons2svgfont.round

> Type: `Number`  
> Default value: `10e12`

Setup SVG path rounding.

#### svgicons2svgfont.descent

> Type: `Number`  
> Default value: `0`

The font descent. It is useful to fix the font baseline yourself.

**Warning:** The descent is a positive value!

#### svgicons2svgfont.ascent

> Type: `Number`  
> Default value: `fontHeight - descent`

The font ascent. Use this options only if you know what you're doing. A suitable value for this is computed for you.

#### svgicons2svgfont.metadata

> Type: `String`  
> Default value: `undefined`

The font metadata. You can set any character data in but it is the be suited place for a copyright mention.

#### svgicons2svgfont.log

> Type: `Function`  
> Default value: `console.log`

Allows you to provide your own logging function. Set to `function(){}` to disable logging.

### svgoOptions

> Type: `OptimizeOptions` Default value: `undefined`

Some options can be configured with `svgoOptions` though it. svgo

### svg2ttf

This is the setting for svg2ttf

#### svg2ttf.copyright

> Type: `String`

copyright string

#### svg2ttf.ts

> Type: `String`

Unix timestamp (in seconds) to override creation time

#### svg2ttf.version

> Type: `Number`

font version string, can be Version `x.y` or `x.y`.

### website

Define preview web content. Example:

{
  ...
  // website = null, no demo html files
  website: {
    title: "svgtofont",
    logo: path.resolve(process.cwd(), "svg", "git.svg"),
    version: pkg.version,
    meta: {
      description: "Converts SVG fonts to TTF/EOT/WOFF/WOFF2/SVG format.",
      keywords: "svgtofont,TTF,EOT,WOFF,WOFF2,SVG",
      favicon: "./favicon.png"
    },
    // Add a Github corner to your website
    // Like: https://github.com/uiwjs/react-github-corners
    corners: {
      url: 'https://github.com/jaywcjlove/svgtofont',
      width: 62, // default: 60
      height: 62, // default: 60
      bgColor: '#dc3545' // default: '#151513'
    },
    links: \[
      {
        title: "GitHub",
        url: "https://github.com/jaywcjlove/svgtofont"
      },
      {
        title: "Feedback",
        url: "https://github.com/jaywcjlove/svgtofont/issues"
      },
      {
        title: "Font Class",
        url: "index.html"
      },
      {
        title: "Unicode",
        url: "unicode.html"
      }
    \]
  }
}

#### website.template

> Type: `String`  
> Default value: index.njk

Custom template can customize parameters. You can define your own template based on the default template.

{
  website: {
    template: path.join(process.cwd(), "my-template.njk")
  }
}

#### website.index

> Type: `String`  
> Default value: `font-class`, Enum{`font-class`, `unicode`, `symbol`}

Set default home page.

Font Usage
----------

Suppose the font name is defined as `svgtofont`, The default home page is `unicode`, Will generate:

font-class.html
index.html
svgtofont.css
svgtofont.eot
svgtofont.json
svgtofont.less
svgtofont.module.less
svgtofont.scss
svgtofont.styl
svgtofont.svg
svgtofont.symbol.svg
svgtofont.ttf
svgtofont.woff
svgtofont.woff2
symbol.html

Preview demo `font-class.html`, `symbol.html` and `index.html`. Automatically generated style `svgtofont.css` and `svgtofont.less`.

### symbol svg

<svg class\="icon" aria-hidden\="true"\>
  <use xlink:href\="svgtofont.symbol.svg#svgtofont-git"\></use\>
</svg\>

### Unicode

<style\>
.iconfont {
  font-family: "svgtofont-iconfont" !important;
  font-size: 16px;
  font-style: normal;
  \-webkit-font-smoothing: antialiased;
  \-webkit-text-stroke-width: 0.2px;
  \-moz-osx-font-smoothing: grayscale;
}
</style\>
<span class\="iconfont"\>&#59907;</span\>

### Class Name

Support for `.less` and `.css` styles references.

<link rel\="stylesheet" type\="text/css" href\="node\_modules/fonts/svgtofont.css"\>
<i class\="svgtofont-apple"\></i\>

### Using With React

Icons are used as components. `v3.16.7+` support.

import { Adobe, Alipay } from '@uiw/icons';

<Adobe style\={{ fill: 'red' }} />
<Alipay height\="36" /\>

#### In the project created by create-react-app

import logo from './logo.svg';

<img src\={logo}  />

import { ReactComponent as ComLogo } from './logo.svg';

<ComLogo />

#### In the project created by webpack

yarn add babel-plugin-named-asset-import
yarn add @svgr/webpack

// webpack.config.js
\[
  require.resolve('babel-plugin-named-asset-import'),
  {
    loaderMap: {
      svg: {
        ReactComponent: '@svgr/webpack?-svgo,+ref!\[path\]',
      },
    },
  },
\],

import { ReactComponent as ComLogo } from './logo.svg';

<ComLogo />

### Using With ReactNative

A unique component named after the font name is generated.

Props are TextProps and are used as inline style.

In addition, the iconName prop is mandatory and refers to svg names written in camelCase

SvgToFont.jsx
// ↓↓↓↓↓↓↓↓↓↓

import { SvgToFont } from './SvgToFont';

<SvgToFont fontSize\={32} color\="#fefefe" iconName\={"git"}  />

SvgToFont.d.ts
// ↓↓↓↓↓↓↓↓↓↓

import { TextStyle } from 'react-native';

export type SvgToFontIconNames \= 'git'| 'adobe'| 'demo' | 'left' | 'styleInline'

export interface SvgToFontProps extends Omit<TextStyle, 'fontFamily' | 'fontStyle' | 'fontWeight'\> {
  iconName: SvgToFontIconNames
}

export declare const SvgToFont: (props: SvgToFontProps) \=> JSX.Element;

### Using with Vue

Icons are used as components. `v3+` support.

<script setup lang="ts">
  import { Adobe, Alipay } from '@uiw/icons';
</script\>

<template\>
  <Abobe :style\="{fill: red}" />
  <Alipay :height\="36" />
</template\>

Contributors
------------

As always, thanks to our amazing contributors!

Made with contributors.

License
-------

Licensed under the MIT License.
