---
project: video.js
stars: 39298
description: Video.js - open source HTML5 video player
url: https://github.com/videojs/video.js
---

Video.js - Web Video Player & Framework
=======================================

**Update:** Big changes coming in Video.js 10, early 2026! Read the discussion.

Video.js is a full featured, open source video player for all web-based platforms.

Right out of the box, Video.js supports all common media formats used on the web including streaming formats like HLS and DASH. It works on desktops, mobile devices, tablets, and web-based Smart TVs. It can be further extended and customized by a robust ecosystem of plugins.

Video.js was started in May 2010 and since then:

-   Millions of websites have used VideoJS over time (source Builtwith)
-   Billions of end-users every month of just the CDN-hosted copy (source Fastly stats)
-   900+ amazing contributors to the video.js core
-   Hundreds of plugins

Table of Contents
-----------------

-   Quick Start
-   Contributing
-   Code of Conduct
-   License
-   Sponsorship

Quick Start
-----------

Thanks to the awesome folks over at Fastly, there's a free, CDN hosted version of Video.js that anyone can use. Add these tags to your document's `<head>`:

<link href\="//vjs.zencdn.net/8.23.4/video-js.min.css" rel\="stylesheet"\>
<script src\="//vjs.zencdn.net/8.23.4/video.min.js"\></script\>

Alternatively, you can include Video.js by getting it from npm, downloading it from GitHub releases or by including it via unpkg or another JavaScript CDN, like CDNjs.

<!-- unpkg : use the latest version of Video.js -->
<link href\="https://unpkg.com/video.js/dist/video-js.min.css" rel\="stylesheet"\>
<script src\="https://unpkg.com/video.js/dist/video.min.js"\></script\>

<!-- unpkg : use a specific version of Video.js (change the version numbers as necessary) -->
<link href\="https://unpkg.com/video.js@8.23.4/dist/video-js.min.css" rel\="stylesheet"\>
<script src\="https://unpkg.com/video.js@8.23.4/dist/video.min.js"\></script\>

<!-- cdnjs : use a specific version of Video.js (change the version numbers as necessary) -->
<link href\="https://cdnjs.cloudflare.com/ajax/libs/video.js/8.23.4/video-js.min.css" rel\="stylesheet"\>
<script src\="https://cdnjs.cloudflare.com/ajax/libs/video.js/8.23.4/video.min.js"\></script\>

Next, using Video.js is as simple as creating a `<video>` element, but with an additional `data-setup` attribute. At a minimum, this attribute must have a value of `'{}'`, but it can include any Video.js options - just make sure it contains valid JSON!

<video
    id\="my-player"
    class\="video-js"
    controls
    preload\="auto"
    poster\="//vjs.zencdn.net/v/oceans.png"
    data-setup\='{}'\>
  <source src\="//vjs.zencdn.net/v/oceans.mp4" type\="video/mp4"\></source\>
  <source src\="//vjs.zencdn.net/v/oceans.webm" type\="video/webm"\></source\>
  <source src\="//vjs.zencdn.net/v/oceans.ogv" type\="video/ogg"\></source\>
  <p class\="vjs-no-js"\>
    To view this video please enable JavaScript, and consider upgrading to a
    web browser that
    <a href\="https://videojs.com/html5-video-support/" target\="\_blank"\>
      supports HTML5 video
    </a\>
  </p\>
</video\>

When the page loads, Video.js will find this element and automatically setup a player in its place.

If you don't want to use automatic setup, you can leave off the `data-setup` attribute and initialize a `<video>` element manually using the `videojs` function:

var player \= videojs('my-player');

The `videojs` function also accepts an `options` object and a callback to be invoked when the player is ready:

var options \= {};

var player \= videojs('my-player', options, function onPlayerReady() {
  videojs.log('Your player is ready!');

  // In this context, \`this\` is the player that was created by Video.js.
  this.play();

  // How about an event listener?
  this.on('ended', function() {
    videojs.log('Awww...over so soon?!');
  });
});

If you're ready to dive in, the Getting Started page and documentation are the best places to go for more information. If you get stuck, head over to our Slack!

Contributing
------------

Video.js is a free and open source library, and we appreciate any help you're willing to give - whether it's fixing bugs, improving documentation, or suggesting new features. Check out the contributing guide for more! Contributions and project decisions are overseen by the Video.js Technical Steering Committee (TSC).

By submitting a pull request, you agree that your contribution is provided under the Apache 2.0 License and may be included in future releases. No contributor license agreement (CLA) has ever been required for contributions to Video.js. See the Developer's Certificate of Origin 1.1 .

Code of Conduct
---------------

Please note that this project is released with a Contributor Code of Conduct. By participating in this project you agree to abide by its terms.

License
-------

Video.js is licensed under the Apache License, Version 2.0. "Video.js" is a registered trademark of Brightcove, Inc.

Sponsorship
-----------

Project development is sponsored by the role of Corporate Shepherd, held by various companies throughout the project history:

-   2010-2012: Zencoder Inc.
-   2013-2025: Brightcove Inc.
-   2025-present: Mux Inc.

Video.js uses BrowserStack for compatibility testing.

The free CDN-hosted copy of the libray is sponsored by Fastly.

Website hosting is sponsored by Netlify
