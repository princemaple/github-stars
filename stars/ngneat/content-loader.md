---
project: content-loader
stars: 730
description: ⚪️ SVG component to create placeholder loading, like Facebook cards loading. 
url: https://github.com/ngneat/content-loader
---

Angular Content Loader
======================

Angular component that uses SVG to create a collection of loaders which simulates the structure of the content that will be loaded, similar to Facebook cards loaders.

Live Demo

Sponsoring ngneat
-----------------

Sponsorships aid in the continued development and maintenance of ngneat libraries. Consider asking your company to sponsor ngneat as its core to their business and application development.

### Gold Sponsors

Elevate your support by becoming a Gold Sponsor and have your logo prominently featured on our README in the top 5 repositories.

### Silver Sponsors

Boost your backing by becoming a Gold Sponsor and enjoy the spotlight with your logo prominently showcased in the top 3 repositories on our README.

### Bronze Sponsors

Become a bronze sponsor and get your logo on our README on GitHub.

Features
--------

This is an Angular port for react-content-loader.

-   ⚙️ **Completely customizable:** you can change the colors, speed and sizes;
-   ✏️ **Create your own loading:** use the create-react-content-loader to create your custom loadings easily;
-   👌 **You can use right now:** there are a lot of presets to use the loader, see the options;
-   🚀 **Performance:** uses pure SVG to work, so it works without any extra scripts, canvas, etc;

Install
-------

### Yarn

yarn add @ngneat/content-loader

Usage
-----

import { ContentLoaderModule } from '@ngneat/content-loader';

@NgModule({
  imports: \[ContentLoaderModule\]
})
export class AppModule {}

<content-loader\>
  <svg:rect x\="0" y\="0" rx\="3" ry\="3" width\="250" height\="10" />
  <svg:rect x\="20" y\="20" rx\="3" ry\="3" width\="220" height\="10" />
  <svg:rect x\="20" y\="40" rx\="3" ry\="3" width\="170" height\="10" />
  <svg:rect x\="0" y\="60" rx\="3" ry\="3" width\="250" height\="10" />
  <svg:rect x\="20" y\="80" rx\="3" ry\="3" width\="200" height\="10" />
  <svg:rect x\="20" y\="100" rx\="3" ry\="3" width\="80" height\="10" />
</content-loader\>

> Warning: Safari renders the SVG in black in case your Angular application uses the `<base href="/" />` tag in the `<head/>` of your `index.html`. Refer to the input property `baseUrl` below to fix this issue.

### Examples

#### Facebook Style

<facebook-content-loader\></facebook-content-loader\>

#### List Style

<list-content-loader\></list-content-loader\>

#### Bullet list Style

<bullet-list-content-loader\></bullet-list-content-loader\>

API
---

### @Inputs

Prop name and type

Environment

Description

**`animate?: boolean`**  
Defaults to `true`

\-

Opt-out of animations with `false`

**`baseUrl?: string`**  
Defaults to an empty string

\-

Required if you're using `<base url="/" />` document `<head/>`.   
This prop is common used as:   
`<ContentLoader baseUrl={window.location.pathname} />` which will fill the SVG attribute with the relative path. Related #93.

**`speed?: number`**  
Defaults to `1.2`

\-

Animation speed in seconds.

**`interval?: number`**  
Defaults to `0.25`

\-

Interval of time between runs of the animation,   
as a fraction of the animation speed.

**`viewBox?: string`**  
Defaults to `undefined`

\-

Use viewBox props to set a custom viewBox value,  
for more information about how to use it,  
read the article How to Scale SVG.

**`gradientRatio?: number`**  
Defaults to `1.2`

\-

Width of the animated gradient as a fraction of the view box width.

**`rtl?: boolean`**  
Defaults to `false`

\-

Content right-to-left.

**`backgroundColor?: string`**  
Defaults to `#f5f6f7`

\-

Used as background of animation.

**`foregroundColor?: string`**  
Defaults to `#eee`

\-

Used as the foreground of animation.

**`backgroundOpacity?: number`**  
Defaults to `1`

\-

Background opacity (0 = transparent, 1 = opaque)  
used to solve an issue in Safari

**`foregroundOpacity?: number`**  
Defaults to `1`

\-

Animation opacity (0 = transparent, 1 = opaque)  
used to solve an issue in Safari

**`style?: CSSProperties`**  
Defaults to `{}`

\-

Credits
-------

This is basically an Angular port for react-content-loader.

License
-------

MIT © NetanelBasal

Contributors ✨
--------------

Thanks goes to these wonderful people (emoji key):

  
**Netanel Basal**  
💻 🖋 📖

  
**Heo**  
💻

  
**Andreas Aeschlimann**  
📖

  
**alexw10**  
💻 📖

  
**Chinonso Chukwuogor**  
💻

  
**wynfred**  
💻

  
**Rustam**  
💻

  
**Alex Malkevich**  
📖

  
**Daniel Sogl**  
💻 🚧 📦

  
**Alex Szabó‮**  
💻

  
**Roy**  
📖

  
**Robin Van den Broeck**  
💻

This project follows the all-contributors specification. Contributions of any kind welcome!
