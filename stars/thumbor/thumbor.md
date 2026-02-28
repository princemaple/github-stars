---
project: thumbor
stars: 10458
description: thumbor is an open-source photo thumbnail service by globo.com
url: https://github.com/thumbor/thumbor
---

#### Join thumbor-bootcamp for a learning and contribution experience with ❤️ and 🤗 from the thumbor team

### Crop, resize, transform and much more, all on-demand and AI Powered

  

#### thumbor is trusted by hundreds of companies worldwide

                     
and many more!

thumbor is a smart imaging service that enables on-demand cropping, resizing, applying filters and optimizing images.

Cropping photos automatically can be a frustrating experience with severed heads involved. thumbor uses AI for smart detection.

thumbor is an HTTP server and you can create as many different images as you want just by varying path parameters:

```
http://<thumbor-server>/300x200/smart/thumbor.readthedocs.io/en/latest/_images/logo-thumbor.png
```

You should see an image of the thumbor logo in 300x200.

Learn more about all you can do in thumbor's documentation.

⚙️ Installation
---------------

Decide which installation option you want to use.

### Option 1: pip

# thumbor with main dependencies only
pip install thumbor

# thumbor with OpenCV dependency
pip install thumbor\[opencv\]

# thumbor with all dependencies
pip install thumbor\[all\]

### Option 2: Binary

sudo add-apt-repository ppa:thumbor/ppa
sudo aptitude update
sudo aptitude install thumbor

For more ways, please check out Installation.

### Run

Running it is as easy as hit:

thumbor

After this, you can reach it on http://localhost:8888/unsafe/https://raw.githubusercontent.com/thumbor/thumbor/master/example.jpg

### Troubles?

If you experience any troubles, try running:

thumbor-doctor

If you have a `thumbor.conf` file, you can use that to help thumbor-doctor:

thumbor-doctor -c thumbor.conf

If you still need help, please raise an issue. Remember to send your `thumbor-doctor` output in the issue:

thumbor-doctor --nocolor -c thumbor.conf

🎯 Features
-----------

-   supports all common images formats out of the box
-   intelligent cropping and resizing
-   blazing fast using caching
-   supports many storages (local storage, AWS S3, Rackspace, Ceph, ...)
-   AI-powered cropping based on face and feature detection (glasses, interesting points, ...)
-   integrated with many programming languages and frameworks and many more...
-   highly extensible

🌟 Awesome Goodies
------------------

awesome-thumbor is a curated list of all things thumbor. There you can find filters, storages, engines, loaders, docker images, extensions in your favorite language and framework, and much more.

All of it with a clear indication of each project's quality. Have fun!

👍 Contribute
-------------

thumbor is an open-source project with many contributors. Join them contributing code or contributing documentation.

If you use thumbor, please take 1 minute and answer this survey? Only 2 questions!

Join the chat at https://gitter.im/thumbor/thumbor

👀 Demo
-------

You can see thumbor in action at http://thumborize.me/
