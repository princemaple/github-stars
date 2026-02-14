---
project: js-code-to-svg-flowchart
stars: 7119
description: js2flowchart - a visualization library to convert any JavaScript code into beautiful SVG flowchart. Learn other’s code. Design your code. Refactor code. Document code. Explain code.
url: https://github.com/Bogdan-Lyashenko/js-code-to-svg-flowchart
---

> Why? While I've been working on Under-the-hood-ReactJS I spent enormous amount of time on creating schemes. Each change in code or flowchart affects all entire scheme instantly, forcing you to move and align 'broken pieces'. Just repeated manual work...

### For multiple files support (and other cool features to simplify codebase learning and documentation) checkout Codecrumbs project I am building right now.

Imagine a library which takes any JS code and generate SVG flowchart from it, works on client and server. Allows you easily adjust styles scheme for your context or demonstrate your code logic from different abstractions levels. Highlighting, destructing whole blocks, custom modifiers for your needs etc.

js2flowchart.js
===============

js2flowchart is a tool for generating beautiful SVG flowcharts™ from JavaScript code.

To get started install package from NPM

> yarn add js2flowchart

or try it right away at codepen sample, or play with the demo below.

Demo
----

Check out live **code editor**, paste your code and **download SVG file** of flowchart!

### What does js2flowchart do?

js2flowchart takes your JS code and returns SVG flowchart, works on client/server, support ES6.

Main features:

-   **defined abstractions levels** to render only import/exports, classes/function names, function dependencies to learn/explain the code step by step.
-   **custom abstractions levels support** create your own one
-   **presentation generator** to generate list of SVGs in order to different abstractions levels
-   **defined flow tree modifiers** to map well-known APIs like i.e. \[\].map, \[\].forEach, \[\].filter to Loop structure on scheme etc.
-   **destruction modifier** to replace block of code with one shape on scheme
-   **custom flow tree modifiers support** create your own one
-   **flow tree ignore filter** to omit some code nodes completely i.e. log lines
-   **focus node or entire code logic branch** to highlight important section on scheme
-   **blur node or entire code logic branch** to hide less-important stuff
-   **defined styles themes supports** choose one you like
-   **custom themes support** create your own one which fits your context colors better
-   **custom colors and styles support** provides handy API to change specific styles without boilerplate

Use cases:

-   **explain/document** your code by flowcharts
-   **learn** other's code by visual understanding
-   **create** flowcharts for any process simply described by valid JS syntax

### CLI

You can simply generate SVG files from your local JS files using CLI tool. Install js2flowchart globally by running:

> yarn global add js2flowchart

Or in a project by running:

> yarn add js2flowchart --dev

Open terminal and navigate to needed directory with JS file you want to visualize (e.g. './my-project/main.js'). Run the command (if you installed it globally)

```
js2flowchart main.js
```

Or add this to your _package.json_ file:

{
  "scripts": {
    "js2flowchart": "js2flowchart"
  }
}

And run (with either npm or yarn):

```
yarn run js2flowchart main.js
```

After script is executed observe log `SVG file was created: ./js2flowchart/main.js.svg`. SVG file will be placed in new directory '/js2flowchart' near your JS file.

### API and examples

You can find sources for examples explained below in docs directory.

**In examples only** js2flowchart library included explicitly, by `<script>` tag and accessed by global variable from `window` **to make it simpler to run for you without boilerplate**. But feel free to use it through ES6 modules as well, when you have Babel&Webpack local server configured.

/\*\*
\* Access APIs when js2flowchart injected into HTML page
\*/
const {convertCodeToFlowTree, convertFlowTreeToSvg} \= window.js2flowchart;

/\*\*
\* or import from node\_modules 
\*/ 
import {convertCodeToFlowTree, convertFlowTreeToSvg} from 'js2flowchart';//way 1
import \* as js2flowchart from 'js2flowchart';//way 2

#### Default

Here is a code function for classic case Binary search

const code \= \`function indexSearch(list, element) {
    let currentIndex,
        currentElement,
        minIndex = 0,
        maxIndex = list.length - 1;
    while (minIndex <= maxIndex) {
        currentIndex = Math.floor(minIndex + maxIndex) / 2;
        currentElement = list\[currentIndex\];
        if (currentElement === element) {
            return currentIndex;
        }
        if (currentElement < element) {
            minIndex = currentIndex + 1;
        }
        if (currentElement > element) {
            maxIndex = currentIndex - 1;
        }
    }
    return -1;
}\`;

let's convert it to SVG(the simplest way):

const svg \= js2flowchart.convertCodeToSvg(code);

Result:

If you need to modify default behavior you can split `js2flowchart.convertCodeToSvg` into two building block:

-   flow tree building
-   shapes printing

const {convertCodeToFlowTree, convertFlowTreeToSvg} \= js2flowchart;

const flowTree \= convertCodeToFlowTree(code);

const svg \= convertFlowTreeToSvg(flowTree);//XML string

or when you need full control create main instances manually:

const {createFlowTreeBuilder, createSVGRender} \= js2flowchart;

const flowTreeBuilder \= createFlowTreeBuilder(),
    svgRender \= createSVGRender();

const flowTree \= flowTreeBuilder.build(code),
    shapesTree \= svgRender.buildShapesTree(flowTree);

const svg \= shapesTree.print();//XML string

See the example running here or check out complete source code of it.

#### Defined abstraction level

What is called 'abstraction level'? Let's say you would like to omit some details, like, e.g. for given module you are interested only in what the module `exports`, or, what classes it contains. There is a list of defined levels you can do that with. Accessible by `ABSTRACTION_LEVELS` interface.

-   `FUNCTION`
-   `FUNCTION_DEPENDENCIES`
-   `CLASS`
-   `IMPORT`
-   `EXPORT`

Let's take example with module imports&exports. Below is the code of some `print-util.js`.

const code \= \`
    import {format, trim} from 'formattier';
    import {log} from 'logger';
    const data = \[\];
    export default print = (list) => {
        list.forEach(i => {
            console.log(i);
        });
    }
    export const formatString = (str) => formatter(str);
    export const MAX\_STR\_LENGTH = 15;
\`;

we need to instantiate `flowTreeBuilder` and assign abstraction level on it.

    const {
        ABSTRACTION\_LEVELS,  createFlowTreeBuilder, convertFlowTreeToSvg
    } \= js2flowchart;

    const flowTreeBuilder \= createFlowTreeBuilder();

    //you can pass one level or multiple levels
    flowTreeBuilder.setAbstractionLevel(\[
        ABSTRACTION\_LEVELS.IMPORT,
        ABSTRACTION\_LEVELS.EXPORT
    \]);

    const flowTree \= flowTreeBuilder.build(code);
    const svg \= convertFlowTreeToSvg(flowTree);

Result:

See the example running here or check out complete source code of it.

**Custom abstraction level (label:advanced)**

What if you want your 'own' level? To the same API endpoint `flowTreeBuilder.setAbstractionLevel` you can provide configuration object. For example, have a look at the code of function dependencies abstraction level. Check out the export of it

export const getFunctionDependenciesLevel \= () \=> ({
    defined: \[TOKEN\_TYPES.CALL\_EXPRESSION\],
    custom: \[
        getCustomFunctionDeclaration(),
        getCustomAssignmentExpression(),
        getCustomVariableDeclarator()
    \]
});

It's a format of data you need to pass:

flowTreeBuilder.setAbstractionLevel({
    defined: \[TOKEN\_TYPES.CALL\_EXPRESSION\],
    custom: \[
        getCustomFunctionDeclaration(),
        getCustomAssignmentExpression(),
        getCustomVariableDeclarator()
    \]
})

And what is behind of `getCustomAssignmentExpression` for example? There is a token parsing config.

{
    type: 'TokenType', /\*see types in TOKEN\_TYPES map\*/
    getName: (path) \=> {/\*extract name from token\*/},
    ignore: (path) \=> {/\*return true if want to omit entry\*/}
    body: true /\* should it contain nested blocks? \*/
}

Check out more token parsing configs from source code (entryDefinitionsMap.js)

#### Presentation generator

When you learn other's code it's good to go through it by different abstractions levels. Take a look what module exports, which function and classes contains etc. There is a sub-module `createPresentationGenerator` to generate list of SVGs in order to different abstractions levels.

Let's take the next code for example:

const code \= \`
    import {format} from './util/string';
    function formatName(name) {
        if (!name) return 'no-name';
        return format(name);
    }
    class Animal {
        constructor(breed) {
            this.breed = breed;
        }
        getBreed() {
            return this.breed;
        }
        setName(name) {
            if (this.nameExist()) {
                return;
            }
            this.name = name;
        }
    }
    class Man extends Animal {
       sayName() {
            console.log('name', this.name);
       }
    }
    export default Man;
\`;

pass it to

const { createPresentationGenerator } \= js2flowchart;

const presentationGenerator \= createPresentationGenerator(code);
const slides \= presentationGenerator.buildSlides();//array of SVGs

Result (one of slides):

You can switch slides by prev-next buttons.

See the example running here or check out complete source code of it.

#### Defined colors theme

You can apply different themes to your `svgRender` instance. Simply calling e.g. `svgRender.applyLightTheme()` to apply light scheme.

There are next predefined color schemes:

-   DEFAULT: `applyDefaultTheme`
-   BLACK\_AND\_WHITE: `applyBlackAndWhiteTheme`
-   BLURRED: `applyBlurredTheme`
-   LIGHT: `applyLightTheme`

Let's simple code sample of `switch` statement from Mozzila Web Docs.

const code \= \`
    function switchSampleFromMDN() {
        const foo = 0;
        switch (foo) {
          case -1:
            console.log('negative 1');
            break;
          case 0:
            console.log(0);
          case 1:
            console.log(1);
            return 1;
          default:
            console.log('default');
        }
    }
\`;

and apply scheme to render.

const {createSVGRender, convertCodeToFlowTree} \= js2flowchart;

const flowTree \= convertCodeToFlowTree(code),
    svgRender \= createSVGRender();

//applying another theme for render
svgRender.applyLightTheme();

const svg \= svgRender.buildShapesTree(flowTree).print();

Result:

See the example running here or check out complete source code of it.

#### Custom colors theme

Well, but what if you would like to have different colors? Sure, below is an example of Light theme colors but created manually.

svgRender.applyColorBasedTheme({
   strokeColor: '#555',
   defaultFillColor: '#fff',
   textColor: '#333',
   arrowFillColor: '#444',
   rectangleFillColor: '#bbdefb',
   rectangleDotFillColor: '#ede7f6',
   functionFillColor: '#c8e6c9',
   rootCircleFillColor: '#fff9c4',
   loopFillColor: '#d1c4e9',
   conditionFillColor: '#e1bee7',
   destructedNodeFillColor: '#ffecb3',
   classFillColor: '#b2dfdb',
   debuggerFillColor: '#ffcdd2',
   exportFillColor: '#b3e5fc',
   throwFillColor: '#ffccbc',
   tryFillColor: '#FFE082',
   objectFillColor: '#d1c4e9',
   callFillColor: '#dcedc8',
   debugModeFillColor: '#666'
});

#### Custom styles

What if you need different styles, not only colors? Here it's `svgRender.applyTheme({})`. You can apply styles above of current theme, overriding only that behaviour you need. Let's take an example with Return statement.

svgRender.applyTheme({
    common: {
        maxNameLength: 100
    },
    ReturnStatement: {
        fillColor: 'red',
        roundBorder: 10
    }
});

Please check definition of `DefaultBaseTheme` to see all possible shapes names and properties.

#### Shapes tree editor

There is sub-module for modifying shapes tree called 'ShapesTreeEditor'. It provides next interfaces:

-   `findShape`
-   `applyShapeStyles`
-   `blur`
-   `focus`
-   `blurShapeBranch`
-   `focusShapeBranch`
-   `print`

Let's learn its usage on an example as well. Below is the code with some 'devMode hooks'.

const code \= \`
const doStuff = (stuff) => {
    if (stuff) {
        if (devFlag) {
            log('perf start');
            doRecursion();
            log('perf end');
            return;
        }
        doRecursion();
        end();
    } else {
        throw new Error('No stuff!');
    }
    return null;
};
\`;

what we want here is 'blur' that dev-branch condition, because it interferes code readability.

const {
    convertCodeToFlowTree,
    createSVGRender,
    createShapesTreeEditor
} \= js2flowchart;

const flowTree \= convertCodeToFlowTree(code),
    svgRender \= createSVGRender();
    shapesTree \= svgRender.buildShapesTree(flowTree);

const shapesTreeEditor \= createShapesTreeEditor(shapesTree);

shapesTreeEditor.blurShapeBranch(
    (shape) \=> shape.getName() \=== '(devFlag)'
);

const svg \= shapesTreeEditor.print();

Result:

See the example running here or check out complete source code of it.

#### Flow tree modifier

There is sub-module for modifying flow tree called 'FlowTreeModifier' which allows you to apply modifiers defined separately to your existing flow tree. Let's take simple use-case: you want to change 'names'(titles) on tree-nodes, here it is, just define modifier for that. But, actually, there are some behaviours where we already know we need to modify flow tree.

Let's have a look at ES5 Array iterators, like `forEach`, `map` and so on. We all know they behave like a loop, right? Let's treat them as a 'loop' then.

const code \= \`
function print(list) {
    const newList = list.map(i => {
        return i + 1;
    });
    newList.forEach(i => {
        console.debug('iteration start');
        console.log(i);
        console.debug('iteration end');
    });
}
\`;

const {
    createFlowTreeBuilder,
    createFlowTreeModifier,
    convertFlowTreeToSvg,
    MODIFIER\_PRESETS
} \= js2flowchart;

const flowTreeBuilder \= createFlowTreeBuilder(),
    flowTree \= flowTreeBuilder.build(code);

const flowTreeModifier \= createFlowTreeModifier();

flowTreeModifier.setModifier(MODIFIER\_PRESETS.es5ArrayIterators);
flowTreeModifier.applyToFlowTree(flowTree);

const svg \= convertFlowTreeToSvg(flowTree);

Result:

As you can see, both iterators handled as a loop. And `forEach` omit function-callback as well.

See the example running here or check out complete source code of it.

There is one more defined modifier for node destruction. It takes a block you specified and destruct it to on block.

flowTreeModifier.destructNodeTree((node) \=> node.name.indexOf('.forEach') !== \-1, 'and print list...');

What if you want **custom modifier**?

flowTreeModifier.registerNewModifier((node)\=> node.name.includes('hello'), {
    name: 'world'
});

#### Debug rendering

What if you want to select a shape for applying special styles and want some unique id selector? Just pass `debug` flag to `print`;

    const {
        convertCodeToFlowTree,
        createSVGRender,
        createShapesTreeEditor
    } \= js2flowchart;

    const svgRender \= createSVGRender();

    const shapesTree \= svgRender.buildShapesTree(convertCodeToFlowTree(code));
    const shapesTreeEditor \= createShapesTreeEditor(shapesTree);

    shapesTreeEditor.applyShapeStyles(
        shape \=> shape.getNodePathId() \=== 'NODE-ID:|THIS.NAME=N|TCCP-', {
        fillColor: '#90caf9'
    });

    const svg \= shapesTreeEditor.print({debug: true});

Result:

See the example running here or check out complete source code of it.

### Tools

Thanks to @LucasBadico we got Visual Studio extension. Check it out.

### Under the hood

Main stages:

-   get AST from code, Babylon parser is used (develops by Babel team)
-   convert AST to FlowTree, remove and combing nodes (FlowTreeBuilder)
    -   apply modifiers (FlowTreeModifier)
-   create SVG objects based on FlowTree (SVGRender)
    -   apply ShapesTreeEditor
    -   apply theme (see themes)
-   print SVG objects to XML string

### Things planned TODO

-   Full CLI support
-   JSX support
-   Flow support
-   TypeScript support
-   Multi files support
-   Webstorm plugin
-   Chrome extension for dev-tools

### Contributing

Feel free to file an issue if it doesn't work for your code sample (please add 'breaking' lines of code if it's possible to identify) or for any other things you think can be improved. Highly appreciated if you can join and help with any TODOs above. Thanks.

### License

MIT license

### Version

First shoot! Take it easy (check version number above in NPM badge)
