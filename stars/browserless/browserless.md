---
project: browserless
stars: 12219
description: Deploy headless browsers in Docker. Run on our cloud or bring your own. Free for non-commercial uses.
url: https://github.com/browserless/browserless
---

### Deploy headless browsers in Docker. Run on our cloud or bring your own.

     

  

📋 Table of Contents
--------------------

-   Get Started in Seconds
-   Features
-   Customisable Deployment Options
-   Why Browserless?
-   Licensing

🚀 Get Started in Seconds!
--------------------------

Get up and running in three simple steps:

### Step 1: Run the Docker image

docker run -p 3000:3000 ghcr.io/browserless/chromium

### Step 2: Open the docs in your browser

Visit http://localhost:3000/docs

**✅ Success!** Your browser service is live at `ws://localhost:3000`

### Step 3: Connect your script with Puppeteer or Playwright

**📘 Puppeteer Example**

import puppeteer from 'puppeteer-core';

const browser \= await puppeteer.connect({
  browserWSEndpoint: 'ws://localhost:3000',
});

const page \= await browser.newPage();
await page.goto('https://example.com');
console.log(await page.title());
await browser.close();

**🎭 Playwright Example**

import pw from 'playwright-core';

const browser \= await pw.firefox.connect(
  'ws://localhost:3000/firefox/playwright'
);

const page \= await browser.newPage();
await page.goto('https://example.com');
console.log(await page.title());
await browser.close();

**Note:** Use `ghcr.io/browserless/firefox` or `ghcr.io/browserless/multi` for Firefox/Webkit support.

  

### Output:

```
Example Domain
```

✨ Features
----------

### General Features

-   **Parallelism and queueing** — Handle multiple sessions with configurable concurrency limits
-   **Debug Viewer** — Actively view and debug running browser sessions in real-time
-   **Unforked libraries** — Works seamlessly with standard Puppeteer and Playwright
-   **Fonts & emoji** — All system fonts and emoji support out-of-the-box
-   **Configurable timeouts** — Set session timers and health-checks to keep things running smoothly
-   **Error tolerant** — If Chrome crashes, Browserless won't
-   **ARM64 architecture support** — Full support for ARM64 platforms including Apple Silicon; some browsers (Edge, Chrome) have limited ARM64 compatibility

### Premium Features

Our Self-serve cloud and Enterprise offerings include all the general features plus extras, such as:

-   **BrowserQL** for avoiding detectors and solving captchas
-   **Hybrid automations** for streaming live browser sessions during scripts
-   **Persistent Sessions** for persisting browser state (cookies, cache, localStorage) across multiple sessions with configurable data retention up to 90 days
-   **Session Replay** for recording and debugging browser sessions with event capture and video playback
-   **Chrome Extensions Support** for loading custom extensions including ad blockers, captcha solvers, etc.
-   **Advanced Captcha/Stealth Routes** for enhanced anti-detection with Captcha solving, fingerprint randomization, and residential proxy rotation
-   **REST APIs** for tasks such as retrieving HTML, PDFs or Screenshot etc.
-   **Inbuilt residential proxy** for automatic IP rotation and geo-targeting with residential proxy networks
-   **Webhook Integrations** for queue alerts, rejections, timeouts, errors, and health failures

🚢 Customisable Deployment Options
----------------------------------

Select the deployment model that best fits your needs:

### 🔓 Open Source (Self-Hosted)

Free, self-hosted solution with core browser automation capabilities.

**Best for:** Testing, development, and small projects

↓ Quickstart above

### 🏢 Enterprise Docker (Self-Hosted)

Full Enterprise features in a self-hosted container.

**Best for:** Production workloads requiring data sovereignty

→ Learn More

### ☁️ Cloud (Self-Serve)

Fully managed, pay-as-you-go service with automatic scaling.

**Best for:** Quick starts and rapid prototyping

→ Start Free

### 🔒 Private Deployment

Custom Enterprise infrastructure across major cloud providers.

**Best for:** Large-scale enterprise deployments

→ Contact Sales

> **Want to dive deeper?** Check out this detailed guide for advanced stuff including Docker configuration, hosting providers, SDK extensions, and more.

💡 Why Browserless?
-------------------

**Running Chrome in the cloud or CI sucks.**

Missing fonts. Random crashes. Dependency hell. Lambda limits. You know the drill.

**Browserless solves this** by handling browsers as a managed service — locally or in our cloud — so you can focus on automation, not infrastructure. We've taken care of the hard parts: system packages, font libraries, security patches, scaling strategies, and CVEs.

You still own your script. You still control your code. We just make sure the Browser runs smoothly, every time.

📜 Licensing
------------

SPDX-License-Identifier: SSPL-1.0 OR Browserless Commercial License.

If you want to use Browserless to build commercial sites, applications, or in a continuous-integration system that's closed-source then you'll need to purchase a commercial license. This allows you to keep your software proprietary whilst still using browserless. You can purchase a commercial license here. A commercial license grants you:

-   Priority support on issues and features.
-   On-premise running as well as running on public cloud providers for commercial/CI purposes for proprietary systems.
-   Ability to modify the source (forking) for your own purposes.
-   A new admin user-interface.

Not only does it grant you a license to run such a critical piece of infrastructure, but you are also supporting further innovation in this space and our ability to contribute to it.

If you are creating an open source application under a license compatible with the Server Side License 1.0, you may use Browserless under those terms.

**Happy hacking!**

Need help? Reach out to us at **support@browserless.io**
