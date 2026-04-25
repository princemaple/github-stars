---
project: GraphicsJS
stars: 993
description: A lightweight JavaScript graphics library with the intuitive API, based on SVG/VML technology.
url: https://github.com/AnyChart/GraphicsJS
---

GraphicsJS
==========

GraphicsJS is a lightweight JavaScript graphics library with the intuitive API, based on SVG/VML technology.

-   Overview
-   Quick Start
-   Articles
-   Building
-   Contributing
-   Links

Overview
========

GraphicsJS is a JavaScript graphics library that allows you to draw absolutely anything, including any sort of interactive and animated graphics with any visual effects.

You can think of GraphicsJS as a paintbox with a brush, GraphicsJS may be used for data visualization, charting, game design or else. AnyChart charting libraries rendering is based fully on it.

You can find some specific samples at http://www.graphicsjs.org/, along with source code: galaxy, rain, bonfire, Bender, and a playable 15-puzzle. All of these were created with GraphicsJS only.

GraphicsJS allows to visualize complicated mathematical algorithms very conveniently and easily, e.g. the galaxy demo is based on Archimedean spiral.

GraphicsJS has one the most powerful line drawing features among SVG/VML based graphics libraries that provide only Bezier curves out of the box. But GraphicsJS is great at working with mathematical functions. As a result, GraphicsJS allows you to draw not only Bezier curves out of the box, but literally anything; for example, you can draw some arc very quickly, whereas other graphics libraries will make you arrange it through numerous different curves. And surely there are basic shapes available

GraphicsJS has the richest text features, for example, SVG/VML technologies do not provide this out of the box, as well as most of other JavaScript drawing libraries. GraphicsJS supports multiline texts and also offers text measurement, including width, height, as well as wrap, overflow, indent, spacing, align, etc.

GraphicsJS has implements the Virtual DOM which makes drawing more robust and manageable.

GraphicsJS uses smart layering system for elements and layers.

GraphicsJS supports z-index. Typically, if you ever decided to change the overlapping order, you would have to erase everything and draw the whole picture again, from scratch. With GraphicsJS, you are given the power to arrange this dynamically, which is extremely helpful when you are creating some big graphical thing and it is important for you to specify which elements must be seen at one moment or another.

GraphicsJS provides a convenient Transformations API that allows to move, scale, rotate and shear both elements and groups of elements. Transformations, in good hands, when used along with flexible Event Model and Virtual DOM, is a very powerfull tool.

GraphicsJS supports legacy browsers including IE6+.

GraphicsJS API is very convenient to use. GraphicsJS API is very concise and provides chaining support, which makes it possible to use a dozen lines of code where other libraries require a hundred.

GraphicsJS is built on a very reliable technology, Google Closure, just like Google Mail, Google Calendar, Google Drive, and so on.

Quick Start
===========

To get started with GraphicsJS create simple HTML document and copy paste the following code (or just grab the sample from playground):

<!DOCTYPE html\>
<html lang\="en"\>
<head\>
	<meta charset\="utf-8" />
	<script src\="https://cdn.anychart.com/releases/v8/js/graphics.min.js"\></script\>
</head\>
<body\>
	<div id\="stage-container" style\="width: 400px; height: 375px;"\></div\>
	<script\>
		// create a stage for the Deathly Hallows symbol
        stage \= acgraph.create('stage-container');
        // draw the square
        stage.rect(5, 5, 350, 300);
        // draw the circle
        stage.circle(177.5, 205, 100);
        // draw the triangle
        stage.path()
            .moveTo(5, 305)
            .lineTo(175, 5)
            .lineTo(355, 305);
        // draw the wand in the middle
        stage.path()
            .moveTo(175, 5)
            .lineTo(175, 305);
	</script\>
</body\>
</html\>

Launch the page in your browser and here you are: you have created your first drawing with GraphicsJS. See documentation and API to learn more.

Articles
========

-   Introducing GraphicsJS, a Powerful Lightweight Graphics Library by @RomanLubushkin
-   GraphicsJS Overview by AnyChart

Building
========

_Coming soon._

Contributing
============

To contribute to AnyChart project please:

-   Fork GraphicsJS repository.
-   Create a branch from the `develop` branch.
-   Make any changes you want to contribute.
-   Create a pull request against the `develop` branch.

GitHub documentation: Forking repositories. GitHub documentation: Collaborating using pull requests.

Links
=====

-   GraphicsJS Website
-   GraphicsJS Users's Guide
-   GraphicsJS API
-   GraphicsJS at GitHub
-   Report a bug or an issue
