---
project: date-fns
stars: 36281
description: ⏳ Modern JavaScript date utility library ⌛️
url: https://github.com/date-fns/date-fns
---

🔥️ **NEW**: date-fns v4.0 with first-class time zone support is out!

date-fns provides the most comprehensive, yet simple and consistent toolset for manipulating JavaScript dates in a browser & Node.js

👉 Documentation

👉 Blog

* * *

It's like Lodash for dates

-   It has **200+ functions** for all occasions.
-   **Modular**: Pick what you need. Works with webpack, Browserify, or Rollup and also supports tree-shaking.
-   **Native dates**: Uses existing native type. It doesn't extend core objects for safety's sake.
-   **Immutable & Pure**: Built using pure functions and always returns a new date instance.
-   **TypeScript**: The library is 100% TypeScript with brand-new handcrafted types.
-   **I18n**: Dozens of locales. Include only what you need.
-   and many more benefits

import { compareAsc, format } from "date-fns";

format(new Date(2014, 1, 11), "yyyy-MM-dd");
//=> '2014-02-11'

const dates \= \[
  new Date(1995, 6, 2),
  new Date(1987, 1, 11),
  new Date(1989, 6, 10),
\];
dates.sort(compareAsc);
//=> \[
//   Wed Feb 11 1987 00:00:00,
//   Mon Jul 10 1989 00:00:00,
//   Sun Jul 02 1995 00:00:00
// \]

The library is available as an npm package. To install the package run:

npm install date-fns --save

Docs
----

See date-fns.org for more details, API, and other docs.

  

License
-------

MIT © Sasha Koss
