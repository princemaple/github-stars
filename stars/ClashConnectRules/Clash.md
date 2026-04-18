---
project: Clash
stars: 357
description: null
url: https://github.com/ClashConnectRules/Clash
---

Clash Rule Configuration
========================

An optimized Clash proxy rule configuration, providing precise traffic splitting and an efficient web access experience.

📋 Features
-----------

-   **🌐 Intelligent Splitting**: Automatically identifies and splits international and domestic traffic.
-   **🚫 Ad Blocking**: Built-in filtering rules for both domestic and international ads.
-   **🤖 AI Services Optimization**: Specialized routing rules for AI services like OpenAI, Claude, and Gemini.
-   **📱 App-Specific Rules**: Dedicated groups for services like YouTube, Microsoft, Google, and Apple.
-   **🇨🇳 Mainland China Optimization**: A comprehensive whitelist for domestic Chinese websites and IPs.
-   **🛡️ Privacy Protection**: Choose different regional nodes for WeChat to protect privacy.

🚀 Quick Start
--------------

### Supported Clients

-   ✅ Clash for Windows
-   ✅ ClashX (macOS)
-   ✅ Clash for Android
-   ✅ ClashX Pro
-   ✅ Other clients that support the Clash configuration format.

📊 Proxy Group Description
--------------------------

### General Groups

-   **🌐 International Traffic**: The default choice for all foreign websites and services.
-   **🎯 Domestic Traffic**: For domestic Chinese websites and services, set to DIRECT by default.

### Ad-Blocking Groups

-   **🚫 Domestic Ads**: Blocks domestic ads, supports REJECT/DIRECT options.
-   **🚫 International Ads**: Blocks international ads, supports REJECT/DIRECT options.

### Dedicated Service Groups

-   **🤖 AI Services**: OpenAI, Claude, Gemini, Anthropic, Copilot.
-   **📹 YouTube**: Dedicated to YouTube for an optimized video playback experience.
-   **Ⓜ️ Microsoft Services**: Microsoft, OneDrive, and other Microsoft services.
-   **🔍 Google Services**: Google Search, Gmail, Google FCM (does not include YouTube).
-   **🍎 Apple Services**: App Store, iCloud, Apple Music, etc.
-   **🌍 International Media**: Netflix, TikTok, Instagram, Threads, etc.
-   **🫧 WeChat**: Dedicated for WeChat, allowing selection of different regional nodes.

🎯 Rule Priority
----------------

Rules are matched in the following order of priority (from highest to lowest):

1.  **Ad-Blocking Rules** - Highest priority to block ads.
2.  **Domestic Site Rules** - Identifies domestic Chinese websites and services.
3.  **AI Services** - Various AI platforms and services.
4.  **YouTube** - YouTube video services.
5.  **Microsoft Services** - Microsoft-related services.
6.  **Google Services** - Google-related services (excluding YouTube).
7.  **Apple Services** - Apple ecosystem services.
8.  **International Media** - Foreign streaming and social media.
9.  **Other Rules** - WeChat, Telegram, etc.
10.  **Geolocation Rules** - IP-based geographical location determination.
11.  **Final Match** - Traffic that does not match any other rule.

🔧 Custom Configuration
-----------------------

### Modifying Proxy Groups

All proxy groups include the following options:

-   🚀 Proxy Selection
-   ♻️ Auto Select
-   Regional Nodes (Hong Kong, Taiwan, Singapore, Japan, USA, UK, etc.)
-   🚀 Manual Select
-   DIRECT

### WeChat Region Selection

WeChat supports selecting different regions:

-   **DIRECT** - Direct connection within Mainland China.
-   **🇭🇰 Hong Kong** - Access Hong Kong-specific features.
-   **🇨🇳 Taiwan** - Access Taiwan-specific features.
-   **Other Regions** - Select as needed.

📝 Rule Sources
---------------

This configuration uses the following high-quality rule sources:

-   **ACL4SSR**: Base rules for traffic splitting.
-   **blackmatrix7/ios\_rule\_script**: App-specific rules.
-   **DivineEngine/Profiles**: Rules for the Mainland China whitelist.

All rule sources are open-source projects and are regularly updated and maintained.

🤝 Contributing
---------------

Issues and Pull Requests are welcome to improve this configuration!

### How to Contribute

1.  Fork this repository.
2.  Create your feature branch (`git checkout -b feature/AmazingFeature`).
3.  Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4.  Push to the branch (`git push origin feature/AmazingFeature`).
5.  Open a Pull Request.

📄 License
----------

This project is licensed under the MIT License - see the LICENSE file for details.

⚠️ Disclaimer
-------------

-   This configuration is for learning and research purposes only.
-   Please comply with local laws and regulations.
-   The author assumes no responsibility for any issues that may arise from the use of this configuration.

🙏 Acknowledgements
-------------------

Thanks to the following projects and contributors:

-   ACL4SSR
-   blackmatrix7/ios\_rule\_script
-   DivineEngine/Profiles

* * *

If this configuration is helpful to you, please give it a ⭐ Star to show your support!
