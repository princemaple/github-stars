---
project: redroid-doc
stars: 6580
description: redroid (Remote-Android) is a multi-arch, GPU enabled, Android in Cloud solution. Track issues / docs here
url: https://github.com/remote-android/redroid-doc
---

English | 简体中文

Table of contents
=================

-   Overview
-   Getting Started
-   Configuration
-   Native Bridge Support
-   GMS Support
-   WebRTC Streaming
-   How To Build
-   Troubleshooting
-   Contact Me
-   License

Overview
--------

_redroid_ (_Re_mote an_Droid_) is a GPU accelerated AIC (Android In Cloud) solution. You can boot many instances in Linux host (`Docker`, `podman`, `k8s` etc.). _redroid_ supports both `arm64` and `amd64` architectures. _redroid_ is suitable for Cloud Gaming, Virtualise Phones, Automation Test and more.

Currently supported:

-   Android 16 (`redroid/redroid:16.0.0-latest`)
-   Android 16 64bit only (`redroid/redroid:16.0.0_64only-latest`)
-   Android 15 (`redroid/redroid:15.0.0-latest`)
-   Android 15 64bit only (`redroid/redroid:15.0.0_64only-latest`)
-   Android 14 (`redroid/redroid:14.0.0-latest`)
-   Android 14 64bit only (`redroid/redroid:14.0.0_64only-latest`)
-   Android 13 (`redroid/redroid:13.0.0-latest`)
-   Android 13 64bit only (`redroid/redroid:13.0.0_64only-latest`)
-   Android 12 (`redroid/redroid:12.0.0-latest`)
-   Android 12 64bit only (`redroid/redroid:12.0.0_64only-latest`)
-   Android 11 (`redroid/redroid:11.0.0-latest`)
-   Android 10 (`redroid/redroid:10.0.0-latest`)
-   Android 9 (`redroid/redroid:9.0.0-latest`)
-   Android 8.1 (`redroid/redroid:8.1.0-latest`)

Getting Started
---------------

_redroid_ should be able to run on any linux distribution (with some kernel features enabled).

Quick start on _Ubuntu 20.04_ here; Check deploy section for other distros.

#\# install docker https://docs.docker.com/engine/install/#server

#\# install required kernel modules
apt install linux-modules-extra-\`uname -r\`
modprobe binder\_linux devices="binder,hwbinder,vndbinder"
modprobe ashmem\_linux

#\# running redroid
docker run -itd --rm --privileged \\
    --pull always \\
    -v ~/data:/data \\
    -p 5555:5555 \\
    redroid/redroid:12.0.0\_64only-latest

#\## Explanation:
#\##   --pull always    -- use latest image
#\##   -v ~/data:/data  -- mount data partition
#\##   -p 5555:5555     -- expose adb port

#\## DISCLAIMER
#\## Should NOT expose adb port on public network
#\## otherwise, redroid container (even host OS) may get compromised

#\# install adb https://developer.android.com/studio#downloads
adb connect localhost:5555
#\## NOTE: change localhost to IP if running redroid remotely

#\# view redroid screen
#\# install scrcpy https://github.com/Genymobile/scrcpy/blob/master/README.md#get-the-app
scrcpy -s localhost:5555
#\## NOTE: change localhost to IP if running redroid remotely
#\##     typically running scrcpy on your local PC

Configuration
-------------

```
## running redroid with custom settings (custom display for example)
docker run -itd --rm --privileged \
    --pull always \
    -v ~/data:/data \
    -p 5555:5555 \
    redroid/redroid:12.0.0_64only-latest \
    androidboot.redroid_width=1080 \
    androidboot.redroid_height=1920 \
    androidboot.redroid_dpi=480 \
```

Param

Description

Default

`androidboot.redroid_width`

display width

720

`androidboot.redroid_height`

display height

1280

`androidboot.redroid_fps`

display FPS

30(GPU enabled)  
15 (GPU not enabled)

`androidboot.redroid_dpi`

display DPI

320

`androidboot.use_memfd`

use `memfd` to replace deprecated `ashmem`  
plan to enable by default

false

`androidboot.use_redroid_overlayfs`

use `overlayfs` to share `data` partition  
`/data-base`: shared `data` partition  
`/data-diff`: private data

0

`androidboot.redroid_net_ndns`

number of DNS server, `8.8.8.8` will be used if no DNS server specified

0

`androidboot.redroid_net_dns<1..N>`

DNS

`androidboot.redroid_net_proxy_type`

Proxy type; choose from: `static`, `pac`, `none`, `unassigned`

`androidboot.redroid_net_proxy_host`

`androidboot.redroid_net_proxy_port`

3128

`androidboot.redroid_net_proxy_exclude_list`

comma seperated list

`androidboot.redroid_net_proxy_pac`

`androidboot.redroid_gpu_mode`

choose from: `auto`, `host`, `guest`;  
`guest`: use software rendering;  
`host`: use GPU accelerated rendering;  
`auto`: auto detect

`guest`

`androidboot.redroid_gpu_node`

auto-detect

`ro.xxx`

**DEBUG** purpose, allow override `ro.xxx` prop; For example, set `ro.secure=0`, then root adb shell provided by default

Native Bridge Support
---------------------

It's possible to run `arm` Apps in `x86` _redroid_ instance via `libhoudini`, `libndk_translation` or `QEMU translator`.

Check @zhouziyang/libndk\_translation for prebuilt `libndk_translation`. Published `redroid` images already got `libndk_translation` included.

# example structure, be careful the file owner and mode

system/
├── bin
│   ├── arm
│   └── arm64
├── etc
│   ├── binfmt\_misc
│   └── init
├── lib
│   ├── arm
│   └── libnb.so
└── lib64
    ├── arm64
    └── libnb.so

# Dockerfile
FROM redroid/redroid:11.0.0-latest

ADD native-bridge.tar /

# build docker image
docker build . -t redroid:11.0.0-nb

# running
docker run -itd --rm --privileged \\
    -v ~/data11-nb:/data \\
    -p 5555:5555 \\
    redroid:11.0.0-nb \\

GMS Support
-----------

It's possible to add GMS (Google Mobile Service) support in _redroid_ via Open GApps, MicroG or MindTheGapps.

Check android-builder-docker for details.

WebRTC Streaming
----------------

Plan to port `WebRTC` solutions from `cuttlefish`, including frontend (HTML5), backend and many virtual HALs.

How To Build
------------

It's the same way as AOSP building process, but I suggest to use `docker` to build it.

Check android-builder-docker for details.

Troubleshooting
---------------

-   How to collect debug blobs

> `curl -fsSL https://raw.githubusercontent.com/remote-android/redroid-doc/master/debug.sh | sudo bash -s -- [CONTAINER]`
> 
> omit _CONTAINER_ if not exist any more

-   Container disappeared immediately

> make sure the required kernel modules are installed; run `dmesg -T` for detailed logs

-   Container running, but adb cannot connect (device offline etc.)

> run `docker exec -it <container> sh`, then check `ps -A` and `logcat`
> 
> try `dmesg -T` if cannot get a container shell

Contact Me
----------

-   ziyang.zhou@outlook.com

License
-------

_redroid_ itself is under Apache License, since _redroid_ includes many 3rd party modules, you may need to examine license carefully.

_redroid_ kernel modules are under GPL v2
