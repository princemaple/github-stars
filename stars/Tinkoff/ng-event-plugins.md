---
project: ng-event-plugins
stars: 229
description: This is an Angular library for optimizing performance sensitive events and declarative preventDefault, stopPropagation and capture phase listeners.
url: https://github.com/Tinkoff/ng-event-plugins
---

Angular Event Plugins
=====================

**@tinkoff/ng-event-plugins** is a tiny (1KB gzip) library for optimizing change detection cycles for performance sensitive events (such as _touchmove_, _scroll_, _drag_ etc.) and declarative _preventDefault()_ and _stopPropagation()_.

How to use
----------

1.  Add `EventPluginsModule` to your app module:
    
    import {NgModule} from '@angular/core';
    import {BrowserModule} from '@angular/platform-browser';
    import {EventPluginsModule} from '@tinkoff/ng-event-plugins'; // <-- THIS
    
    @NgModule({
      bootstrap: \[
        /\*...\*/
      \],
      imports: \[
        /\*...\*/
        BrowserModule,
        EventPluginsModule, // <-- GOES HERE
      \],
      declarations: \[
        /\*...\*/
      \],
    })
    export class AppModule {}
    

> `BrowserModule` or `BrowserAnimationsModule` must go first. You will see a warning if you mess the order.

1.  Use new modifiers for events in templates and in `@HostListener`:
    
    -   `.stop` to call stopPropagation() on event
    -   `.prevent` to call preventDefault() on event
    -   `.self` to skip bubbled events
    -   `.silent` to call event handler outside Angular's `NgZone`
    -   `.capture` to listen to events in capture phase
    -   `.passive` to add passive event listener
    -   `.once` to remove event listener after first callback
    
    For example:
    
    <div (mousedown.prevent)\="onMouseDown()"\>Clicking on this DIV will not move focus</div\>
    
    <div (click.stop)\="onClick()"\>Clicks on this DIV will not bubble up</div\>
    
    <div (mousemove.silent)\="onMouseMove()"\>Callbacks to mousemove will not trigger change detection</div\>
    
    <div (click.capture.stop)\="onClick()"\>
      <div (click)\="never()"\>Clicks will be stopped before reaching this DIV</div\>
    </div\>
    
2.  You can also re-enter `NgZone` and trigger change detection, using `@shouldCall` decorator that takes a predicate function as argument:
    

<div (scroll.silent)\="onScroll($event.currentTarget)"\>
  Scrolling this DIV will only trigger change detection and onScroll callback if it is scrolled to bottom
</div\>

import {shouldCall} from '@tinkoff/ng-event-plugins';

export function scrollFilter({
 scrollTop, scrollHeight, clientHeight
}: HTMLElement): boolean {
    return scrollTop \=== scrollHeight \- clientHeight;
}

// ...

@shouldCall(scrollFilter)
onScroll(\_element: HTMLElement): void {
    this.someService.requestMoreData();
}

> All examples above work the same when used with `@HostListener` and `CustomEvent`

### Important notes

-   Predicate is called with the same arguments as the decorated method and in the context of class instance (has access to `this`)
    
-   Decorated method will be called and change detection triggered if predicate returns `true`.
    
-   Predicates must be exported named function for AOT, arrow functions will trigger build error.
    
-   `.silent` modifier will not work with built-in keyboard pseudo-events, such as `keydown.enter` or `keydown.arrowDown` since Angular re-enters `NgZone` inside internal handlers.
    

Observable host bindings
------------------------

In this library there's also a plugin that enables observable host bindings. Sounds weird to do host binding with event plugin, but the code is actually pretty simple. You can read more about it in this article.

To use it you need to couple `@HostListener` and `@HostBinding` on the same `Observable` property with following syntax:

@HostBinding('$.disabled')
@HostListener('$.disabled')
readonly disabled$ \= asCallable(this.service.loading$)

This supports all the native Angular syntax, such as `class.class-name` or `style.width.px`.

**IMPORTANT NOTES:**

-   Until this issue is resolved you would have to use `NO_ERRORS_SCHEMA` in your module in order to bind to arbitrary properties
-   `asCallable` is a utility function from this library that simply adds `Function` to the type so Angular thinks it could be a host listener
-   To bind attributes you need to add `.attr` modifier in the end, not the beginning like in basic Angular binding. This is due to Angular using regexp to match for `attr.` string in `@HostBinding` decorator:

@HostBinding('$.aria-label.attr')
@HostListener('$.aria-label.attr')
readonly label$ \= asCallable(this.translations.get$('label'));

Demo
----

You can try this interactive demo

You can also read this detailed article explaining how this library works

Maintained
----------

**@tinkoff/ng-event-plugins** is a part of Taiga UI libraries family which is backed and used by a large enterprise. This means you can rely on timely support and continuous development.

License
-------

🆓 Feel free to use our library in your commercial and private applications

All **@tinkoff/ng-event-plugins** packages are covered by Apache 2.0

Read more about this license here

Open-source
-----------

Do you also want to open-source something, but hate the collateral work? Check out this Angular Open-source Library Starter we’ve created for our projects. It got you covered on continuous integration, pre-commit checks, linting, versioning + changelog, code coverage and all that jazz.
