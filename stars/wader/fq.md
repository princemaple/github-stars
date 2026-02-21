---
project: fq
stars: 10414
description: jq for binary formats - tool, language and decoders for working with binary and text formats
url: https://github.com/wader/fq
---

fq
==

Tool, language and decoders for working with binary data.

TLDR: it aims to be jq, hexdump, dd and gdb for files combined into one.

Basic usage is `fq . file`, `fq d file` or `fq 'some query' file ...`.

For details see usage.md.

### Background

fq is inspired by the jq tool and language and allows you to work with binary formats in the same way. In addition to using jq expressions it can also present decoded tree structures, transform, slice and concatenate binary data. It also supports nested formats and features an interactive REPL with auto-completion of functions and names.

It was originally designed to query, inspect and debug media codecs and containers like MP4, FLAC and JPEG but has since been extended to support a variety of formats like executables, packet captures (with TCP reassembly) and serialization formats like JSON, YAML, XML, CBOR, protobuf. In addition it also has functions to work with URLs, convert to/from hex, number bases, search for patterns etc.

### Goals

-   Make binaries more accessible, queryable and sliceable.
-   Nested formats and bit-oriented decoding.
-   Quick and comfortable CLI tool.
-   Bits and bytes transformations.

### Hopes

-   Make it useful enough that people want to help improve it.
-   Inspire people to create similar tools.

### Supported formats

aac\_frame, adts, adts\_frame, aiff, amf0, apev2, apple\_bookmark, ar, asn1\_ber, av1\_ccr, av1\_frame, av1\_obu, avc\_annexb, avc\_au, avc\_dcr, avc\_nalu, avc\_pps, avc\_sei, avc\_sps, avi, avro\_ocf, bencode, bitcoin\_blkdat, bitcoin\_block, bitcoin\_script, bitcoin\_transaction, bits, bplist, bsd\_loopback\_frame, bson, bytes, bzip2, caff, cbor, csv, dns, dns\_tcp, elf, ether8023\_frame, exif, fairplay\_spc, fit, flac, flac\_frame, flac\_metadatablock, flac\_metadatablocks, flac\_picture, flac\_streaminfo, gif, gzip, hevc\_annexb, hevc\_au, hevc\_dcr, hevc\_nalu, hevc\_pps, hevc\_sps, hevc\_vps, html, icc\_profile, icmp, icmpv6, id3v1, id3v11, id3v2, ipv4\_packet, ipv6\_packet, jp2c, jpeg, json, jsonl, leveldb\_descriptor, leveldb\_log, leveldb\_table, luajit, macho, macho\_fat, markdown, matroska, midi, moc3, mp3, mp3\_frame, mp3\_frame\_vbri, mp3\_frame\_xing, mp4, mpeg\_asc, mpeg\_es, mpeg\_pes, mpeg\_pes\_packet, mpeg\_spu, mpeg\_ts, msgpack, negentropy, nes, ogg, ogg\_page, opentimestamps, opus\_packet, pcap, pcapng, pg\_btree, pg\_control, pg\_heap, png, prores\_frame, protobuf, protobuf\_widevine, pssh\_playready, rtmp, safetensors, sll2\_packet, sll\_packet, tap, tar, tcp\_segment, tiff, tls, toml, tzif, tzx, udp\_datagram, vorbis\_comment, vorbis\_packet, vp8\_frame, vp9\_cfm, vp9\_frame, vpx\_ccr, wasm, wav, webp, xml, yaml, zip

It can also work with some common text formats like URLs, hex, base64, PEM etc and for some serialization formats like XML, YAML, etc. it can transform both from and to jq values.

For details see formats.md and usage.md.

Presentations and media
-----------------------

-   PBS Tidbit 8 of Y: Interview with jq Maintainer Mattias Wadman - English podcast episode about jq and some fq.
-   Kodsnack 585 - Polymorfisk JSON - Swedish podcast episode about jq and fq
-   "fq - jq for binary formats" at FOSDEM 2023 - video & slides
-   "fq - jq for binary formats" at No time to wait 6 - video - slides
-   "fq - jq for binary formats" at Binary Tools Summit 2022 - video - slides

Install
-------

Use one of the methods listed below or download a pre-built release for macOS, Linux or Windows. Unarchive it and move the executable to `PATH` etc.

On macOS if you don't install using one of the method below then you might have to manually allow the binary to run. This can be done by trying to run the binary, ignore the warning and then go into security preference and allow it. Same can be done with these commands:

xattr -d com.apple.quarantine fq
# for macOS version before Sequoia you might need this also
spctl --add fq

### Homebrew (macOS)

brew install wader/tap/fq

### MacPorts

On macOS, `fq` can also be installed via MacPorts. More details here.

sudo port install fq

### Windows

`fq` can be installed via scoop.

scoop install fq

### Arch Linux

`fq` can be installed from the extra repository using pacman:

pacman -S fq

You can also build and install the development (VCS) package using an AUR helper:

paru -S fq-git

### Guix

guix shell fq -- fq --help # in develompen shell
guix install fq            # into current profile

### Nix

nix-shell -p fq

### FreeBSD

Use the fq port.

### Alpine

Currently in edge testing but should work fine in stable also.

```
apk add -X http://dl-cdn.alpinelinux.org/alpine/edge/testing fq
```

### Build from source

Make sure you have go 1.22 or later installed.

To install directly from git repository (no git clone needed):

# build and install latest release
go install github.com/wader/fq@latest

# build and install latest master
go install github.com/wader/fq@master

# copy binary to $PATH if needed
cp "$(go env GOPATH)/bin/fq" /usr/local/bin

To build, run and test from source:

# build and run
go run .
# build and run with arguments
go run . -d mp3 . file.mp3
# just build
go build -o fq .
# run all tests and build binary
make test fq

Development and adding a new decoder
------------------------------------

See dev.md

Thanks and related projects
---------------------------

This project would not have been possible without itchyny's jq implementation gojq. I also want to thank HexFiend for inspiration and ideas and stedolan for inventing the jq language.

### Similar or related works

#### Tools

-   HexFiend - Hex editor for macOS with format template support.
-   ImHex - A Hex Editor for Reverse Engineers.
-   binspector - Binary format analysis tool with query language and REPL.
-   kaitai - Declarative binary format parsing.
-   Wireshark - Decodes network traffic (tip: `tshark -T json`).
-   MediaInfo - Analyze media files (tip `mediainfo --Output=JSON` and `mediainfo --Details=1`).
-   GNU poke - The extensible editor for structured binary data.
-   ffmpeg/ffprobe - Powerful media libraries and tools.
-   hexdump - Hex viewer tool.
-   hex - Interactive hex viewer with format support via lua.
-   hachoir - General python library for working binary data.
-   scapy - Decode/Encode formats, focus on network protocols.

#### Projects and Standards

-   Let's Solve the File Format Problem.
-   PRONOM file format registry.
-   Sustainability of Digital Formats at Library of Congress.
-   Data Format Description Language (DFDL).

TODO and ideas
--------------

See TODO.md

License
-------

`fq` is distributed under the terms of the MIT License.

See the LICENSE file for license details.

Licenses of direct dependencies:

-   Forked version of gojq - https://github.com/itchyny/gojq/blob/main/LICENSE (MIT)
-   github.com/ergochat/readline - https://github.com/ergochat/readline/blob/master/LICENSE (MIT)
-   github.com/BurntSushi/toml - https://github.com/BurntSushi/toml/blob/master/COPYING (MIT)
-   github.com/creasty/defaults - https://github.com/creasty/defaults/blob/master/LICENSE (MIT)
-   github.com/gomarkdown/markdown - https://github.com/gomarkdown/markdown/blob/master/LICENSE.txt (BSD)
-   github.com/gopacket/gopacket - https://github.com/gopacket/gopacket/blob/master/LICENSE (BSD)
-   github.com/mitchellh/copystructure - https://github.com/mitchellh/copystructure/blob/master/LICENSE (MIT)
-   github.com/mitchellh/mapstructure - https://github.com/mitchellh/mapstructure/blob/master/LICENSE (MIT)
-   github.com/pmezard/go-difflib - https://github.com/pmezard/go-difflib/blob/master/LICENSE (BSD)
-   golang/snappy - https://github.com/golang/snappy/blob/master/LICENSE (BSD)
-   golang/x/\* - https://github.com/golang/text/blob/master/LICENSE (BSD)
-   gopkg.in/yaml.v3 - https://github.com/go-yaml/yaml/blob/v3/LICENSE (MIT)
-   Parts of go crypto/tls and github.com/zmap/zcrypto - https://github.com/zmap/zcrypto/blob/master/LICENSE (Apache)
