---
project: libvips
stars: 10910
description: A fast image processing library with low memory needs.
url: https://github.com/libvips/libvips
---

libvips: an image processing library
====================================

Introduction
============

libvips is a demand-driven, horizontally threaded image processing library. Compared to similar libraries, libvips runs quickly and uses little memory. libvips is licensed under the LGPL-2.1-or-later.

It has around 300 operations covering arithmetic, histograms, convolution, morphological operations, frequency filtering, colour, resampling, statistics and others. It supports a large range of numeric types, from 8-bit int to 128-bit complex. Images can have any number of bands. It supports a good range of image formats, including JPEG, JPEG 2000, JPEG XL, TIFF, PNG, WebP, HEIC, AVIF, FITS, Matlab, OpenEXR, PDF, SVG, HDR, PPM / PGM / PFM, CSV, GIF, Analyze, NIfTI, DeepZoom, and OpenSlide. It can also load images via ImageMagick or GraphicsMagick, letting it work with formats like DICOM.

It comes with bindings for C, C++, and the command-line. Full bindings are available for:

Language

Binding

Ruby

ruby-vips

Python

pyvips

PHP

php-vips

C# / .NET

NetVips

Go

vips-gen

Lua

lua-vips

Crystal

crystal-vips

Elixir

vix

Java

vips-ffm

Nim

libvips-nim

libvips is used as an image processing engine by:

Mastodon

sharp (on Node.js)

imgproxy

wsrv.nl

bimg

Ruby on Rails

CarrierWave

MediaWiki

and others. The official libvips GUI is nip2, a strange combination of a spreadsheet and a photo editor.

Install
=======

There are packages for most Unix-like operating systems, including macOS. Check your package manager.

There are binaries for Windows in releases.

The libvips website has detailed install notes.

Building from source
====================

libvips uses the Meson build system, version 0.56 or later. Meson can use `ninja`, Visual Studio or XCode as a backend, so you'll also need one of them.

libvips must have `build-essential`, `pkg-config`, `libglib2.0-dev`, `libexpat1-dev`. See the **Dependencies** section below for a full list of the libvips optional dependencies.

There are basic bash completions in `completions/`, see the README in there.

Cheatsheet
----------

```
cd libvips-x.y.x
meson setup build --prefix /my/install/prefix
cd build
meson compile
meson test
meson install
```

Check the output of `meson setup` carefully and make sure it found everything you wanted it to find. Add arguments to `meson setup` to change the build configuration.

-   Add flags like `-Dnsgif=false` to turn libvips options on and off, see `meson_options.txt` for a list of all the build options libvips supports.
    
-   Add flags like `-Dmagick=disabled` to turn libvips dependencies on and off, see `meson_options.txt` and the list below for a summary of all the libvips dependencies.
    
-   You might need to add `--libdir lib` on Debian if you don't want the arch name in the library path.
    
-   Add `--default-library static` for a static build.
    
-   Use e.g. `CC=clang CXX=clang++ meson setup ...` to change compiler.
    
-   You can have an alternative build directory, pick whatever names you like, for example one for release and one for debug.
    

There's a more comprehensive test suite you can run once libvips has been installed. Use `pytest` in the libvips base directory.

Optional dependencies
---------------------

If suitable versions are found, libvips will add support for the following libraries automatically. Packages are generally found with `pkg-config`, so make sure that is working.

### libjpeg

Anything that is compatible with the IJG JPEG library. Use `mozjpeg` if you can. Another option is `libjpeg-turbo`.

### libultrahdr (libuhdr)

If present, libvips will load UltraHDR images with Google's libultrahdr library. The `pkg-config` name is libuhdr.

### libexif

If available, libvips adds support for EXIF metadata in JPEG files.

### librsvg

The usual SVG loader. If this is not present, vips will try to load SVGs via imagemagick instead.

### libraw

The usual camera RAW loader. If this is not present, vips will try to load raw camera images via imagemagick instead.

### PDFium

If present, libvips will attempt to load PDFs with PDFium. Download the prebuilt pdfium binary from:

https://github.com/bblanchon/pdfium-binaries/releases/latest

Untar to the libvips install prefix, for example:

```
cd ~/vips
tar xf ~/pdfium-linux.tgz
```

Create a `pdfium.pc` like this (update the version number):

```
VIPSHOME=$HOME/vips
mkdir -p $VIPSHOME/lib/pkgconfig
cat > $VIPSHOME/lib/pkgconfig/pdfium.pc << EOF
prefix=$VIPSHOME
exec_prefix=\${prefix}
libdir=\${exec_prefix}/lib
includedir=\${prefix}/include

Name: pdfium
Description: PDFium
Version: 4290
Libs: -L\${libdir} -lpdfium
Cflags: -I\${includedir}
EOF
```

If PDFium is not detected, libvips will look for `poppler-glib` instead.

### poppler-glib

The Poppler PDF renderer, with a glib API. If this is not present, vips will try to load PDFs via imagemagick.

### cgif

If available, libvips will save GIFs with cgif. If this is not present, vips will try to save gifs via imagemagick instead.

### libarchive

If available, libvips adds support for creating image pyramids with `dzsave`.

### libtiff

The TIFF library. It needs to be built with support for JPEG and ZIP compression. 3.4b037 and later are known to be OK.

### fftw3

If libvips finds this library, it uses it for fourier transforms.

### lcms2

If present, `vips_icc_import()`, `vips_icc_export()` and `vips_icc_transform()` can be used to manipulate images with ICC profiles.

### libpng

If present, libvips will load and save PNG files using libpng. If not, it will look for the spng package.

### libimagequant, quantizr

If one of these quantisation packages is present, libvips can write 8-bit palette-ised PNGs and GIFs.

### ImageMagick, or optionally GraphicsMagick

If available, libvips adds support for loading and saving all libMagick-supported image file types. You can enable and disable load and save separately.

Imagemagick 6.9+ needs to have been built with `--with-modules`. Most packaged IMs are, I think.

If you are going to be using libvips with untrusted images, perhaps in a web server, for example, you should consider the security implications of enabling a package with such a large attack surface.

### pangocairo

If available, libvips adds support for text rendering. You need the package pangocairo in `pkg-config --list-all`.

### highway

If present, libvips will accelerate some operations with SIMD. If not, it will look for the orc-0.4 package.

### matio

If available, vips can load images from Matlab save files.

### cfitsio

If available, vips can load FITS images.

### libwebp

If available, vips can load and save WebP images.

### libniftiio

If available, vips can load and save NIfTI images.

### OpenEXR

If available, libvips will directly read (but not write, sadly) OpenEXR images.

### OpenJPEG

If available, libvips will read and write JPEG2000 images.

### libjxl

If available, libvips will read and write JPEG-XL images.

### OpenSlide

If available, libvips can load OpenSlide-supported virtual slide files: Aperio, Hamamatsu, Leica, MIRAX, Sakura, Trestle, and Ventana.

### libheif

If available, libvips can load and save HEIC and AVIF images. Your libheif (in turn) needs to be built with the correct decoders and encoders. You can check with eg.:

$ heif-convert --list-decoders
HEIC decoders:
\- libde265 = libde265 HEVC decoder, version 1.0.9
AVIF decoders:
\- dav1d = dav1d v6.6.0
\- aom = AOMedia Project AV1 Decoder v3.5.0
$ heif-enc --list-encoders
HEIC encoders:
\- x265 = x265 HEVC encoder (3.5+1-f0c1022b6) \[default\]
AVIF encoders:
\- aom = AOMedia Project AV1 Encoder v3.5.0 \[default\]
\- svt = SVT-AV1 encoder v1.1.0
\- rav1e = Rav1e encoder

Contributors
============

### Code Contributors

This project exists thanks to all the people who contribute.

### Organizations

We've had generous financial support from our sponsors. Thank you very much!
