---
project: Ciphey
stars: 21281
description: ⚡ Automatically decrypt encryptions without knowing the key or cipher, decode encodings, and crack hashes ⚡
url: https://github.com/bee-san/Ciphey
---

Translations  
🇩🇪 DE 🇫🇷 FR 🇭🇺 HU 🇮🇩 ID 🇮🇹 IT 🇳🇱 NL 🇧🇷 PT-BR 🇷🇺 RU 🇨🇳 ZH 🇹🇭 TH  
  
➡️ Documentation | Discord | Installation Guide ⬅️  

  
Fully automated decryption/decoding/cracking tool using natural language processing & artificial intelligence, along with some common sense.

* * *

Installation Guide
------------------

🐍 Python

🐋 Docker (Universal)

🍎 MacPorts (macOS)

🍺 Homebrew (macOS/Linux)

`python3 -m pip install ciphey --upgrade`

`docker run -it --rm remnux/ciphey`

`sudo port install ciphey`

`brew install ciphey`

Linux

Mac OS

Windows

* * *

🤔 What is this?
================

Input encrypted text, get the decrypted text back.

> "What type of encryption?"

That's the point. You don't know, you just know it's possibly encrypted. Ciphey will figure it out for you.

Ciphey can solve most things in 3 seconds or less.

Ciphey aims to be a tool to automate a lot of decryptions & decodings such as multiple base encodings, classical ciphers, hashes or more advanced cryptography.

If you don't know much about cryptography, or you want to quickly check the ciphertext before working on it yourself, Ciphey is for you.

**The technical part.** Ciphey uses a custom built artificial intelligence module (_AuSearch_) with a _Cipher Detection Interface_ to approximate what something is encrypted with. And then a custom-built, customisable natural language processing _Language Checker Interface_, which can detect when the given text becomes plaintext.

No neural networks or bloated AI here. We only use what is fast and minimal.

And that's just the tip of the iceberg. For the full technical explanation, check out our documentation.

✨ Features
==========

-   **50+ encryptions/encodings supported** such as binary, Morse code and Base64. Classical ciphers like the Caesar cipher, Affine cipher and the Vigenere cipher. Along with modern encryption like repeating-key XOR and more. **For the full list, click here**
-   **Custom Built Artificial Intelligence with Augmented Search (AuSearch) for answering the question "what encryption was used?"** Resulting in decryptions taking less than 3 seconds.
-   **Custom built natural language processing module** Ciphey can determine whether something is plaintext or not. Whether that plaintext is JSON, a CTF flag, or English, Ciphey can get it in a couple of milliseconds.
-   **Multi Language Support** at present, only German & English (with AU, UK, CAN, USA variants).
-   **Supports encryptions and hashes** Which the alternatives such as CyberChef Magic do not.
-   **C++ core** Blazingly fast.

🔭 Ciphey vs CyberChef
======================

🔁 Base64 Encoded 42 times
--------------------------

Name

⚡ Ciphey ⚡

🐢 CyberChef 🐢

Gif

Time

2 seconds

6 seconds

Setup

-   Run ciphey on the file

-   Set the regex param to "{"
-   You need to know how many times to recurse
-   You need to know it's Base64 all the way down
-   You need to load CyberChef (it's a bloated JS app)
-   Know enough about CyberChef to create this pipeline
-   Invert the match

**Note** The gifs may load at different times, so one may appear significantly faster than another.  
**A note on magic** CyberChef's most similar feature to Ciphey is Magic. Magic fails instantly on this input and crashes. The only way we could force CyberChef to compete was to manually define it.

We also tested CyberChef and Ciphey with a **6gb file**. Ciphey cracked it in **5 minutes and 54 seconds**. CyberChef crashed before it even started.

📊 Ciphey vs Katana vs CyberChef Magic
--------------------------------------

**Name**

⚡ Ciphey ⚡

🗡️ Katana 🗡️

🐢 CyberChef Magic 🐢

Advanced Language Checker

✅

❌

✅

Supports Encryptions

✅

✅

❌

Releases named after Dystopian themes 🌃

✅

❌

❌

Supports hashes

✅

✅

❌

Easy to set up

✅

❌

✅

Can guess what something is encrypted with

✅

❌

❌

Created for hackers by hackers

✅

✅

❌

🎬 Getting Started
==================

If you're having trouble with installing Ciphey, read this.

‼️ Important Links (Docs, Installation guide, Discord Support)
--------------------------------------------------------------

Installation Guide

Documentation

Discord

Docker Image (from REMnux)

📖 Installation Guide

📚 Documentation

🦜 Discord

🐋 Docker Documentation

🏃‍♀️Running Ciphey
-------------------

There are 3 ways to run Ciphey.

1.  File Input `ciphey -f encrypted.txt`
2.  Unqualified input `ciphey -- "Encrypted input"`
3.  Normal way `ciphey -t "Encrypted input"`

To get rid of the progress bars, probability table, and all the noise use the quiet mode.

`ciphey -t "encrypted text here" -q`

For a full list of arguments, run `ciphey --help`.

### ⚗️ Importing Ciphey

You can import Ciphey's main and use it in your own programs and code. `from Ciphey.__main__ import main`

🎪 Contributors
===============

Ciphey was invented by Bee in 2008, and revived in 2019. Ciphey wouldn't be where it was today without Cyclic3 - president of UoL's Cyber Security Society.

Ciphey was revived & recreated by the Cyber Security Society for use in CTFs. If you're ever in Liverpool, consider giving a talk or sponsoring our events. Email us at `cybersecurity@society.liverpoolguild.org` to find out more 🤠

**Major Credit** to George H for working out how we could use proper algorithms to speed up the search process. **Special thanks** to varghalladesign for designing the logo. Check out their other design work!

🐕‍🦺 Contributing
------------------

Don't be afraid to contribute! We have many, many things you can do to help out. Each of them labelled and easily explained with examples. If you're trying to contribute but stuck, tag @bee-san ✨

Alternatively, join the Discord group and send a message there (link in contrib file) or at the top of this README as a badge.

Please read the contributing file for exact details on how to contribute ✨

By doing so, you'll get your name added to the README below and get to be apart of an ever-growing project!

💰 Financial Contributors
-------------------------

The contributions will be used to fund not only the future of Ciphey and its authors, but also Cyber Security Society at the University of Liverpool.

GitHub doesn't support "sponsor this project and we'll evenly distribute the money", so pick a link and we'll sort it out on our end 🥰

✨ Contributors
--------------

Thanks goes to these wonderful people (emoji key):

  
**cyclic3**  
🎨 🚧 💻 🤔

  
**Brandon**  
🎨 🚧 💻 🤔

  
**michalani**  
💻

  
**ashb07**  
💻

  
**Shardion**  
🐛

  
**Bryan**  
🌍 📖

  
**Lukas Gabriel**  
💻 🐛 🌍 🤔

  
**Darshan**  
🐛

  
**SkeletalDemise**  
💻

  
**Christian Clauss**  
💻 🐛

  
**Machinexa2**  
🖋

  
**Anant Verma**  
💻 🐛

  
**XVXTOR**  
📖

  
**Itamikame**  
💻

  
**MikeMerz**  
💻

  
**Jacob Galam**  
💻 🐛

  
**TuxTheXplorer**  
🌍

  
**Itamai**  
💻 🐛

  
**Filipe**  
🌍

  
**Malathi**  
💻

  
**Jack**  
🌍

  
**Younes**  
🌍

  
**Marnick Vandecauter**  
🌍

  
**Michael V**  
💻

  
**chuinzer**  
🌍

  
**blackcat-917**  
🌍 📖

  
**Åsmund Brekke**  
💻

  
**Sashreek Shankar**  
💻

  
**cryptobadger**  
💻 🐛

  
**elf**  
💻

  
**Roger Yu**  
💻

  
**dysleixa**  
💻

  
**Mohammad Zulfikar**  
📖

  
**Alexander Burchenko**  
🌍

This project follows the all-contributors specification. Contributions of any kind welcome!
