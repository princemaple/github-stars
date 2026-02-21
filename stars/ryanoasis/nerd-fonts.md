---
project: nerd-fonts
stars: 61737
description: Iconic font aggregator, collection, & patcher. 3,600+ icons, 50+ patched fonts: Hack, Source Code Pro, more. Glyph collections: Font Awesome, Material Design Icons, Octicons, & more
url: https://github.com/ryanoasis/nerd-fonts
---

Releases   |   Fonts   |   Font Patcher   |   Wiki Documentation   |   Stickers   |   VimDevIcons

**Nerd Fonts** is a project that patches developer targeted fonts with a high number of glyphs (icons). Specifically to add a high number of extra glyphs from popular 'iconic fonts' such as Font Awesome, Devicons, Octicons, and others.

The following flow diagram shows the current glyph sets included:

_Diagram created using @SankeyMATIC_

Important Notices
-----------------

-   `master` branch file paths are **not** considered stable. Verify your repository URI references
-   cloning this repository is **not** recommended (due to Repo size) unless you are going to be contributing to development

Table of Contents
-----------------

**TL;DR**

**Installation Options**

-   **1 - Release Archive Download**
-   **2 - Homebrew Fonts (macOS (OS X))**
-   **3 - Chocolatey or Scoop (Windows)**
-   **4 - Arch Linux Repository (Extra, AUR)**
-   **5 - PowerShell Installer (Multi-Platform)**
-   **6 - Ad Hoc Curl Download**
-   **7 - Install Script**
-   **8 - Use Fontfallback**
-   **9 - Clone Repo**
-   **10 - Patch Your Own Font**

**Features**

-   **Glyph/Icon sets**
-   **Patched Fonts**
-   **Variations**
-   **Font Patcher**

**Developer / Contributor**

-   **Font Patcher**
-   **Gotta Patch 'em All Font Patcher!**
-   **Other Good Fonts to Patch**
-   **Contributing**

**Project Motivation**

**Additional Info**

-   **In case of problems**
-   **Unstable file paths on master**
-   **Changelog**
-   **License**

TL;DR
-----

Nerd Fonts takes popular programming fonts and adds a bunch of Glyphs. There is also a font patcher available if your desired font isn't already patched. For more high level information see the wiki. If you are looking for the Vim plugin see VimDevIcons ➶.

### Various Download Options for Fonts

_If you..._

-   `Option 1.` want to download a **font family** package of variations (bold, italic, etc.) see download an archive
-   `Option 2.` are on **macOS** and want to use **Homebrew** see Homebrew Fonts
-   `Option 3.` are on **Windows** and want to use **Chocolatey** or **Scoop** see Unofficial Chocolatey or Scoop Repositories
-   `Option 4.` are on **Arch Linux** and want to use **Extra packages** see Arch Extra Repositories
-   `Option 5.` are using **PowerShell** and want an **interactive setup** or **use in scripts** see the PowerShell Installer
-   `Option 6.` want to use the **`curl` command** or use in **scripts** see Ad Hoc Curl Download
-   `Option 7.` want to **automate** installing or use in **scripts** see the Install Script
-   `Option 8.` want to install only one font for all fonts see Font Fallback
-   `Option 9.` want **complete control** then see cloning the repo
-   `Option 10.` want to patch your own font see the Font Patcher

Features
--------

-   A FontForge Python script to patch any font
    -   Includes an option to create **Monospaced (fixed-pitch, fixed-width)** _or_ **double-width (non-monospaced)** glyphs
    -   For more details see the **Font Patcher** section
-   **`67`** already patched font families
-   Over **`10,000`** glyphs/icons combined (more details)
    -   Current glyph sets include: Powerline with Extra Symbols, Font Awesome, Material Design Icons, Weather, Devicons, Octicons, Font Logos (Formerly Font Linux), Pomicons, Codeicons
-   **Monospaced (fixed-pitch, fixed-width)** _or_ **double-width (non-monospaced)** _or_ **proportional** glyphs version of each font
    -   This refers to the Nerd Font glyphs themselves not necessarily the Font as a whole
-   A Developer/Contributor provided bash script to re-patch all the fonts

Glyph Sets
----------

🔍 🔍 You can search for glyphs easily on NerdFonts.com via the Cheat Sheet

See Wiki: Glyph Sets and Codepoints for more details

### Icon names in shell

See Wiki: Icon names in shell

Patched Fonts
-------------

A preview of all fonts can be found here.

Font Name

Original Font Name and Repository

ver

\*RFN

0xProto Nerd Font

0xProto

2.300

NO

3270 Nerd Font

3270

3.0.1

NO

AdwaitaMono Nerd Font

Adwaita Mono

32.4

NO

Agave Nerd Font

Agave

37

NO

AnonymicePro Nerd Font

Anonymous Pro

1.002

YES

Arimo Nerd Font

Arimo

1.33

NO

AtkynsonMono Nerd Font

Atkinson Hyperlegible Mono

2.001

YES

AurulentSansMono Nerd Font

Aurulent Sans Mono (Stephen G. Hartke)

NO

BigBlueTerminal Nerd Font

BigBlueTerminal (VileR)

NO

BitstromWera Nerd Font

Vera Sans Mono (Bitstream Inc)

1.1

YES

BlexMono Nerd Font

IBM Plex Mono

2.004

YES

CaskaydiaCove Nerd Font

Cascadia Code

2407.24

YES

CaskaydiaMono Nerd Font

Cascadia Mono

2407.24

YES

CodeNewRoman Nerd Font

Code New Roman (Sam Radian)

2.0

NO

ComicShannsMono Nerd Font

Comic Shanns Mono

1.3.2

NO

CommitMono Nerd Font

Commit Mono

1.143

NO

Cousine Nerd Font

Cousine

1.211

NO

D2Coding Nerd Font

D2Coding

1.3.2

NO

DaddyTimeMono Nerd Font

DaddyTimeMono

1.2.3

NO

DepartureMono Nerd Font

Departure Mono

1.422

NO

DejaVuSansMono Nerd Font

DejaVu

2.37

NO

DroidSansMono Nerd Font

Droid Sans Mono (Ascender Corp)

1.00-113

NO

EnvyCodeR Nerd Font

Envy Code R

0.79

YES

FantasqueSansMono Nerd Font

Fantasque Sans Mono

1.8.0

NO

FiraCode Nerd Font

Fira Code

6.2

NO

FiraMono Nerd Font

Fira Mono

3.206

NO

GeistMono Nerd Font

Geist Mono

1.401

NO

GoMono Nerd Font

Go-Mono

2.010

NO

Gohu Nerd Font

Gohu TTF, Gohu

2.0

NO

Hack Nerd Font

Hack

3.003

NO

Hasklug Nerd Font

Hasklig

1.2

YES

HeavyDataMono Nerd Font

HeavyData (Vic Fieger)

1

NO

Hurmit Nerd Font

Hermit

2.0

YES

iM-Writing Nerd Font

iA-Writer

Dec 2018

YES

Inconsolata Nerd Font

Inconsolata

3.000

NO

InconsolataGo Nerd Font

InconsolataGo

1.013

NO

Inconsolata LGC Nerd Font

Inconsolata LGC

1.13

NO

IntoneMono Nerd Font

Intel One Mono

1.4.0

YES

Iosevka Nerd Font

Iosevka

33.2.1

NO

IosevkaTerm Nerd Font

Iosevka Term

33.2.1

NO

IosevkaTermSlab Nerd Font

Iosevka Term Slab

33.2.1

NO

JetBrainsMono Nerd Font

JetBrains Mono

2.304

NO

Lekton Nerd Font

Lekton

34

NO

Literation Nerd Font

Liberation

2.1.5

YES

Lilex Nerd Font

Lilex

2.600

NO

MartianMono Nerd Font

MartianMono

1.1.0

NO

Meslo Nerd Font

Meslo

1.21

NO

Monaspice Nerd Font

Monaspace

1.200

YES

Monofur Nerd Font

Monofur (Tobias B Koehler)

1.0

NO

Monoid Nerd Font

Monoid

0.61

NO

Mononoki Nerd Font

Mononoki

1.6

YES

M+ Nerd Font

MPlus Fonts

1.007

NO

Noto Nerd Font

Noto

div

NO

OpenDyslexic Nerd Font

OpenDyslexic

2.001

NO

Overpass Nerd Font

Overpass

3.0.5

NO

ProFont Nerd Font

ProFont

2.3, 2.2

NO

ProggyClean Nerd Font

ProggyClean (Tristan Grimmer)

2004/04/15

NO

RecMono Nerd Font

Recursive Mono

1.085

NO

RobotoMono Nerd Font

Roboto Mono

3.0

NO

SauceCodePro Nerd Font

Source Code Pro

2.042

YES

ShureTechMono Nerd Font

Share Tech Mono

1.003

YES

SpaceMono Nerd Font

Space Mono

1.001

NO

Terminess Nerd Font

Terminus TTF

4.49.3

YES

Tinos Nerd Font

Tinos

1.23

NO

Ubuntu Nerd Font

Ubuntu Font

0.83

NO

UbuntuMono Nerd Font

Ubuntu Font

0.80

NO

UbuntuSans Nerd Font

Ubuntu Sans

1.006

NO

VictorMono Nerd Font

Victor Mono

1.5.6

NO

ZedMono Nerd Font

Zed Mono

1.2.0

NO

_\*RFN = Reserved Font Name_

### Variations

-   no flags given (defaults to only **Seti-UI + Custom** and **Devicons**)
-   **double _(variable/proportional)_** or **single _(fixed/monospaced)_** or **proportional** width icon-glyphs
-   Font Awesome
-   Font Awesome Extension
-   Material Design Icons
-   Weather
-   GitHub Octicons
-   Font Logos (Formerly Font Linux)
-   Powerline Extra Symbols
-   IEC Power Symbols
-   Pomicons
-   Codicons

Font Installation
-----------------

Some of the options below just help you to download the font file(s) (i.e. `.ttf` or `.otf`) or archives of font files. These must be installed on your system, depending on your OS. Usually (double) clicking the font files individually does the trick. Ask your OS' community if installing a font file is a problem.

### `Option 1: Release Archive Download`

> Best option if you want an **archive** or complete **font family** of variations (Bold, Italic, etc.).

Fonts are available for download as packages in the latest release A nice overview is on the Nerd Font site (but misses the more compact `xv` archives).

If you want download the latest release of a given font inside a script you can use (replace "JetBrainsMono" with your font):

curl -OL https://github.com/ryanoasis/nerd-fonts/releases/latest/download/JetBrainsMono.tar.xz

### `Option 2: Homebrew Fonts`

> Best option if on **macOS** and want to use **Homebrew**.

All fonts are available via Homebrew Cask on macOS (OS X)

brew install font-hack-nerd-font

_On Linux you have to add `--cask` after `install`._

### `Option 3: Unofficial Chocolatey or Scoop Repositories`

> Option for **Windows** and wanting to use **Chocolatey** or **Scoop**.

Chocolatey users can download fonts published to the Chocolatey Community Repository (CCR):

choco install nerd\-fonts\-hack

Scoop users can download fonts using the Scoop bucket for Nerd Fonts:

scoop bucket add nerd\-fonts
scoop install Hack\-NF

### `Option 4: Arch Extra Repository`

> Option for **Arch Linux** and wanting to use **Extra packages**.

Most fonts are available via Arch Extra packages. Some special packages are in AUR.

### `Option 5: PowerShell Installer`

> Best option for **interactive setup guidance** or **automating** installations through **PowerShell scripts**.

#### PSModule NerdFonts

This is a 3rd-party community tool. More information can be found on its GitHub repository here.

To install the module:

Install-PSResource \-Name NerdFonts
Import-Module \-Name NerdFonts

To install one font:

Install-NerdFont \-Name 'FiraCode' # Tab completion works on name

#### Powershell Web Installer

This is a 3rd-party community tool. More information can be found on its GitHub repository here.

-   **Requires PowerShell 7+** to be installed on Windows, macOS, or Linux.
-   **Windows PowerShell 5.1** is also supported.

To run the interactive installer, use the following command:

& (\[scriptblock\]::Create((iwr 'https://to.loredo.me/Install-NerdFont.ps1')))

To install specific fonts directly, use the following command:

& (\[scriptblock\]::Create((iwr 'https://to.loredo.me/Install-NerdFont.ps1'))) \-Name hack, heavy\-data

### `Option 6: Ad Hoc Curl Download`

> Option if you want to use the **`curl` command** or for use in **scripts**.

_Note_: Will not work to get newer fonts as they are not inside the repo anymore.

#### Linux

mkdir -p ~/.local/share/fonts
cd ~/.local/share/fonts && curl -fLO https://github.com/ryanoasis/nerd-fonts/raw/HEAD/patched-fonts/DroidSansMono/DroidSansMNerdFont-Regular.otf

_Note:_ deprecated alternative paths: `~/.fonts`

#### macOS (OS X)

cd ~/Library/Fonts && curl -fLO https://github.com/ryanoasis/nerd-fonts/raw/HEAD/patched-fonts/DroidSansMono/DroidSansMNerdFont-Regular.otf

### `Option 7: Install Script`

> Best option if you want to **automate** installing or for use in **scripts**.

_Note_:

-   **Requires (shallow) cloning** the repo as of now :-(
-   Will not work to get newer fonts as they are not inside the repo anymore.

#### All fonts:

-   Installs all the patched Fonts (_Warning: This is a lot of Fonts adding up to a large size_)

./install.sh

or, in PowerShell (Windows only):

./install.ps1

#### Single font:

-   Installs a single Font of your choice

./install.sh <FontName\>
./install.sh Hack
./install.sh HeavyData

or, in PowerShell (Windows only):

./install.ps1 <FontName\>
./install.ps1 Hack
./install.ps1 HeavyData
./install.ps1 FiraCode, Hack
./install.ps1 DejaVuSansMono \-WhatIf

### `Option 8: Font Fallback`

Most systems have a mechanism to search for an alternative font when the current font does not have a glyph that is needed. For example you edit a Latin text and insert a Chinese character, that glyph is taken not from your active font (it does not have it) but from some other font.

For this font fallback you can use one of the `SymbolsOnly` fonts.

For fontconfig based systems like Linux you can improve the behavior with the `10-nerd-font-symbols.conf` configuration file, that needs to be manually installed.

-   Pro: One symbol font is sufficient for all text fonts
-   Con: Scaling and placement of the fallback symbols can be hit or miss

### `Option 9: Clone the Repo`

> Best option for **full control**, **all** or **some** of the fonts, or **contributing** to development.

_Note_: Will not work to get newer fonts as they are not inside the repo anymore.

A full clone of this repository is **not** required nor efficient (mostly due to Repository size) if you are simply only interested in a limited set of fonts.

If you do want to clone the entire repo be sure to _shallow_ clone:

git clone --depth 1

Even if you develop you probably do not need the old versions of the font files. With this command you have all commits but not all the old data - it will be loaded only if you check out old binaries (or do a blame):

git clone --filter=blob:none git@github.com:ryanoasis/nerd-fonts

If you want to clone just a sub-directory, use `git sparse-checkout`.

git clone --filter=blob:none --sparse git@github.com:ryanoasis/nerd-fonts
cd nerd-fonts
git sparse-checkout add patched-fonts/JetBrainsMono

### `Option 10: Patch Your Own Font`

> The option for **patching** your **own font** or fully **customizing** the patched font.

Use the provided Python command line script to generate a patched font from your own font to get the extra new glyphs

See: Font Patcher for usage

-   use this option if you do **not** want to use one of the fonts provided
-   you will still need to copy the generated font to the correct font directory on your system

font-patcher
------------

Patching the font of your own choosing:

-   Use the script
    
    -   Download script and its helper files as archive and extract
    -   Just downloading the `font-patcher` script is not enough.
    -   Requires: Fontforge, Python 3, `python-fontforge` and `argparse` packages
        -   Fontforge can be installed as package
        -   or on OSX via `brew install fontforge`
        -   or as AppImage
    -   Usage, recommended:
    
    ```
    fontforge -script font-patcher PATH_TO_FONT
    ```
    
    -   Usage, direct (more convenient call, if it works for you):
    
    ```
    ./font-patcher PATH_TO_FONT
    ```
    
    -   Usage, with Fontforge AppImage
        
        _Note_: `chmod u+x` the AppImage after download. All supplied paths need to be **absolute** and an explicit output path is required! If everything is located in the same directory, you can use the `$PWD` shorthand.
        
    
    ```
    ./FontForge.AppImage -script $PWD/font-patcher $PWD/BaseFont.ttf -out /tmp
    ```
    
-   Use docker
    
    -   Default parallel tasks
    
    ```
    docker run --rm -v /path/to/fonts:/in:Z -v /path/for/output:/out:Z nerdfonts/patcher [OPTIONS]
    ```
    
    -   Single process (slow)
    
    ```
    docker run --rm -v /path/to/fonts:/in:Z -v /path/for/output:/out:Z -e "PN=1" nerdfonts/patcher [OPTIONS]
    ```
    
    -   Specify the parallel tasks number to 10
    
    ```
    docker run --rm -v /path/to/fonts:/in:Z -v /path/for/output:/out:Z -e "PN=10" nerdfonts/patcher [OPTIONS]
    ```
    
    -   Update docker image
    
    ```
    docker pull nerdfonts/patcher
    ```
    
    -   Run interatively to get full control of `font-patcher` invocation and all debug output and error messages:
    
    ```
    docker run -it -v /path/to/fonts:/in:Z --entrypoint=/bin/sh nerdfonts/patcher
    ```
    
    And then in the container for example:
    
    ```
    / # cd /in
    /in # fontforge --script ../nerd/font-patcher [OPTIONS] your_font.ttf
    ```
    

Note

The resulting font's family (aka font name) will be set to the original family after CamelCasing, removing whitespace and appending `Nerd Font`. For example, `iosevka term` would become `IosevkaTerm Nerd Font`.

Full options follow, see also **page explaining all options**:

```
Nerd Fonts Patcher v3.4.0-91 (4.22.1) (ff 20230101)
usage: font-patcher [--careful] [--debug [{0,1,2,3}]] [--extension EXTENSION]
                    [--help] [--makegroups [{-1,0,1,2,3,4,5,6}]] [--mono]
                    [--outputdir OUTPUTDIR] [--quiet] [--single-width-glyphs]
                    [--variable-width-glyphs] [--version]
                    [--braille [{rectangle,circle,gapless}]] [--complete]
                    [--codicons] [--fontawesome] [--fontawesomeext] [--fontlogos]
                    [--material] [--octicons] [--pomicons] [--powerline]
                    [--powerlineextra] [--powersymbols] [--weather]
                    [--adjust-line-height] [--boxdrawing] [--cell CELLOPT]
                    [--configfile CONFIGFILE] [--custom CUSTOM] [--dry]
                    [--glyphdir GLYPHDIR] [--has-no-italic]
                    [--metrics {HHEA,TYPO,WIN}] [--name FORCE_NAME]
                    [--postprocess POSTPROCESS] [--removeligs]
                    [--xavgcharwidth [XAVGWIDTH]] [--progressbars | --no-progressbars]
                    font

Nerd Fonts Font Patcher: patches a given font with programming and development related glyphs

* Website: https://www.nerdfonts.com
* Version: 3.4.0-88
* Development Website: https://github.com/ryanoasis/nerd-fonts
* Changelog: https://github.com/ryanoasis/nerd-fonts/blob/-/changelog.md

positional arguments:
  font                  The path to the font to patch (e.g., Inconsolata.otf)

options:
  --careful             Do not overwrite existing glyphs if detected
  --debug [{0,1,2,3}]   Verbose mode (optional: 1=just to file; 2*=just to terminal; 3=display and file)
  --extension, -ext EXTENSION
                        Change font file type to create (e.g., ttf, otf)
  --help, -h            Show this help message and exit
  --makegroups [{-1,0,1,2,3,4,5,6}]
                        Use alternative method to name patched fonts (default=1)
  --mono, -s            Create monospaced font, existing and added glyphs are single-width (implies --single-width-glyphs)
  --outputdir, -out OUTPUTDIR
                        The directory to output the patched font file to
  --quiet, -q           Do not generate verbose output
  --single-width-glyphs
                        Whether to generate the glyphs as single-width not double-width (default is double-width) (Nerd Font Mono)
  --variable-width-glyphs
                        Do not adjust advance width (no "overhang") (Nerd Font Propo)
  --version, -v         Show program's version number and exit

Symbol Fonts:
  --braille [{rectangle,circle,gapless}]
                        Add Braille Glyphs, can pass a string to control style (optional: *rectangle, circle, gapless)
  --complete, -c        Add all available Glyphs
  --codicons            Add Codicons Glyphs (https://github.com/microsoft/vscode-codicons)
  --fontawesome         Add Font Awesome Glyphs (http://fontawesome.io/)
  --fontawesomeext      Add Font Awesome Extension Glyphs (https://andrelzgava.github.io/font-awesome-extension/)
  --fontlogos           Add Font Logos Glyphs (https://github.com/Lukas-W/font-logos)
  --material, --mdi     Add Material Design Icons (https://github.com/templarian/MaterialDesign)
  --octicons            Add Octicons Glyphs (https://octicons.github.com)
  --pomicons            Add Pomicon Glyphs (https://github.com/gabrielelana/pomicons)
  --powerline           Add Powerline Glyphs
  --powerlineextra      Add Powerline Extra Glyphs (https://github.com/ryanoasis/powerline-extra-symbols)
  --powersymbols        Add IEC Power Symbols (https://unicodepowersymbol.com/)
  --weather             Add Weather Icons (https://github.com/erikflowers/weather-icons)

Expert Options:
  --adjust-line-height, -l
                        Whether to adjust line heights (attempt to center powerline separators more evenly)
  --boxdrawing          Force patching in (over existing) box drawing glyphs
  --cell CELLOPT        Adjust or query the cell size, e.g. use "0:1000:-200:800" or "?"
  --configfile CONFIGFILE
                        Specify a file path for configuration file (see sample: src/config.sample.cfg)
  --custom CUSTOM       Specify a custom symbol font, all glyphs will be copied; absolute path suggested
  --dry                 Do neither patch nor store the font, to check naming
  --glyphdir GLYPHDIR   Path to glyphs to be used for patching
  --has-no-italic       Font family does not have Italic (but Oblique), to help create correct RIBBI set
  --metrics {HHEA,TYPO,WIN}
                        Select vertical metrics source (for problematic cases)
  --name FORCE_NAME     Specify naming source ('full', 'postscript', 'filename', or concrete free name-string)
  --postprocess POSTPROCESS
                        Specify a Script for Post Processing
  --removeligs, --removeligatures
                        Removes ligatures specified in configuration file (needs --configfile)
  --xavgcharwidth [XAVGWIDTH]
                        Adjust xAvgCharWidth (optional: concrete value)
  --progressbars        Show percentage completion progress bars per Glyph Set (default)
  --no-progressbars     Don't show percentage completion progress bars per Glyph Set
```

#### Examples

```
./font-patcher Droid\ Sans\ Mono\ for\ Powerline.otf
./font-patcher Droid\ Sans\ Mono\ for\ Powerline.otf -s -q
./font-patcher Droid\ Sans\ Mono\ for\ Powerline.otf --mono --quiet

./font-patcher Inconsolata.otf --fontawesome
./font-patcher Inconsolata.otf --fontawesome --octicons --pomicons
./font-patcher Inconsolata.otf

./FontForge.AppImage -script /tmp/nerdfonts/font-patcher /tmp/nerdfonts/CascadiaMonoPL-Semibold.ttf --fontawesome -out /tmp
./FontForge.AppImage -script $PWD/font-patcher $PWD/CascadiaMonoPL-Semibold.ttf --octicons -out $HOME

docker run --rm -v ~/myfont/patchme:/in:Z -v ~/myfont/patched:/out:Z nerdfonts/patcher
docker run --rm -v ~/Desktop/myfont/patchme:/in:Z -v ~/Desktop/myfont/patched:/out:Z nerdfonts/patcher --fontawesome
```

Usually you want the `--complete` option.

Gotta Patch 'em All Font Patcher!
---------------------------------

-   for Contributor or Developer use
    
-   re-patches **all** fonts in the unpatched directory:
    
    ```
    ./gotta-patch-em-all-font-patcher\!.sh
    ```
    
-   can optionally limit to specific font name pattern:
    
    ```
    ./gotta-patch-em-all-font-patcher\!.sh Hermit
    ```
    
-   or to specific directory name start:
    
    ```
    ./gotta-patch-em-all-font-patcher\!.sh /Heavy
    ```
    

Full options:

```
Usage: ./gotta-patch-em-all-font-patcher!.sh [OPTION] [FILTER]

    OPTION:
        -c, --checkfont     Create the font(s) in check-fonts/ instead
        -t, --keeptime      Try to preserve timestamp of previously patched
                            font in patched-fonts/ directory
        -v, --verbose       Show more information when running
        -i, --info          Rebuild JUST the readmes
        -j, --jobs          Run up to 8 patch processes in parallel
        -h, --help          Show this help

    FILTER:
        The filter argument to this script is a filter for the fonts to patch.
        The filter is a regex (glob * is expressed as [^/]*, see `man 7 glob`)
        All font files that start with that filter (and are ttf, otf, or sfd files) will
        be processed only.
          Example ./gotta-patch-em-all-font-patcher\!.sh "iosevka"
          Process all font files that start with "iosevka"
        If the argument starts with a '/' all font files in a directory that matches
        the filter are processed only.
          Example ./gotta-patch-em-all-font-patcher\!.sh "/iosevka"
          Process all font files that are in directory "iosevka"
```

Contributing
------------

See contributing.md

Common Problems
---------------

Some solutions can be found on the Wiki, if you are lucky. For example hints to use the pager `less` are there:

-   https://github.com/ryanoasis/nerd-fonts/wiki/FAQ-and-Troubleshooting
-   https://github.com/ryanoasis/nerd-fonts/wiki/Terminal-Emulators
-   https://github.com/ryanoasis/nerd-fonts/wiki/Reporting-Issues

Unstable File Paths
-------------------

⚠️ Warning: File paths may change based on releases (especially **major** version bumps)

Reference the **release** tag or branch and _not_ the master branch because paths are subject to change for each release

-   For example:
    -   ✅ Use: `https://github.com/ryanoasis/nerd-fonts/tree/**v3.0.0**/patched-fonts/Hermit/Regular/HurmitNerdFont-Regular.otf`
    -   ✅ Use: `https://github.com/ryanoasis/nerd-fonts/blob/**0.9.0**/patched-fonts/Hermit/Medium/complete/Hurmit%20Medium%20Nerd%20Font%20Complete.otf`
    -   ❌ Instead of: `https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/Hermit/Medium/complete/Hurmit%20Medium%20Nerd%20Font%20Complete.otf`

Other Good Fonts to Patch
-------------------------

Non exhaustive list of fonts that would benefit from being patched but are not included in Nerd Fonts due to their license (proprietary, commercial, etc.):

-   Consolas
-   Dank Mono
-   Input Mono
-   Operator Mono
-   PragmataPro
-   SF Mono

Project Motivation
------------------

See Wiki: Project Purpose

Changelog
---------

See changelog.md

License
-------

See LICENSE
