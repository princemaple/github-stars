---
project: jumpserver
stars: 31568
description: JumpServer is an Open-source Privileged Access Management (PAM) platform with AI-powered capabilities, providing DevOps and IT teams a unified workspace to securely access SSH, RDP, Kubernetes, databases, websites, RemoteApp, VirtualApp, and more.
url: https://github.com/jumpserver/jumpserver
---

An open-source PAM platform (Bastion Host)
------------------------------------------

English · 中文(简体) · 中文(繁體) · 日本語 · Português (Brasil) · Español · Русский · 한국어 · Tiếng Việt

  

What is JumpServer?
-------------------

JumpServer is an open-source Privileged Access Management (PAM) platform with AI-powered capabilities. It gives DevOps and IT teams a unified workspace for secure access to SSH, RDP, Kubernetes, databases, websites, RemoteApp, VirtualApp, and more.

Quickstart
----------

Prepare a clean 64-bit Linux server with at least 4 CPU cores and 8 GB of RAM.

curl -sSL https://github.com/jumpserver/jumpserver/releases/latest/download/quick\_start.sh | bash

Open JumpServer in your browser at `http://your-jumpserver-ip/`

-   Username: `admin`
-   Password: `ChangeMe`

Screenshots
-----------

Components
----------

JumpServer groups its components by role. Core projects provide the platform, web interface, terminal, protocol connections, and AI capabilities. Enterprise components extend application and protocol access. Supporting services handle session recordings and host operations, while deployment tools simplify installation and web delivery.

### Core Projects

Project

Version

Description

JumpServer

Open-source Privileged Access Management platform

Lina

JumpServer web interface

Luna

JumpServer web terminal and native client

KoKo

JumpServer general-purpose protocol connector and proxy

Chen

JumpServer web database connector

Kael

JumpServer AI component

### Enterprise Components

Project

Version

Description

Tinker

JumpServer Windows application connector (free for Community Edition)

Panda

JumpServer Enterprise Edition Linux application connector

Razor

JumpServer Enterprise Edition RDP protocol proxy

Magnus

JumpServer Enterprise Edition database protocol proxy

Nec

JumpServer Enterprise Edition VNC protocol proxy

### Supporting Services

Project

Version

Description

Video Worker

JumpServer Enterprise Edition session recording transcoding worker

JDMC

JumpServer Enterprise Edition host operations and management service

### Deployment & Tooling

Project

Version

Description

Installer

JumpServer installation and management tool

Docker Web

JumpServer web gateway and static assets

Contributing
------------

Contributions are welcome. See CONTRIBUTING.md for guidelines.

License
-------

Copyright (c) 2014-2026 FIT2CLOUD, All rights reserved.

Licensed under The GNU General Public License version 3 (GPLv3) (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

https://www.gnu.org/licenses/gpl-3.0.html

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an " AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
