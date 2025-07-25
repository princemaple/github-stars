---
project: ngx-graph
stars: 972
description: Graph visualization library for angular
url: https://github.com/swimlane/ngx-graph
---

ngx-graph
=========

A Graph visualization for angular

Documentation & Demos
---------------------

https://swimlane.github.io/ngx-graph/

Installation
------------

1.  `npm install @swimlane/ngx-graph --save`
2.  Import `NgxGraphModule` into your module
3.  Use the `ngx-graph` component in your components

Usage
-----

### Simple

<ngx-graph
  class\="chart-container"
  \[view\]\="\[500, 200\]"
  \[links\]\="\[
    {
      id: 'a',
      source: 'first',
    target: 'second',
      label: 'is parent of'
    }, {
      id: 'b',
      source: 'first',
      target: 'third',
      label: 'custom label'
    }
  \]"
  \[nodes\]\="\[
    {
      id: 'first',
      label: 'A'
    }, {
      id: 'second',
      label: 'B'
    }, {
      id: 'third',
      label: 'C'
    }
  \]"
  (select)\="onNodeSelect($event)"
\>
</ngx-graph\>

### Custom Templates

<ngx-graph
  class\="chart-container"
  \[view\]\="\[500, 550\]"
  \[links\]\="\[
    {
      id: 'a',
      source: 'first',
      target: 'second',
      label: 'is parent of'
    }, {
      id: 'b',
      source: 'first',
      target: 'c1',
      label: 'custom label'
    }, {
      id: 'd',
      source: 'first',
      target: 'c2',
      label: 'custom label'
    }, {
      id: 'e',
      source: 'c1',
      target: 'd',
      label: 'first link'
    }, {
      id: 'f',
      source: 'c1',
      target: 'd',
      label: 'second link'
    }
  \]"
  \[nodes\]\="\[
    {
      id: 'first',
      label: 'A'
    }, {
      id: 'second',
      label: 'B'
    }, {
      id: 'c1',
      label: 'C1'
    }, {
      id: 'c2',
      label: 'C2'
    }, {
      id: 'd',
      label: 'D'
    }
  \]"
  \[clusters\]\="\[
    {
      id: 'third',
      label: 'Cluster node',
      childNodeIds: \['c1', 'c2'\]
    }
  \]"
  layout\="dagreCluster"
\>
  <ng-template #defsTemplate\>
    <svg:marker id\="arrow" viewBox\="0 -5 10 10" refX\="8" refY\="0" markerWidth\="4" markerHeight\="4" orient\="auto"\>
      <svg:path d\="M0,-5L10,0L0,5" class\="arrow-head" />
    </svg:marker\>
  </ng-template\>

  <ng-template #clusterTemplate let-cluster\>
    <svg:g class\="node cluster"\>
      <svg:rect
        rx\="5"
        ry\="5"
        \[attr.width\]\="cluster.dimension.width"
        \[attr.height\]\="cluster.dimension.height"
        \[attr.fill\]\="cluster.data.color"
      />
    </svg:g\>
  </ng-template\>

  <ng-template #nodeTemplate let-node\>
    <svg:g
      (click)\="onNodeClick($event)"
      (dblclick)\="onNodeClick($event)"
      class\="node"
      ngx-tooltip
      \[tooltipPlacement\]\="'top'"
      \[tooltipType\]\="'tooltip'"
      \[tooltipTitle\]\="node.label"
    \>
      <svg:rect
        \[attr.width\]\="node.dimension.width"
        \[attr.height\]\="node.dimension.height"
        \[attr.fill\]\="node.data.color"
      />
      <svg:text alignment-baseline\="central" \[attr.x\]\="10" \[attr.y\]\="node.dimension.height / 2"\>
        {{node.label}}
      </svg:text\>
    </svg:g\>
  </ng-template\>

  <ng-template #linkTemplate let-link\>
    <svg:g class\="edge"\>
      <svg:path class\="line" stroke-width\="2" marker-end\="url(#arrow)"\></svg:path\>
      <svg:text class\="edge-label" text-anchor\="middle"\>
        <textPath
          class\="text-path"
          \[attr.href\]\="'#' + link.id"
          \[style.dominant-baseline\]\="link.dominantBaseline"
          startOffset\="50%"
        \>
          {{link.label}}
        </textPath\>
      </svg:text\>
    </svg:g\>
  </ng-template\>
</ngx-graph\>

Data
----

### Nodes

\[
  {
    id: '1',
    label: 'Node A'
  },
  {
    id: '2',
    label: 'Node B'
  },
  {
    id: '3',
    label: 'Node C'
  },
  {
    id: '4',
    label: 'Node D'
  },
  {
    id: '5',
    label: 'Node E'
  },
  {
    id: '6',
    label: 'Node F'
  }
\];

### Edges

\[
  {
    id: 'a',
    source: '1',
    target: '2'
  },
  {
    id: 'b',
    source: '1',
    target: '3'
  },
  {
    id: 'c',
    source: '3',
    target: '4'
  },
  {
    id: 'd',
    source: '3',
    target: '5'
  },
  {
    id: 'e',
    source: '4',
    target: '5'
  },
  {
    id: 'f',
    source: '2',
    target: '6'
  }
\];

### Clusters

\[
  {
    id: 'cluster0',
    label: 'Cluster node',
    childNodeIds: \['2', '3'\]
  }
\];

Building ngx-graph
------------------

To get started with development, clone a fork of the repository and run `yarn`.

Development server
------------------

Run `yarn start` to serve Storybook at `http://localhost:6006/`. Storybook serves as the development and test environment for ngx-graph.

Building
--------

Run `yarn build:storybook` to build Storybook to check for production issues. The build artifacts will be stored in the `dist/` directory.

Run `yarn build:lib` to build ngx-graph.

Running tests
-------------

Run `yarn test` to execute the linter.

Release
-------

-   Checkout master (`git checkout master`)
-   Pull master (`git pull`)
-   Run tests (`yarn ci`)
-   Examine log to determine next version (X.Y.Z)
-   Run `git checkout -b release/X.Y.Z`
-   Update version in `projects/swimlane/ngx-graph/package.json`.
-   Update changelog in `CHANGELOG.md`
-   Run `yarn package` to check the package format
-   Run `git commit -am "(release): X.Y.Z"`
-   Run `git tag X.Y.Z`
-   Run `git push origin HEAD --tags`
-   Run `yarn publish:lib`
-   Submit PR

Credits
-------

`ngx-graph` is a Swimlane open-source project; we believe in giving back to the open-source community by sharing some of the projects we build for our application. Swimlane is an automated cyber security operations and incident response platform that enables cyber security teams to leverage threat intelligence, speed up incident response and automate security operations.

SecOps Hub is an open, product-agnostic, online community for security professionals to share ideas, use cases, best practices, and incident response strategies.
