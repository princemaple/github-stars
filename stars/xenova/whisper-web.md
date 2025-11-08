---
project: whisper-web
stars: 3138
description: ML-powered speech recognition directly in your browser
url: https://github.com/xenova/whisper-web
---

Whisper Web
===========

ML-powered speech recognition directly in your browser! Built with 🤗 Transformers.js.

Check out the demo site here.

Important

Experimental WebGPU support has been added to this branch (demo), if you'd like to run with GPU acceleration!

whisper-web-demo.mp4

Running locally
---------------

1.  Clone the repo and install dependencies:
    
    git clone https://github.com/xenova/whisper-web.git
    cd whisper-web
    npm install
    
2.  Run the development server:
    
    npm run dev
    
    > Firefox users need to change the `dom.workers.modules.enabled` setting in `about:config` to `true` to enable Web Workers. Check out this issue for more details.
    
3.  Open the link (e.g., http://localhost:5173/) in your browser.
