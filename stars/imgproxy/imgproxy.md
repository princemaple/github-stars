---
project: imgproxy
stars: 10196
description: Fast and secure standalone server for resizing, processing, and converting images on the fly
url: https://github.com/imgproxy/imgproxy
---

**Website | Blog | Documentation | imgproxy Pro**

* * *

imgproxy is a fast and secure standalone server for resizing, processing, and converting images. The guiding principles behind imgproxy are speed, security, and simplicity.

imgproxy is able to quickly and easily resize, process, and optimize images on the fly, and it's well-equipped to handle a large amount of image processing. imgproxy is a drop-in replacement for all the image processing code inside your web application (such as using image processing libraries or calling command-line tools). With imgproxy, you don’t need to repeatedly re-prepare images to fit your design every time it changes, as imgproxy does this on demand.

To get an even better introduction and to dive deeper into the nitty-gritty details, check out this article by Evil Martians: imgproxy: Resize your images instantly and securely

_Photo by Joshua Patton_

✨ Features
----------

imgproxy is packed with features to the brim to cover all your image processing needs:

Feature

imgproxy OSS

imgproxy Pro

Image formats

Basic formats: JPEG, PNG, GIF, WebP, AVIF, JPEG XL, and more

Preview generation for video, PDF, and Photoshop documents

Processing

Resizing, cropping, rotating, watermarking, filters

Getting image info, advanced watermarking, color adjustment

Optimization

Color profile and metadata stripping, PNG quantization

Advanced compression settings, GIF to MP4 conversion, SVG minification

Smart features

Simple smart cropping, auto-quality by file size

Object detection, advanced smart cropping, auto-quality by SSIM, best format selection

Check out the full feature list for more details.

🛠️ How it works
----------------

imgproxy works as a standalone HTTP server. You provide it with a source image URL and a set of processing options via a specially crafted URL, and imgproxy fetches the image, processes it according to your specifications, and serves the resulting image back to you. You can use imgproxy URLs directly in your HTML, CSS, or JavaScript code, just like you would with any other image URL.

This way, imgproxy offloads all the image processing work from your application. The only thing your application needs to do is to generate imgproxy URLs with the desired processing options.

⚖️ Main principles
------------------

### Simplicity

> Keep it simple, stupid!

We believe that software should be simple yet powerful. If your grandma can't get it up and running, you should make it simpler. That's why we designed imgproxy to be ready to use in a couple of minutes with minimal configuration. Check out the Getting Started guide to see how easy it is.

> No code is better than no code.

We believe in the single responsibility principle. If something can be done better outside of imgproxy, we won't reinvent the wheel. As a couple of examples:

-   HTTPS support sounds like a must-have feature for a web server. However, imgproxy will live behind a CDN, a load balancer, or a reverse proxy in a production environment anyway, so there is no need to implement HTTPS support inside imgproxy itself.
-   Rounding image corners or applying masks sounds useful, but doing this with CSS is way easier and more flexible.

### Speed

We strive to tune every little piece of imgproxy to make it as fast as possible.

imgproxy takes advantage of probably the most efficient image processing library out there – libvips. It’s scary fast and comes with a very low memory footprint. Our extensive experience with libvips has enabled us to optimize our image-processing pipeline to its maximum.

You can take a look at some benchmarking results and compare imgproxy with some well-known alternatives in our benchmark report.

### Security

Image processing is a wide attack surface. That's why we treat security very seriously. imgproxy offers several security measures that enable you to strike the optimal balance between security and usability for your specific use case. For example:

-   imgproxy supports signing image URLs to prevent abusing your image processing server for denial-of-service attacks or simply using it for the attacker's own needs.
-   imgproxy checks the image type before fully downloading it to prevent unwanted resource consumption.
-   imgproxy checks the real image dimensions before decoding it to prevent so-called "image bombs", like those described in this doc.
-   imgproxy supports authorization by HTTP header to prevent direct access to it, bypassing your CDN or caching server.
-   imgproxy allows restricting image sources, maximum image file size, processing options, etc.

Check out our documentation for more details on security features.

🚀 Getting started
------------------

The easiest and recommended way to run imgproxy is using Docker. It's just a matter of a single command:

docker run -p 8080:8080 -it ghcr.io/imgproxy/imgproxy:latest

That's it! imgproxy is ready to accept image processing requests at `http://localhost:8080`.

Check out the Getting Started guide for a step-by-step tutorial on how to get your first image processed with imgproxy.

📚 Documentation
----------------

You can find the full documentation at docs.imgproxy.net.

💙 Supporting imgproxy
----------------------

imgproxy is not a side project; it's what we do for a living. We work hard to make it better every day. If you find imgproxy useful and want to support its development, here are some ways you can do that:

-   **imgproxy Pro subscription.** imgproxy Pro is a more feature-rich version of imgproxy. By subscribing to imgproxy Pro, you not only support the development of imgproxy but also get access to advanced features and priority support.
-   **Sponsorship.** If you don't need the Pro features but still want to support the project, consider sponsoring us on GitHub Sponsors.
-   **Spread the word.** If you like imgproxy, give it a shoutout. We don't spend much on marketing, and imgproxy's popularity is primarily a result of our valued users sharing it on social media and blogs.

🙏 Special thanks
-----------------

Many thanks to:

-   Evil Martians for providing a steady launch pad for imgproxy
-   Roman Shamin for the awesome logo and website design
-   John Cupitt and Kleis Auke Wolthuizen for developing libvips and for helping me optimize its usage with imgproxy
-   Kirill Kuznetsov for the Helm chart

📄 License
----------

imgproxy is licensed under the MIT license.

See LICENSE for the full license text.

⚠️ Security Contact
-------------------

To report a security vulnerability, please contact us at security@imgproxy.net. We will coordinate the fix and disclosure.
