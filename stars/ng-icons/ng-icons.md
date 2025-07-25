---
project: ng-icons
stars: 480
description: The ultimate icon library for Angular
url: https://github.com/ng-icons/ng-icons
---

Ng Icons
========

The all-in-one icon library for Angular. This allows you to use icons from multiple icon sets with a single icon component. Containing over 96,000 icons for you to use in your projects.

Currently, we support the following libraries:

-   Bootstrap Icons
-   Heroicons
-   Ionicons
-   Material Icons
-   Material File Icons
-   CSS.gg
-   Feather Icons
-   Jam Icons
-   Octicons
-   Radix UI Icons
-   Tabler Icons
-   Akar Icons
-   Iconoir
-   Cryptocurrency Icons
-   Simple Icons
-   Typicons
-   Dripicons
-   UX Aspects
-   Circum Icons
-   Remix Icon
-   Font Awesome
-   Iconsax
-   TDesign Icons
-   Phosphor Icons
-   Lets Icons
-   Huge Icons
-   Devicon
-   Game Icons
-   Flag Icons
-   Solar Icons
-   SVGL
-   Material Symbols
-   MynaUI
-   Boxicons
-   Mono Icons

Got suggestions for additional iconsets? Create an issue and we can consider adding them!

Supporting Ng Icons
-------------------

Ng Icons is an MIT-licensed open source project with its ongoing development made possible by contributors and sponsors.

Become a Sponsor!.

Supported Versions
------------------

Angular Version

Ng Icon Version

11.x.x

12.x.x

12.x.x

12.x.x - 13.x.x

13.x.x

13.x.x - 17.x.x

14.x.x

17.x.x - 22.x.x

15.x.x

23.x.x - 24.x.x

16.x.x

25.x.x

17.x.x

26.x.x - 27.x.x

18.x.x

28.x.x - 29.x.x

19.x.x

30.x.x - 31.x.x

20.x.x

32.x.x

> **Note**: Ng Icons relies on modern browser features and is designed to work on evergreen browsers. We do not support older browsers such as IE11.

Installation
------------

You must install the `@ng-icons/core` package, however you only need to install the iconset libraries you intend to use.

E.g:

npm i @ng-icons/core @ng-icons/heroicons ...

or

yarn add @ng-icons/core @ng-icons/heroicons ...

Packages
--------

The following packages are available:

Package

License

`@ng-icons/core`

MIT

`@ng-icons/bootstrap-icons`

MIT

`@ng-icons/heroicons`

MIT

`@ng-icons/ionicons`

MIT

`@ng-icons/material-icons`

Apache 2.0

`@ng-icons/material-file-icons`

MIT

`@ng-icons/css.gg`

MIT

`@ng-icons/feather-icons`

MIT

`@ng-icons/jam-icons`

MIT

`@ng-icons/octicons`

MIT

`@ng-icons/radix-icons`

MIT

`@ng-icons/tabler-icons`

MIT

`@ng-icons/akar-icons`

MIT

`@ng-icons/iconoir`

MIT

`@ng-icons/cryptocurrency-icons`

CC0-1.0

`@ng-icons/simple-icons`

CC0-1.0

`@ng-icons/typicons`

CC-BY-SA-4.0

`@ng-icons/dripicons`

CC-BY-SA-4.0

`@ng-icons/ux-aspects`

Apache 2.0

`@ng-icons/circum-icons`

MPL-2.0

`@ng-icons/remixicon`

Apache 2.0

`@ng-icons/font-awesome`

CC BY 4.0

`@ng-icons/iconsax`

Custom

`@ng-icons/tdesign-icons`

MIT

`@ng-icons/phosphor-icons`

MIT

`@ng-icons/lets-icons`

CC-BY-4.0

`@ng-icons/huge-icons`

CC0-1.0

`@ng-icons/devicon`

MIT

`@ng-icons/game-icons`

CC BY 3.0

`@ng-icons/solar-icons`

CC BY 4.0

`@ng-icons/svgl`

MIT

`@ng-icons/material-symbols`

Apache 2.0

`@ng-icons/mynaui`

MIT

`@ng-icons/boxicons`

MIT

`@ng-icons/mono-icons`

MIT

Usage
-----

Import the `NgIconsModule` and register the icons you wish to use:

import { NgIconsModule } from '@ng-icons/core';
import { featherAirplay } from '@ng-icons/feather-icons';
import { heroUsers } from '@ng-icons/heroicons/outline';

@NgModule({
  imports: \[BrowserModule, NgIconsModule.withIcons({ featherAirplay, heroUsers })\],
})
export class AppModule {}

You can register icons in multiple modules, this allows icons to be lazy loaded in child modules.

You can then use the icon in your templates:

<ng-icon name\="featherAirplay"\></ng-icon\>

Name

Type

Description

size

`string`

Define the size of the icon. This defaults to the current font size.

color

`string`

Define the color of the icon. This defaults to the current text color.

strokeWidth

`string` | `number`

Define the stroke-width of the icon. This only works on iconsets that use strokes.

### Standalone Components

As of version 18.0.0 Ng Icons nows supports standalone components. You can import icons using the `provideIcons` function which can be placed anywhere you can register providers. The optimal location would be in the `@Component` providers array.

You can also import the component directly by importing `NgIcon` or the `NG_ICON_DIRECTIVES` constant.

import { NgIcon, provideIcons } from '@ng-icons/core';
import { featherAirplay } from '@ng-icons/feather-icons';
import { heroUsers } from '@ng-icons/heroicons/outline';

@Component({
  standalone: true,
  imports: \[NgIcon\],
  providers: \[provideIcons({ featherAirplay, heroUsers })\],
})
export class AppComponent {}

#### Directly supplying an SVG

Should you need to supply an SVG directly set the `svg` input to the SVG string. This avoids the need to register the icon. Only icons from NG Icons iconsets will support the `color`, `size` and `strokeWidth` inputs.

import { featherAirplay } from '@ng-icons/feather-icons';

// parent.component.ts
@Component({
  standalone: true,
  template: '<app-child \[icon\]="icon" />',
})
export class ParentComponent {
  icon \= featherAirplay;
}

// child.component.ts
import { NgIcon } from '@ng-icons/core';

@Component({
  standalone: true,
  selector: 'app-child',
  imports: \[NgIcon\],
  template: '<ng-icon \[svg\]="icon" />',
})
export class ChildComponent {
  @Input({ required: true }) icon!;
}

### Global Configuration

You can configure the default size of icons by providing a `NgIconsConfig` object to the `provideNgIconsConfig`:

#### NgModule

import { NgIconsModule, provideNgIconsConfig } from '@ng-icons/core';
import { featherAirplay } from '@ng-icons/feather-icons';

@NgModule({
  imports: \[BrowserModule, NgIconsModule.withIcons({ featherAirplay, heroUsers })\],
  providers: \[
    provideNgIconsConfig({
      size: '1.5em',
      color: 'red',
    }),
  \],
})
export class AppModule {}

#### Standalone

import { NgIcon, provideIcons, provideNgIconsConfig } from '@ng-icons/core';

bootstrapApplication(AppComponent, {
  providers: \[
    provideNgIconsConfig({
      size: '1.5em',
    }),
  \],
});

### Content Security Policy

If your application has a strict Content Security Policy (CSP) you may need to add the following to your global configuration to ensure you do not get any errors.

import { NgIcon, provideIcons, provideNgIconsConfig, withContentSecurityPolicy } from '@ng-icons/core';

bootstrapApplication(AppComponent, {
  providers: \[provideNgIconsConfig({}, withContentSecurityPolicy())\],
});

### Logging

By default Ng Icons will log warnings or errors to the console - notably if you try to use an icon that has not been registered. Should you want stricter checks you can enable the `ExceptionLogger` which will throw an error if you try to use an icon that has not been registered.

You can enable this by providing the `withExceptionLogger` function to the `provideNgIconsConfig` function.

import { NgIcon, provideIcons, provideNgIconsConfig, withExceptionLogger } from '@ng-icons/core';

bootstrapApplication(AppComponent, {
  providers: \[provideNgIconsConfig({}, withExceptionLogger())\],
});

### Dynamically Loading Icons

The most common way to load icons is simply by registering them individually, however you may want to load icons lazily from a URL, or generate an SVG programatically on the fly. This can be achived using an icon loader. Icon loaders are a function that receives the name of the requested icon, and can return an `Observable<string>`, `Promise<string>` or a `string` containing the SVG to render. Within this function you can do whatever you need to retrieve an icon.

The function is also run within the injection context, this allows you to inject dependencies as you need such as the `HttpClient`.

bootstrapApplication(AppComponent, {
  providers: \[
    provideNgIconLoader(name \=> {
      const http \= inject(HttpClient);
      return http.get(\`/assets/icons/${name}.svg\`, { responseType: 'text' });
    }),
  \],
});

Additionally add caching to your loader to prevent multiple requests for the same icon.

bootstrapApplication(AppComponent, {
  providers: \[
    provideNgIconLoader(name \=> {...}, withCaching()),
  \],
});

Experimental Features
---------------------

### Icon Stack

Ng Icons now supports icon stacking. This allows you to layer multiple icons on top of each other. This is useful for creating complex icons from multiple simpler icons.

<ng-icon-stack size\="32px"\>
  <ng-icon name\="faCircle" />
  <ng-icon name\="faFlag" size\="16px" />
</ng-icon-stack\>

The `size` must be defined on the `ng-icon-stack` component. Any icons within the stack will inherit this size unless it is overridden.

### Variable Icon Fonts

We have added support for variable icon fonts. This is currently only supported by the Material Symbols iconset.

To enable this feature you must install the icon font and load the `material-symbols` stylesheet. Unlike the static SVG icons, Ng Icons does not bundle the icon font, you must load it yourself.

To use it you must register the variable fonts you want to use. The default iconset will be the first one registered.

import { provideNgGlyphs } from '@ng-icons/core';
import { withMaterialSymbolsOutlined, withMaterialSymbolsRounded } from '@ng-icons/material-symbols';

bootstrapApplication(AppComponent, {
  providers: \[provideNgGlyphs(withMaterialSymbolsOutlined(), withMaterialSymbolsRounded())\],
});

You can then use the following in your HTML:

<ng-glyph name\="settings" />

The following inputs are available on `ng-glyph`:

Name

Type

Description

name

`string`

Define the name of the icon.

glyphset

`string`

Define the glyphset to use. This defaults to the first registered glyphset.

size

`string` | `number`

Define the size of the icon as a pixel value or as a CSS value. This defaults to the current text size.

opticalSize

`number`

Define the optical size of the icon in `px`. This defaults to `20`

color

`string`

Define the color of the icon. This defaults to the current text color.

weight

`number`

Define the weight of the icon. This defaults to `400`.

grade

`number`

Define the grade of the icon. This defaults to `0`.

fill

`boolean`

Define if the icon should be filled. This defaults to `false`.

The default values for `size`, `weight`, `grade` and `fill` can be configured using the `provideNgGlyphsConfig` function.

import { provideNgGlyphsConfig } from '@ng-icons/core';

bootstrapApplication(AppComponent, {
  providers: \[
    provideNgGlyphsConfig({
      size: 24,
      weight: 400,
      grade: 0,
      fill: false,
    }),
  \],
});

This feature is experimental and does not follow the same versioning as the rest of the library. Breaking changes may be introduced at any time.

We appreciate any feedback you have on this feature.
