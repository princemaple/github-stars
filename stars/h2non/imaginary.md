---
project: imaginary
stars: 5886
description: Fast, simple, scalable, Docker-ready HTTP microservice for high-level image processing
url: https://github.com/h2non/imaginary
---

imaginary
=========

**Fast HTTP microservice** written in Go **for high-level image processing** backed by bimg and libvips. `imaginary` can be used as private or public HTTP service for massive image processing with first-class support for Docker & Fly.io. It's almost dependency-free and only uses `net/http` native package without additional abstractions for better performance.

Supports multiple image operations exposed as a simple HTTP API, with additional optional features such as **API token authorization**, **URL signature protection**, **HTTP traffic throttle** strategy and **CORS support** for web clients.

`imaginary` **can read** images **from HTTP POST payloads**, **server local path** or **remote HTTP servers**, supporting **JPEG**, **PNG**, **WEBP**, **HEIF**, and optionally **TIFF**, **PDF**, **GIF** and **SVG** formats if `libvips@8.3+` is compiled with proper library bindings.

`imaginary` is able to output images as JPEG, PNG and WEBP formats, including transparent conversion across them.

`imaginary` optionally **supports image placeholder fallback mechanism** in case of image processing error or server error of any nature, hence an image will be always returned by imaginary even in case of error, trying to match the requested image size and format type transparently. The error details will be provided in the response HTTP header `Error` field serialized as JSON.

`imaginary` uses internally `libvips`, a powerful and efficient library written in C for fast image processing which requires a low memory footprint and it's typically 4x faster than using the quickest ImageMagick and GraphicsMagick settings or Go native `image` package, and in some cases it's even 8x faster processing JPEG images.

To get started, take a look the installation steps, usage cases and API docs.

Contents
--------

-   Supported image operations
-   Prerequisites
-   Installation
    -   Docker
    -   Fly.io
    -   Cloud Foundry
    -   Google Cloud Run
-   Recommended resources
-   Production notes
-   Scalability
-   Clients
-   Performance
-   Benchmark
-   Command-line usage
-   HTTP API
    -   Authorization
    -   URL signature
    -   Errors
    -   Form data
    -   Params
    -   Endpoints
-   Logging
    -   Fluentd log ingestion
-   Authors
-   License

Supported image operations
--------------------------

-   Resize
-   Enlarge
-   Crop
-   SmartCrop (based on libvips built-in algorithm)
-   Rotate (with auto-rotate based on EXIF orientation)
-   AutoRotate with further image transformations (based on EXIF metadata orientation)
-   Flip (with auto-flip based on EXIF metadata)
-   Flop
-   Zoom
-   Thumbnail
-   Fit
-   Pipeline of multiple independent image transformations in a single HTTP request.
-   Configurable image area extraction
-   Embed/Extend image, supporting multiple modes (white, black, mirror, copy or custom background color)
-   Watermark (customizable by text)
-   Watermark image
-   Custom output color space (RGB, black/white...)
-   Format conversion (with additional quality/compression settings)
-   Info (image size, format, orientation, alpha...)
-   Reply with default or custom placeholder image in case of error.
-   Blur

Prerequisites
-------------

-   libvips 8.8+ (8.9+ recommended)
-   C compatible compiler such as gcc 4.6+ or clang 3.0+
-   Go 1.12+

Installation
------------

go get -u github.com/h2non/imaginary

Also, be sure you have the latest version of `bimg`:

go get -u github.com/h2non/bimg

### libvips

Run the following script as `sudo` (supports OSX, Debian/Ubuntu, Redhat, Fedora, Amazon Linux):

curl -s https://raw.githubusercontent.com/h2non/bimg/master/preinstall.sh | sudo bash -

The install script requires `curl` and `pkg-config`

### Docker

See Dockerfile for image details.

Fetch the image (comes with latest stable Go and `libvips` versions)

```
docker pull h2non/imaginary
```

Start the container with optional flags (default listening on port 9000)

```
docker run -p 9000:9000 h2non/imaginary -cors
```

Start the container enabling remote URL source image processing via GET requests and `url` query param.

```
docker run -p 9000:9000 h2non/imaginary -p 9000 -enable-url-source
```

Start the container enabling local directory image process via GET requests and `file` query param.

```
docker run -p 9000:9000 h2non/imaginary -p 900 -mount /volume/images
```

Start the container in debug mode:

```
docker run -p 9000:9000 -e "DEBUG=*" h2non/imaginary
```

Enter to the interactive shell in a running container

```
sudo docker exec -it <containerIdOrName> bash
```

Stop the container

```
docker stop h2non/imaginary
```

For more usage examples, see the command line usage.

All Docker images tags are available here.

#### Docker Compose

You can add `imaginary` to your `docker-compose.yml` file:

version: "3"
services:
  imaginary:
    image: h2non/imaginary:latest
    # optionally mount a volume as local image source
    volumes:
      - images:/mnt/data
    environment:
       PORT: 9000
    command: \-enable-url-source -mount /mnt/data
    ports:
      - "9000:9000"

### Fly.io

Deploy imaginary in seconds close to your users in Fly.io cloud by clicking on the button below:

#### About Fly.io

Fly is a platform for applications that need to run globally. It runs your code close to users and scales compute in cities where your app is busiest. Write your code, package it into a Docker image, deploy it to Fly's platform and let that do all the work to keep your app snappy.

You can learn more about how Fly.io can reduce latency and provide a better experience by serving traffic close to your users location.

#### Global image service tutorial

Learn more about how to run a custom deployment of imaginary on the Fly.io cloud.

### CloudFoundry

Assuming you have cloudfoundry account, bluemix or pivotal and command line utility installed.

Clone this repository:

```
git clone https://github.com/h2non/imaginary.git
```

Push the application

```
cf push -b https://github.com/yacloud-io/go-buildpack-imaginary.git imaginary-inst01 --no-start
```

Define the library path

```
cf set-env imaginary-inst01 LD_LIBRARY_PATH /home/vcap/app/vendor/vips/lib
```

Start the application

```
cf start imaginary-inst01
```

### Google Cloud Run

Click to deploy on Google Cloud Run:

### Recommended resources

Given the multithreaded native nature of Go, in terms of CPUs, most cores means more concurrency and therefore, a better performance can be achieved. From the other hand, in terms of memory, 512MB of RAM is usually enough for small services with low concurrency (<5 requests/second). Up to 2GB for high-load HTTP service processing potentially large images or exposed to an eventual high concurrency.

If you need to expose `imaginary` as public HTTP server, it's highly recommended to protect the service against DDoS-like attacks. `imaginary` has built-in support for HTTP concurrency throttle strategy to deal with this in a more convenient way and mitigate possible issues limiting the number of concurrent requests per second and caching the awaiting requests, if necessary.

### Production notes

In production focused environments it's highly recommended to enable the HTTP concurrency throttle strategy in your `imaginary` servers.

The recommended concurrency limit per server to guarantee a good performance is up to `20` requests per second.

You can enable it simply passing a flag to the binary:

```
$ imaginary -concurrency 20
```

### Memory issues

In case you are experiencing any persistent unreleased memory issues in your deployment, you can try passing this environment variables to `imaginary`:

```
MALLOC_ARENA_MAX=2 imaginary -p 9000 -enable-url-source
```

### Graceful shutdown

When you use a cluster, it is necessary to control how the deployment is executed, and it is very useful to finish the containers in a controlled manner.

You can use the next command:

```
$ ps auxw | grep 'bin/imaginary' | awk 'NR>1{print buf}{buf = $2}' | xargs kill -TERM > /dev/null 2>&1
```

### Scalability

If you're looking for a large scale solution for massive image processing, you should scale `imaginary` horizontally, distributing the HTTP load across a pool of imaginary servers.

Assuming that you want to provide a high availability to deal efficiently with, let's say, 100 concurrent req/sec, a good approach would be using a front end balancer (e.g: HAProxy) to delegate the traffic control flow, ensure the quality of service and distribution the HTTP across a pool of servers:

```
        |==============|
        |  Dark World  |
        |==============|
              ||||
        |==============|
        |   Balancer   |
        |==============|
           |       |
          /         \
         /           \
        /             \
 /-----------\   /-----------\
 | imaginary |   | imaginary | (*n)
 \-----------/   \-----------/
```

Clients
-------

-   node.js

Feel free to send a PR if you created a client for other language.

Performance
-----------

libvips is probably the faster open source solution for image processing. Here you can see some performance test comparisons for multiple scenarios:

-   libvips speed and memory usage
-   bimg (Go library with C bindings to libvips)

Benchmark
---------

See benchmark.sh for more details

Environment: Go 1.4.2. libvips-7.42.3. OSX i7 2.7Ghz

```
Requests  [total]       200
Duration  [total, attack, wait]   10.030639787s, 9.949499515s, 81.140272ms
Latencies [mean, 50, 95, 99, max]   83.124471ms, 82.899435ms, 88.948008ms, 95.547765ms, 104.384977ms
Bytes In  [total, mean]     23443800, 117219.00
Bytes Out [total, mean]     175517000, 877585.00
Success   [ratio]       100.00%
Status Codes  [code:count]      200:200
```

### Conclusions

`imaginary` can deal efficiently with up to 20 request per second running in a multicore machine, where it crops a JPEG image of 5MB and spending per each request less than 100 ms

The most expensive image operation under high concurrency scenarios (> 20 req/sec) is the image enlargement, which requires a considerable amount of math operations to scale the original image. In this kind of operation the required processing time usually grows over the time if you're stressing the server continuously. The advice here is as simple as taking care about the number of concurrent enlarge operations to avoid server performance bottlenecks.

Command-line usage
------------------

```
Usage:
  imaginary -p 80
  imaginary -cors
  imaginary -concurrency 10
  imaginary -path-prefix /api/v1
  imaginary -enable-url-source
  imaginary -disable-endpoints form,health,crop,rotate
  imaginary -enable-url-source -allowed-origins http://localhost,http://server.com,http://*.example.org
  imaginary -enable-url-source -enable-auth-forwarding
  imaginary -enable-url-source -authorization "Basic AwDJdL2DbwrD=="
  imaginary -enable-placeholder
  imaginary -enable-url-source -placeholder ./placeholder.jpg
  imaginary -enable-url-signature -url-signature-key 4f46feebafc4b5e988f131c4ff8b5997
  imaginary -enable-url-source -forward-headers X-Custom,X-Token
  imaginary -h | -help
  imaginary -v | -version

Options:
  -a <addr>                 Bind address [default: *]
  -p <port>                 Bind port [default: 8088]
  -h, -help                 Show help
  -v, -version              Show version
  -path-prefix <value>      Url path prefix to listen to [default: "/"]
  -cors                     Enable CORS support [default: false]
  -gzip                     Enable gzip compression (deprecated) [default: false]
  -disable-endpoints        Comma separated endpoints to disable. E.g: form,crop,rotate,health [default: ""]
  -key <key>                Define API key for authorization
  -mount <path>             Mount server local directory
  -http-cache-ttl <num>     The TTL in seconds. Adds caching headers to locally served files.
  -http-read-timeout <num>  HTTP read timeout in seconds [default: 60]
  -http-write-timeout <num> HTTP write timeout in seconds [default: 60]
  -enable-url-source        Enable remote HTTP URL image source processing (?url=http://..)
  -enable-placeholder       Enable image response placeholder to be used in case of error [default: false]
  -enable-auth-forwarding   Forwards X-Forward-Authorization or Authorization header to the image source server. -enable-url-source flag must be defined. Tip: secure your server from public access to prevent attack vectors
  -forward-headers          Forwards custom headers to the image source server. -enable-url-source flag must be defined.
  -enable-url-signature     Enable URL signature (URL-safe Base64-encoded HMAC digest) [default: false]
  -url-signature-key        The URL signature key (32 characters minimum)
  -allowed-origins <urls>   Restrict remote image source processing to certain origins (separated by commas). Note: Origins are validated against host *AND* path.
  -max-allowed-size <bytes> Restrict maximum size of http image source (in bytes)
  -max-allowed-resolution <megapixels> Restrict maximum resolution of the image [default: 18.0]
  -certfile <path>          TLS certificate file path
  -keyfile <path>           TLS private key file path
  -authorization <value>    Defines a constant Authorization header value passed to all the image source servers. -enable-url-source flag must be defined. This overwrites authorization headers forwarding behavior via X-Forward-Authorization
  -placeholder <path>       Image path to image custom placeholder to be used in case of error. Recommended minimum image size is: 1200x1200
  -concurrency <num>        Throttle concurrency limit per second [default: disabled]
  -burst <num>              Throttle burst max cache size [default: 100]
  -mrelease <num>           OS memory release interval in seconds [default: 30]
  -cpus <num>               Number of used cpu cores.
                            (default for current machine is 8 cores)
  -log-level                Set log level for http-server. E.g: info,warning,error [default: info].
                            Or can use the environment variable GOLANG_LOG=info.
```

Start the server in a custom port:

imaginary -p 8080

Also, you can pass the port as environment variable:

PORT=8080 imaginary

Enable HTTP server throttle strategy (max 10 requests/second):

```
imaginary -p 8080 -concurrency 10
```

Enable remote URL image fetching (then you can do GET request passing the `url=http://server.com/image.jpg` query param):

```
imaginary -p 8080 -enable-url-source
```

Mount local directory (then you can do GET request passing the `file=image.jpg` query param):

```
imaginary -p 8080 -mount ~/images
```

Enable authorization header forwarding to image origin server. `X-Forward-Authorization` or `Authorization` (by priority) header value will be forwarded as `Authorization` header to the target origin server, if one of those headers are present in the incoming HTTP request. Security tip: secure your server from public access to prevent attack vectors when enabling this option:

```
imaginary -p 8080 -enable-url-source -enable-auth-forwarding
```

Or alternatively you can manually define an constant Authorization header value that will be always sent when fetching images from remote image origins. If defined, `X-Forward-Authorization` or `Authorization` headers won't be forwarded, and therefore ignored, if present. **Note**:

```
imaginary -p 8080 -enable-url-source -authorization "Bearer s3cr3t"
```

Send fixed caching headers in the response. The headers can be set in either "cache nothing" or "cache for N seconds". By specifying `0` imaginary will send the "don't cache" headers, otherwise it sends headers with a TTL. The following example informs the client to cache the result for 1 year:

```
imaginary -p 8080 -enable-url-source -http-cache-ttl 31556926
```

Enable placeholder image HTTP responses in case of server error/bad request. The placeholder image will be dynamically and transparently resized matching the expected image `width`x`height` define in the HTTP request params. Also, the placeholder image will be also transparently converted to the desired image type defined in the HTTP request params, so the API contract should be maintained as much better as possible.

This feature is particularly useful when using `imaginary` as public HTTP service consumed by Web clients. In case of error, the appropriate HTTP status code will be used to reflect the error, and the error details will be exposed serialized as JSON in the `Error` response HTTP header, for further inspection and convenience for API clients.

```
imaginary -p 8080 -enable-placeholder -enable-url-source
```

You can optionally use a custom placeholder image. Since the placeholder image should fit a variety of different sizes, it's recommended to use a large image, such as `1200`x`1200`. Supported custom placeholder image types are: `JPEG`, `PNG` and `WEBP`.

```
imaginary -p 8080 -placeholder=placeholder.jpg -enable-url-source
```

Enable URL signature (URL-safe Base64-encoded HMAC digest).

This feature is particularly useful to protect against multiple image operations attacks and to verify the requester identity.

```
imaginary -p 8080 -enable-url-signature -url-signature-key 4f46feebafc4b5e988f131c4ff8b5997
```

It is recommended to pass key as environment variables:

```
URL_SIGNATURE_KEY=4f46feebafc4b5e988f131c4ff8b5997 imaginary -p 8080 -enable-url-signature
```

Increase libvips threads concurrency (experimental):

```
VIPS_CONCURRENCY=10 imaginary -p 8080 -concurrency 10
```

Enable debug mode:

```
DEBUG=* imaginary -p 8080
```

Or filter debug output by package:

```
DEBUG=imaginary imaginary -p 8080
```

Disable info logs:

```
GOLANG_LOG=error imaginary -p 8080
```

#### Examples

Reading a local image (you must pass the `-mount=<directory>` flag):

```
curl -O "http://localhost:8088/crop?width=500&height=400&file=foo/bar/image.jpg"
```

Fetching the image from a remote server (you must pass the `-enable-url-source` flag):

```
curl -O "http://localhost:8088/crop?width=500&height=400&url=https://raw.githubusercontent.com/h2non/imaginary/master/testdata/large.jpg"
```

Crop behaviour can be influenced with the `gravity` parameter. You can specify a preference for a certain region (north, south, etc.). To enable Smart Crop you can specify the value "smart" to autodetect the most interesting section to consider as center point for the crop operation:

```
curl -O "http://localhost:8088/crop?width=500&height=200&gravity=smart&url=https://raw.githubusercontent.com/h2non/imaginary/master/testdata/smart-crop.jpg"
```

#### Playground

`imaginary` exposes an ugly HTML form for playground purposes in: `http://localhost:8088/form`

HTTP API
--------

### Allowed Origins

imaginary can be configured to block all requests for images with a src URL this is not specified in the `allowed-origins` list. Imaginary will validate that the remote url matches the hostname and path of at least one origin in allowed list. Perhaps the easiest way to show how this works is to show some examples.

`allowed-origins` setting

image url

is valid

`-allowed-origins https://s3.amazonaws.com/some-bucket/`

`s3.amazonaws.com/some-bucket/images/image.png`

VALID

`-allowed-origins https://s3.amazonaws.com/some-bucket/`

`s3.amazonaws.com/images/image.png`

NOT VALID (no matching basepath)

`-allowed-origins https://s3.amazonaws.com/some-*`

`s3.amazonaws.com/some-bucket/images/image.png`

VALID

`-allowed-origins https://*.amazonaws.com/some-bucket/`

`anysubdomain.amazonaws.com/some-bucket/images/image.png`

VALID

`-allowed-origins https://*.amazonaws.com`

`anysubdomain.amazonaws.comimages/image.png`

VALID

`-allowed-origins https://*.amazonaws.com`

`www.notaws.comimages/image.png`

NOT VALID (no matching host)

`-allowed-origins https://*.amazonaws.com, foo.amazonaws.com/some-bucket/`

`bar.amazonaws.com/some-other-bucket/image.png`

VALID (matches first condition but not second)

### Authorization

imaginary supports a simple token-based API authorization. To enable it, you should pass the `-key` flag to the binary.

API token can be defined as HTTP header (`API-Key`) or query param (`key`).

Example request with API key:

```
POST /crop HTTP/1.1
Host: localhost:8088
API-Key: secret
```

### URL signature

The URL signature is provided by the `sign` request parameter.

The HMAC-SHA256 hash is created by taking the URL path (including the leading /), the request parameters (alphabetically-sorted and concatenated with & into a string). The hash is then base64url-encoded.

Here an example in Go:

```
signKey  := "4f46feebafc4b5e988f131c4ff8b5997"
urlPath  := "/resize"
urlQuery := "file=image.jpg&height=200&type=jpeg&width=300"

h := hmac.New(sha256.New, []byte(signKey))
h.Write([]byte(urlPath))
h.Write([]byte(urlQuery))
buf := h.Sum(nil)

fmt.Println("sign=" + base64.RawURLEncoding.EncodeToString(buf))
```

### Errors

`imaginary` will always reply with the proper HTTP status code and JSON body with error details.

Here an example response error when the payload is empty:

{
  "message": "Cannot read payload: no such file",
  "code": 1
}

See all the predefined supported errors here.

#### Placeholder

If `-enable-placeholder` or `-placeholder <image path>` flags are passed to `imaginary`, a placeholder image will be used in case of error or invalid request input.

If `-enable-placeholder` is passed, the default `imaginary` placeholder image will be used, however you can customized it via `-placeholder` flag, loading a custom compatible image from the file system.

Since `imaginary` has been partially designed to be used as public HTTP service, including web pages, in certain scenarios the response MIME type must be respected, so the server will always reply with a placeholder image in case of error, such as image processing error, read error, payload error, request invalid request or any other.

You can customize the placeholder image passing the `-placeholder <image path>` flag when starting `imaginary`.

In this scenarios, the error message details will be exposed in the `Error` response header field as JSON for further inspection from API clients.

In some edge cases the placeholder image resizing might fail, so a 400 Bad Request will be used as response status and the `Content-Type` will be `application/json` with the proper message info. Note that this scenario won't be common.

### Form data

If you're pushing images to `imaginary` as `multipart/form-data` (you can do it as well as `image/*`), you must define at least one input field called `file` with the raw image data in order to be processed properly by imaginary.

### Params

Complete list of available params. Take a look to each specific endpoint to see which params are supported. Image measures are always in pixels, unless otherwise indicated.

-   **width** `int` - Width of image area to extract/resize
-   **height** `int` - Height of image area to extract/resize
-   **top** `int` - Top edge of area to extract. Example: `100`
-   **left** `int` - Left edge of area to extract. Example: `100`
-   **areawidth** `int` - Height area to extract. Example: `300`
-   **areaheight** `int` - Width area to extract. Example: `300`
-   **quality** `int` - JPEG image quality between 1-100. Defaults to `80`
-   **compression** `int` - PNG compression level. Default: `6`
-   **palette** `bool` - Enable 8-bit quantisation. Works with only PNG images. Default: `false`
-   **rotate** `int` - Image rotation angle. Must be multiple of `90`. Example: `180`
-   **factor** `int` - Zoom factor level. Example: `2`
-   **margin** `int` - Text area margin for watermark. Example: `50`
-   **dpi** `int` - DPI value for watermark. Example: `150`
-   **textwidth** `int` - Text area width for watermark. Example: `200`
-   **opacity** `float` - Opacity level for watermark text or watermark image. Default: `0.2`
-   **flip** `bool` - Transform the resultant image with flip operation. Default: `false`
-   **flop** `bool` - Transform the resultant image with flop operation. Default: `false`
-   **force** `bool` - Force image transformation size. Default: `false`
-   **nocrop** `bool` - Disable crop transformation. Defaults depend on the operation
-   **noreplicate** `bool` - Disable text replication in watermark. Defaults to `false`
-   **norotation** `bool` - Disable auto rotation based on EXIF orientation. Defaults to `false`
-   **noprofile** `bool` - Disable adding ICC profile metadata. Defaults to `false`
-   **stripmeta** `bool` - Remove original image metadata, such as EXIF metadata. Defaults to `false`
-   **text** `string` - Watermark text content. Example: `copyright (c) 2189`
-   **font** `string` - Watermark text font type and format. Example: `sans bold 12`
-   **color** `string` - Watermark text RGB decimal base color. Example: `255,200,150`
-   **image** `string` - Watermark image URL pointing to the remote HTTP server.
-   **type** `string` - Specify the image format to output. Possible values are: `jpeg`, `png`, `webp` and `auto`. `auto` will use the preferred format requested by the client in the HTTP Accept header. A client can provide multiple comma-separated choices in `Accept` with the best being the one picked.
-   **gravity** `string` - Define the crop operation gravity. Supported values are: `north`, `south`, `centre`, `west`, `east` and `smart`. Defaults to `centre`.
-   **file** `string` - Use image from server local file path. In order to use this you must pass the `-mount=<dir>` flag.
-   **url** `string` - Fetch the image from a remote HTTP server. In order to use this you must pass the `-enable-url-source` flag.
-   **colorspace** `string` - Use a custom color space for the output image. Allowed values are: `srgb` or `bw` (black&white)
-   **field** `string` - Custom image form field name if using `multipart/form`. Defaults to: `file`
-   **extend** `string` - Extend represents the image extend mode used when the edges of an image are extended. Defaults to `mirror`. Allowed values are: `black`, `copy`, `mirror`, `white`, `lastpixel` and `background`. If `background` value is specified, you can define the desired extend RGB color via `background` param, such as `?extend=background&background=250,20,10`. For more info, see libvips docs.
-   **background** `string` - Background RGB decimal base color to use when flattening transparent PNGs. Example: `255,200,150`
-   **sigma** `float` - Size of the gaussian mask to use when blurring an image. Example: `15.0`
-   **minampl** `float` - Minimum amplitude of the gaussian filter to use when blurring an image. Default: Example: `0.5`
-   **operations** `json` - Pipeline of image operation transformations defined as URL safe encoded JSON array. See pipeline endpoints for more details.
-   **sign** `string` - URL signature (URL-safe Base64-encoded HMAC digest)
-   **interlace** `bool` - Use progressive / interlaced format of the image output. Defaults to `false`
-   **aspectratio** `string` - Apply aspect ratio by giving either image's height or width. Exampe: `16:9`

#### GET /

Content-Type: `application/json`

Serves as JSON the current `imaginary`, `bimg` and `libvips` versions.

Example response:

{
  "imaginary": "0.1.28",
  "bimg": "1.0.5",
  "libvips": "8.4.1"
}

#### GET /health

Content-Type: `application/json`

Provides some useful statistics about the server stats with the following structure:

-   **uptime** `number` - Server process uptime in seconds.
-   **allocatedMemory** `number` - Currently allocated memory in megabytes.
-   **totalAllocatedMemory** `number` - Total allocated memory over the time in megabytes.
-   **goroutines** `number` - Number of running goroutines.
-   **cpus** `number` - Number of used CPU cores.

Example response:

{
  "uptime": 1293,
  "allocatedMemory": 5.31,
  "totalAllocatedMemory": 34.3,
  "goroutines": 19,
  "cpus": 8
}

#### GET /form

Content Type: `text/html`

Serves an ugly HTML form, just for testing/playground purposes

#### GET | POST /info

Accepts: `image/*, multipart/form-data`. Content-Type: `application/json`

Returns the image metadata as JSON:

{
  "width": 550,
  "height": 740,
  "type": "jpeg",
  "space": "srgb",
  "hasAlpha": false,
  "hasProfile": true,
  "channels": 3,
  "orientation": 1
}

#### GET | POST /crop

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

Crop the image by a given width or height. Image ratio is maintained

##### Allowed params

-   width `int`
-   height `int`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   force `bool`
-   rotate `int`
-   embed `bool`
-   norotation `bool`
-   noprofile `bool`
-   flip `bool`
-   flop `bool`
-   stripmeta `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   gravity `string`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`

#### GET | POST /smartcrop

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

Crop the image by a given width or height using the libvips built-in smart crop algorithm.

##### Allowed params

-   width `int`
-   height `int`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   force `bool`
-   rotate `int`
-   embed `bool`
-   norotation `bool`
-   noprofile `bool`
-   flip `bool`
-   flop `bool`
-   stripmeta `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   gravity `string`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`

#### GET | POST /resize

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

Resize an image by width or height. Image aspect ratio is maintained

##### Allowed params

-   width `int` `required`
-   height `int`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   rotate `int`
-   nocrop `bool` - Defaults to `true`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`
-   palette `bool`

#### GET | POST /enlarge

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

##### Allowed params

-   width `int` `required`
-   height `int` `required`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   rotate `int`
-   nocrop `bool` - Defaults to `false`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   palette `bool`

#### GET | POST /extract

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

##### Allowed params

-   top `int` `required`
-   left `int`
-   areawidth `int` `required`
-   areaheight `int`
-   width `int`
-   height `int`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   rotate `int`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`
-   palette `bool`

#### GET | POST /zoom

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

##### Allowed params

-   factor `number` `required`
-   width `int`
-   height `int`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   rotate `int`
-   nocrop `bool` - Defaults to `true`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`
-   palette `bool`

#### GET | POST /thumbnail

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

##### Allowed params

-   width `int` `required`
-   height `int` `required`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   rotate `int`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`
-   palette `bool`

#### GET | POST /fit

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

Resize an image to fit within width and height, without cropping. Image aspect ratio is maintained The width and height specify a maximum bounding box for the image.

##### Allowed params

-   width `int` `required`
-   height `int` `required`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   rotate `int`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`
-   palette `bool`

#### GET | POST /rotate

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

#### GET | POST /autorotate

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

Automatically rotate the image with no further image transformations based on EXIF orientation metadata.

Returns a new image with the same size and format as the input image.

##### Allowed params

-   rotate `int` `required`
-   width `int`
-   height `int`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`
-   palette `bool`

#### GET | POST /flip

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

##### Allowed params

-   width `int`
-   height `int`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`
-   palette `bool`

#### GET | POST /flop

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

##### Allowed params

-   width `int`
-   height `int`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`
-   palette `bool`

#### GET | POST /convert

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

##### Allowed params

-   type `string` `required`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   rotate `int`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`
-   palette `bool`

#### GET | POST /pipeline

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

This endpoint allow the user to declare a pipeline of multiple independent image transformation operations all in a single HTTP request.

**Note**: a maximum of 10 independent operations are current allowed within the same HTTP request.

Internally, it operates pretty much as a sequential reducer pattern chain, where given an input image and a set of operations, for each independent image operation iteration, the output result image will be passed to the next one, as the accumulated result, until finishing all the operations.

In imperative programming, this would be pretty much analog to the following code:

var image
for operation in operations {
  image \= operation.Run(image, operation.Options)
}

##### Allowed params

-   operations `json` `required` - URL safe encoded JSON with a list of operations. See below for interface details.
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present

##### Operations JSON specification

Self-documented JSON operation schema:

\[
  {
    "operation": string, // Operation name identifier. Required.
    "ignore\_failure": boolean, // Ignore error in case of failure and continue with the next operation. Optional.
    "params": map\[string\]mixed, // Object defining operation specific image transformation params, same as supported URL query params per each endpoint.
  }
\]

###### Supported operations names

-   **crop** - Same as `/crop` endpoint.
-   **smartcrop** - Same as `/smartcrop` endpoint.
-   **resize** - Same as `/resize` endpoint.
-   **enlarge** - Same as `/enlarge` endpoint.
-   **extract** - Same as `/extract` endpoint.
-   **rotate** - Same as `/rotate` endpoint.
-   **autorotate** - Same as `/autorotate` endpoint.
-   **flip** - Same as `/flip` endpoint.
-   **flop** - Same as `/flop` endpoint.
-   **thumbnail** - Same as `/thumbnail` endpoint.
-   **zoom** - Same as `/zoom` endpoint.
-   **convert** - Same as `/convert` endpoint.
-   **watermark** - Same as `/watermark` endpoint.
-   **watermarkImage** - Same as `/watermarkimage` endpoint.
-   **blur** - Same as `/blur` endpoint.

###### Example

\[
  {
    "operation": "crop",
    "params": {
      "width": 500,
      "height": 300
    }
  },
  {
    "operation": "watermark",
    "params": {
      "text": "I need some covfete",
      "font": "Verdana",
      "textwidth": 100,
      "opacity": 0.8
    }
  },
  {
    "operation": "rotate",
    "params": {
      "rotate": 180
    }
  },
  {
    "operation": "convert",
    "params": {
      "type": "webp"
    }
  }
\]

#### GET | POST /watermark

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

##### Allowed params

-   text `string` `required`
-   margin `int`
-   dpi `int`
-   textwidth `int`
-   opacity `float`
-   noreplicate `bool`
-   font `string`
-   color `string`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   rotate `int`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   palette `bool`

#### GET | POST /watermarkimage

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

##### Allowed params

-   image `string` `required` - URL to watermark image, example: `?image=https://logo-server.com/logo.jpg`
-   top `int` - Top position of the watermark image
-   left `int` - Left position of the watermark image
-   opacity `float` - Opacity value of the watermark image
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   rotate `int`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   sigma `float`
-   minampl `float`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   palette `bool`

#### GET | POST /blur

Accepts: `image/*, multipart/form-data`. Content-Type: `image/*`

##### Allowed params

-   sigma `float` `required`
-   minampl `float`
-   width `int`
-   height `int`
-   quality `int` (JPEG-only)
-   compression `int` (PNG-only)
-   type `string`
-   file `string` - Only GET method and if the `-mount` flag is present
-   url `string` - Only GET method and if the `-enable-url-source` flag is present
-   embed `bool`
-   force `bool`
-   norotation `bool`
-   noprofile `bool`
-   stripmeta `bool`
-   flip `bool`
-   flop `bool`
-   extend `string`
-   background `string` - Example: `?background=250,20,10`
-   colorspace `string`
-   field `string` - Only POST and `multipart/form` payloads
-   interlace `bool`
-   aspectratio `string`
-   palette `bool`

Logging
-------

Imaginary uses an apache compatible log format.

### Fluentd log ingestion

You can ingest Imaginary logs with fluentd using the following fluentd config :

```
# use your own tag name (*.imaginary for this example)
<filter *.imaginary>
    @type parser
    key_name log
    reserve_data true

    <parse>
        @type multi_format
        # access logs parser
        <pattern>
            format regexp
            expression /^[^ ]* [^ ]* [^ ]* \[(?<time>[^\]]*)\] "(?<method>\S+)(?: +(?<path>[^ ]*) +\S*)?" (?<code>[^ ]*) (?<size>[^ ]*) (?<response_time>[^ ]*)$/
            types code:integer,size:integer,response_time:float
            time_key time
            time_format %d/%b/%Y %H:%M:%S
        </pattern>
        # warnings / error logs parser
        <pattern>
            format none
            message_key message
        </pattern>
    </parse>
</filter>

<match *.imaginary>
    @type rewrite_tag_filter

    # Logs with code field are access logs, and logs without are error logs
    <rule>
        key code
        pattern ^.+$
        tag ${tag}.access
    </rule>
    <rule>
        key code
        pattern ^.+$
        invert true
        tag ${tag}.error
    </rule>
</match>
```

In the end, access records are tagged with `*.imaginary.access`, and warning / error records are tagged with `*.imaginary.error`.

Support
-------

### Backers

Support us with a monthly donation and help us continue our activities. \[Become a backer\]

### Support this project

### Sponsors

Become a sponsor and get your logo on our README on Github with a link to your site. \[Become a sponsor\]

Authors
-------

-   Tomás Aparicio - Original author and maintainer.

License
-------

MIT - Tomas Aparicio
