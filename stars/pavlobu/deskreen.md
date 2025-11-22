---
project: deskreen
stars: 19812
description: Deskreen turns any device with a web browser into a secondary screen for your computer. ⭐️ Star to support our work!
url: https://github.com/pavlobu/deskreen
---

Deskreen CE (Community Edition)
===============================

(Over 2M downloads during 5 years since launch)

Deskreen turns any device with a web browser into a secondary screen for your computer
--------------------------------------------------------------------------------------

To learn more visit our website: deskreen.com
---------------------------------------------

Donate to support Deskreen Open-Source
--------------------------------------

Deskreen is an `electron.js` based application that uses `WebRTC` to make a live stream of your computer screen to a web browser on any device. It is available for MacOS, Windows and Linux operating systems. The current open-source Community Edition version has limited features. If you need more features please consider upgrading to Pro version for more features when it is released.

* * *

### ▶️ See how people use Deskreen on Youtube (video tutorials, demos, use cases for Deskreen day to day usage)

* * *

Deskreen Frequently Asked Questions
-----------------------------------

* * *

### Prerequisites

You will need to have `node>=v23` `pnpm>=v10.20.0` installed.

1.  git clone this repo
2.  `pnpm i`
3.  `cd ./src/client-viewer && pnpm i && cd ../..`
4.  `pnpm clean && pnpm build && pnpm start` -- run in prod like mode

#### for more pnpm commands look at `package.json`

Starting with Custom Local IP
-----------------------------

You can start Deskreen CE with a custom local IP address using the `--local-ip` or `--ip` CLI flag. This is useful when you want to specify a particular network interface IP address.

### macOS

# Using open command (recommended)
open -a "Deskreen CE" --args --ip 192.168.1.100

# Or using the executable directly
/Applications/Deskreen\\ CE.app/Contents/MacOS/Deskreen\\ CE --ip 192.168.1.100

# Get your IP automatically and launch
open -a "Deskreen CE" --args --ip "192.168.1.100"

### Windows

# Using Start-Process (PowerShell)
Start-Process "Deskreen CE" \-ArgumentList "\--ip", "192.168.1.100"

# Or using the executable directly
"C:\\Program Files\\Deskreen CE\\Deskreen CE.exe" \--ip 192.168.1.100

# Or from Command Prompt
start "" "C:\\Program Files\\Deskreen CE\\Deskreen CE.exe" \--ip 192.168.1.100

### Linux

# If installed via AppImage
./Deskreen\\ CE-\*.AppImage --ip 192.168.1.100

# If installed via .deb/.rpm package (usually in /usr/bin or /opt)
deskreen-ce --ip 192.168.1.100

# Or using full path
/opt/Deskreen\\ CE/deskreen-ce --ip 192.168.1.100

**Note:** Replace `192.168.1.100` with your actual local IP address. You can find your IP using:

-   **macOS/Linux:** `ipconfig getifaddr en0` or `ifconfig | grep "inet "`
-   **Windows:** `ipconfig` (look for IPv4 Address)

When using the `--ip` or `--local-ip` flag, the app will use the specified IP for QR codes and connection URLs, while still monitoring the actual network interface status for WiFi connection detection.

Maintainer
----------

-   Pavlo (Paul) Buidenkov

License
-------

AGPL-3.0 License © Pavlo (Paul) Buidenkov

Copyright
---------

Electron-Vite MIT License © electron-vite

React MIT License © Facebook, Inc. and its affiliates

Vite MIT License © Vite.js

Electron Builder MIT License © electron-builder contributors

Apache 2.0 © blueprintjs

simple-peer MIT. Copyright © Feross Aboukhadijeh

tweetnacl ISC License © Dmitry Chestnykh, Devi Mandiri, and contributors (https://github.com/dchest/tweetnacl-js)

darkwire.io MIT License © darkwire/darkwire.io

And many many others...

Thanks
------

🙏 Many thanks to all 🌍 open source community members and maintainers of libraries used in this project.
