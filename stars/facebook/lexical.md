---
project: lexical
stars: 22989
description: Lexical is an extensible text editor framework that provides excellent reliability, accessibility and performance.
url: https://github.com/facebook/lexical
---

An extensible text editor framework that provides excellent reliability, accessibility and performance.

Documentation | Getting Started | Playground | Gallery

  

Features
--------

-   **Framework Agnostic Core** - Works with any UI framework, with official React bindings
-   **Reliable & Accessible** - Built-in accessibility support and WCAG compliance
-   **Extensible** - Plugin-based architecture with powerful extension points
-   **Immutable State Model** - Time-travel ready with built-in undo/redo
-   **Collaborative Editing** - Real-time collaboration via Yjs integration
-   **Serialization** - Import/export from JSON, Markdown, and HTML
-   **Rich Content** - Support for tables, lists, code blocks, images, and custom nodes
-   **Cross-browser** - Firefox 115+, Safari 15+, Chrome 86+ (see Supported Browsers)
-   **Type Safe** - Written in TypeScript with comprehensive type definitions

Quick Start
-----------

npm install lexical @lexical/react

import { $getRoot, $getSelection } from 'lexical';
import { LexicalComposer } from '@lexical/react/LexicalComposer';
import { PlainTextPlugin } from '@lexical/react/LexicalPlainTextPlugin';
import { ContentEditable } from '@lexical/react/LexicalContentEditable';
import { HistoryPlugin } from '@lexical/react/LexicalHistoryPlugin';
import { LexicalErrorBoundary } from '@lexical/react/LexicalErrorBoundary';

const initialConfig \= {
  namespace: 'MyEditor',
  onError: (error) \=> console.error(error),
};

function Editor() {
  return (
    <LexicalComposer initialConfig\={initialConfig}\>
      <PlainTextPlugin
        contentEditable\={<ContentEditable />}
        ErrorBoundary\={LexicalErrorBoundary}
      />
      <HistoryPlugin />
    </LexicalComposer\>
  );
}

Try it yourself:

-   Plain Text Example
-   Rich Text Example

Development
-----------

# Install dependencies
pnpm install

# Start playground dev server
pnpm run start

# Run tests
pnpm run test-unit
pnpm run test-e2e-chromium

# Lint and type check
pnpm run ci-check

See CONTRIBUTING.md for detailed development guidelines.

Documentation
-------------

-   **User Guide**: lexical.dev/docs/intro
-   **API Reference**: lexical.dev/docs/api
-   **Developer Guide**: AGENTS.md - Architecture and development workflows
-   **Examples**: examples/ - Sample implementations

Community & Support
-------------------

-   **Discord**: Join our Discord server for questions and discussions
-   **Twitter**: Follow @lexicaljs for updates
-   **Issues**: Report bugs and request features on GitHub Issues

Browser Support
---------------

Browser

Version

Chrome

86+

Firefox

115+

Safari

15+

Edge

86+

Contributors
------------

We welcome contributions! Please read our Contributing Guide to learn about our development process and how to propose bugfixes and improvements.

License
-------

MIT License © Meta Platforms, Inc.
