---
project: flex-layout
stars: 5864
description: Provides HTML UI layout for Angular applications; using Flexbox and a Responsive API 
url: https://github.com/angular/flex-layout
---

Angular Flex-Layout
===================

**NOTE: The Angular team no longer publishes new releases of this project. Please review this blog post for alternatives, and this article for the explanation and next steps.**

Angular Flex Layout provides a sophisticated layout API using Flexbox CSS + mediaQuery. This module provides Angular developers with component layout features using a custom Layout API, mediaQuery observables, and injected DOM flexbox-2016 CSS stylings.

The Flex Layout engine intelligently automates the process of applying appropriate Flexbox CSS to browser view hierarchies. This automation also addresses many of the complexities and workarounds encountered with the traditional, manual, CSS-only application of box CSS.

The **real** power of Flex Layout, however, is its **responsive** engine. The Responsive API enables developers to easily specify different layouts, sizing, visibilities for different viewport sizes and display devices.

* * *

### Getting Started

Start by installing the Angular Layout library from `npm`

`npm i -s @angular/flex-layout @angular/cdk`

Next, you'll need to import the Layout module in your app's module.

**app.module.ts**

import { FlexLayoutModule } from '@angular/flex-layout';
...

@NgModule({
    ...
    imports: \[ FlexLayoutModule \],
    ...
});

After that is configured, you can use the Angular Layout attributes in your HTML tags for flex layout:

<div fxLayout\="row" fxLayoutAlign\="space-between"\>
</div\>

Check out all of the available options for using Angular Layout in your application.

* * *

### Quick Links

-   ChangeLog
-   Wiki Documentation

### Demos

-   Explore Examples Online
-   Demo Source Code

### StackBlitz Templates

-   Flex-Layout Template
-   Flex-Layout + Material

### Developers

-   API Documentation
-   Developer Setup
-   Builds + Fast Start
-   Integration with Angular CLI

* * *

### Browser Support

 

  

* * *

### License

The sources for this package are in the Flex Layout repository.  
Please file issues and pull requests against that repo.

License: MIT
