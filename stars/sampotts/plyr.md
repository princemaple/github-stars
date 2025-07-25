---
project: plyr
stars: 28907
description: A simple HTML5, YouTube and Vimeo player
url: https://github.com/sampotts/plyr
---

🎉

Plyr is merging into Vidstack

🎉

Plyr is a simple, lightweight, accessible and customizable HTML5, YouTube and Vimeo media player that supports _modern_ browsers.

Checkout the demo - Donate - Slack

Features
========

-   📼 **HTML Video & Audio, YouTube & Vimeo** - support for the major formats
-   💪 **Accessible** - full support for VTT captions and screen readers
-   🔧 **Customizable** - make the player look how you want with the markup you want
-   😎 **Clean HTML** - uses the _right_ elements. `<input type="range">` for volume and `<progress>` for progress and well, `<button>`s for buttons. There's no `<span>` or `<a href="#">` button hacks
-   📱 **Responsive** - works with any screen size
-   💵 **Monetization** - make money from your videos
-   📹 **Streaming** - support for hls.js, Shaka and dash.js streaming playback
-   🎛 **API** - toggle playback, volume, seeking, and more through a standardized API
-   🎤 **Events** - no messing around with Vimeo and YouTube APIs, all events are standardized across formats
-   🔎 **Fullscreen** - supports native fullscreen with fallback to "full window" modes
-   ⌨️ **Shortcuts** - supports keyboard shortcuts
-   🖥 **Picture-in-Picture** - supports picture-in-picture mode
-   📱 **Playsinline** - supports the `playsinline` attribute
-   🏎 **Speed controls** - adjust speed on the fly
-   📖 **Multiple captions** - support for multiple caption tracks
-   🌎 **i18n support** - support for internationalization of controls
-   👌 **Preview thumbnails** - support for displaying preview thumbnails
-   🤟 **No frameworks** - written in "vanilla" ES6 JavaScript, no jQuery required
-   💁‍♀️ **Sass** - to include in your build processes

Demos
-----

You can try Plyr in Codepen using our minimal templates: HTML5 video, HTML5 audio, YouTube, Vimeo. For Streaming we also have example integrations with: Dash.js, Hls.js and Shaka Player

Quick setup
===========

HTML
----

Plyr extends upon the standard HTML5 media element markup so that's all you need for those types.

### HTML5 Video

<video id\="player" playsinline controls data-poster\="/path/to/poster.jpg"\>
  <source src\="/path/to/video.mp4" type\="video/mp4" />
  <source src\="/path/to/video.webm" type\="video/webm" />

  <!-- Captions are optional -->
  <track kind\="captions" label\="English captions" src\="/path/to/captions.vtt" srclang\="en" default />
</video\>

**Note**: The poster image should be specified using `data-poster`. This is to prevent it being downloaded twice. If you're sure the image will be cached, you can still use the `poster` attribute for true progressive enhancement.

### HTML5 Audio

<audio id\="player" controls\>
  <source src\="/path/to/audio.mp3" type\="audio/mp3" />
  <source src\="/path/to/audio.ogg" type\="audio/ogg" />
</audio\>

For YouTube and Vimeo players, Plyr uses progressive enhancement to enhance the default `<iframe>` embeds. Below are some examples. The `plyr__video-embed` classname will make the embed responsive. You can add the `autoplay`, `loop`, `hl` (YouTube only) and `playsinline` (YouTube only) query parameters to the URL and they will be set as config options automatically. For YouTube, the `origin` should be updated to reflect the domain you're hosting the embed on, or you can opt to omit it.

### YouTube

We recommend progressive enhancement with the embedded players. You can elect to use an `<iframe>` as the source element (which Plyr will progressively enhance) or a bog standard `<div>` with two essential data attributes - `data-plyr-provider` and `data-plyr-embed-id`.

<div class\="plyr\_\_video-embed" id\="player"\>
  <iframe
    src\="https://www.youtube.com/embed/bTqVqk7FSmY?origin=https://plyr.io&amp;iv\_load\_policy=3&amp;modestbranding=1&amp;playsinline=1&amp;showinfo=0&amp;rel=0&amp;enablejsapi=1"
    allowfullscreen
    allowtransparency
    allow\="autoplay"
  \></iframe\>
</div\>

_Note_: The `plyr__video-embed` classname will make the player a responsive 16:9 (most common) iframe embed. When plyr itself kicks in, your custom `ratio` config option will be used.

Or the `<div>` non progressively enhanced method:

<div id\="player" data-plyr-provider\="youtube" data-plyr-embed-id\="bTqVqk7FSmY"\></div\>

_Note_: The `data-plyr-embed-id` can either be the video ID or URL for the media.

### Vimeo

Much the same as YouTube above.

<div class\="plyr\_\_video-embed" id\="player"\>
  <iframe
    src\="https://player.vimeo.com/video/76979871?loop=false&amp;byline=false&amp;portrait=false&amp;title=false&amp;speed=true&amp;transparent=0&amp;gesture=media"
    allowfullscreen
    allowtransparency
    allow\="autoplay"
  \></iframe\>
</div\>

Or the `<div>` non progressively enhanced method:

<div id\="player" data-plyr-provider\="vimeo" data-plyr-embed-id\="76979871"\></div\>

JavaScript
----------

You can use Plyr as an ES6 module as follows:

import Plyr from 'plyr';

const player \= new Plyr('#player');

Alternatively you can include the `plyr.js` script before the closing `</body>` tag and then in your JS create a new instance of Plyr as below.

<script src\="path/to/plyr.js"\></script\>
<script\>
  const player \= new Plyr('#player');
</script\>

See initialising for more information on advanced setups.

You can use our CDN (provided by Cloudflare) for the JavaScript. There's 2 versions; one with and one without polyfills. My recommendation would be to manage polyfills separately as part of your application but to make life easier you can use the polyfilled build.

<script src\="https://cdn.plyr.io/3.7.8/plyr.js"\></script\>

...or...

<script src\="https://cdn.plyr.io/3.7.8/plyr.polyfilled.js"\></script\>

CSS
---

Include the `plyr.css` stylesheet into your `<head>`.

<link rel\="stylesheet" href\="path/to/plyr.css" />

If you want to use our CDN (provided by Cloudflare) for the default CSS, you can use the following:

<link rel\="stylesheet" href\="https://cdn.plyr.io/3.7.8/plyr.css" />

SVG Sprite
----------

The SVG sprite is loaded automatically from our CDN (provided by Cloudflare). To change this, see the options below. For reference, the CDN hosted SVG sprite can be found at `https://cdn.plyr.io/3.7.8/plyr.svg`.

### Self hosting

If you don't want to create a build system to include Plyr as an npm module, you can use the pre-built files. You have a few options:

-   Download the files from the CDN links above, they're already minified.
-   Download the files from unpkg or similar services.
-   Build the project yourself using `npm i && npm run build`, which installs the dependencies and spits out a build to `dist`.

Ads
===

Plyr has partnered up with vi.ai to offer monetization options for your videos. Getting setup is easy:

-   Sign up for a vi.ai account
-   Grab your publisher ID from the code snippet
-   Enable ads in the config options and enter your publisher ID

Any questions regarding the ads can be sent straight to vi.ai and any issues with rendering raised through GitHub issues.

If you do not wish to use Vi, you can set your own `ads.tagUrl` option.

Advanced
========

Customizing the CSS
-------------------

If you want to change any design tokens used for the rendering of the player, you can do so using CSS Custom Properties.

Here's a list of the properties and what they are used for:

Name

Description

Default / Fallback

`--plyr-color-main`

The primary UI color.

`#00b3ff`

`--plyr-video-background`

The background color of video and poster wrappers for using alpha channel videos and poster images.

`rgba(0, 0, 0, 1)`

`--plyr-focus-visible-color`

The color used for the focus styles when an element is `:focus-visible` (keyboard focused).

`--plyr-color-main`

`--plyr-badge-background`

The background color for badges in the menu.

`#4a5464`

`--plyr-badge-text-color`

The text color for badges.

`#ffffff`

`--plyr-badge-border-radius`

The border radius used for badges.

`2px`

`--plyr-captions-background`

The color for the background of captions.

`rgba(0, 0, 0, 0.8)`

`--plyr-captions-text-color`

The color used for the captions text.

`#ffffff`

`--plyr-control-icon-size`

The size of the icons used in the controls.

`18px`

`--plyr-control-spacing`

The space between controls (sometimes used in a multiple - e.g. `10px / 2 = 5px`).

`10px`

`--plyr-control-padding`

The padding inside controls.

`--plyr-control-spacing * 0.7` (`7px`)

`--plyr-control-radius`

The border radius used on controls.

`3px`

`--plyr-control-toggle-checked-background`

The background color used for checked menu items.

`--plyr-color-main`

`--plyr-video-controls-background`

The background for the video controls.

`linear-gradient(rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.75))`

`--plyr-video-control-color`

The text/icon color for video controls.

`#ffffff`

`--plyr-video-control-color-hover`

The text/icon color used when video controls are `:hover`, `:focus` and `:focus-visible` (equivalent).

`#ffffff`

`--plyr-video-control-background-hover`

The background color used when video controls are `:hover`, `:focus` and `:focus-visible` (equivalent).

`--plyr-color-main`

`--plyr-audio-controls-background`

The background for the audio controls.

`#ffffff`

`--plyr-audio-control-color`

The text/icon color for audio controls.

`#4a5464`

`--plyr-audio-control-color-hover`

The text/icon color used when audio controls are `:hover`, `:focus` and `:focus-visible` (equivalent).

`#ffffff`

`--plyr-audio-control-background-hover`

The background color used when video controls are `:hover`, `:focus` and `:focus-visible` (equivalent).

`--plyr-color-main`

`--plyr-menu-background`

The background color for menus.

`rgba(255, 255, 255, 0.9)`

`--plyr-menu-color`

The text/icon color for menu items.

`#4a5464`

`--plyr-menu-shadow`

The shadow used on menus.

`0 1px 2px rgba(0, 0, 0, 0.15)`

`--plyr-menu-radius`

The border radius on the menu.

`4px`

`--plyr-menu-arrow-size`

The size of the arrow on the bottom of the menu.

`6px`

`--plyr-menu-item-arrow-color`

The color of the arrows in the menu.

`#728197`

`--plyr-menu-item-arrow-size`

The size of the arrows in the menu.

`4px`

`--plyr-menu-border-color`

The border color for the bottom of the back button in the top of the sub menu pages.

`#dcdfe5`

`--plyr-menu-border-shadow-color`

The shadow below the border of the back button in the top of the sub menu pages.

`#ffffff`

`--plyr-progress-loading-size`

The size of the stripes in the loading state in the scrubber.

`25px`

`--plyr-progress-loading-background`

The background color on the loading state in the scrubber.

`rgba(35, 40, 47, 0.6)`

`--plyr-video-progress-buffered-background`

The fill color for the buffer indication in the scrubber for video.

`rgba(255, 255, 255, 0.25)`

`--plyr-audio-progress-buffered-background`

The fill color for the buffer indication in the scrubber for audio.

`rgba(193, 200, 209, 0.6)`

`--plyr-range-thumb-height`

The height of the scrubber handle/thumb.

`13px`

`--plyr-range-thumb-background`

The background of the scrubber handle/thumb.

`#ffffff`

`--plyr-range-thumb-shadow`

The shadow of the scrubber handle/thumb.

`0 1px 1px rgba(215, 26, 18, 0.15), 0 0 0 1px rgba(215, 26, 18, 0.2)`

`--plyr-range-thumb-active-shadow-width`

The width of the shadow when the scrubber handle/thumb is `:active` (pressed).

`3px`

`--plyr-range-track-height`

The height of the scrubber/progress track.

`5px`

`--plyr-range-fill-background`

The fill color of the scrubber/progress.

`--plyr-color-main`

`--plyr-video-range-track-background`

The background of the scrubber/progress.

`--plyr-video-progress-buffered-background`

`--plyr-video-range-thumb-active-shadow-color`

The color of the shadow when the video scrubber handle/thumb is `:active` (pressed).

`rgba(255, 255, 255, 0.5)`

`--plyr-audio-range-track-background`

The background of the scrubber/progress.

`--plyr-video-progress-buffered-background`

`--plyr-audio-range-thumb-active-shadow-color`

The color of the shadow when the audio scrubber handle/thumb is `:active` (pressed).

`rgba(215, 26, 18, 0.1)`

`--plyr-tooltip-background`

The background color for tooltips.

`rgba(255, 255, 255, 0.9)`

`--plyr-tooltip-color`

The text color for tooltips.

`#4a5464`

`--plyr-tooltip-padding`

The padding for tooltips.

`calc(var(--plyr-control-spacing) / 2))`

`--plyr-tooltip-arrow-size`

The size of the arrow under tooltips.

`4px`

`--plyr-tooltip-radius`

The border radius on tooltips.

`3px`

`--plyr-tooltip-shadow`

The shadow on tooltips.

`0 1px 2px rgba(0, 0, 0, 0.15)`

`--plyr-font-family`

The font family used in the player.

`--plyr-font-size-base`

The base font size. Mainly used for captions.

`15px`

`--plyr-font-size-small`

The smaller font size. Mainly used for captions.

`13px`

`--plyr-font-size-large`

The larger font size. Mainly used for captions.

`18px`

`--plyr-font-size-xlarge`

The even larger font size. Mainly used for captions.

`21px`

`--plyr-font-size-time`

The font size for the time.

`--plyr-font-size-small`

`--plyr-font-size-menu`

The font size used in the menu.

`--plyr-font-size-small`

`--plyr-font-size-badge`

The font size used for badges.

`9px`

`--plyr-font-weight-regular`

The regular font weight.

`400`

`--plyr-font-weight-bold`

The bold font weight.

`600`

`--plyr-line-height`

The line height used within the player.

`1.7`

`--plyr-font-smoothing`

Whether to enable font antialiasing within the player.

`false`

You can set them in your CSS for all players:

:root {
  \--plyr-color-main: #1ac266;
}

...or for a specific class name:

.player {
  \--plyr-color-main: #1ac266;
}

...or in your HTML:

<video class\="player" style\="\--plyr-color-main: #1ac266;"\>...</video\>

### Sass

You can use `plyr.scss` file included in `/src/sass` as part of your build and change variables to suit your design. The Sass requires you to use autoprefixer (you should be already!) as all declarations use the W3C definitions.

The HTML markup uses the BEM methodology with `plyr` as the block, e.g. `.plyr__controls`. You can change the class hooks in the options to match any custom CSS you write. Check out the JavaScript source for more on this.

SVG
---

The icons used in the Plyr controls are loaded in an SVG sprite. The sprite is automatically loaded from our CDN by default. If you already have an icon build system in place, you can include the source plyr icons (see `/src/sprite` for source icons).

### Using the `iconUrl` option

You can however specify your own `iconUrl` option and Plyr will determine if the url is absolute and requires loading by AJAX/CORS due to current browser limitations or if it's a relative path, just use the path directly.

If you're using the `<base>` tag on your site, you may need to use something like this: svgfixer.js

More info on SVG sprites here: http://css-tricks.com/svg-sprites-use-better-icon-fonts/ and the AJAX technique here: http://css-tricks.com/ajaxing-svg-sprite/

Cross Origin (CORS)
-------------------

You'll notice the `crossorigin` attribute on the example `<video>` elements. This is because the TextTrack captions are loaded from another domain. If your TextTrack captions are also hosted on another domain, you will need to add this attribute and make sure your host has the correct headers setup. For more info on CORS checkout the MDN docs: https://developer.mozilla.org/en-US/docs/Web/HTTP/Access\_control\_CORS

Captions
--------

WebVTT captions are supported. To add a caption track, check the HTML example above and look for the `<track>` element. Be sure to validate your caption files.

JavaScript
----------

### Initializing

You can specify a range of arguments for the constructor to use:

-   A CSS string selector
-   A `HTMLElement`
-   A jQuery object

_Note_: If a `NodeList`, `Array`, or jQuery object are passed, the first element will be used for setup. To setup multiple players, see multiple players below.

#### Single player

Passing a CSS string selector that's compatible with `querySelector`:

const player \= new Plyr('#player');

Passing a HTMLElement:

const player \= new Plyr(document.getElementById('player'));

const player \= new Plyr(document.querySelector('.js-player'));

The HTMLElement or string selector can be the target `<video>`, `<audio>`, or `<div>` wrapper for embeds.

#### Multiple players

You have two choices here. You can either use a simple array loop to map the constructor:

const players \= Array.from(document.querySelectorAll('.js-player')).map((p) \=> new Plyr(p));

...or use a static method where you can pass a CSS string selector, a NodeList, an Array of HTMLElement, or a JQuery object:

const players \= Plyr.setup('.js-player');

Both options will also return an array of instances in the order of they were in the DOM for the string selector or the source NodeList or Array.

#### Options

The second argument for the constructor is the options object:

const player \= new Plyr('#player', {
  title: 'Example Title',
});

Options can be passed as an object to the constructor as above or as JSON in `data-plyr-config` attribute on each of your target elements:

<video src\="/path/to/video.mp4" id\="player" controls data-plyr-config\='{ "title": "Example Title" }'\></video\>

Note the single quotes encapsulating the JSON and double quotes on the object keys. Only string values need double quotes.

Option

Type

Default

Description

`enabled`

Boolean

`true`

Completely disable Plyr. This would allow you to do a User Agent check or similar to programmatically enable or disable Plyr for a certain UA. Example below.

`debug`

Boolean

`false`

Display debugging information in the console

`controls`

Array, Function or Element

`['play-large', 'play', 'progress', 'current-time', 'mute', 'volume', 'captions', 'settings', 'pip', 'airplay', 'fullscreen']`

If a function is passed, it is assumed your method will return either an element or HTML string for the controls. Three arguments will be passed to your function; `id` (the unique id for the player), `seektime` (the seektime step in seconds), and `title` (the media title). See CONTROLS.md for more info on how the html needs to be structured.

`settings`

Array

`['captions', 'quality', 'speed', 'loop']`

If the default controls are used, you can specify which settings to show in the menu

`i18n`

Object

See defaults.js

Used for internationalization (i18n) of the text within the UI.

`loadSprite`

Boolean

`true`

Load the SVG sprite specified as the `iconUrl` option (if a URL). If `false`, it is assumed you are handling sprite loading yourself.

`iconUrl`

String

`null`

Specify a URL or path to the SVG sprite. See the SVG section for more info.

`iconPrefix`

String

`plyr`

Specify the id prefix for the icons used in the default controls (e.g. "plyr-play" would be "plyr"). This is to prevent clashes if you're using your own SVG sprite but with the default controls. Most people can ignore this option.

`blankVideo`

String

`https://cdn.plyr.io/static/blank.mp4`

Specify a URL or path to a blank video file used to properly cancel network requests.

`autoplay`²

Boolean

`false`

Autoplay the media on load. If the `autoplay` attribute is present on a `<video>` or `<audio>` element, this will be automatically set to true.

`autopause`¹

Boolean

`true`

Only allow one player playing at once.

`playsinline`³

Boolean

`true`

Allow inline playback on iOS. Note this has no effect on iPadOS.

`seekTime`

Number

`10`

The time, in seconds, to seek when a user hits fast forward or rewind.

`volume`

Number

`1`

A number, between 0 and 1, representing the initial volume of the player.

`muted`

Boolean

`false`

Whether to start playback muted. If the `muted` attribute is present on a `<video>` or `<audio>` element, this will be automatically set to true.

`clickToPlay`

Boolean

`true`

Click (or tap) of the video container will toggle play/pause.

`disableContextMenu`

Boolean

`true`

Disable right click menu on video to _help_ as very primitive obfuscation to prevent downloads of content.

`hideControls`

Boolean

`true`

Hide video controls automatically after 2s of no mouse or focus movement, on control element blur (tab out), on playback start or entering fullscreen. As soon as the mouse is moved, a control element is focused or playback is paused, the controls reappear instantly.

`resetOnEnd`

Boolean

false

Reset the playback to the start once playback is complete.

`keyboard`

Object

`{ focused: true, global: false }`

Enable keyboard shortcuts for focused players only or globally

`tooltips`

Object

`{ controls: false, seek: true }`

`controls`: Display control labels as tooltips on `:hover` & `:focus` (by default, the labels are screen reader only). `seek`: Display a seek tooltip to indicate on click where the media would seek to.

`duration`

Number

`null`

Specify a custom duration for media.

`displayDuration`

Boolean

`true`

Displays the duration of the media on the "metadataloaded" event (on startup) in the current time display. This will only work if the `preload` attribute is not set to `none` (or is not set at all) and you choose not to display the duration (see `controls` option).

`invertTime`

Boolean

`true`

Display the current time as a countdown rather than an incremental counter.

`toggleInvert`

Boolean

`true`

Allow users to click to toggle the above.

`listeners`

Object

`null`

Allows binding of event listeners to the controls before the default handlers. See the `defaults.js` for available listeners. If your handler prevents default on the event (`event.preventDefault()`), the default handler will not fire.

`captions`

Object

`{ active: false, language: 'auto', update: false }`

`active`: Toggles if captions should be active by default. `language`: Sets the default language to load (if available). 'auto' uses the browser language. `update`: Listen to changes to tracks and update menu. This is needed for some streaming libraries, but can result in non-selectable language options).

`fullscreen`

Object

`{ enabled: true, fallback: true, iosNative: false, container: null }`

`enabled`: Toggles whether fullscreen should be enabled. `fallback`: Allow fallback to a full-window solution (`true`/`false`/`'force'`). `iosNative`: whether to use native iOS fullscreen when entering fullscreen (no custom controls) - note this has no effect on iPadOS. `container`: A selector for an ancestor of the player element, allows contextual content to remain visual in fullscreen mode. Non-ancestors are ignored.

`ratio`

String

`null`

Force an aspect ratio for all videos. The format is `'w:h'` - e.g. `'16:9'` or `'4:3'`. If this is not specified then the default for HTML5 and Vimeo is to use the native resolution of the video. As dimensions are not available from YouTube via SDK, 16:9 is forced as a sensible default.

`storage`

Object

`{ enabled: true, key: 'plyr' }`

`enabled`: Allow use of local storage to store user settings. `key`: The key name to use.

`speed`

Object

`{ selected: 1, options: [0.5, 0.75, 1, 1.25, 1.5, 1.75, 2, 4] }`

`selected`: The default speed for playback. `options`: The speed options to display in the UI. YouTube and Vimeo will ignore any options outside of the 0.5-2 range, so options outside of this range will be hidden automatically.

`quality`

Object

`{ default: 576, options: [4320, 2880, 2160, 1440, 1080, 720, 576, 480, 360, 240] }`

`default` is the default quality level (if it exists in your sources). `options` are the options to display. This is used to filter the available sources.

`loop`

Object

`{ active: false }`

`active`: Whether to loop the current video. If the `loop` attribute is present on a `<video>` or `<audio>` element, this will be automatically set to true This is an object to support future functionality.

`ads`

Object

`{ enabled: false, publisherId: '', tagUrl: '' }`

`enabled`: Whether to enable advertisements. `publisherId`: Your unique vi.ai publisher ID. `tagUrl` is a URL for a custom VAST tag if you're not using Vi.

`urls`

Object

See source.

If you wish to override any API URLs then you can do so here. You can also set a custom download URL for the download button.

`vimeo`

Object

`{ byline: false, portrait: false, title: false, speed: true, transparent: false }`

See Vimeo embed options. Some are set automatically based on other config options, namely: `loop`, `autoplay`, `muted`, `gesture`, `playsinline`

`youtube`

Object

`{ noCookie: false, rel: 0, showinfo: 0, iv_load_policy: 3, modestbranding: 1 }`

See YouTube embed options. The only custom option is `noCookie` to use an alternative to YouTube that doesn't use cookies (useful for GDPR, etc). Some are set automatically based on other config options, namely: `autoplay`, `hl`, `controls`, `disablekb`, `playsinline`, `cc_load_policy`, `cc_lang_pref`, `widget_referrer`

`previewThumbnails`

Object

`{ enabled: false, src: '' }`

`enabled`: Whether to enable the preview thumbnails (they must be generated by you). `src` must be either a string or an array of strings representing URLs for the VTT files containing the image URL(s). Learn more about preview thumbnails below.

`mediaMetadata`

Object

`{ title: '', artist: '', album: '', artwork: [] }`

The MediaMetadata interface of the Media Session API allows a web page to provide rich media metadata for display in a platform UI.

`markers`

Object

`{ enabled: false, points: [] }`

`enabled`: Whether to enable markers. `points` is an array of `{ time: number; label: string; }` objects where `time` represents the marker position in seconds and `label` is the HTML string to be displayed.

1.  Vimeo only
2.  Autoplay is generally not recommended as it is seen as a negative user experience. It is also disabled in many browsers. Before raising issues, do your homework. More info can be found here:

-   https://webkit.org/blog/6784/new-video-policies-for-ios/
-   https://developers.google.com/web/updates/2017/09/autoplay-policy-changes
-   https://hacks.mozilla.org/2019/02/firefox-66-to-block-automatically-playing-audible-video-and-audio/

1.  YouTube does not support programatically toggling the native fullscreen player via it's API. This means on iOS you have two options, neither being perfect:

-   Use the fallback/faux fullscreen option which covers the whole viewport (this is the default)
-   Set `playsinline` to `false` and/or `fullscreen.iosNative` to `true` - either option hides the fullscreen toggle in the UI (because of the above API issue) and means iOS will play the video in it's native player.

API
===

There are methods, setters and getters on a Plyr object.

Object
------

The easiest way to access the Plyr object is to set the return value from your call to the constructor to a variable. For example:

const player \= new Plyr('#player', {
  /\* options \*/
});

You can also access the object through any events:

element.addEventListener('ready', (event) \=> {
  const player \= event.detail.plyr;
});

Methods
-------

Example method use:

player.play(); // Start playback
player.fullscreen.enter(); // Enter fullscreen

Method

Parameters

Description

`play()`¹

\-

Start playback.

`pause()`

\-

Pause playback.

`togglePlay(toggle)`¹

Boolean

Toggle playback, if no parameters are passed, it will toggle based on current status.

`stop()`

\-

Stop playback and reset to start.

`restart()`

\-

Restart playback.

`rewind(seekTime)`

Number

Rewind playback by the specified seek time. If no parameter is passed, the default seek time will be used.

`forward(seekTime)`

Number

Fast forward by the specified seek time. If no parameter is passed, the default seek time will be used.

`increaseVolume(step)`

Number

Increase volume by the specified step. If no parameter is passed, the default step will be used.

`decreaseVolume(step)`

Number

Increase volume by the specified step. If no parameter is passed, the default step will be used.

`toggleCaptions(toggle)`

Boolean

Toggle captions display. If no parameter is passed, it will toggle based on current status.

`fullscreen.enter()`

\-

Enter fullscreen. If fullscreen is not supported, a fallback "full window/viewport" is used instead.

`fullscreen.exit()`

\-

Exit fullscreen.

`fullscreen.toggle()`

\-

Toggle fullscreen.

`airplay()`

\-

Trigger the airplay dialog on supported devices.

`setPreviewThumbnails(source: PreviewThumbnailsOptions)`

\-

Sets the preview thumbnails for the current source.

`toggleControls(toggle)`

Boolean

Toggle the controls (video only). Takes optional truthy value to force it on/off.

`on(event, function)`

String, Function

Add an event listener for the specified event.

`once(event, function)`

String, Function

Add an event listener for the specified event once.

`off(event, function)`

String, Function

Remove an event listener for the specified event.

`supports(type)`

String

Check support for a mime type.

`destroy()`

\-

Destroy the instance and garbage collect any elements.

1.  For HTML5 players, `play()` will return a `Promise` for most browsers - e.g. Chrome, Firefox, Opera, Safari and Edge according to MDN at time of writing.

Getters and Setters
-------------------

Example setters:

player.volume \= 0.5; // Sets volume at 50%
player.currentTime \= 10; // Seeks to 10 seconds

Example getters:

player.volume; // 0.5;
player.currentTime; // 10
player.fullscreen.active; // false;

Property

Getter

Setter

Description

`isHTML5`

✓

\-

Returns a boolean indicating if the current player is HTML5.

`isEmbed`

✓

\-

Returns a boolean indicating if the current player is an embedded player.

`playing`

✓

\-

Returns a boolean indicating if the current player is playing.

`paused`

✓

\-

Returns a boolean indicating if the current player is paused.

`stopped`

✓

\-

Returns a boolean indicating if the current player is stopped.

`ended`

✓

\-

Returns a boolean indicating if the current player has finished playback.

`buffered`

✓

\-

Returns a float between 0 and 1 indicating how much of the media is buffered

`currentTime`

✓

✓

Gets or sets the currentTime for the player. The setter accepts a float in seconds.

`seeking`

✓

\-

Returns a boolean indicating if the current player is seeking.

`duration`

✓

\-

Returns the duration for the current media.

`volume`

✓

✓

Gets or sets the volume for the player. The setter accepts a float between 0 and 1.

`muted`

✓

✓

Gets or sets the muted state of the player. The setter accepts a boolean.

`hasAudio`

✓

\-

Returns a boolean indicating if the current media has an audio track.

`speed`

✓

✓

Gets or sets the speed for the player. The setter accepts a value in the options specified in your config. Generally the minimum should be 0.5.

`quality`¹

✓

✓

Gets or sets the quality for the player. The setter accepts a value from the options specified in your config.

`loop`

✓

✓

Gets or sets the current loop state of the player. The setter accepts a boolean.

`source`

✓

✓

Gets or sets the current source for the player. The setter accepts an object. See source setter below for examples.

`poster`

✓

✓

Gets or sets the current poster image for the player. The setter accepts a string; the URL for the updated poster image.

`previewThumbnails`

✓

✓

Gets or sets the current preview thumbnail source for the player. The setter accepts a string

`autoplay`

✓

✓

Gets or sets the autoplay state of the player. The setter accepts a boolean.

`currentTrack`

✓

✓

Gets or sets the caption track by index. `-1` means the track is missing or captions is not active

`language`

✓

✓

Gets or sets the preferred captions language for the player. The setter accepts an ISO two-letter language code. Support for the languages is dependent on the captions you include. If your captions don't have any language data, or if you have multiple tracks with the same language, you may want to use `currentTrack` instead.

`fullscreen.active`

✓

\-

Returns a boolean indicating if the current player is in fullscreen mode.

`fullscreen.enabled`

✓

\-

Returns a boolean indicating if the current player has fullscreen enabled.

`pip`¹

✓

✓

Gets or sets the picture-in-picture state of the player. The setter accepts a boolean. This currently only supported on Safari 10+ (on MacOS Sierra+ and iOS 10+) and Chrome 70+.

`ratio`

✓

✓

Gets or sets the video aspect ratio. The setter accepts a string in the same format as the `ratio` option.

`download`

✓

✓

Gets or sets the URL for the download button. The setter accepts a string containing a valid absolute URL.

1.  HTML5 only

### The `.source` setter

This allows changing the player source and type on the fly.

Video example:

player.source \= {
  type: 'video',
  title: 'Example title',
  sources: \[
    {
      src: '/path/to/movie.mp4',
      type: 'video/mp4',
      size: 720,
    },
    {
      src: '/path/to/movie.webm',
      type: 'video/webm',
      size: 1080,
    },
  \],
  poster: '/path/to/poster.jpg',
  previewThumbnails: {
    src: '/path/to/thumbnails.vtt',
  },
  tracks: \[
    {
      kind: 'captions',
      label: 'English',
      srclang: 'en',
      src: '/path/to/captions.en.vtt',
      default: true,
    },
    {
      kind: 'captions',
      label: 'French',
      srclang: 'fr',
      src: '/path/to/captions.fr.vtt',
    },
  \],
};

Audio example:

player.source \= {
  type: 'audio',
  title: 'Example title',
  sources: \[
    {
      src: '/path/to/audio.mp3',
      type: 'audio/mp3',
    },
    {
      src: '/path/to/audio.ogg',
      type: 'audio/ogg',
    },
  \],
};

YouTube example:

player.source \= {
  type: 'video',
  sources: \[
    {
      src: 'bTqVqk7FSmY',
      provider: 'youtube',
    },
  \],
};

Vimeo example

player.source \= {
  type: 'video',
  sources: \[
    {
      src: '76979871',
      provider: 'vimeo',
    },
  \],
};

_Note:_ `src` property for YouTube and Vimeo can either be the video ID or the whole URL.

Property

Type

Description

`type`

String

Either `video` or `audio`. _Note:_ YouTube and Vimeo are currently not supported as audio sources.

`title`

String

_Optional._ Title of the new media. Used for the `aria-label` attribute on the play button, and outer container. YouTube and Vimeo are populated automatically.

`sources`

Array

This is an array of sources. For HTML5 media, the properties of this object are mapped directly to HTML attributes so more can be added to the object if required.

`poster`¹

String

The URL for the poster image (HTML5 video only).

`tracks`¹

String

An array of track objects. Each element in the array is mapped directly to a track element and any keys mapped directly to HTML attributes so as in the example above, it will render as `<track kind="captions" label="English" srclang="en" src="https://cdn.selz.com/plyr/1.0/example_captions_en.vtt" default>` and similar for the French version. Booleans are converted to HTML5 value-less attributes.

`previewThumbnails`¹

Object

The same object like in the `previewThumbnails` constructor option. This means you can either change the thumbnails vtt via the `src` key or disable the thumbnails plugin for the next video by passing `{ enabled: false }`.

1.  HTML5 only

Events
======

You can listen for events on the target element you setup Plyr on (see example under the table). Some events only apply to HTML5 audio and video. Using your reference to the instance, you can use the `on()` API method or `addEventListener()`. Access to the API can be obtained this way through the `event.detail.plyr` property. Here's an example:

player.on('ready', (event) \=> {
  const instance \= event.detail.plyr;
});

Standard Media Events
---------------------

Event Type

Description

`progress`

Sent periodically to inform interested parties of progress downloading the media. Information about the current amount of the media that has been downloaded is available in the media element's `buffered` attribute.

`playing`

Sent when the media begins to play (either for the first time, after having been paused, or after ending and then restarting).

`play`

Sent when playback of the media starts after having been paused; that is, when playback is resumed after a prior `pause` event.

`pause`

Sent when playback is paused.

`timeupdate`

The time indicated by the element's `currentTime` attribute has changed.

`volumechange`

Sent when the audio volume changes (both when the volume is set and when the `muted` state is changed).

`seeking`

Sent when a seek operation begins.

`seeked`

Sent when a seek operation completes.

`ratechange`

Sent when the playback speed changes.

`ended`

Sent when playback completes. _Note:_ This does not fire if `autoplay` is true.

`enterfullscreen`

Sent when the player enters fullscreen mode (either the proper fullscreen or full-window fallback for older browsers).

`exitfullscreen`

Sent when the player exits fullscreen mode.

`captionsenabled`

Sent when captions are enabled.

`captionsdisabled`

Sent when captions are disabled.

`languagechange`

Sent when the caption language is changed.

`controlshidden`

Sent when the controls are hidden.

`controlsshown`

Sent when the controls are shown.

`ready`

Triggered when the instance is ready for API calls.

### HTML5 only

Event Type

Description

`loadstart`

Sent when loading of the media begins.

`loadeddata`

The first frame of the media has finished loading.

`loadedmetadata`

The media's metadata has finished loading; all attributes now contain as much useful information as they're going to.

`qualitychange`

The quality of playback has changed.

`canplay`

Sent when enough data is available that the media can be played, at least for a couple of frames. This corresponds to the `HAVE_ENOUGH_DATA` `readyState`.

`canplaythrough`

Sent when the ready state changes to `CAN_PLAY_THROUGH`, indicating that the entire media can be played without interruption, assuming the download rate remains at least at the current level. _Note:_ Manually setting the `currentTime` will eventually fire a `canplaythrough` event in firefox. Other browsers might not fire this event.

`stalled`

Sent when the user agent is trying to fetch media data, but data is unexpectedly not forthcoming.

`waiting`

Sent when the requested operation (such as playback) is delayed pending the completion of another operation (such as a seek).

`emptied`

he media has become empty; for example, this event is sent if the media has already been loaded (or partially loaded), and the `load()` method is called to reload it.

`cuechange`

Sent when a `TextTrack` has changed the currently displaying cues.

`error`

Sent when an error occurs. The element's `error` attribute contains more information.

### YouTube only

Event Type

Description

`statechange`

The state of the player has changed. The code can be accessed via `event.detail.code`. Possible values are `-1`: Unstarted, `0`: Ended, `1`: Playing, `2`: Paused, `3`: Buffering, `5`: Video cued. See the YouTube Docs for more information.

_Note:_ These events also bubble up the DOM. The event target will be the container element.

Some event details borrowed from MDN.

Embeds
======

YouTube and Vimeo are currently supported and function much like a HTML5 video. Similar events and API methods are available for all types. However if you wish to access the API's directly. You can do so via the `embed` property of your player object - e.g. `player.embed`. You can then use the relevant methods from the third party APIs. More info on the respective API's here:

-   YouTube iframe API Reference
-   Vimeo player.js Reference

_Note_: Not all API methods may work 100%. Your mileage may vary. It's better to use the Plyr API where possible.

Shortcuts
=========

By default, a player will bind the following keyboard shortcuts when it has focus. If you have the `global` option to `true` and there's only one player in the document then the shortcuts will work when any element has focus, apart from an element that requires input.

Key

Action

`0` to `9`

Seek from 0 to 90% respectively

`space`

Toggle playback

`K`

Toggle playback

←

Seek backward by the `seekTime` option

→

Seek forward by the `seekTime` option

↑

Increase volume

↓

Decrease volume

`M`

Toggle mute

`F`

Toggle fullscreen

`C`

Toggle captions

`L`

Toggle loop

Preview thumbnails
==================

It's possible to display preview thumbnails as per the demo when you hover over the scrubber or while you are scrubbing in the main video area. This can be used for all video types but is easiest with HTML5 of course. You will need to generate the sprite or images yourself. This is possible using something like AWS transcoder to generate the frames and then combine them into a sprite image. Sprites are recommended for performance reasons - they will be much faster to download and easier to compress into a small file size making them load faster.

You can see the example VTT files here and here for how the sprites are done. The coordinates are set as the `xywh` hash on the URL in the order X Offset, Y Offset, Width, Height (e.g. `240p-00001.jpg#xywh=1708,480,427,240` is offset `1708px` from the left, `480px` from the top and is `427x240px`. If you want to include images per frame, this is also possible but will be slower, resulting in a degraded experience.

Fullscreen
==========

Fullscreen in Plyr is supported by all browsers that currently support it.

Browser support
===============

Plyr supports the last 2 versions of most _modern_ browsers.

Browser

Supported

Safari

✓

Mobile Safari

✓¹

Firefox

✓

Chrome

✓

Opera

✓

Edge

✓

IE11

✓³

IE10

✓2,3

1.  Mobile Safari on the iPhone forces the native player for `<video>` unless the `playsinline` attribute is present. Volume controls are also disabled as they are handled device wide.
2.  Native player used (no support for `<progress>` or `<input type="range">`) but the API is supported. No native fullscreen support, fallback can be used (see options).
3.  Polyfills required. See below.

Polyfills
---------

Plyr uses ES6 which isn't supported in all browsers quite yet. This means some features will need to be polyfilled to be available otherwise you'll run into issues. We've elected to not burden the ~90% of users that do support these features with extra JS and instead leave polyfilling to you to work out based on your needs.

Checking for support
--------------------

You can use the static method to check for support. For example

const supported \= Plyr.supported('video', 'html5');

The arguments are:

-   Media type (`'audio' | 'video'`)
-   Provider (`'html5' | 'youtube' | 'vimeo'`)

Disable support programmatically
--------------------------------

The `enabled` option can be used to disable certain User Agents. For example, if you don't want to use Plyr for smartphones, you could use:

{
  enabled: !/Android|webOS|iPhone|iPad|iPod|BlackBerry/i.test(navigator.userAgent);
}

If a User Agent is disabled but supports `<video>` and `<audio>` natively, it will use the native player.

Plugins & Components
====================

Some awesome folks have made plugins for CMSs and Components for JavaScript frameworks:

Type

Maintainer

Link

WordPress

Brandon Lavigne (@drrobotnik)

https://wordpress.org/plugins/plyr/

Angular

Simon Bobrov (@smnbbrv)

https://github.com/smnbbrv/ngx-plyr

React

Chintan Prajapati (@chintan9)

https://github.com/chintan9/plyr-react

Vue

Gabe Dunn (@redxtech)

https://github.com/redxtech/vue-plyr

Neos

Jon Uhlmann (@jonnitto)

https://packagist.org/packages/jonnitto/plyr

Kirby

Dominik Pschenitschni (@dpschen)

https://github.com/dpschen/kirby-plyrtag

REDAXO

FriendsOfRedaxo / skerbis (@skerbis)

https://github.com/FriendsOfREDAXO/plyr

svelte-plyr

Ben Woodward / benwoodward (@benwoodward)

https://github.com/benwoodward/svelte-plyr

Issues
======

If you find anything weird with Plyr, please let us know using the GitHub issues tracker.

Author
======

Plyr is developed by @sam\_potts / sampotts.me with help from the awesome contributors

Donate
======

Plyr costs money to run, not only my time. I donate my time for free as I enjoy building Plyr but unfortunately have to pay for domains, hosting, and more. Any help with costs is appreciated...

-   Donate via Patreon
-   Donate via PayPal

Mentions
========

-   ProductHunt
-   The Changelog
-   HTML5 Weekly #177
-   Responsive Design #149
-   Web Design Weekly #174
-   Front End Focus #177
-   Hacker News
-   Web Platform Daily
-   LayerVault Designer News
-   The Treehouse Show #131
-   noupe.com

Used by
=======

-   Selz.com
-   Peugeot.fr
-   Peugeot.de
-   TomTom.com
-   DIGBMX
-   Grime Archive
-   koel - A personal music streaming server that works.
-   Oscar Radio
-   Sparkk TV
-   @halfhalftravel
-   BitChute
-   Rutheneum-Bote
-   pressakey.com | Blog-Magazin für Videospiele
-   STROLLÿN: Work with a View
-   CFDA Runway360
-   NKLAV | Filmmaker
-   GDI.JS.ORG - Google Drive Index

If you want to be added to the list, open a pull request. It'd be awesome to see how you're using Plyr 😎

Useful links and credits
========================

-   PayPal's Accessible HTML5 Video Player (which Plyr was originally ported from)
-   An awesome guide for Plyr in Japanese! by @arayutw

Thanks
======

-   Cloudflare and Fastly for providing the CDN services.
-   Sentry for error logging service on the demo website.

Contributors
------------

### Code Contributors

This project exists thanks to all the people who contribute. \[Contribute\].

### Financial Contributors

Become a financial contributor and help us sustain our community. \[Contribute\]

#### Individuals

#### Organizations

Support this project with your organization. Your logo will show up here with a link to your website. \[Contribute\]

Copyright and License
=====================

The MIT license
