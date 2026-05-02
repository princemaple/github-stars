---
project: appmetrics.js
stars: 1364
description: A small (< 1kb) library for measuring things in your web app and reporting the results to Google Analytics.
url: https://github.com/ebidel/appmetrics.js
---

appmetrics.js
-------------

> A small (803 bytes gzipped) library for measuring things in your web app, annotating the DevTools timeline, and reporting the results to Google Analytics.

This library is a small wrapper around the the User Timing API. It makes it easier to use. appmetrics.js allows you to instrument your app, record performance metrics, and (optionally) report those metrics to Google Analytics. Over time, you'll be able to track the performance of your web app!

### What does it do?

If you want to measure the performance of certain events in your web app. How long did that take?

In browsers that support the full User Timing API, this library integrates with DevTools. App measurements in the timeline:

Marks you create will also show up in webpagetest.org results:

If you chose to send metrics to Google Analytics, values will show up its UI. See below.

### Installing

Bower:

```
bower install --save-dev ebidel/appmetrics.js
```

npm (https://www.npmjs.com/package/appmetrics.js):

```
npm install --save-dev appmetrics.js
```

### Usage

Drop one of these on your page:

<script src\="bower\_components/appmetrics.js/dist/appmetrics.min.js"\></script\>
  or
<script src\="node\_modules/appmetrics.js/dist/appmetrics.min.js"\></script\>

To measure how long something takes in your app, first create a new metric:

let metric \= new Metric('my\_event'); // each metric name should be unique.

Specify the beginning of your event by calling `start()`. This adds a mark in the DevTools timeline:

metric.start(); // mark name will be "mark\_my\_event\_start"

When the event completes, call `end()`. This adds another mark in the DevTools timeline and measures the duration:

metric.end(); // mark name will be "mark\_my\_event\_end".
console.log(\`${metric.name} took ${metric.duration} ms\`);
metric.log(); // Helper for logging the metric info to the console.

From here, you can examine performance of your measurements in the console:

Or view the records in the DevTools Timeline under "Input" (see screen shot above).

### Reporting metrics to Google Analytics (optional)

**Be sure to load the Google Analytics library on your page.**

Metrics can be reported to Google Analytics using `sendToAnalytics(<category>)`. These show up in the Analytics UI under User Timing.

metric1.sendToAnalytics('page load');
metric2.sendToAnalytics('render', 'first paint'); // Optional 2nd arg is an event name
metric3.sendToAnalytics('JS Dependencies', 'load', 1234567890); // Optional 3rd arg to override metric3.duration.

The first argument to `sendToAnalytics()` is the category of your metric ('load', 'gallery', 'video'). The second argument is an optional name of the metric ('first paint', 'reveal', 'watch\_started'). By default, `metric.name` is used, but oftentimes it's more convenient to send a shorter to Google Analytics so it renders it nicely in its UI.

Values sent to Analytics will show up in its UI under **Behavior > Site Speed > User Timings**:

### Examples

Example - measure how long it takes a json file to load, and report it to Google Analytics:

<script\>
  const metric \= new Metric('features\_loaded');
  metric.start();

  function onFeaturesLoad() {
    metric.end().log().sendToAnalytics('features', 'loaded');
  }
</script\>
<script src\="features.json" onload\="onFeaturesLoad()"\></script\>

Example - report the first paint to Google Analytics.

/\*\*
 \* Returns the browser's first paint metric (if available).
 \* @return {number} The first paint time in ms.
 \*/
function getFirstPaintIfSupported() {
  if (window.chrome && window.chrome.loadTimes) {
    const load \= window.chrome.loadTimes();
    const fp \= (load.firstPaintTime \- load.startLoadTime) \* 1000;
    return Math.round(fp);
  } else if ('performance' in window) {
    const navTiming \= window.performance.timing;
    // See http://msdn.microsoft.com/ff974719
    if (navTiming && navTiming.msFirstPaint && navTiming.navigationStart !== 0) {
      // See http://msdn.microsoft.com/ff974719
      return navTiming.msFirstPaint \- navTiming.navigationStart;
    }
  }
  return null;
}

// Take measurement after page load.
window.addEventListener('load', function() {
  const fp \= getFirstPaintIfSupported();
  if (fp) {
    const metric \= new Metric('firstpaint');

    // No need to call start()/end(). Can send a value, directly.
    metric.sendToAnalytics('load', metric.name, fp);
  }
});

### Browser support

Any browser that supports `performance.now()`! That's all the modern stuff: Chrome, Firefox, Safari 9.2+, Edge, IE 10, Android Browser 4.4, UC Browser.

**Caveat**: In Safari, the User Timing API (`performance.mark()`) is not available, so the DevTools timeline will not be annotated with marks.

See caniuse.com for full support.

### Tips

All methods can be chained for easier use:

```
metric.start();
// ... some time later ...
metric.end().log().sendToAnalytics('extras', 'syntax highlight');
```

### Contributing

Checkout and install the dependencies:

```
git clone git@github.com:ebidel/appmetrics.js.git
cd appmetrics.js
npm install
gulp
```

#### Run the tests

Start a web server in the project directory and navigate to http://localhost:3000/test/. If you makes changes to the library, be sure to run `gulp` to rebuild the library in `/dist`.

### License

Apache 2. See the LICENSE.
