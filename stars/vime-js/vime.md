---
project: vime
stars: 2844
description: Customizable, extensible, accessible and framework agnostic media player. Modern alternative to Video.js and Plyr. Supports HTML5, HLS, Dash, YouTube, Vimeo, Dailymotion...
url: https://github.com/vime-js/vime
---

⚠️  Vime will be deprecated soon! Read more ⚠️

Vime is a customizable, extensible, accessible and framework agnostic media player.

✨ Features
----------

-   🎥  Multi-provider support (HTML5, HLS, YouTube, Vimeo etc.).
-   👑  One API to rule them all! Don't re-learn anything the next time you need a player.
-   ♾️  Avoid cross-browser differences on media related APIs, such as fullscreen and picture-in-picture.
-   👐  Accessible to all via ARIA roles/states/properties and keyboard support.
-   🌎  I18N support.
-   🖥  Designed with both mobile and desktop in mind.
-   👌  Touch input friendly.
-   🎨  Style anything you want with CSS variables. Default light and dark themes are included.
-   🏎️  Performant with preconnections + lazy loading of components and media out of the box.
-   🧩  Easily build your own components and extend Vime.
-   🗑️  Lightweight - ~25kB (gzip) standalone, and ~47kB with the default Vime UI.
-   ️🧰  Awesome default custom UI's for audio/video/live media.
-   🛠  Comprehensive player API with a heap of properties, methods and events.
-   💪  Built with TypeScript so you can enjoy completely typed components.
-   🏠  Feel right at home with HTML/CSS/JS thanks to web components.
-   🏗️  Framework specific bindings for React, Vue, Svelte, Stencil and Angular.

🍭 Examples
-----------

**The examples below are using web components but there are bindings for React, Vue, Svelte, Stencil and Angular. If you want to see how they look check out our Demo.**

<vm-player autoplay muted\>
  <vm-video poster\="/media/poster.png" cross-origin\>
    <!-- Why \`data-src\`? Lazy loading. You can always use \`src\` if you don't need it. -->
    <source data-src\="/media/video.mp4" type\="video/mp4" />
    <track
      default
      kind\="subtitles"
      src\="/media/subs/en.vtt"
      srclang\="en"
      label\="English"
    />
  </vm-video\>

  <!-- Loads the default Vime UI. -->
  <vm-default-ui />
</vm-player\>

_Native UI?_

<!-- Here we are requesting to use the native controls. -->
<vm-player autoplay muted controls\>
  <vm-audio cross-origin\>
    <source data-src\="/media/audio.mp3" type\="audio/mp3" />
  </vm-audio\>
</vm-player\>

_Custom UI?_

<!-- Lets add a little splash of color throughout the player. -->
<vm-player autoplay muted style\="\--vm-player-theme: #1873d3"\>
  <!-- Loading a YouTube video. -->
  <vm-youtube video-id\="DyTCOwB0DVw" />

  <vm-ui\>
    <vm-click-to-play />
    <vm-captions />
    <vm-poster />
    <vm-spinner />
    <vm-default-settings />
    <vm-controls pin\="bottomLeft" active-duration\="2750" full-width\>
      <!-- 
        These are all predefined controls that you can easily customize. You could also build 
        your own controls completely from scratch.
      -->
      <vm-playback-control tooltip-direction\="right" />
      <vm-volume-control />
      <vm-time-progress />
      <vm-control-spacer />
      <vm-caption-control />
      <vm-pip-control keys\="p" />
      <vm-settings-control />
      <vm-fullscreen-control keys\="f" tooltip-direction\="left" />
    </vm-controls\>
  </vm-ui\>
</vm-player\>

🏗️ Frameworks
--------------

There are framework specific bindings for:

-   React
-   Vue
-   Svelte
-   Stencil
-   Angular

Keep in mind, that at its core Vime is still simply web components. Even if your framework is not mentioned in the list above, it most likely still supports Vime natively. You can check here if your framework has complete support for web components.

There are also examples for loading and using Vime with:

-   HTML
-   Rollup
-   Webpack
-   React
-   Vue 2
-   Vue 3
-   Svelte
-   Stencil
-   Angular

🖥️ Browsers
------------

Vime is forward thinking and built for the modern web. All ES6 Compatible browsers are supported, some of which are listed below.

-   Edge 79+
-   Firefox 68+
-   Chrome 61+
-   Safari 11+
-   iOS Safari 11+
-   Opera 48+

🎥 Providers
------------

-   HTML5
-   HLS
-   Dash
-   YouTube
-   Vimeo
-   Dailymotion

📖 Documentation
----------------

Documentation can be found at https://vimejs.com.

🙋 Support
----------

Feel free to join our Discord channel if you'd like help with anything related to Vime. Please remember to be respectful and patient as this is a community driven project.

🔨 Contributing
---------------

If you'd like to contribute and help in building a better media player for the web, then everything you need to get started can be found in the Contributing Guide.

❤️ Sponsors
-----------

A huge thanks to our sponsors who support open-source projects like Vime.
