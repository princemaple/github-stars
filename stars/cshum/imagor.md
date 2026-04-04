---
project: imagor
stars: 3927
description: Fast, secure image processing server and Go library, using libvips
url: https://github.com/cshum/imagor
---

imagor
======

imagor is a fast, secure image processing server and Go library.

imagor uses one of the most efficient image processing library libvips with Go binding vipsgen. It is typically 4-8x faster than using the quickest ImageMagick settings. imagor implements libvips streaming that facilitates parallel processing pipelines, achieving high network throughput.

imagor features a ton of image processing use cases, available as a HTTP server with first-class Docker support. It adopts the thumbor URL syntax representing a high-performance drop-in replacement.

imagor is a Go library built with speed, security and extensibility in mind. Alongside there is imagorvideo bringing video thumbnail capability through ffmpeg C bindings.

### Quick Start

docker run -p 8000:8000 shumc/imagor -imagor-unsafe -imagor-auto-webp

Original images:

```
https://raw.githubusercontent.com/cshum/imagor/master/testdata/gopher.png
https://raw.githubusercontent.com/cshum/imagor/master/testdata/dancing-banana.gif
https://raw.githubusercontent.com/cshum/imagor/master/testdata/gopher-front.png
```

Try out the following image URLs:

```
http://localhost:8000/unsafe/fit-in/200x200/filters:fill(white)/https://raw.githubusercontent.com/cshum/imagor/master/testdata/gopher.png
http://localhost:8000/unsafe/200x200/smart/filters:fill(white):format(jpeg):quality(80)/https://raw.githubusercontent.com/cshum/imagor/master/testdata/gopher.png
http://localhost:8000/unsafe/fit-in/-180x180/10x10/filters:hue(290):saturation(100):fill(yellow)/raw.githubusercontent.com/cshum/imagor/master/testdata/gopher.png
http://localhost:8000/unsafe/30x40:100x150/filters:fill(cyan)/raw.githubusercontent.com/cshum/imagor/master/testdata/dancing-banana.gif
http://localhost:8000/unsafe/fit-in/200x150/filters:fill(yellow):watermark(raw.githubusercontent.com/cshum/imagor/master/testdata/gopher-front.png,repeat,bottom,0,40,40)/raw.githubusercontent.com/cshum/imagor/master/testdata/dancing-banana.gif
```

Note

Ready to dive deeper? Check out Documentation
