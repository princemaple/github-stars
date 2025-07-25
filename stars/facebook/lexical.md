---
project: lexical
stars: 21612
description: Lexical is an extensible text editor framework that provides excellent reliability, accessibility and performance.
url: https://github.com/facebook/lexical
---

Lexical
=======

Lexical is an extensible JavaScript web text-editor framework with an emphasis on reliability, accessibility, and performance. Lexical aims to provide a best-in-class developer experience, so you can easily prototype and build features with confidence. Combined with a highly extensible architecture, Lexical allows developers to create unique text editing experiences that scale in size and functionality.

For documentation and more information about Lexical, be sure to visit the Lexical website.

Here are some examples of what you can do with Lexical:

-   Lexical Playground
-   Plain text sandbox
-   Rich text sandbox

* * *

**Overview:**

-   Getting started with React
    
-   Lexical is a framework
    
-   Working with Lexical
    
-   Contributing to Lexical
    

* * *

Getting started with React
--------------------------

> Note: Lexical is not only limited to React. Lexical can support any underlying DOM based library once bindings for that library have been created.

Install `lexical` and `@lexical/react`:

```
npm install --save lexical @lexical/react
```

Below is an example of a basic plain text editor using `lexical` and `@lexical/react` (try it yourself).

import {$getRoot, $getSelection} from 'lexical';
import {useEffect} from 'react';

import {LexicalComposer} from '@lexical/react/LexicalComposer';
import {PlainTextPlugin} from '@lexical/react/LexicalPlainTextPlugin';
import {ContentEditable} from '@lexical/react/LexicalContentEditable';
import {HistoryPlugin} from '@lexical/react/LexicalHistoryPlugin';
import {OnChangePlugin} from '@lexical/react/LexicalOnChangePlugin';
import {useLexicalComposerContext} from '@lexical/react/LexicalComposerContext';
import {LexicalErrorBoundary} from '@lexical/react/LexicalErrorBoundary';

const theme \= {
  // Theme styling goes here
  // ...
}

// When the editor changes, you can get notified via the
// LexicalOnChangePlugin!
function onChange(editorState) {
  editorState.read(() \=> {
    // Read the contents of the EditorState here.
    const root \= $getRoot();
    const selection \= $getSelection();

    console.log(root, selection);
  });
}

// Lexical React plugins are React components, which makes them
// highly composable. Furthermore, you can lazy load plugins if
// desired, so you don't pay the cost for plugins until you
// actually use them.
function MyCustomAutoFocusPlugin() {
  const \[editor\] \= useLexicalComposerContext();

  useEffect(() \=> {
    // Focus the editor when the effect fires!
    editor.focus();
  }, \[editor\]);

  return null;
}

// Catch any errors that occur during Lexical updates and log them
// or throw them as needed. If you don't throw them, Lexical will
// try to recover gracefully without losing user data.
function onError(error) {
  console.error(error);
}

function Editor() {
  const initialConfig \= {
    namespace: 'MyEditor',
    theme,
    onError,
  };

  return (
    <LexicalComposer initialConfig\={initialConfig}\>
      <PlainTextPlugin
        contentEditable\={
          <ContentEditable
            aria-placeholder\={'Enter some text...'}
            placeholder\={<div\>Enter some text...</div\>}
          />
        }
        ErrorBoundary\={LexicalErrorBoundary}
      />
      <OnChangePlugin onChange\={onChange} />
      <HistoryPlugin />
      <MyCustomAutoFocusPlugin />
    </LexicalComposer\>
  );
}

Lexical is a framework
----------------------

The core of Lexical is a dependency-free text editor framework that allows developers to build powerful, simple and complex, editor surfaces. Lexical has a few concepts that are worth exploring:

### Editor instances

Editor instances are the core thing that wires everything together. You can attach a contenteditable DOM element to editor instances, and also register listeners and commands. Most importantly, the editor allows for updates to its `EditorState`. You can create an editor instance using the `createEditor()` API, however you normally don't have to worry when using framework bindings such as `@lexical/react` as this is handled for you.

### Editor States

An Editor State is the underlying data model that represents what you want to show on the DOM. Editor States contain two parts:

-   a Lexical node tree
-   a Lexical selection object

Editor States are immutable once created, and in order to create one, you must do so via `editor.update(() => {...})`. However, you can also "hook" into an existing update using node transforms or command handlers – which are invoked as part of an existing update workflow to prevent cascading/waterfalling of updates. You can retrieve the current editor state using `editor.getEditorState()`.

Editor States are also fully serializable to JSON and can easily be serialized back into the editor using `editor.parseEditorState()`.

### Reading and Updating Editor State

When you want to read and/or update the Lexical node tree, you must do it via `editor.update(() => {...})`. You may also do read-only operations with the editor state via `editor.read(() => {...})` or `editor.getEditorState().read(() => {...})`. The closure passed to the update or read call is important, and must be synchronous. It's the only place where you have full "lexical" context of the active editor state, and providing you with access to the Editor State's node tree. We promote using the convention of using `$` prefixed functions (such as `$getRoot()`) to convey that these functions must be called in this context. Attempting to use them outside of a read or update will trigger a runtime error.

For those familiar with React Hooks, you can think of these $functions as having similar functionality:

_Feature_

React Hooks

Lexical $functions

Naming Convention

`useFunction`

`$function`

Context Required

Can only be called while rendering

Can only be called while in an update or read

Can be composed

Hooks can call other hooks

$functions can call other $functions

Must be synchronous

✅

✅

Other rules

❌ Must be called unconditionally in the same order

✅ None

Node Transforms and Command Listeners are called with an implicit `editor.update(() => {...})` context.

It is permitted to do nested updates, or nested reads, but an update should not be nested in a read or vice versa. For example, `editor.update(() => editor.update(() => {...}))` is allowed. It is permitted to nest an `editor.read` at the end of an `editor.update`, but this will immediately flush the update and any additional update in that callback will throw an error.

All Lexical Nodes are dependent on the associated Editor State. With few exceptions, you should only call methods and access properties of a Lexical Node while in a read or update call (just like `$` functions). Methods on Lexical Nodes will first attempt to locate the latest (and possibly a writable) version of the node from the active editor state using the node's unique key. All versions of a logical node have the same key. These keys are managed by the Editor, are only present at runtime (not serialized), and should be considered to be random and opaque (do not write tests that assume hard-coded values for keys).

This is done because the editor state's node tree is recursively frozen after reconciliation to support efficient time travel (undo/redo and similar use cases). Methods that update nodes first call `node.getWritable()`, which will create a writable clone of a frozen node. This would normally mean that any existing references (such as local variables) would refer to a stale version of the node, but having Lexical Nodes always refer to the editor state allows for a simpler and less error-prone data model.

:::tip

If you use `editor.read(() => { /* callback */ })` it will first flush any pending updates, so you will always see a consistent state. When you are in an `editor.update`, you will always be working with the pending state, where node transforms and DOM reconciliation may not have run yet. `editor.getEditorState().read()` will use the latest reconciled `EditorState` (after any node transforms, DOM reconciliation, etc. have already run), any pending `editor.update` mutations will not yet be visible.

:::

### DOM Reconciler

Lexical has its own DOM reconciler that takes a set of Editor States (always the "current" and the "pending") and applies a "diff" on them. It then uses this diff to update only the parts of the DOM that need changing. You can think of this as a kind-of virtual DOM, except Lexical is able to skip doing much of the diffing work, as it knows what was mutated in a given update. The DOM reconciler adopts performance optimizations that benefit the typical heuristics of a content editable – and is able to ensure consistency for LTR and RTL languages automatically.

### Listeners, Node Transforms and Commands

Outside of invoking updates, the bulk of work done with Lexical is via listeners, node transforms and commands. These all stem from the editor and are prefixed with `register`. Another important feature is that all the register methods return a function to easily unsubscribe them. For example here is how you listen to an update to a Lexical editor:

const unregisterListener \= editor.registerUpdateListener(({editorState}) \=> {
  // An update has occurred!
  console.log(editorState);
});

// Ensure we remove the listener later!
unregisterListener();

Commands are the communication system used to wire everything together in Lexical. Custom commands can be created using `createCommand()` and dispatched to an editor using `editor.dispatchCommand(command, payload)`. Lexical dispatches commands internally when key presses are triggered and when other important signals occur. Commands can also be handled using `editor.registerCommand(handler, priority)`, and incoming commands are propagated through all handlers by priority until a handler stops the propagation (in a similar way to event propagation in the browser).

Working with Lexical
--------------------

This section covers how to use Lexical, independently of any framework or library. For those intending to use Lexical in their React applications, it's advisable to check out the source-code for the hooks that are shipped in `@lexical/react`.

### Creating an editor and using it

When you work with Lexical, you normally work with a single editor instance. An editor instance can be thought of as the one responsible for wiring up an EditorState with the DOM. The editor is also the place where you can register custom nodes, add listeners, and transforms.

An editor instance can be created from the `lexical` package and accepts an optional configuration object that allows for theming and other options:

import {createEditor} from 'lexical';

const config \= {
  namespace: 'MyEditor',
  theme: {
    ...
  },
};

const editor \= createEditor(config);

Once you have an editor instance, when ready, you can associate the editor instance with a content editable `<div>` element in your document:

const contentEditableElement \= document.getElementById('editor');

editor.setRootElement(contentEditableElement);

If you want to clear the editor instance from the element, you can pass `null`. Alternatively, you can switch to another element if need be, just pass an alternative element reference to `setRootElement()`.

### Working with Editor States

With Lexical, the source of truth is not the DOM, but rather an underlying state model that Lexical maintains and associates with an editor instance. You can get the latest editor state from an editor by calling `editor.getEditorState()`.

Editor states are serializable to JSON, and the editor instance provides a useful method to deserialize stringified editor states.

const stringifiedEditorState \= JSON.stringify(editor.getEditorState().toJSON());

const newEditorState \= editor.parseEditorState(stringifiedEditorState);

### Updating an editor

There are a few ways to update an editor instance:

-   Trigger an update with `editor.update()`
-   Setting the editor state via `editor.setEditorState()`
-   Applying a change as part of an existing update via `editor.registerNodeTransform()`
-   Using a command listener with `editor.registerCommand(EXAMPLE_COMMAND, () => {...}, priority)`

The most common way to update the editor is to use `editor.update()`. Calling this function requires a function to be passed in that will provide access to mutate the underlying editor state. When starting a fresh update, the current editor state is cloned and used as the starting point. From a technical perspective, this means that Lexical leverages a technique called double-buffering during updates. There's an editor state to represent what is current on the screen, and another work-in-progress editor state that represents future changes.

Reconciling an update is typically an async process that allows Lexical to batch multiple synchronous updates of the editor state together in a single update to the DOM – improving performance. When Lexical is ready to commit the update to the DOM, the underlying mutations and changes in the update batch will form a new immutable editor state. Calling `editor.getEditorState()` will then return the latest editor state based on the changes from the update.

Here's an example of how you can update an editor instance:

import {$getRoot, $getSelection, $createParagraphNode} from 'lexical';

// Inside the \`editor.update\` you can use special $ prefixed helper functions.
// These functions cannot be used outside the closure, and will error if you try.
// (If you're familiar with React, you can imagine these to be a bit like using a hook
// outside of a React function component).
editor.update(() \=> {
  // Get the RootNode from the EditorState
  const root \= $getRoot();

  // Get the selection from the EditorState
  const selection \= $getSelection();

  // Create a new ParagraphNode
  const paragraphNode \= $createParagraphNode();

  // Create a new TextNode
  const textNode \= $createTextNode('Hello world');

  // Append the text node to the paragraph
  paragraphNode.append(textNode);

  // Finally, append the paragraph to the root
  root.append(paragraphNode);
});

If you want to know when the editor updates so you can react to the changes, you can add an update listener to the editor, as shown below:

editor.registerUpdateListener(({editorState}) \=> {
  // The latest EditorState can be found as \`editorState\`.
  // To read the contents of the EditorState, use the following API:

  editorState.read(() \=> {
    // Just like editor.update(), .read() expects a closure where you can use
    // the $ prefixed helper functions.
  });
});

Contributing to Lexical
-----------------------

Please read the CONTRIBUTING.md.

### Optional but recommended, use VSCode for development

1.  Download and install VSCode
    
    -   Download from here (it’s recommended to use the unmodified version)
2.  Install extensions
    
    -   Flow Language Support
        -   Make sure to follow the setup steps in the README
    -   Prettier
        -   Set prettier as the default formatter in `editor.defaultFormatter`
        -   Optional: set format on save `editor.formatOnSave`
    -   ESlint

Documentation
-------------

-   Getting started
-   Concepts
-   How Lexical was designed
-   Testing
-   Maintainers' Guide

Browser Support
---------------

-   Firefox 52+
-   Chrome 49+
-   Edge 79+ (when Edge switched to Chromium)
-   Safari 11+
-   iOS 11+ (Safari)
-   iPad OS 13+ (Safari)
-   Android Chrome 72+

Note: Lexical does not support Internet Explorer or legacy versions of Edge.

Contributing
------------

1.  Create a new branch
    -   `git checkout -b my-new-branch`
2.  Commit your changes
    -   `git commit -a -m 'Description of the changes'`
        -   There are many ways of doing this and this is just a suggestion
3.  Push your branch to GitHub
    -   `git push origin my-new-branch`
4.  Go to the repository page in GitHub and click on "Compare & pull request"
    -   The GitHub CLI allows you to skip the web interface for this step (and much more)

Support
-------

If you have any questions about Lexical, would like to discuss a bug report, or have questions about new integrations, feel free to join us at our Discord server.

Lexical engineers are checking this regularly.

Running tests
-------------

-   `npm run test-unit` runs only unit tests.
-   `npm run test-e2e-chromium` runs only chromium e2e tests.
-   `npm run debug-test-e2e-chromium` runs only chromium e2e tests in head mode for debugging.
-   `npm run test-e2e-firefox` runs only firefox e2e tests.
-   `npm run debug-test-e2e-firefox` runs only firefox e2e tests in head mode for debugging.
-   `npm run test-e2e-webkit` runs only webkit e2e tests.
-   `npm run debug-test-e2e-webkit` runs only webkit e2e tests in head mode for debugging.

### License

Lexical is MIT licensed.
