---
project: helipopper
stars: 447
description: 🚁 A Powerful Tooltip and Popover for Angular Applications
url: https://github.com/ngneat/helipopper
---

  

> A Powerful Tooltip and Popover for Angular Applications

Tippy.js is the complete tooltip, popover, dropdown, and menu solution for the web, powered by Popper.js.

It is an abstraction over Popper that provides the logic and optionally the styling involved in all types of elements that pop out from the flow of the document and get overlaid on top of the UI, positioned next to a reference element.

This is a lightweight wrapper with additional features that lets you use it declaratively in Angular. Tippy has virtually no restrictions over Popper and gives you limitless control while providing useful behavior and defaults.

If you're using v1 and don't want to migrate, you can find it here.

Features
--------

✅ Position Tooltips, Menus, Dropdowns, and Popovers  
✅ Predefined Variations  
✅ TemplateRef/Component Support  
✅ Lazy Registration  
✅ Manual Trigger Support  
✅ Text Overflow Support  
✅ Context Menu Support  

### Installation

$ npm i @ngneat/helipopper
# Or if you're using yarn
$ yarn add @ngneat/helipopper
# Or if you're using pnpm
$ pnpm i @ngneat/helipopper

Configure it as shown below:

import { provideTippyLoader, provideTippyConfig, tooltipVariation, popperVariation } from '@ngneat/helipopper/config';

bootstrapApplication(AppComponent, {
  providers: \[
    provideTippyLoader(() \=> import('tippy.js')),
    provideTippyConfig({
      defaultVariation: 'tooltip',
      variations: {
        tooltip: tooltipVariation,
        popper: popperVariation,
      },
    }),
  \],
});

Please note that the `provideTippyLoader` is required, as it specifies how Tippy is loaded - either synchronously or asynchronously. When dynamic import is used, the library will load only when the first Tippy directive is rendered. If we want it to load synchronously, we use the following:

import tippy from 'tippy.js';

provideTippyLoader(() \=> tippy);

Add the styles you want to `styles.scss`:

@import 'tippy.js/dist/tippy.css';
@import 'tippy.js/themes/light.css';
@import 'tippy.js/animations/scale.css';

You have the freedom to customize it if you need to.

Import the standalone `TippyDirective` in your components:

import { TippyDirective } from '@ngneat/helipopper';

@Component({
  standalone: true,
  imports: \[TippyDirective\],
})
class ExampleComponent {}

And use it in your templates:

<button tp\="Helpful Message"\>I have a tooltip</button\>

The library exposes default variations for `tooltip` and `popper`. You can use them, extend them, or pass your own variations. A `variation` is a set of predefined `tippy` properties. For example, here's how the built-in `tooltip` variation looks like:

export const tooltipVariation \= {
  theme: null,
  arrow: false,
  animation: 'scale',
  trigger: 'mouseenter',
  offset: \[0, 5\],
};

### Use `TemplateRef` as content

<button \[tp\]\="tpl" tpVariation\="popper"\>Click Me</button\>

<ng-template #tpl let-hide\>
  <h6\>Popover title</h6\>
  <p\>And here's some amazing content. It's very engaging. Right?</p\>
</ng-template\>

### Use `Component` as content

import type { TippyInstance } from '@ngneat/helipopper/config';
import { injectTippyRef } from '@ngneat/helipopper';

@Component()
class MyComponent {
  tippy \= injectTippyRef();
}

<button \[tp\]\="MyComponent"\>Click Me</button\>

### Text Overflow

You can pass the `onlyTextOverflow` input to show the tooltip only when the host overflows its container:

<div style\="max-width: 100px;" class\="overflow-hidden flex"\>
  <p class\="ellipsis" \[tp\]\="text" tpPlacement\="right" \[tpOnlyTextOverflow\]\="true"\>
    {{ text }}
  </p\>
</div\>

Note: this feature is using `ResizeObserver` api.

You might have cases where the host has a static width and the content is dynamic. In this case, use the `tpStaticWidthHost` input with combination with `tpOnlyTextOverflow`:

<div style\="max-width: 100px;" class\="overflow-hidden flex"\>
  <p
    style\="width: 100px"
    class\="ellipsis"
    \[tp\]\="dynamicText"
    tpPlacement\="right"
    \[tpOnlyTextOverflow\]\="true"
    tpStaticWidthHost
  \>
    {{ dynamicText }}
  </p\>
</div\>

Note: when using `tpStaticWidthHost` you can't use `tpUseTextContent`, you need to explicitly pass the content to `tp` in order to trigger content change.

### Use Text Content

You can instruct tippy to use the element textContent as the tooltip content:

<p tp tpUseTextContent\>{{ text }}</p\>

### Lazy

You can pass the `tpIsLazy` input when you want to defer the creation of tippy only when the element is in the view:

<div \*ngFor\="let item of items" \[tp\]\="item.label" \[tpIsLazy\]\="true"\>{{ item.label }}</div\>

Note that it's using `IntersectionObserver` api.

### Context Menu

First, define the `contextMenu` variation:

import {
  popperVariation,
  tooltipVariation,
  provideTippyConfig,
  withContextMenuVariation,
} from '@ngneat/helipopper/config';

bootstrapApplication(AppComponent, {
  providers: \[
    provideTippyConfig({
      defaultVariation: 'tooltip',
      variations: {
        tooltip: tooltipVariation,
        popper: popperVariation,
        contextMenu: withContextMenuVariation(popperVariation),
      },
    }),
  \],
});

Now you can use it in your template:

<ng-template #contextMenu let-hide let-item\="data"\>
  <ul\>
    <li (click)\="copy(item); hide()"\>Copy</li\>
    <li (click)\="duplicate(item); hide()"\>Duplicate</li\>
  </ul\>
</ng-template\>

<ul\>
  <li
    \*ngFor\="let item of list"
    \[tp\]\="contextMenu"
    \[tpData\]\="item"
    tpVariation\="contextMenu"
  \>
    {{ item.label }}
  </li\>
</ul\>

### Manual Trigger

<div tp\="Helpful Message" tpTrigger\="manual" #tooltip\="tippy"\>Click Open to see me</div\>

<button (click)\="tooltip.show()"\>Open</button\>
<button (click)\="tooltip.hide()"\>Close</button\>

### Declarative show/hide

Use isVisible to trigger show and hide. Set trigger to manual.

<div tp\="Helpful Message" tpTrigger\="manual" \[tpIsVisible\]\="visibility"\>
  Click Open to see me
</div\>

<button (click)\="visibility = true"\>Open</button\>
<button (click)\="visibility = false"\>Close</button\>

You can see more examples in our playground, or live here.

### Inputs

tp: string | TemplateRef<any\> | Type<any\> | undefined | null;
tpAppendTo: TippyProps\['appendTo'\];
tpDelay: TippyProps\['delay'\];
tpDuration: TippyProps\['duration'\];
tpHideOnClick: TippyProps\['hideOnClick'\];
tpInteractive: TippyProps\['interactive'\];
tpInteractiveBorder: TippyProps\['interactiveBorder'\];
tpMaxWidth: TippyProps\['maxWidth'\];
tpOffset: TippyProps\['offset'\];
tpPlacement: TippyProps\['placement'\];
tpPopperOptions: TippyProps\['popperOptions'\];
tpShowOnCreate: TippyProps\['showOnCreate'\];
tpTrigger: TippyProps\['trigger'\];
tpTriggerTarget: TippyProps\['triggerTarget'\];
tpZIndex: TippyProps\['zIndex'\];
tpAnimation: TippyProps\['animation'\];
tpUseTextContent: boolean;
tpIsLazy: boolean;
tpVariation: string;
tpIsEnabled: boolean;
tpIsVisible: boolean;
tpClassName: string;
tpOnlyTextOverflow: boolean;
tpData: any;
tpUseHostWidth: boolean;
tpHideOnEscape: boolean;
tpDetectChangesComponent: boolean;
tpPopperWidth: number | string;
tpHost: HTMLElement;
tpIsVisible: boolean;

### Outputs

tpVisible \= new EventEmitter<boolean\>();

### Global Config

-   You can pass any `tippy` option at global config level.
-   `beforeRender` - Hook that'll be called before rendering the tooltip content ( applies only for string )

### Create `tippy` Programmatically

import type { TippyInstance } from '@ngneat/helipopper/config';
import { TippyService } from '@ngneat/helipopper';

class Component {
  @ViewChild('inputName') inputName: ElementRef;
  tippy: TippyInstance;
  private tippyService \= inject(TippyService);

  async show() {
    if (!this.tippy) {
      this.tippy \= await firstValueFrom(
        this.tippyService.create(this.inputName, 'this field is required')
      );
    }

    this.tippy.show();
  }

  ngOnDestroy() {
    this.tippy?.destroy();
  }
}

Contributors ✨
--------------

Thank goes to all these wonderful people who contributed ❤️
