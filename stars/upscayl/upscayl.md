---
project: upscayl
stars: 42860
description: 🆙 Upscayl - #1 Free and Open Source AI Image Upscaler for Linux, MacOS and Windows.
url: https://github.com/upscayl/upscayl
---

v2.15 is out! 🥳 Download Now ⬇️
================================

### Special thanks to our sponsors:

**Warp, the intelligent terminal for developers**

Use images as AI context in your terminal!

**Requestly - Free & Open-Source alternative to Postman**

All-in-one platform to Test, Mock and Intercept APIs.

  
  

🆙 Upscayl
==========

#### Free and Open Source AI Image Upscaler

Upscayl lets you enlarge and enhance low-resolution images using advanced AI algorithms. Enlarge images without losing quality. It's almost like magic! 🎩🪄

**https://upscayl.org**

Demo.Showcase.mp4

Contents
========

-   👨‍💻 Installation
    -   🐧 Linux
    -   🍎 macOS
    -   🐌 Windows
-   👨‍🏫 Documentation - Tutorials and Guides
-   ⚖️ Demo Results (Before and After)
-   🤫 Roadmap
-   🛠 Developing Upscayl
-   🤓 FAQ
-   🎁 Donate and support the project
-   ❤ Credits

👨‍💻 Installation
==================

Important

You'll need a Vulkan compatible GPU (Graphics Card) to upscale images. Many iGPUs (integrated graphics) do not work but, no harm in trying :)

🐧 Linux
--------

Upscayl should be available on the software listings of most Linux operating systems. Your distro's Store app might also support the Flatpak or Snap version.

### 💼 Portable Method

1.  Go to releases section or our official website.
2.  Download the `upscayl-x.x.x-linux.AppImage` file.
3.  Right Click AppImage -> Go to Permissions tab -> Check 'allow file to execute' and then double click the file to run Upscayl.

_You can also choose to install using other formats like RPM (Fedora), DEB (Debian/Ubuntu based), and ZIP (Any x86 Linux OS)._

🍎 macOS
--------

(MacOS 12 and later)

1.  Go to releases section or our official website.
2.  Download the `upscayl-x.x.x-mac.dmg` file.
3.  Double click dmg, drag Upscayl icon into Applications folder.
4.  Open Finder, click 'Applications' tab in the left sidebar. Find Upscayl and right click on it. Select 'Open'.
5.  In the window that appears, press 'Open' yet again.

### 🍺 Homebrew

`brew install --cask upscayl`

🐌 Windows
----------

(Windows 10 and later)

1.  Go to releases section or our official website.
2.  Download the `upscayl-x.x.x-win.exe` file.
3.  Double click exe file to launch.
4.  If you get a SmartScreen warning - click 'More Info' and then 'Run Anyway' OR press 'YES' on the unverified publisher dialog.
5.  Follow the installation steps.
6.  Profit!

👨‍🏫 Documentation - Tutorials and Guides
==========================================

Check out our Documentation here.

-   Try out even more new models!
-   Convert your own models
-   Compatibility List
-   Troubleshooting

⚖️ Results
==========

Check out Upscayl before/after comparisons here.

🤫 Roadmap
==========

You can track all the progress here: https://github.com/orgs/upscayl/projects/1

-   Fix bugs
-   Make the whole world use FOSS (WIP 🚧)

🛠 Development
==============

I recommend using Volta: https://volta.sh for installing Node.js. Download and install volta, then do: `volta install node`.

🏃 Running
----------

Note

If you are not willing to install git, you can skip the first line, download the source zip and extract it to `upscayl` instead and carry on with the rest of the instructions.

git clone https://github.com/upscayl/upscayl
cd upscayl

# INSTALL DEPENDENCIES
npm install

# RUN THE DEVELOPMENT SERVER LOCALLY
#\# YOUR LOGS WILL NOW APPEAR IN THE TERMINAL
npm run start

🏗️ Building
------------

# INSTALL DEPENDENCIES
npm install

# PACKAGE THE APP
npm run dist

# PUBLISH THE APP, MAKE SURE TO ADD GH\_TOKEN= IN SHELL
# ONLY DO THIS IF YOU'RE A MAINTAINER
npm run publish-app

🤓 FAQ
======

-   **How does Upscayl work?**
    -   Upscayl uses AI models to enhance your images by guessing what the details could be. It uses Real-ESRGAN and Vulkan architecture to achieve this. Our backend is fully open-source under the AGPLv3 license.
-   **I don't see a drastic change in my upscaled image. Why is that?**
    -   Upscayl can enhance low resolution images and images that are pixelated but it cannot de-blur or do focus adjustment on your image. If your image is out-of-focus or totally blurred, Upscayl is not the right tool for it. Please use images that are similar to the examples we've given here.
-   **Is there a CLI available?**
    -   The CLI tool is called upscayl-ncnn.
-   **Do I need a GPU for this to work?**
    -   Yes, unfortunately. NCNN Vulkan requires a Vulkan-compatible GPU. Upscayl won't work with **most** iGPUs or CPUs. But hey, no harm in trying ;)
        -   @Wyrdgirn has contributed a workaround for Windows and Linux in #390! Nobody knows how to manipulate the macOS and Haiku frameworks...
-   **I stopped the magic Batch Upscayl and my images haven't been processed, compressed, or are in the wrong scale!**
    -   When a model doesn't support an action, Upscayl will finish upscayling all the images first before post-processing them. What this means is that you should simply **wait** for the process to finish.
-   **How can I contribute?**
    -   You can report issues, fix code and add features by submitting PRs, or donate! 😊
-   **What's the GPU ID for?**
    -   It is for selecting which GPU to use. The specific procedure is detailed in the Wiki.
        -   Note that for Windows systems, if Upscayl is not set to performance mode, the system may override this setting.
-   **Where do I find more models?**
    -   More models can be taken from here: https://github.com/upscayl/custom-models

🎁 Donate
=========

❤ Credits
=========

-   Real-ESRGAN for their wonderful research work. Real-ESRGAN: Copyright (c) 2021, Xintao Wang
-   @JanDeDinoMan, @xanderfrangos, @Fdawgs, @keturn for their code contributions
-   @aaronliu0130 for providing community support :)
-   Helaman for their HFA2k model (included as "High Fidelity")
-   Foolhardy for their Remacri model.
-   Kim2091 for their Ultrasharp and Ultramix Balanced model.
-   @NicKoehler for their amazing logo :)

Copyright © 2023 - **Upscayl**  
By Nayam Amarshe and TGS963  
Made with 🖱 & ⌨
