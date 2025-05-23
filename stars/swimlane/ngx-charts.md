---
project: ngx-charts
stars: 4325
description: :bar_chart: Declarative Charting Framework for Angular
url: https://github.com/swimlane/ngx-charts
---

ngx-charts
==========

Declarative Charting Framework for Angular!

ngx-charts is unique because we don't merely wrap d3, nor any other chart engine for that matter. It is using Angular to render and animate the SVG elements with all of its binding and speed goodness, and uses d3 for the excellent math functions, scales, axis and shape generators. By having Angular do all of the rendering it opens us up to endless possibilities the Angular platform provides such as AoT, SSR, etc.

Data visualization is a science but that doesn't mean it has to be ugly. One of the big efforts we've made while creating this project is to make the charts aesthetically pleasing. The styles are also completely customizable through CSS, so you can override them as you please.

Also, constructing custom charts is possible by leveraging the various ngx-charts components that are exposed through the ngx-charts module.

For more info, check out the documentation and the demos.

Features
--------

### Chart Types

-   Horizontal & Vertical Bar Charts (Standard, Grouped, Stacked, Normalized)
-   Line
-   Area (Standard, Stacked, Normalized)
-   Pie (Explodable, Grid, Custom legends)
-   Bubble
-   Donut
-   Gauge (Linear & Radial)
-   Heatmap
-   Treemap
-   Number Cards
-   Sankey Diagram

### Customization

-   Autoscaling
-   Timeline Filtering
-   Line Interpolation
-   Configurable Axis Labels
-   Legends (Labels & Gradient)
-   Advanced Label Positioning
-   Real-time data support
-   Advanced Tooltips
-   Data point Event Handlers
-   Works with ngUpgrade

Install
-------

To use ngx-charts in your project install it via npm:

```
npm i @swimlane/ngx-charts --save
```

Custom Charts
-------------

To learn how to use the ngx-charts components to build custom charts and find examples, please refer to our Custom Charts Page.

Release
-------

-   Checkout master (`git checkout master`)
-   Pull master (`git pull`)
-   Refresh node modules (`yarn install --frozen-lockfile`)
-   Run tests (`yarn test`)
-   Examine log to determine next version (X.Y.Z)
-   Run `git checkout -b release/X.Y.Z`
-   Update version in `projects/swimlane/ngx-charts/package.json`
-   Update changelog in `projects/docs/changelog.md`
-   Run `git commit -am "(release): X.Y.Z"`
-   Run `git tag X.Y.Z`
-   Run `git push origin HEAD --tags`
-   Run `yarn publish:lib`
-   Submit PR

Credits
-------

`ngx-charts` is a Swimlane open-source project; we believe in giving back to the open-source community by sharing some of the projects we build for our application. Swimlane is an automated cyber security operations and incident response platform that enables cyber security teams to leverage threat intelligence, speed up incident response and automate security operations.

SecOps Hub is an open, product-agnostic, online community for security professionals to share ideas, use cases, best practices, and incident response strategies.
