---
project: angular-grid-layout
stars: 517
description: Responsive grid with draggable and resizable items for Angular applications.
url: https://github.com/katoid/angular-grid-layout
---

Angular Grid Layout
===================

Angular Grid Layout is a grid layout system with draggable and resizable items for Angular Applications. It is mainly designed to create highly customizable dashboards.

Its core functionalities are based in the well known React-Grid-Layout library. It can be considered a 'port' (with some changes) to the Angular ecosystem. Both cover the same necessities.

Features
--------

-   No dependencies
-   Draggable items
-   Resizable items
-   REDUX friendly (akita, ngrx, ngxs...)
-   Customizable Drag & Resize handles. Custom Handles Example
-   3 modes of grid compaction: vertical, horizontal and free (exact same algorithm as React-Grid-Layout)
-   Add/Remove items
-   High performance
-   Supports touch devices
-   Auto-scrolling while dragging. Scroll Example
-   Multi Item mode, drag and resize more than 1 item at a time. Multi Item Drag & Resize Example

Compatibility
-------------

Version

Compatibility

\>= 3.0.0

Angular 16, 17, 18 & 19

\>= 2.0.0

Angular 14, 15

\>= 1.1.0 && < 2.0.0

Angular 12, 13 & 14

\>= 0.1.1 && < 1.1.0

Angular 9, 10 & 11

Demos
-----

Playground - Stackblitz

Custom Handles

Real Life Example

Scroll Test

Row Height Fit

Multi Item Drag & Resize

Installation
------------

To use @katoid/angular-grid-layout in your project install it via npm:

```
npm install @katoid/angular-grid-layout --save
```

Usage
-----

Import KtdGridModule to the module where you want to use the grid:

import { KtdGridModule } from '@katoid/angular-grid-layout';

@NgModule({
  imports: \[KtdGridModule\]
})

Use it in your template:

<ktd-grid \[cols\]\="cols"
          \[rowHeight\]\="rowHeight"
          \[layout\]\="layout"
          (layoutUpdated)\="onLayoutUpdated($event)"\>
    <ktd-grid-item \*ngFor\="let item of layout; trackBy:trackById" \[id\]\="item.id"\>
        <!-- Your grid item content goes here -->

        <!-- Optional Custom placeholder template -->
        <ng-template ktdGridItemPlaceholder\>
            <!-- Custom placeholder content goes here -->
        </ng-template\>
    </ktd-grid-item\>
</ktd-grid\>

Where template variables could be:

import { ktdTrackById } from '@katoid/angular-grid-layout';

cols: number \= 6;
rowHeight: number \= 100;
layout: KtdGridLayout \= \[
    {id: '0', x: 0, y: 0, w: 3, h: 3},
    {id: '1', x: 3, y: 0, w: 3, h: 3},
    {id: '2', x: 0, y: 3, w: 3, h: 3, minW: 2, minH: 3},
    {id: '3', x: 3, y: 3, w: 3, h: 3, minW: 2, maxW: 3, minH: 2, maxH: 5},
\];
trackById \= ktdTrackById

API
---

Here is listed the basic API of both KtdGridComponent and KtdGridItemComponent. See source code for full knowledge of the API.

#### KtdGridComponent

/\*\* Type of compaction that will be applied to the layout (vertical, horizontal or free). Defaults to 'vertical' \*/
@Input() compactType: KtdGridCompactType \= 'vertical';

/\*\*
 \* Row height as number or as 'fit'.
 \* If rowHeight is a number value, it means that each row would have those css pixels in height.
 \* if rowHeight is 'fit', it means that rows will fit in the height available. If 'fit' value is set, a 'height' should be also provided.
 \*/
@Input() rowHeight: number | 'fit' \= 100;

/\*\* Number of columns  \*/
@Input() cols: number \= 6;

/\*\* Layout of the grid. Array of all the grid items with its 'id' and position on the grid. \*/
@Input() layout: KtdGridLayout;

/\*\* Grid gap in css pixels \*/
@Input() gap: number \= 0;

/\*\*
 \* If height is a number, fixes the height of the grid to it, recommended when rowHeight = 'fit' is used.
 \* If height is null, height will be automatically set according to its inner grid items.
 \* Defaults to null.
 \* \*/
@Input() height: number | null \= null;

/\*\*
 \* Multiple items drag/resize
 \* A list of selected items to move (drag or resize) together as a group.
 \* The multi-selection of items is managed externally. By default, the library manages a single item, but if a set of item IDs is provided, the specified group will be handled as a unit."
 \*/
@Input()
selectedItemsIds(): string\[\] | null;

/\*\*
 \* Parent element that contains the scroll. If an string is provided it would search that element by id on the dom.
 \* If no data provided or null autoscroll is not performed.
 \*/
@Input() scrollableParent: HTMLElement | Document | string | null \= null;

/\*\* Number of CSS pixels that would be scrolled on each 'tick' when auto scroll is performed. \*/
@Input() scrollSpeed: number \= 2;

/\*\* Whether or not to update the internal layout when some dependent property change. \*/
@Input() compactOnPropsChange \= true;

/\*\* If true, grid items won't change position when being dragged over. Handy when using no compaction \*/
@Input() preventCollision \= false;

/\*\* Emits when layout change \*/
@Output() layoutUpdated: EventEmitter<KtdGridLayout\> \= new EventEmitter<KtdGridLayout\>();

/\*\* Emits when drag starts \*/
@Output() dragStarted: EventEmitter<KtdDragStart\> \= new EventEmitter<KtdDragStart\>();

/\*\* Emits when resize starts \*/
@Output() resizeStarted: EventEmitter<KtdResizeStart\> \= new EventEmitter<KtdResizeStart\>();

/\*\* Emits when drag ends \*/
@Output() dragEnded: EventEmitter<KtdDragEnd\> \= new EventEmitter<KtdDragEnd\>();

/\*\* Emits when resize ends \*/
@Output() resizeEnded: EventEmitter<KtdResizeEnd\> \= new EventEmitter<KtdResizeEnd\>();

/\*\* Emits when a grid item is being resized and its bounds have changed \*/
@Output() gridItemResize: EventEmitter<KtdGridItemResizeEvent\> \= new EventEmitter<KtdGridItemResizeEvent\>();

#### KtdGridItem

/\*\* Id of the grid item. This property is strictly compulsory. \*/
@Input() id: string;

/\*\* Min and max sizes of the grid item. Any of these would 'override' the min/max values specified in the layout. \*\*/
@Input() minW?: number;
@Input() minH?: number;
@Input() maxW?: number;
@Input() maxH?: number;

/\*\* Whether the item is draggable or not. Defaults to true. Does not affect manual dragging using the startDragManually method. \*/
@Input() draggable: boolean \= true;

/\*\* Whether the item is resizable or not. Defaults to true. \*/
@Input() resizable: boolean \= true;

/\*\* CSS transition style. Note that for more performance is preferable only make transition on transform property. \*/
@Input() transition: string \= 'transform 500ms ease, width 500ms ease, height 500ms ease';

/\*\* Minimum amount of pixels that the user should move before it starts the drag sequence. \*/
@Input() dragStartThreshold: number \= 0;

/\*\*
 \* To manually start dragging, route the desired pointer events to this method.
 \* Dragging initiated by this method will work regardless of the value of the draggable Input.
 \* It is the caller's responsibility to call this method with only the events that are desired to cause a drag.
 \* For example, if you only want left clicks to cause a drag, it is your responsibility to filter out other mouse button events.
 \* @param startEvent The pointer event that should initiate the drag.
 \*/
startDragManually(startEvent: MouseEvent | TouchEvent);

TODO features
-------------

-   Add delete feature to Playground page.
-   Add example with custom drag handles.
-   Add Real life example with charts and grid items with some kind of controls.
-   Add dragStartThreshold option to grid items.
-   Auto Scroll vertical/horizontal if container is scrollable when dragging a grid item. (commit).
-   Grid support for minWidth/maxWidth and minHeight/maxHeight on grid items.
-   Add grid gap feature. (commit)
-   Customizable drag placeholder. (commit).
-   rowHeight to support also 'fit' as value instead of only CSS pixels (commit).
-   Check grid compact horizontal algorithm, estrange behaviour when overflowing, also in react-grid-layout.
-   Grid support for static grid items.
-   Add all other resize options (now is only available 'se-resize').
-   Documentation.

**IMPORTANT**: These features would be done in the near future. If any lib user needs them earlier, we encourage you to contribute to this project and speed up the process! To do so, please:

1.  Open an issue mentioning one of these features.
2.  Explain your thoughts on how to implement it & we will discuss the possible solutions.
3.  Do a Merge Request when the feature is done and tested.

Troubleshooting
---------------

-   Mutating the layout would cause an error like: 'ERROR TypeError: Cannot read property 'id' of undefined'. Never mutate the layout, always return a new instance when modifying it.
-   Always use trackBy for the ngFor that renders the ktd-grid-items. If not, Angular would always re-render all items when layout changes.
-   My Grid Item 'content' doesn't resize well when size changes. This may be caused for 'transform' property in ktd-grid-item, try to remove transform animations on 'width' and 'height' properties. You can also watch the real-life-example which uses other technique valid also.
