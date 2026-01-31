---
project: ConvertX
stars: 15594
description: 💾 Self-hosted online file converter. Supports 1000+ formats ⚙️
url: https://github.com/C4illin/ConvertX
---

ConvertX
========

A self-hosted online file converter. Supports over a thousand different formats. Written with TypeScript, Bun and Elysia.

Features
--------

-   Convert files to different formats
-   Process multiple files at once
-   Password protection
-   Multiple accounts

Converters supported
--------------------

Converter

Use case

Converts from

Converts to

Inkscape

Vector images

7

17

libjxl

JPEG XL

11

11

resvg

SVG

1

1

Vips

Images

45

23

libheif

HEIF

2

4

XeLaTeX

LaTeX

1

1

Calibre

E-books

26

19

LibreOffice

Documents

41

22

Dasel

Data Files

5

4

Pandoc

Documents

43

65

msgconvert

Outlook

1

1

VCF to CSV

Contacts

1

1

dvisvgm

Vector images

4

2

ImageMagick

Images

245

183

GraphicsMagick

Images

167

130

Assimp

3D Assets

77

23

FFmpeg

Video

~472

~199

Potrace

Raster to vector

4

11

VTracer

Raster to vector

8

1

Markitdown

Documents

6

1

Any missing converter? Open an issue or pull request!

Deployment
----------

Warning

If you can't login, make sure you are accessing the service over localhost or https otherwise set HTTP\_ALLOWED=true

# docker-compose.yml
services:
  convertx:
    image: ghcr.io/c4illin/convertx
    container\_name: convertx
    restart: unless-stopped
    ports:
      - "3000:3000"
    environment:
      - JWT\_SECRET=aLongAndSecretStringUsedToSignTheJSONWebToken1234 # will use randomUUID() if unset
      # - HTTP\_ALLOWED=true # uncomment this if accessing it over a non-https connection
    volumes:
      - ./data:/app/data

or

docker run -p 3000:3000 -v ./data:/app/data ghcr.io/c4illin/convertx

Then visit `http://localhost:3000` in your browser and create your account. Don't leave it unconfigured and open, as anyone can register the first account.

If you get unable to open database file run `chown -R $USER:$USER path` on the path you choose.

### Environment variables

All are optional, JWT\_SECRET is recommended to be set.

Name

Default

Description

JWT\_SECRET

when unset it will use the value from randomUUID()

A long and secret string used to sign the JSON Web Token

ACCOUNT\_REGISTRATION

false

Allow users to register accounts

HTTP\_ALLOWED

false

Allow HTTP connections, only set this to true locally

ALLOW\_UNAUTHENTICATED

false

Allow unauthenticated users to use the service, only set this to true locally

AUTO\_DELETE\_EVERY\_N\_HOURS

24

Checks every n hours for files older then n hours and deletes them, set to 0 to disable

WEBROOT

The address to the root path setting this to "/convert" will serve the website on "example.com/convert/"

FFMPEG\_ARGS

Arguments to pass to the input file of ffmpeg, e.g. `-hwaccel vaapi`. See #190 for more info about hw-acceleration.

FFMPEG\_OUTPUT\_ARGS

Arguments to pass to the output of ffmpeg, e.g. `-preset veryfast`

HIDE\_HISTORY

false

Hide the history page

LANGUAGE

en

Language to format date strings in, specified as a BCP 47 language tag

UNAUTHENTICATED\_USER\_SHARING

false

Shares conversion history between all unauthenticated users

MAX\_CONVERT\_PROCESS

0

Maximum number of concurrent conversion processes allowed. Set to 0 for unlimited.

### Docker images

There is a `:latest` tag that is updated with every release and a `:main` tag that is updated with every push to the main branch. `:latest` is recommended for normal use.

The image is available on GitHub Container Registry and Docker Hub.

Image

What it is

`image: ghcr.io/c4illin/convertx`

The latest release on ghcr

`image: ghcr.io/c4illin/convertx:main`

The latest commit on ghcr

`image: c4illin/convertx`

The latest release on docker hub

`image: c4illin/convertx:main`

The latest commit on docker hub

### Tutorial

Note

These are written by other people, and may be outdated, incorrect or wrong.

Tutorial in french: https://belginux.com/installer-convertx-avec-docker/

Tutorial in chinese: https://xzllll.com/24092901/

Tutorial in polish: https://www.kreatywnyprogramista.pl/convertx-lokalny-konwerter-plikow

Screenshots
-----------

Development
-----------

1.  Install Bun and Git
2.  Clone the repository
3.  `bun install`
4.  `bun run dev`

Pull requests are welcome! See open issues for the list of todos. The ones tagged with "converter request" are quite easy. Help with docs and cleaning up in issues are also very welcome!

Use conventional commits for commit messages.

Contributors
------------

Star History
------------
