---
project: trzsz-ssh
stars: 2451
description: trzsz-ssh ( tssh ) is an ssh client designed as a drop-in replacement for the openssh client. It aims to provide complete compatibility with openssh, mirroring all its features, while also offering additional useful features. Such as login prompt, batch login, remember password, automated interaction, trzsz, zmodem(rz/sz), udp mode like mosh, etc.
url: https://github.com/trzsz/trzsz-ssh
---

trzsz-ssh ( tssh ) - an ssh client alternative that meets your needs
--------------------------------------------------------------------

trzsz-ssh ( tssh ) is an ssh client designed as a drop-in replacement for the openssh client. It aims to provide complete compatibility with openssh, mirroring all its features, while also offering additional useful features not found in the openssh client.

trzsz-ssh ( tssh ) with tsshd also supports intermittent connectivity, allows roaming, and can be used on high-latency links such as cellular data connections, unstable Wi-Fi, etc.

### Basic Features

trzsz-ssh ( tssh ) works exactly like the openssh client. The following common features have been implemented:

Features

Support Options

Cipher

`-c` `Ciphers`

Pseudo TTY

`-t` `-T` `RequestTTY`

SSH Proxy

`-J` `-W` `ProxyJump` `ProxyCommand`

Network

`-4` `-6` `AddressFamily` `ConnectTimeout`

Multiplexing

`ControlMaster` `ControlPath` `ControlPersist`

Command

`-s` `RemoteCommand` `LocalCommand` `PermitLocalCommand`

Known Hosts

`UserKnownHostsFile` `GlobalKnownHostsFile` `StrictHostKeyChecking`

SSH Agent

`-a` `-A` `ForwardAgent` `IdentityAgent` `IdentitiesOnly` `SSH_AUTH_SOCK`

Basic Login

`-l` `-p` `-i` `-F` `HostName` `Port` `User` `IdentityFile` `SendEnv` `SetEnv`

X11 Forward

`-x` `-X` `-Y` `ForwardX11` `ForwardX11Trusted` `ForwardX11Timeout` `XAuthLocation`

Authentication

`PubkeyAuthentication` `PasswordAuthentication` `KbdInteractiveAuthentication` `GSSAPIAuthentication`

Port Forward

`-g` `-f` `-N` `-L` `-R` `-D` `LocalForward` `RemoteForward` `DynamicForward` `GatewayPorts` `ClearAllForwardings`

Others

`EscapeChar`

### Extra Features

trzsz-ssh ( tssh ) offers additional useful features:

English

中文

Login Prompt

登录界面

Custom Theme

主题风格

Trzsz ( trz / tsz )

支持 trz tsz

Zmodem ( rz / sz )

支持 rz sz

Support scp sftp

支持 scp sftp

Batch Login

批量登录

Group Labels

分组标签

Automated Interaction

自动交互

Remember Password

记住密码

Custom Configuration

个性配置

Comments of Config

配置注释

Wayland Integration

Wayland 集成

Clipboard Integration

剪贴板集成

SSH Console

SSH 控制台

Other Features

其他功能

UDP Mode ( mosh )

UDP 模式 ( mosh )

UDP Port Forwarding

UDP 端口转发

### Installation

-   Install with scoop / winget / choco on Windows
    
    `scoop install tssh` / `winget install tssh` / `choco install tssh`
    
    scoop install tssh
    
    winget install tssh
    
    choco install tssh
    
-   Install with Homebrew on MacOS
    
    `brew install trzsz-ssh`
    
    brew install trzsz-ssh
    
-   Install with apt on Ubuntu
    
    `sudo apt install tssh`
    
    sudo apt update && sudo apt install software-properties-common
    sudo add-apt-repository ppa:trzsz/ppa && sudo apt update
    
    sudo apt install tssh
    
-   Install with apt on Debian
    
    `sudo apt install tssh`
    
    sudo apt install curl gpg
    curl -s 'https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x7074ce75da7cc691c1ae1a7c7e51d1ad956055ca' \\
      | gpg --dearmor -o /usr/share/keyrings/trzsz.gpg
    echo 'deb \[signed-by=/usr/share/keyrings/trzsz.gpg\] https://ppa.launchpadcontent.net/trzsz/ppa/ubuntu jammy main' \\
      | sudo tee /etc/apt/sources.list.d/trzsz.list
    sudo apt update
    
    sudo apt install tssh
    
-   Install with yum on Linux
    
    `sudo yum install tssh`
    
    -   Install with gemfury repository.
        
        echo '\[trzsz\]
        name=Trzsz Repo
        baseurl=https://yum.fury.io/trzsz/
        enabled=1
        gpgcheck=0' | sudo tee /etc/yum.repos.d/trzsz.repo
        
        sudo yum install tssh
        
    -   Install with wlnmp repository. It's not necessary to configure the epel repository for tssh.
        
        curl -fsSL "https://sh.wlnmp.com/wlnmp.sh" | bash
        
        sudo yum install tssh
        
    
-   Install with yay on ArchLinux
    
    `yay -S tssh`
    
    yay -Syu
    yay -S tssh
    
-   Install with Chromebrew on ChromeOS
    
    `crew install tssh`
    
    crew install tssh
    
-   Install with Go ( Requires go 1.25 or later )
    
    `go install github.com/trzsz/trzsz-ssh/cmd/tssh@latest`
    
    go install github.com/trzsz/trzsz-ssh/cmd/tssh@latest
    
    The binaries are usually located in ~/go/bin/ ( C:\\Users\\your\_name\\go\\bin\\ on Windows ).
    
-   Build from source ( Requires go 1.25 or later )
    
    `sudo make install`
    
    git clone --depth 1 https://github.com/trzsz/trzsz-ssh.git
    cd trzsz-ssh
    make
    sudo make install
    
-   Download from the GitHub Releases and install locally
    
    `download and install locally`
    
    sudo apt install /tmp/tssh\_\*.deb
    
    sudo dpkg -i /tmp/tssh\_\*.deb
    
    sudo dnf install /tmp/tssh\_\*.rpm
    
    sudo yum install /tmp/tssh\_\*.rpm
    
    sudo rpm -i /tmp/tssh\_\*.rpm
    
    tar zxvf tssh\_\*.tar.gz && sudo cp tssh\_\*/tssh /usr/bin/
    

### Development

The `github.com/trzsz/trzsz-ssh/tssh` can be used as a library, for example:

package main

import (
	"log"
	"os"

	"github.com/trzsz/trzsz-ssh/tssh"
)

func main() {
	// Example 1: execute command on remote server
	client, err := tssh.SshLogin(&tssh.SshArgs{Destination: "root@192.168.0.1"})
	if err != nil {
		log.Fatal(err)
	}
	defer client.Close()
	session, err := client.NewSession()
	if err != nil {
		log.Fatal(err)
	}
	defer session.Close()
	output, err := session.CombinedOutput("whoami")
	if err != nil {
		log.Fatal(err)
	}
	log.Printf("I'm %s", string(output))

	// Example 2: run the tssh program
	code := tssh.TsshMain(\[\]string{"-t", "root@192.168.0.1", "bash -l"})
	os.Exit(code)
}

### Contributing

Welcome and thank you for considering contributing. We appreciate all forms of support, from coding and testing to documentation and CI/CD improvements.

-   Fork and clone the repository `https://github.com/trzsz/trzsz-ssh.git`.
    
-   Make your changes just ensure that the unit tests `go test ./tssh` pass.
    
-   Build the binary `go build -o ./bin/ ./cmd/tssh` and test it `./bin/tssh`.
    
-   Once you are happy with your changes, please submit a pull request.
    

### Screenshot

### Contact

Feel free to email the author lonnywong@qq.com, or create an issue. Welcome to join the QQ group: 318578930.

### Sponsor

❤️ Sponsor trzsz ❤️, buy the author a drink 🍺 ? Thank you for your support!
