---
project: superfile
stars: 15781
description: Pretty fancy and modern terminal file manager
url: https://github.com/yorukot/superfile
---

#### superfile is supported by the community.

Special thanks to:  
  

### Warp, the AI terminal for developers

Available for MacOS, Linux, & Windows  

* * *

Demo
----

Perform common operations

Content
-------

-   Installation
-   Build
-   Supported Systems
-   Tutorial
-   Plugins
-   Themes
-   Hotkeys
-   Notes
-   Contributing
-   Troubleshooting
-   Thanks
    -   Support
    -   Core maintainer
    -   Contributors
    -   Star History

Installation
------------

### MacOS and Linux

bash -c "$(curl -sLo- https://superfile.dev/install.sh)"

If you want to inspect the script, see : install.sh

### Windows

#### Powershell

powershell \-ExecutionPolicy Bypass \-Command "Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://superfile.dev/install.ps1'))"

If you want to inspect the script, see : install.ps1

#### Winget

winget install \--id yorukot.superfile

#### Scoop

```
scoop install superfile
```

### More installation methods

Click me to check on how to install

Build
-----

You can build the source code yourself by using these steps:

**Requirements**

-   golang

**Build Steps**

Clone this repository using the following command:

```
git clone https://github.com/yorukot/superfile.git --depth=1
```

Enter the downloaded directory:

cd superfile

### For MacOS/Linux

Run the `build.sh` file:

./build.sh

Add the binary file to your $PATH, e.g., in `/usr/local/bin`:

sudo mv ./bin/spf /usr/local/bin

### For Windows

go build -o bin/spf.exe

Edit System Environment Variables and add superfile repo's `bin` directory to your PATH

Start superfile
---------------

spf

Supported Systems
-----------------

-   Linux
-   MacOS
-   Windows (Not fully supported yet)

Tutorial
--------

After you install superfile, you can go here to briefly understand how to use superfile!

Plugins
-------

Click me to the plugins wiki

Themes
------

Click me to the theme wiki

Hotkeys
-------

Warning

If you are vim/nvim user please change your default hotkeys config to vim version!

**Click me to see the hotkey wiki**

Notes
-----

We have an auto update functionality, that fetches superfile's latest released version from github (if last timestamp of last version check was less than 24 hours) and prints a prompt to user, if there is a newer version available.

You can turn this off, by setting `auto_check_update` to false in superfile config. **Click me to see the config wiki**

Troubleshooting
---------------

**Click me to see common problem fix**

Uninstalling
------------

### MacOS and Linux

On MacOS and Linux, you can uninstall superfile by simply removing the binary. If you installed superfile with sudo, runw

sudo rm /usr/local/bin/spf

If you installed superfile without sudo, run

rm ~/.local/bin/spf

If you don't rember, just try removing both.

### Window

To uninstall superfile on Windows, use this powershell script.

powershell \-ExecutionPolicy Bypass \-Command "Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://superfile.dev/uninstall.ps1'))"

Contributing
------------

If you want to contribute please follow the contribution guide

**Click me to see changelog**

Thanks
------

### Support

-   a Star on my GitHub repository would be nice 🌟
-   You can buy a coffee for me 💖

### Core maintainer

> We welcome anyone who wants to become a core maintainer. Feel free to reach out!

-   **@yorukot** - Original author and maintainer
-   **@lazysegtree** - Core maintainer

### Contributors

**Thanks to all the contributors for making this project even greater!**

### Star History

**THANKS FOR All OF YOUR STARS!** Your stars are my motivation to keep updating!

༼ つ ◕\_◕ ༽つ Please share.
-------------------------
