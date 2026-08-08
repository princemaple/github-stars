---
project: croc
stars: 39524
description: Easily and securely send things from one computer to another :crocodile: :package:
url: https://github.com/schollz/croc
---

  

**This project’s future depends on community support. Become a sponsor today.**

About
-----

`croc` is a tool that allows any two computers to simply and securely transfer files and folders. AFAIK, _croc_ is the only CLI file-transfer tool that does **all** of the following:

-   Allows **any two computers** to transfer data (using a relay)
-   Provides **end-to-end encryption** (using PAKE)
-   Enables easy **cross-platform** transfers (Windows, Linux, Mac, Browser)
-   Allows **multiple file** transfers
-   Allows **resuming transfers** that are interrupted
-   No need for local server or port-forwarding
-   **IPv6-first** with IPv4 fallback
-   Can **use a proxy**, like Tor

For more information about `croc`, see my blog post or read a recent interview I did.

No-install
----------

You can use croc without installing anything at getcroc.com.

The browser version is fully compatible with the CLI, so you can send and receive files between them.

Install
-------

You can download the latest release for your system, or install a release from the command-line:

curl https://getcroc.com | bash

### On macOS

Using Homebrew:

brew install croc

Using MacPorts:

sudo port selfupdate
sudo port install croc

### On Windows

You can install the latest release with Scoop, Chocolatey, or Winget:

scoop install croc

choco install croc

winget install schollz.croc

### Using nix-env

You can install the latest release with Nix:

nix-env -i croc

### On NixOS

You can add this to your configuration.nix:

environment.systemPackages \= \[
  pkgs.croc
\];

### On Alpine Linux

First, install dependencies:

apk add bash coreutils
wget -qO- https://getcroc.com | bash

### On Arch Linux

Install with `pacman`:

pacman -S croc

### On Fedora

Install with `dnf`:

dnf install croc

### On Gentoo

Install with `portage`:

emerge net-misc/croc

### On Termux

Install with `pkg`:

pkg install croc

### On FreeBSD

Install with `pkg`:

pkg install croc

### On Linux, macOS, and Windows via Conda

You can install from conda-forge globally with `pixi`:

pixi global install croc

Or install into a particular environment with `conda`:

conda install --channel conda-forge croc

### On Linux, macOS via Docker

Add the following one-liner function to your ~/.profile (works with any POSIX-compliant shell):

croc() { \[ $# \-eq 0 \] && set -- ""; mkdir -p "$HOME/.config/croc"; docker run --rm -it --user "$(id -u):$(id -g)" -v "$(pwd):/c" -v "$HOME/.config/croc:/.config/croc" -w /c -e CROC\_SECRET docker.io/schollz/croc "$@"; }

You can also just paste it in the terminal for current session. On first run Docker will pull the image. `croc` via Docker will only work within the current directory and its subdirectories.

### Build from Source

If you prefer, you can install Go and build from source (requires Go 1.22+):

go install github.com/schollz/croc/v10@latest

### On Android

There are F-Droid apps available:

-   crocgui — original port (Go, basic UI)
-   croc-app — native Kotlin/Jetpack Compose client with a modern, mobile-first interface
-   FlCroc — cross-platform Flutter GUI (Android, Windows, Linux) that wraps the `croc` binary as its transfer core.

### On Desktop

Community made desktop apps:

-   Croc GUI — unofficial desktop GUI for macOS, Windows, and Linux that bundles the `croc` binary for drag-and-drop transfers, QR codes, LAN mode, and relay/proxy options.
-   croc-desktop — unofficial desktop GUI for Linux, macOS, and Windows (experimental iOS/Android) built with Wails v3; embeds croc in-process for send/receive, QR codes, history, logs, and optional relay hosting.
-   Swamp Swap — unofficial PyQt6 GUI desktop app for macOS, Windows, and Linux, requires installing `croc` on its own normally in order to use. Made to be compact and simple.

Usage
-----

To send a file, simply do:

$ croc send \[file(s)-or-folder\]
Sending 'file-or-folder' (X MB)
Code is: code-phrase

Then, to receive the file (or folder) on another computer, run:

croc code-phrase

The code phrase is used to establish password-authenticated key agreement (PAKE) which generates a secret key for the sender and recipient to use for end-to-end encryption.

### Customizations & Options

#### Encrypted temporary storage

When an immediate peer-to-peer transfer is inconvenient, `croc` can upload regular files as client-side encrypted ciphertext:

croc send --store \[file1\] \[file2\]

The command prints a browser link and a CLI token. The transfer expires after 24 hours or after the first receiver downloads, authenticates, and verifies every file—whichever happens first. Run `croc` with no arguments and paste the token at the prompt to receive it. For automation, keep the token out of the process list:

CROC\_STORE\_TOKEN='croc-store-v1....' croc --out ./downloads

The browser link has the form `https://host/s/id#v1.decryption-key`. The decryption key is after `#` because URL fragments are not included in HTTP requests, so the storage service gets the opaque transfer ID but not the key. The full link is still a secret: anyone who has it can decrypt and claim the one allowed download.

Until a transfer is downloaded or expires, its sender can delete it with the locally saved revoke receipt:

croc --revoke \[transfer-id\]

Stored mode is opt-in and separate from croc's normal live relay transfers. A self-hosted service can be selected with `--store-url` or `CROC_STORE_URL`. See the stored-transfer design and operator guide for protocol, privacy, limits, and deployment details.

#### Using `croc` on Linux or macOS

On Linux and macOS, the sending and receiving process is slightly different to avoid leaking the secret via the process name. You will need to run `croc` with the secret as an environment variable. For example, to receive with the secret `***`:

CROC\_SECRET=\*\*\* croc

For single-user systems, the default behavior can be permanently enabled by running:

croc --classic

#### Custom Code Phrase

You can send with your own code phrase (must be at least 6 characters):

croc send --code \[code-phrase\] \[file(s)-or-folder\]

#### Allow Overwriting Without Prompt

To automatically overwrite files without prompting, use the `--overwrite` flag:

croc --yes --overwrite <code\>

#### Keep Both Files Without Prompt

To keep an existing file and receive the incoming one under a new name (e.g. `video (1).mkv`), use the `--rename` flag:

croc --yes --rename <code\>

#### Excluding Folders

To exclude folders from being sent, use the `--exclude` flag with comma-delimited exclusions. This does a case-insensitive **substring** match against each file's relative path, so any path containing one of the given strings anywhere is excluded:

croc send --exclude "node\_modules,.venv" \[folder\]

If you need to exclude one specific file rather than every path containing a substring (for example, two files share a name at different depths and only one should be excluded), use `--exclude-file` instead. It takes comma-delimited relative paths and matches them **exactly**:

croc send --exclude-file "subfolder/image.jpg" \[folder\]

#### Use Pipes - stdin and stdout

You can pipe to `croc`:

cat \[filename\] | croc send

To receive the file to `stdout`, you can use:

croc --yes \[code-phrase\] \> out

#### Send Text

To send URLs or short text, use:

croc send --text "hello world"

#### Send Multiple Files

You can send multiple files directly by listing the files and/or folders:

croc send \[file1\] \[file2\] \[file3\] \[folder1\] \[folder2\]

#### Show QR Code

To show QR code (for mobile devices), use:

croc send --qr \[file(s)-or-folder\]

The QR code opens `https://getcroc.com/?code=...`, where the web client automatically connects in receive-only mode.

#### Use a Proxy

You can send files via a proxy by adding `--socks5`:

croc --socks5 "127.0.0.1:9050" send SOMEFILE

#### Change Encryption Curve

To choose a different elliptic curve for encryption, use the `--curve` flag:

croc --curve p521 <codephrase\>

#### Change Hash Algorithm

For faster hashing, use the `imohash` algorithm:

croc send --hash imohash SOMEFILE

#### Clipboard Options

By default, the code phrase is copied to your clipboard. To disable this:

croc --disable-clipboard send \[filename\]

To copy the full command with the secret as an environment variable (useful on Linux/macOS):

croc --extended-clipboard send \[filename\]

This copies the full command like `CROC_SECRET="code-phrase" croc` (including any relay/pass flags).

#### Quiet Mode

To suppress all output (useful for scripts and automation):

croc --quiet send \[filename\]

#### Self-host Relay

You can run your own relay:

croc relay

By default, it uses TCP ports 9009-9013. You can customize the ports (e.g., `croc relay --ports 1111,1112`), but at least **2** ports are required.

To send files using your relay:

croc --relay "myrelay.example.com:9009" send \[filename\]

#### Self-host Relay with Docker

You can also run a relay with Docker:

docker run -d -p 9009-9013:9009-9013 -e CROC\_PASS='YOURPASSWORD' docker.io/schollz/croc

To send files using your custom relay:

croc --pass YOURPASSWORD --relay "myreal.example.com:9009" send \[filename\]

To use custom ports, set `CROC_PORTS` (comma-separated) or `CROC_PORT` (base port):

docker run -d -p 9010-9011:9010-9011 -e CROC\_PORTS='9010,9011' -e CROC\_PASS='YOURPASSWORD' docker.io/schollz/croc

#### Web client

The React/Vite client in `web/` can send and receive multiple files with normal croc CLI peers. The production client and its WebAssembly protocol runtime are bundled only in the standalone `croc-web` server, keeping generated assets and web-server code out of the cross-platform `croc` binary. Linux amd64 builds of `croc-web` are published separately with each release. It serves both the site and its same-origin WebSocket relay:

croc-web getcroc.com

This binds to `127.0.0.1:9014` by default for an HTTPS reverse proxy. `/` serves the website and `/ws` bridges to `ipv4.getcroc.com`. For a directly accessible local development server, `croc-web localhost:5173` binds and serves on `localhost:5173`. Use `--bind`, `--relay`, and `--ports` before the website address to customize the local listener or upstream croc relay.

Run `make build-web` to generate the ignored production assets and build a local server. See `web/README.md` for frontend development, custom relay, and reverse-proxy instructions.

Deployment
----------

### Disco

Disco is used to deploy. The root `Dockerfile` and `disco.json` deploy the `croc-web` web client and `croc` TCP relay as two Disco services built from the same image. Disco serves the website over HTTPS, while relay ports 9009-9017 are published directly as TCP ports.

Set the deployment environment variables with:

disco env:set \\
  STORE\_DIR=/www/croc/storage \\
  SITE\_URL=yoururl.com \\
  CROC\_RELAY\_PORTS=9009,9010,9011,9012,9013,9014,9015,9016,9017 \\
  CROC\_PASS=yourpass \\
  --project croc

`SITE_URL` must be the public website hostname without `https://`. Change the project name if it is not `croc`. The storage directory is intentionally not attached to a Disco volume, so stored transfers are erased whenever the container is replaced.

The ports in `CROC_RELAY_PORTS` must match the `publishedPorts` entries in `disco.json`; Disco cannot generate host port mappings from an environment variable. Make sure the same TCP ports are also open in the server's firewall or cloud security group.

Acknowledgements
----------------

`croc` has evolved through many iterations, and I am thankful for the contributions! Special thanks to:

-   @warner for the idea
-   @tscholl2 for the encryption gists
-   @skorokithakis for proxying two connections

And many more!
