---
project: CloakBrowser
stars: 27741
description: Stealth Chromium that passes every bot detection test. Drop-in Playwright replacement with source-level fingerprint patches. 30/30 tests passed.
url: https://github.com/CloakHQ/CloakBrowser
---

  

  

### Stealth Chromium that passes every bot detection test.

Not a patched config. Not a JS injection. A real Chromium binary with fingerprints modified at the C++ source level. Antibot systems score it as a normal browser — because it _is_ a normal browser.

  

  
_Cloudflare Turnstile — 3 live tests passing (headed mode, macOS)_

  

Drop-in Playwright/Puppeteer replacement for Python and JavaScript.  
Same API, same code — just swap the import. **3 lines of code, 30 seconds to unblock.**

-   **58 source-level C++ patches** — canvas, WebGL, audio, fonts, GPU, screen, WebRTC, network timing, automation signals, CDP input behavior
-   **`humanize=True`** — human-like mouse curves, keyboard timing, and scroll patterns. One flag, behavioral detection passes
-   **Pro: 0.9 reCAPTCHA v3 score** — human-level, server-verified
-   **Passes Cloudflare Turnstile**, FingerprintJS, BrowserScan — tested against 30+ detection sites
-   **Auto-downloads the right binary** — free or Pro based on your license
-   **`pip install cloakbrowser`** or **`npm install cloakbrowser`** — binary auto-downloads, zero config
-   **Open-source wrappers** — free v146 binary, Pro for latest builds

**Try it now** — no install needed:

docker run --rm cloakhq/cloakbrowser cloaktest

**Python:**

from cloakbrowser import launch

browser \= launch()
page \= browser.new\_page()
page.goto("https://example.com")
browser.close()

**JavaScript (Playwright):**

import { launch } from 'cloakbrowser';

const browser \= await launch();
const page \= await browser.newPage();
await page.goto('https://example.com');
await browser.close();

Also works with Puppeteer: `import { launch } from 'cloakbrowser/puppeteer'` (details)

**For sites with anti-bot protection**, add a residential proxy and these flags:

browser \= launch(
    proxy\="http://user:pass@residential-proxy:port",  \# residential IP, not datacenter
    geoip\=True,       \# match timezone + locale to proxy IP
    headless\=False,    \# some sites detect headless even with C++ patches
    humanize\=True,     \# human-like mouse, keyboard, scroll
)

const browser \= await launch({
    proxy: 'http://user:pass@residential-proxy:port',
    geoip: true,
    headless: false,
    humanize: true,
});

See Troubleshooting for site-specific issues (FingerprintJS, Kasada, reCAPTCHA).

Install
-------

**Python:**

pip install cloakbrowser

**JavaScript / Node.js:**

# With Playwright
npm install cloakbrowser playwright-core

# With Puppeteer
npm install cloakbrowser puppeteer-core

**.NET / C#:**

dotnet add package CloakBrowser

> Community-maintained .NET client built on Microsoft.Playwright. See `dotnet/README.md` for the full API.

* * *

On first run, the stealth Chromium binary is automatically downloaded (~200MB, cached locally).

**Optional:** Auto-detect timezone/locale from proxy IP:

pip install cloakbrowser\[geoip\]

**Migrating from Playwright?** One-line change:

\- from playwright.sync\_api import sync\_playwright
\- pw = sync\_playwright().start()
\- browser = pw.chromium.launch()
+ from cloakbrowser import launch
+ browser = launch()

page = browser.new\_page()
page.goto("https://example.com")
# ... rest of your code works unchanged

> ⭐ **Star** to show support — **Watch releases** to get notified when new builds drop.

* * *

Latest: v0.4.7 — 59 source-level stealth patches, now on every platform (Chromium 148.0.7778.215.3)
---------------------------------------------------------------------------------------------------

-   **CloakBrowser Pro** — the latest binary (Chromium 148.0.7778.215.3, 59 source-level patches) is available to Pro subscribers, now on **all platforms including macOS** (Apple Silicon + Intel); v146 stays free forever. Set a `license_key` (`licenseKey` in JS) or the `CLOAKBROWSER_LICENSE_KEY` env var and the wrapper fetches the latest build automatically. See CloakBrowser Pro
-   **.NET 8 / C# client** — CloakBrowser now ships as a NuGet package (`CloakBrowser`), mirroring the Python and JS wrappers.
-   **58 fingerprint patches** — rendering consistency improvements across Linux and Windows, corrected GPU/display/graphics parameters to match stock Chrome 146 profiles
-   **Windows native GPU passthrough** — real hardware values pass through directly instead of being spoofed, matching real browser behavior
-   **HTTP proxy inline credentials** — new network-layer support for proxies with inline authentication
-   **`extension_paths`** — load Chrome extensions in all launch functions
-   **Humanize actionability** — auto-wait for visible, enabled, stable elements before humanized actions
-   **Per-call `human_config`** — override humanize settings on individual method calls
-   **Composable JS helpers** — `buildLaunchOptions()` and `humanizeBrowser()` for custom Playwright integrations
-   **Native SOCKS5 proxy** — `proxy="socks5://user:pass@host:port"` works directly in all launch functions, Python + JS. QUIC/HTTP3 tunnels through SOCKS5 via UDP ASSOCIATE
-   **Proxy signal removal** — DNS/connect/SSL timing zeroed, proxy cache headers stripped, Proxy-Connection header leak removed
-   **Chromium 146 upgrade** — rebased all patches from 145.0.7632.x to 146.0.7680.177
-   **WebRTC IP spoofing** — `--fingerprint-webrtc-ip=auto` resolves your proxy's exit IP and spoofs WebRTC ICE candidates. Auto-injected when using `geoip=True` (no extra network call)
-   **`humanize=True`** — one flag makes all mouse, keyboard, and scroll interactions behave like a real user. Bézier curves, per-character typing, realistic scroll patterns
-   **Stealthy with zero flags** — binary auto-generates a random fingerprint seed at startup. No configuration required
-   **Timezone & locale from proxy IP** — `launch(proxy="...", geoip=True)` auto-detects timezone and locale
-   **Persistent profiles** — `launch_persistent_context()` keeps cookies and localStorage across sessions, bypasses incognito detection

See the full CHANGELOG.md for details.

Why CloakBrowser?
-----------------

-   **Config-level patches break** — `playwright-stealth`, `undetected-chromedriver`, and `puppeteer-extra` inject JavaScript or tweak flags. Every Chrome update breaks them. Antibot systems detect the patches themselves.
-   **CloakBrowser patches Chromium source code** — fingerprints are modified at the C++ level, compiled into the binary. Detection sites see a real browser because it _is_ a real browser.
-   **Source-level stealth** — C++ patches handle fingerprints (GPU, screen, UA, hardware reporting) at the binary level. No JavaScript injection, no config-level hacks. Most stealth tools only patch at the surface.
-   **Same behavior everywhere** — works identically local, in Docker, and on VPS. No environment-specific patches or config needed.
-   **Works with AI agents and automation frameworks** — drop-in stealth for browser-use, Crawl4AI, Scrapling, Stagehand, LangChain, Selenium, and more. See integrations.

CloakBrowser doesn't solve CAPTCHAs — it prevents them from appearing. No CAPTCHA-solving services, no proxy rotation built in — bring your own proxies, use the Playwright API you already know.

CloakBrowser Pro
----------------

The wrapper (Python + JS) is MIT, free forever. The binary uses a delayed free-release model:

-   **Free (v146)** — the previous binary, on GitHub Releases. Goes stale within weeks as detection evolves.
-   **Pro (latest, Chromium 148.0.7778.215.3)** — the newest patches and Chromium upgrades first, so the results below stay green as anti-bot systems change. Linux, Windows, and macOS (Apple Silicon + Intel).

Anti-bot detection updates constantly, and an older binary degrades fast. Pro keeps you on the build that's actively maintained against it.

Use Pro if CloakBrowser is part of production scraping, QA, monitoring, or automation where stale browser fingerprints cost you time or blocked runs.

Activate with your license key (env var, `license_key=` param, or `~/.cloakbrowser/license.key`):

export CLOAKBROWSER\_LICENSE\_KEY=cb\_xxxxxxxx

Pro plans → **cloakbrowser.dev**

Test Results
------------

All tests verified against live detection services. Results below are for the latest Pro/current build unless noted. Last tested: Jul 2026 (Chromium 148).

Detection Service

Stock Playwright

CloakBrowser

Notes

**reCAPTCHA v3**

0.1 (bot)

**0.9** (human)

Pro/current build; server-side verified

**Cloudflare Turnstile** (non-interactive)

FAIL

**PASS**

Auto-resolve

**Cloudflare Turnstile** (managed)

FAIL

**PASS**

Single click

**ShieldSquare**

BLOCKED

**PASS**

Production site

**FingerprintJS** bot detection

DETECTED

**PASS**

Pro/current build; demo.fingerprint.com

**BrowserScan** bot detection

DETECTED

**NORMAL** (4/4)

browserscan.net

**bot.incolumitas.com**

13 fails

**1 fail**

WEBDRIVER spec only

**deviceandbrowserinfo.com**

6 true flags

**0 true flags**

`isBot: false`

`navigator.webdriver`

`true`

**`false`**

Source-level patch

`navigator.plugins.length`

0

**5**

Real plugin list

`window.chrome`

`undefined`

**`object`**

Present like real Chrome

UA string

`HeadlessChrome`

**`Chrome/146.0.0.0`**

No headless leak

CDP detection

Detected

**Not detected**

`isAutomatedWithCDP: false`

TLS fingerprint

Mismatch

**Identical to Chrome**

ja3n/ja4/akamai match

**Tested against 30+ detection sites**

### Proof

  
_Pro/latest build: reCAPTCHA v3 score 0.9 — server-side verified (human-level)_

  
_Cloudflare Turnstile non-interactive challenge — auto-resolved_

  
_BrowserScan bot detection — NORMAL (4/4 checks passed)_

  
_Pro/latest build: FingerprintJS web-scraping demo — data served, not blocked_

  
_deviceandbrowserinfo.com behavioral bot detection — "You are human!" with humanize=True (24/24 signals passed)_

Comparison
----------

Feature

Playwright

playwright-stealth

undetected-chromedriver

Camoufox

CloakBrowser

reCAPTCHA v3 score (Pro/current)

0.1

0.3-0.5

0.3-0.7

0.7-0.9

**0.9**

Cloudflare Turnstile

Fail

Sometimes

Sometimes

Pass

**Pass**

Patch level

None

JS injection

Config patches

C++ (Firefox)

**C++ (Chromium)**

Survives Chrome updates

N/A

Breaks often

Breaks often

Yes

**Yes**

Maintained

Yes

Stale

Stale

Unstable

**Active**

Browser engine

Chromium

Chromium

Chrome

Firefox

**Chromium**

Playwright API

Native

Native

No (Selenium)

No

**Native**

How It Works
------------

CloakBrowser is a thin wrapper (Python + JavaScript) around a custom-built Chromium binary:

1.  **You install** → `pip install cloakbrowser` or `npm install cloakbrowser`
2.  **First launch** → binary auto-downloads for your platform (Chromium 146)
3.  **Every launch** → Playwright or Puppeteer starts with our binary + stealth args
4.  **You write code** → standard Playwright/Puppeteer API, nothing new to learn

The binary includes 58 source-level patches covering canvas, WebGL, audio, fonts, GPU, screen properties, WebRTC, network timing, hardware reporting, automation signal removal, and CDP input behavior mimicking.

These are compiled into the Chromium binary — not injected via JavaScript, not set via flags.

Binary downloads are verified against a pinned Ed25519 signature on the published checksums before extraction, so the download is confirmed authentic (genuinely ours) and not just intact. A compromised mirror cannot serve a tampered or downgraded binary.

API
---

### `launch()`

from cloakbrowser import launch

\# Basic — headless, default stealth config
browser \= launch()

\# Headed mode (see the browser window)
browser \= launch(headless\=False)

\# Pro — use the latest binary (or set CLOAKBROWSER\_LICENSE\_KEY env var)
browser \= launch(license\_key\="cb\_xxxxxxxx")

\# With proxy (HTTP or SOCKS5)
browser \= launch(proxy\="http://user:pass@proxy:8080")
browser \= launch(proxy\="socks5://user:pass@proxy:1080")

\# With proxy dict (bypass, separate auth fields)
browser \= launch(proxy\={"server": "http://proxy:8080", "bypass": ".google.com", "username": "user", "password": "pass"})

\# With extra Chrome args
browser \= launch(args\=\["--disable-gpu"\])

\# With timezone and locale (sets binary flags — no detectable CDP emulation)
browser \= launch(timezone\="America/New\_York", locale\="en-US")

\# Auto-detect timezone/locale from proxy IP (requires: pip install cloakbrowser\[geoip\])
\# Also auto-injects --fingerprint-webrtc-ip to prevent WebRTC IP leaks (no extra cost)
\# Note: makes HTTP calls through your proxy to resolve exit IP (ipify.org, checkip.amazonaws.com)
browser \= launch(proxy\="http://proxy:8080", geoip\=True)

\# Explicit timezone/locale always win over auto-detection
browser \= launch(proxy\="http://proxy:8080", geoip\=True, timezone\="Europe/London")

\# WebRTC IP spoofing only (no geoip dep needed — resolves exit IP via HTTP call through proxy)
browser \= launch(proxy\="http://proxy:8080", args\=\["--fingerprint-webrtc-ip=auto"\])

\# Explicit WebRTC IP (no network call)
browser \= launch(proxy\="http://proxy:8080", args\=\["--fingerprint-webrtc-ip=1.2.3.4"\])

\# Human-like mouse, keyboard, and scroll behavior
browser \= launch(humanize\=True)

\# With slower, more deliberate movements
browser \= launch(humanize\=True, human\_preset\="careful")

\# Without default stealth args (bring your own fingerprint flags)
browser \= launch(stealth\_args\=False, args\=\["--fingerprint=12345"\])

Returns a standard Playwright `Browser` object. All Playwright methods work: `new_page()`, `new_context()`, `close()`, etc.

### `launch_async()`

import asyncio
from cloakbrowser import launch\_async

async def main():
    browser \= await launch\_async()
    page \= await browser.new\_page()
    await page.goto("https://example.com")
    print(await page.title())
    await browser.close()

asyncio.run(main())

### `launch_context()`

Convenience function that creates browser + context in one call with user agent, viewport, locale, and timezone:

from cloakbrowser import launch\_context

context \= launch\_context(
    user\_agent\="Custom UA",
    viewport\={"width": 1920, "height": 1080},
    locale\="en-US",
    timezone\="America/New\_York",
)
page \= context.new\_page()
page.goto("https://protected-site.com")
context.close()

Extra kwargs are forwarded to Playwright's `browser.new_context()` — use this for `storage_state`, `permissions`, `extra_http_headers`, etc. without needing a persistent profile folder:

from cloakbrowser import launch\_context

\# Restore a saved session (cookies, localStorage) from a JSON file
context \= launch\_context(storage\_state\="state.json")
page \= context.new\_page()
page.goto("https://example.com")
\# Save state back for next run
context.storage\_state(path\="state.json")
context.close()

### `launch_context_async()`

Async counterpart to `launch_context()`. Same signature and kwargs forwarding:

import asyncio
from cloakbrowser import launch\_context\_async

async def main():
    ctx \= await launch\_context\_async(storage\_state\="state.json")
    page \= await ctx.new\_page()
    await page.goto("https://example.com")
    await ctx.storage\_state(path\="state.json")
    await ctx.close()

asyncio.run(main())

### `launch_persistent_context()`

Same as `launch_context()`, but with a persistent user profile. Cookies, localStorage, and cache persist across sessions.

Use this when you need to:

-   **Stay logged in** across runs (cookies/sessions survive restarts)
-   **Bypass incognito detection** (some sites flag empty, ephemeral profiles)
-   **Load Chrome extensions** (extensions only work from a real user data dir)
-   **Build natural browsing history** (cached fonts, service workers, IndexedDB accumulate over time, making the profile look more realistic)
-   **Play DRM-protected video** (Widevine) — with a sideloaded CDM, the wrapper enables Widevine on the first launch (see Widevine / DRM)

from cloakbrowser import launch\_persistent\_context

\# First run — creates the profile
ctx \= launch\_persistent\_context("./my-profile", headless\=False)
page \= ctx.new\_page()
page.goto("https://protected-site.com")
ctx.close()  \# profile saved

\# Next run — cookies, localStorage restored automatically
ctx \= launch\_persistent\_context("./my-profile", headless\=False)

\# Load Chrome extensions
ctx \= launch\_persistent\_context(
    "./my-profile",
    headless\=False,
    extension\_paths\=\["./my-extension"\],
)

Supports all the same options as `launch_context()`: `proxy`, `user_agent`, `viewport`, `locale`, `timezone`, `color_scheme`, `geoip`, `extension_paths`.

Async version: `launch_persistent_context_async()`.

**Storage quota and incognito detection:** the binary normalizes storage quota by default (this also hides the real disk size). Detectors that infer private/incognito mode from quota — e.g. BrowserScan's incognito check (−10%) — read the default as incognito. Raise it to present as a regular profile:

ctx \= launch\_persistent\_context("./my-profile", args\=\["--fingerprint-storage-quota=5000"\])

### Widevine / DRM

The binary is built with Widevine support, but the Widevine CDM is a proprietary Google component we can't redistribute. Get it one of two ways (full background in #96):

**Fetch it** — no Chrome install needed; pulls the CDM from Google's component server (Linux x86-64 only; SHA-256 + CRX3-signature verified). It lands at `~/.cloakbrowser/WidevineCdm`, which the wrapper auto-detects — no env var needed:

python3 bin/fetch-widevine.py

**Or copy it** from an existing Chrome install, next to the binary:

cp -r /opt/google/chrome/WidevineCdm ~/.cloakbrowser/chromium-<version\>/WidevineCdm

(In Docker, just pass `-e CLOAKBROWSER_FETCH_WIDEVINE=1` — the entrypoint runs the fetch automatically; see the Docker note below.)

With the CDM in place, `launch_persistent_context()` enables Widevine **on the first launch** — the wrapper auto-writes the CDM hint file into the profile, so you don't need the manual two-launch workaround. This lets you play DRM-protected video (e.g. Netflix, Spotify Web).

from cloakbrowser import launch\_persistent\_context

\# WidevineCdm sideloaded next to the binary -> Widevine works on first launch
ctx \= launch\_persistent\_context("./my-profile", headless\=False)

-   **Linux only.** Chromium's hint-file mechanism is Linux/ChromeOS-specific. On Windows the CDM can't initialise (DRM host verification) and macOS uses a different layout, so seeding is a no-op there.
-   **Auto by presence.** No flag needed — a sideloaded CDM is the opt-in. Point at a CDM in a non-default location with `CLOAKBROWSER_WIDEVINE_CDM=/path/to/WidevineCdm`, or disable seeding entirely with `CLOAKBROWSER_WIDEVINE=0`.
-   **Docker — auto-fetch (opt-in).** No Chrome to copy from inside the image, so the official image can fetch the CDM for you. Run with `-e CLOAKBROWSER_FETCH_WIDEVINE=1` and it pulls the CDM from Google's component server (the same source Chrome uses) on first launch, caches it at `~/.cloakbrowser/WidevineCdm` in the mounted volume, where the wrapper auto-detects it — for free or Pro binaries, and for `docker exec`'d scripts alike. **Off by default** — no network call unless you opt in — and best-effort, so a failed fetch never blocks launch. The download is signature- and checksum-verified before install. Bare-metal Linux users can run the same fetcher directly: `python3 bin/fetch-widevine.py` (pip-only installs can grab that one self-contained file from the repo).

### CLI

Pre-download the binary, diagnose your setup, or manage the cache from the command line:

python -m cloakbrowser install      # Download binary with progress output
python -m cloakbrowser info         # Diagnostics: binary that will launch, license tier, env checks
python -m cloakbrowser update       # Check for and download newer binary
python -m cloakbrowser clear-cache  # Remove cached binaries

`info` reports the binary that will actually launch given your license, runs a quick launch test (and flags missing system libraries on Linux), shows your license tier, and checks fonts, GeoIP, and optional dependencies. Add `--quick` to skip the launch test or `--json` for machine-readable output. The same commands are available via `npx cloakbrowser <command>` (JS) and the `cloakbrowser` CLI (.NET).

### Utility Functions

from cloakbrowser import binary\_info, clear\_cache, ensure\_binary

\# Check binary installation status
print(binary\_info())
\# {'version': '146.0.7680.177.5', 'platform': 'linux-x64', 'installed': True, ...}

\# Force re-download
clear\_cache()

\# Pre-download binary (e.g., during Docker build)
ensure\_binary()

JavaScript / Node.js API
------------------------

CloakBrowser ships a TypeScript package with full type definitions. Choose Playwright or Puppeteer — same stealth binary underneath.

### Playwright (default)

import { launch, launchContext, launchPersistentContext } from 'cloakbrowser';

// Basic
const browser \= await launch();

// Pro — use the latest binary (or set CLOAKBROWSER\_LICENSE\_KEY env var)
const browser \= await launch({ licenseKey: 'cb\_xxxxxxxx' });

// With options
const browser \= await launch({
  headless: false,
  proxy: 'http://user:pass@proxy:8080',
  args: \['--fingerprint=12345'\],
  timezone: 'America/New\_York',
  locale: 'en-US',
  humanize: true,
});

// Convenience: browser + context in one call
const context \= await launchContext({
  userAgent: 'Custom UA',
  viewport: { width: 1920, height: 1080 },
  locale: 'en-US',
  timezone: 'America/New\_York',
});
const page \= await context.newPage();

// Persistent profile — cookies/localStorage survive restarts, avoids incognito detection
const ctx \= await launchPersistentContext({
  userDataDir: './chrome-profile',
  headless: false,
  proxy: 'http://user:pass@proxy:8080',
});

> **Note:** Each example above is standalone — not meant to run as one block.

All Python options work in JS: `stealthArgs: false` to disable defaults, `geoip: true` to auto-detect timezone/locale from proxy IP.

### Puppeteer

> **Note:** The Playwright wrapper is recommended for sites with reCAPTCHA Enterprise. Puppeteer's CDP protocol leaks automation signals that reCAPTCHA Enterprise can detect, causing intermittent 403 errors. This is a known Puppeteer limitation, not specific to CloakBrowser. Use Playwright for best results.

import { launch } from 'cloakbrowser/puppeteer';

const browser \= await launch({ headless: true });
const page \= await browser.newPage();
await page.goto('https://example.com');
await browser.close();

### Utility Functions (JS)

import { ensureBinary, clearCache, binaryInfo } from 'cloakbrowser';

// Pre-download binary (e.g., during Docker build)
await ensureBinary();

// Check installation status
console.log(binaryInfo());

// Force re-download
clearCache();

Human Behavior
--------------

Pass `humanize=True` to make all mouse, keyboard, and scroll interactions indistinguishable from real users. All Playwright calls (`page.click()`, `page.fill()`, `page.type()`, `page.mouse.*`, `page.keyboard.*`, Locator API) and Puppeteer calls (`page.click()`, `page.type()`, `page.mouse.*`, `page.keyboard.*`, ElementHandle API) are automatically replaced with human-like equivalents. No code changes needed.

browser \= launch(humanize\=True)
page \= browser.new\_page()
page.goto("https://example.com")
page.locator("#email").fill("user@example.com")  \# per-character timing, thinking pauses
page.locator("button\[type=submit\]").click()       \# Bézier curve, realistic aim point

// Playwright
import { launch } from 'cloakbrowser';
const browser \= await launch({ humanize: true });

// Puppeteer
import { launch } from 'cloakbrowser/puppeteer';
const browser \= await launch({ humanize: true });

**What changes:**

Interaction

Default

With `humanize=True`

Mouse movement

Instant teleport

Bézier curve with easing and slight overshoot

Clicks

Instant

Realistic aim point + hold duration

Keyboard

Instant fill

Per-character timing, thinking pauses, occasional typos with self-correction

Scroll

Jump

Accelerate → cruise → decelerate micro-steps

`fill()`

Instant value set

Clears existing content, types character by character

**Presets** — `default` (normal speed) or `careful` (slower, more deliberate, idle micro-movements between actions):

browser \= launch(humanize\=True, human\_preset\="careful")

const browser \= await launch({ humanize: true, humanPreset: 'careful' });

**Custom config** — override any parameter:

browser \= launch(humanize\=True, human\_config\={
    "mistype\_chance": 0.05,              \# 5% typo rate with self-correction
    "typing\_delay": 100,                 \# slower typing (ms per character)
    "idle\_between\_actions": True,        \# micro-movements between clicks
    "idle\_between\_duration": \[0.3, 0.8\], \# idle duration range (seconds)
})

const browser \= await launch({
    humanize: true,
    humanConfig: {
        mistype\_chance: 0.05,
        typing\_delay: 100,
        idle\_between\_actions: true,
        idle\_between\_duration: \[0.3, 0.8\],
    }
});

Access the original un-patched Playwright page at `page._original` if you need raw speed for a specific call.

> **Note (Playwright):** Always use `page.click(selector)`, `page.type(selector, text)`, `page.hover(selector)`, or `page.locator(selector).*` — these go through the full humanize pipeline. Avoid `page.query_selector()` — `ElementHandle` objects bypass all patches, so mouse movement teleports, keyboard events fire without timing, and scroll has no human curve.
> 
> **Note (Puppeteer):** Both selector-based methods (`page.click()`, `page.type()`) and ElementHandle methods (`el.click()`, `el.type()`) are fully humanized. `page.$()`, `page.$$()`, and `page.waitForSelector()` return patched handles automatically.

> Contributed by @evelaa123 — full Playwright and Puppeteer API coverage.

Configuration
-------------

Env Variable

Default

Description

`CLOAKBROWSER_BINARY_PATH`

—

Skip download, use a local Chromium binary

`CLOAKBROWSER_CACHE_DIR`

`~/.cloakbrowser`

Binary cache directory

`CLOAKBROWSER_DOWNLOAD_URL`

`cloakbrowser.dev`

Custom download URL for binary

`CLOAKBROWSER_AUTO_UPDATE`

`true`

Set to `false` to disable background update checks

`CLOAKBROWSER_SKIP_CHECKSUM`

`false`

Only applies to a custom `CLOAKBROWSER_DOWNLOAD_URL`: set to `true` to skip its checksum check. Signature verification on the official download path is mandatory and cannot be skipped.

`CLOAKBROWSER_GEOIP_TIMEOUT_SECONDS`

`5`

Max seconds for GeoIP resolution before continuing without it

`CLOAKBROWSER_WIDEVINE_CDM`

—

Path to a sideloaded `WidevineCdm` directory (overrides auto-detection next to the binary). See Widevine / DRM

`CLOAKBROWSER_WIDEVINE`

`1`

Set to `0` to disable automatic Widevine hint-file seeding for persistent contexts

`CLOAKBROWSER_FETCH_WIDEVINE`

`0`

Docker only: set to `1` to auto-fetch the Widevine CDM on container start (Linux x86-64 only). See Widevine / DRM

`CLOAKBROWSER_VERSION`

—

Pin to an exact Chromium version for rollback (e.g. `148.0.7778.215.2`). Works with Free and Pro binaries

Fingerprint Management
----------------------

The binary is **stealthy by default** — no flags needed. It auto-generates a random fingerprint seed at startup and spoofs all detectable values (GPU, hardware specs, screen dimensions, canvas, WebGL, audio, fonts). Every launch produces a fresh, coherent identity.

**How fingerprinting works:**

Scenario

What happens

**No flags**

Random seed auto-generated at startup. GPU, screen, hardware specs, and all noise patches are spoofed automatically. Fresh identity each launch.

**`--fingerprint=seed`**

Deterministic identity from the seed. Same seed = same fingerprint across launches. Use this for session persistence (returning visitor).

**`--fingerprint=seed` + explicit flags**

Explicit flags override individual auto-generated values. The seed fills in everything else.

The binary detects its platform at compile time — a macOS binary reports as macOS with Apple GPU, a Linux binary reports as Linux with NVIDIA GPU. The **wrapper** overrides this on Linux by passing `--fingerprint-platform=windows`, so sessions appear as Windows desktops (more common fingerprint, harder to cluster). Use `--fingerprint-platform` for cross-platform spoofing when running the binary directly.

> **Tip: Use a fixed seed when revisiting the same site.** A random seed makes every session look like a different device — which can be suspicious when hitting the same site repeatedly from the same IP. For reCAPTCHA v3 Enterprise and similar scoring systems, a fixed seed produces a consistent fingerprint across sessions, making you look like a returning visitor:
> 
> browser \= launch(args\=\["--fingerprint=12345"\])
> 
> const browser \= await launch({ args: \['--fingerprint=12345'\] });

### Default Fingerprint

Every `launch()` call sets these automatically. The **wrapper** applies platform-aware defaults — on Linux it spoofs as Windows for a more common fingerprint, on macOS it runs as a native Mac browser:

Flag

Linux/Windows Default

macOS Default

Controls

`--fingerprint`

Random (10000–99999)

Random (10000–99999)

Master seed for canvas, WebGL, audio, fonts, client rects

`--fingerprint-platform`

`windows`

`macos`

`navigator.platform`, User-Agent OS, GPU pool selection

The binary auto-generates everything else from the seed: GPU, hardware concurrency, device memory, and screen dimensions. Each seed produces a unique, consistent fingerprint. Override with explicit flags if needed.

> **Using the binary directly?** It works out of the box with zero flags -- the binary auto-spoofs everything. Pass `--fingerprint=seed` for a persistent identity, or use explicit flags like `--fingerprint-gpu-renderer` to override any auto-generated value.

### Additional Flags

Supported by the binary but **not set by default** — pass via `args` to customize:

Flag

Controls

`--fingerprint-gpu-vendor`

WebGL `UNMASKED_VENDOR_WEBGL` (auto-generated from seed + platform)

`--fingerprint-gpu-renderer`

WebGL `UNMASKED_RENDERER_WEBGL` (auto-generated from seed + platform)

`--fingerprint-hardware-concurrency`

`navigator.hardwareConcurrency` (auto-generated: `8`)

`--fingerprint-device-memory`

`navigator.deviceMemory` in GB (auto-generated: `8`)

`--fingerprint-screen-width`

Screen width (auto-generated: `1920` Win/Linux, `1440` macOS)

`--fingerprint-screen-height`

Screen height (auto-generated: `1080` Win/Linux, `900` macOS)

`--fingerprint-brand`

Browser brand: `Chrome`, `Edge`, `Opera`, `Vivaldi`

`--fingerprint-brand-version`

Brand version (UA + Client Hints)

`--fingerprint-platform-version`

Client Hints platform version

`--fingerprint-location`

Geolocation coordinates

`--fingerprint-timezone`

Timezone (e.g. `America/New_York`)

`--fingerprint-locale`

Locale (e.g. `en-US`)

`--fingerprint-storage-quota`

Override storage quota in MB — affects `storage.estimate()`, `storageBuckets`, and legacy webkit APIs. Auto-normalized when `--fingerprint` is set

`--fingerprint-taskbar-height`

Override taskbar height (binary defaults: Win=48, Mac=95, Linux=0)

`--fingerprint-fonts-dir`

Path to directory containing target-platform fonts (see Font Setup on Linux)

`--fingerprint-windows-font-metrics`

**Chromium 148+ binary only** (no-op on earlier builds). Align font metrics with the Windows platform when spoofing Windows on Linux — used in the FingerprintJS config. Requires Windows fonts installed (see Font Setup on Linux); no effect without them

`--fingerprint-webrtc-ip`

WebRTC ICE candidate IP replacement. Use `auto` to resolve from proxy exit IP (makes an HTTP call through the proxy), or pass an explicit IP. Auto-injected when `geoip=True`

`--fingerprint-noise=false`

Disable noise injection (canvas, WebGL, audio, client rects) while keeping the deterministic fingerprint seed active

`--enable-blink-features=FakeShadowRoot`

Access closed shadow DOM elements

> **Note:** All stealth tests were verified with the default fingerprint config above. Changing these flags may affect detection results — test your configuration before using in production.

### Font Setup on Linux

**Required for aggressive anti-bot sites (Kasada, Akamai).** These systems render emoji on a hidden canvas and hash the pixel output. Minimal Linux environments (Docker, cloud VMs) often lack emoji and extended fonts, producing hashes that don't match any real browser. Install standard font packages to fix this:

sudo apt install -y fonts-noto-color-emoji fonts-freefont-ttf fonts-unifont \\
    fonts-ipafont-gothic fonts-wqy-zenhei fonts-tlwg-loma-otf

The Docker image (`cloakhq/cloakbrowser`) ships with these pre-installed. If you run the binary directly on a Linux server or in a custom Docker image, install them manually.

**Optional: Windows fonts for CreepJS font enumeration.** The packages above fix anti-bot canvas checks but won't improve your CreepJS font score. For that, you need actual Windows fonts (Segoe UI, Calibri, Bahnschrift, etc.) from a Windows machine's `C:\Windows\Fonts\` directory — `ttf-mscorefonts-installer` only has old XP-era fonts and isn't enough.

mkdir -p ~/.local/share/fonts/windows
cp /path/to/windows/fonts/\*.ttf ~/.local/share/fonts/windows/
cp /path/to/windows/fonts/\*.TTF ~/.local/share/fonts/windows/
fc-cache -f  # mandatory for manually copied fonts

browser \= launch(
    args\=\["--fingerprint-fonts-dir=/home/user/.local/share/fonts/windows"\],
)

### Examples

\# Pin a seed for a persistent identity
browser \= launch(args\=\["--fingerprint=42069"\])

\# Full control — disable defaults, set everything yourself
browser \= launch(stealth\_args\=False, args\=\[
    "--fingerprint=42069",
    "--fingerprint-platform=windows",
\])

\# Override GPU to look like a specific machine
browser \= launch(args\=\[
    "--fingerprint-gpu-vendor=Intel Inc.",
    "--fingerprint-gpu-renderer=Intel Iris OpenGL Engine",
\])

Examples
--------

**Python** — see `examples/`:

-   `basic.py` — Launch and load a page
-   `persistent_context.py` — Persistent profile with cookie/localStorage persistence
-   `recaptcha_score.py` — Check your reCAPTCHA v3 score
-   `stealth_test.py` — Run against 6 detection sites
-   `fingerprint_scan_test.py` — Test against fingerprint-scan.com and CreepJS

**JavaScript** — see `js/examples/`:

-   `basic-playwright.ts` — Playwright launch and load
-   `basic-puppeteer.ts` — Puppeteer launch and load
-   `stealth-test.ts` — Run against 6 detection sites

### Framework Integrations

CloakBrowser works with any framework that uses Playwright or Chromium:

\# Option 1: Framework launches our binary directly (Selenium, Stagehand, UC)
from cloakbrowser.download import ensure\_binary
from cloakbrowser.config import get\_default\_stealth\_args
binary\_path \= ensure\_binary()          \# auto-downloads if needed
stealth\_args \= get\_default\_stealth\_args()  \# all fingerprint flags

\# Option 2: CloakBrowser launches first, framework connects via CDP (browser-use, Crawl4AI, Scrapling)
from cloakbrowser import launch\_async
browser \= await launch\_async(args\=\["--remote-debugging-port=9242"\])
\# Connect your framework to http://127.0.0.1:9242 — all stealth flags are set
\# Note: humanize requires the wrapper (see below)

> **Humanize over CDP**: Stealth fingerprint patches work automatically over CDP, but `humanize=True` is a wrapper-level feature. If you connect to CloakBrowser via CDP from a separate script, import the patching functions to add humanization:
> 
> import { patchBrowser, resolveConfig } from 'cloakbrowser/human';
> patchBrowser(browser, resolveConfig('default'));

Framework

Stars

Language

Example

browser-use

70K

Python

`browser_use_example.py`

Crawl4AI

58K

Python

`crawl4ai_example.py`

Crawlee

8.6K

Python

`crawlee_example.py`

Scrapling

21K

Python

`scrapling_example.py`

Stagehand

21K

TypeScript

`stagehand.ts`

LangChain

100K+

Python

`langchain_loader.py`

Selenium

—

Python

`selenium_example.py`

undetected-chromedriver

12K

Python

`undetected_chromedriver.py`

agent-browser

—

Shell

`agent_browser.sh`

### Deployment Integrations

Platform

Example

AWS Lambda

`aws_lambda/` — One-shot scrapes in Lambda (container image)

Platforms
---------

Platform

Free

Pro

Status

Linux x86\_64

Chromium 146 (58 patches)

Chromium 148 (59 patches)

✅

Linux arm64 (RPi, Graviton)

Chromium 146 (58 patches)

Chromium 148 (59 patches)

✅

macOS arm64 (Apple Silicon)

Chromium 145 (26 patches)

Chromium 148 (59 patches)

✅

macOS x86\_64 (Intel)

Chromium 145 (26 patches)

Chromium 148 (59 patches)

✅

Windows x86\_64

Chromium 146 (58 patches)

Chromium 148 (59 patches)

✅

The wrapper auto-downloads the correct binary for your platform.

**macOS first launch:** The binary is ad-hoc signed. On first run, macOS Gatekeeper will block it. Right-click the app → **Open** → click **Open** in the dialog. This is only needed once.

Docker
------

Pre-built image on Docker Hub — no install, no setup.

> **Pro:** the image ships with the free binary. Set `CLOAKBROWSER_LICENSE_KEY` (e.g. `-e CLOAKBROWSER_LICENSE_KEY=cb_xxx`, or in Compose) and the latest binary downloads at runtime.

### Quick test

docker run --rm cloakhq/cloakbrowser cloaktest

### Run a script

# Inline script
docker run --rm cloakhq/cloakbrowser python -c "
from cloakbrowser import launch
browser = launch()
page = browser.new\_page()
page.goto('https://example.com')
print(page.title())
browser.close()
"

# Mount your own script
docker run --rm -v ./my\_script.py:/app/my\_script.py cloakhq/cloakbrowser python my\_script.py

# With a proxy
docker run --rm cloakhq/cloakbrowser python -c "
from cloakbrowser import launch
browser = launch(proxy='http://user:pass@proxy:8080')
page = browser.new\_page()
page.goto('https://example.com')
print(page.title())
browser.close()
"

### CDP server mode

Start a persistent stealth browser and connect to it remotely via Chrome DevTools Protocol:

docker run -d --name cloak -p 127.0.0.1:9222:9222 cloakhq/cloakbrowser cloakserve

Then connect from your host machine:

from playwright.sync\_api import sync\_playwright

pw \= sync\_playwright().start()
browser \= pw.chromium.connect\_over\_cdp("http://localhost:9222")
page \= browser.new\_page()
page.goto("https://example.com")
print(page.title())
browser.close()

If your framework needs a direct WebSocket endpoint, fetch Chrome's discovery document and use the rewritten `webSocketDebuggerUrl`. The URL points back through `cloakserve` so the CDP proxy can keep per-seed routing intact:

curl http://localhost:9222/json/version | jq -r .webSocketDebuggerUrl
# ws://localhost:9222/devtools/browser/<browser-id>

curl 'http://localhost:9222/json/version?fingerprint=11111' | jq -r .webSocketDebuggerUrl
# ws://localhost:9222/fingerprint/11111/devtools/browser/<browser-id>

When `cloakserve` runs behind a reverse proxy or TLS terminator, forward the public host/protocol headers so generated WebSocket URLs use the address clients can actually reach:

proxy\_set\_header Host $host;
proxy\_set\_header X-Forwarded-Host $host;
proxy\_set\_header X-Forwarded-Proto $scheme;

With those headers, `/json/version` returns public endpoints such as `wss://cdp.example.com/fingerprint/11111/devtools/browser/<browser-id>` instead of an internal container host.

Pass extra flags to the browser:

# With proxy
docker run -d --name cloak -p 127.0.0.1:9222:9222 cloakhq/cloakbrowser \\
  cloakserve --proxy-server=http://proxy:8080

# Headed mode (renders to Xvfb inside container)
docker run -d --name cloak -p 127.0.0.1:9222:9222 cloakhq/cloakbrowser \\
  cloakserve --headless=false

# Reap disconnected per-seed browser processes after 5 minutes
docker run -d --name cloak -p 127.0.0.1:9222:9222 cloakhq/cloakbrowser \\
  cloakserve --idle-timeout=300

Stop the server:

docker stop cloak && docker rm cloak

> **Security:** CDP gives full control over the browser (execute JS, read pages, access files). The examples bind to `127.0.0.1` so only your machine can connect. Never expose port 9222 to the public internet without additional authentication.

### Docker Compose

services:
  cloakbrowser:
    image: cloakhq/cloakbrowser
    command: cloakserve
    restart: unless-stopped
    ports:
      - "127.0.0.1:9222:9222"
    healthcheck:
      test: \["CMD", "curl", "-f", "http://localhost:9222/json/version"\]
      interval: 30s
      timeout: 5s
      retries: 3
      start\_period: 10s

**Per-connection fingerprint seeds** — run multiple browser identities from a single container. Each unique seed spawns a separate Chrome process with its own fingerprint:

\# Each seed gets unique canvas noise, client rects, and other browser signals
b1 \= pw.chromium.connect\_over\_cdp("http://localhost:9222?fingerprint=11111")
b2 \= pw.chromium.connect\_over\_cdp("http://localhost:9222?fingerprint=22222")

\# Full identity control via query params
b3 \= pw.chromium.connect\_over\_cdp(
    "http://localhost:9222?fingerprint=33333"
    "&timezone=Asia/Tokyo&locale=ja-JP&platform=macos"
    "&hardware-concurrency=4&device-memory=8"
)

\# Auto-detect timezone/locale from proxy exit IP
b4 \= pw.chromium.connect\_over\_cdp(
    "http://localhost:9222?fingerprint=44444"
    "&proxy=http://proxy:8080&geoip=true"
)

Supported query params: `fingerprint`, `timezone`, `locale`, `platform`, `platform-version`, `brand`, `brand-version`, `gpu-vendor`, `gpu-renderer`, `hardware-concurrency`, `device-memory`, `screen-width`, `screen-height`, `proxy`, `geoip`. Same seed reuses the same process (first connection's params win). No seed = shared default process (backward compatible).

By default, per-seed processes stay alive until `cloakserve` exits. If clients create many unique seeds, set `--idle-timeout=SECONDS` or `CLOAKSERVE_IDLE_TIMEOUT=SECONDS` to automatically terminate a seed's Chrome process after its last CDP WebSocket disconnects. `0`, `off`, `false`, `none`, or `disabled` disable idle cleanup. When cleanup runs, the seed's temporary profile directory under `--data-dir` is removed too. Check active processes at `GET /` (returns JSON with PIDs, ports, connection counts, idle timeout, and pending cleanup status).

**Persistent profiles** — mount a volume to keep cookies and sessions across container restarts:

docker run --rm -v ./my-profile:/profile cloakhq/cloakbrowser python -c "
from cloakbrowser import launch\_persistent\_context
ctx = launch\_persistent\_context('/profile')
page = ctx.new\_page()
page.goto('https://example.com')
ctx.close()
"

Run again with the same volume — cookies, localStorage, and cache are restored automatically.

To enable Widevine DRM (Netflix, Spotify Web, etc.) in a persistent profile, add `-e CLOAKBROWSER_FETCH_WIDEVINE=1` to auto-fetch the CDM on first launch (see Widevine / DRM); it caches in the mounted volume.

**Resource usage:** ~190MB RAM idle, ~280MB with 3 tabs. ~30MB per additional tab.

### Extend with your own image

FROM cloakhq/cloakbrowser
COPY your\_script.py /app/
CMD \["python", "your\_script.py"\]

**Building your own image from pip** — use `python -m cloakbrowser install` to download the binary during build with visible progress:

FROM python:3.12-slim
RUN pip install cloakbrowser && python -m cloakbrowser install
COPY your\_script.py /app/
CMD \["python", "/app/your\_script.py"\]

**Building from source** — a `Dockerfile` is also included if you prefer to build your own image:

docker build -t cloakbrowser .

CloakBrowser works identically local, in Docker, and on VPS. No environment-specific config needed.

**Note:** If you run CloakBrowser inside a web server with uvloop (e.g., `uvicorn[standard]`), use `--loop asyncio` to avoid subprocess pipe hangs.

Troubleshooting
---------------

* * *

### Still getting blocked on aggressive sites (DataDome, Turnstile)?

Some sites detect headless mode even with our C++ patches. Run in **headed mode** with a virtual display:

# Install Xvfb (virtual framebuffer)
sudo apt install xvfb

# Start virtual display
Xvfb :99 -screen 0 1920x1080x24 &
export DISPLAY=:99

from cloakbrowser import launch

\# Headed mode + residential proxy for maximum stealth
browser \= launch(headless\=False, proxy\="http://your-residential-proxy:port")
page \= browser.new\_page()
page.goto("https://heavily-protected-site.com")  \# passes DataDome, etc.
browser.close()

This runs a real headed browser rendered on a virtual display — no physical monitor needed. Combine with the recommended config below for maximum stealth.

* * *

### Recommended config for anti-bot sites

Most blocks come from missing one of these three things, not from browser fingerprint detection:

browser \= launch(
    proxy\="http://your-residential-proxy:port",  \# residential IP — datacenter IPs get blocked by reputation alone
    geoip\=True,      \# matches timezone + locale to proxy exit IP (without this: UTC + en-US = bot signal)
    headless\=False,   \# headed mode — some sites detect headless even with C++ patches
    humanize\=True,    \# human-like mouse, keyboard, scroll behavior
)

const browser \= await launch({
    proxy: 'http://your-residential-proxy:port',
    geoip: true,
    headless: false,
    humanize: true,
});

If your proxy supports SOCKS5, use it for better compatibility — SOCKS5 tunnels raw TCP, avoiding HTTP CONNECT issues that some proxies have with HTTP/2:

browser \= launch(proxy\="socks5://user:pass@proxy:1080", geoip\=True, headless\=False, humanize\=True)

If you're still blocked after this, check the font setup below.

* * *

### Detected by FingerprintJS?

FingerprintJS (`demo.fingerprint.com/playground`) checks multiple signals. Each detection has a specific cause:

Detection

Cause

Fix

**`nodriver` / bad bot**

Stale binary/wrapper, missing current FPJS patches, or poor proxy IP reputation

Upgrade to the latest Pro binary (`148.0.7778.215.3+`), use a residential proxy with `geoip=True`, and use the config below.

**Browser tampering**

Noise injection detected by ML

`--fingerprint-noise=false`

**Browser tampering** (fonts)

Font metrics don't match the spoofed Windows platform

`--fingerprint-windows-font-metrics` (Chromium 148+ binary; requires Windows fonts installed)

**Virtual machine**

Screen dimensions don't match viewport

`--fingerprint-screen-width/height` matching viewport

Config that passes FPJS on the latest binary (Linux, residential proxy):

browser \= launch(
    headless\=False,
    proxy\="http://user:pass@residential-proxy:port",
    geoip\=True,
    args\=\[
        "--fingerprint-noise=false",          \# prevents tampering detection
        "--fingerprint-windows-font-metrics", \# align font metrics — 148+ binary, needs Windows fonts
    \],
)

const browser \= await launch({
    headless: false,
    proxy: 'http://user:pass@residential-proxy:port',
    geoip: true,
    args: \[
        '--fingerprint-noise=false',
        '--fingerprint-windows-font-metrics',  // align font metrics — 148+ binary, needs Windows fonts
    \],
});

Requires a **Chromium 148+ binary** and **Windows fonts** installed (see Font Setup on Linux); run with a **residential proxy** and `geoip=True`.

**Persistent contexts** (`launch_persistent_context` / `launchPersistentContext`) use the same FPJS config on the latest Pro binary. Use a real `userDataDir`. Storage-quota tuning is unrelated to FingerprintJS here; it only affects detectors that infer incognito from quota, such as BrowserScan (see storage quota). For DRM/media playback, see Widevine / DRM.

* * *

### Blocked on Kasada / Akamai sites despite correct config?

On minimal Linux environments, missing font packages cause canvas emoji rendering to produce hashes that anti-bot systems don't recognize. This is the most common cause of blocks on aggressive sites after proxy, geoip, and headed mode are already set up correctly.

Install the font packages listed in Font Setup on Linux above.

* * *

### Sites challenge fresh sessions but work after first visit

Some sites challenge first-time visitors with no cookies over HTTP/2. This affects all Chromium browsers, not just CloakBrowser. Use a persistent profile to warm up cookies once, then reuse across sessions:

from cloakbrowser import launch\_persistent\_context

\# First run: warm up with --disable-http2
ctx \= launch\_persistent\_context("./profile", args\=\["--disable-http2"\])
page \= ctx.new\_page()
page.goto("https://example.com")  \# warms up cookies
ctx.close()

\# Future runs — no --disable-http2 needed
ctx \= launch\_persistent\_context("./profile")
page \= ctx.new\_page()
page.goto("https://example.com")  \# passes with saved cookies

import { launchPersistentContext } from 'cloakbrowser';

// First run: warm up with --disable-http2
let ctx \= await launchPersistentContext({ userDataDir: './profile', args: \['--disable-http2'\] });
let page \= await ctx.newPage();
await page.goto('https://example.com');
await ctx.close();

// Future runs — no --disable-http2 needed
ctx \= await launchPersistentContext({ userDataDir: './profile' });

For stateless/ephemeral use cases, `launch(args=["--disable-http2"])` forces HTTP/1.1 which bypasses the check. Only use this flag for sites that require it — most work fine with HTTP/2. If your proxy supports SOCKS5, use `proxy="socks5://user:pass@host:port"` instead — SOCKS5 bypasses HTTP CONNECT entirely.

* * *

### Something not working? Make sure you're on the latest version

Older versions may use outdated stealth args or download an older binary:

pip install -U cloakbrowser    # Python
npm install cloakbrowser@latest # JavaScript
docker pull cloakhq/cloakbrowser:latest  # Docker

### New update broke something? Roll back

Two ways to go back to a working version:

**Pin the binary** (keep current wrapper, just use an older Chromium) — works for Free and Pro:

\# Free — pin a public release
browser \= launch(browser\_version\="146.0.7680.177.5")

\# Pro — pin a previous Pro version
browser \= launch(license\_key\="cb\_xxxxxxxx", browser\_version\="148.0.7778.215.2")

export CLOAKBROWSER\_VERSION=146.0.7680.177.5   # env var for all launches

// Free — pin a public release
const browser \= await launch({ browserVersion: '146.0.7680.177.5' });

The pin is never sticky — unpinned launches always use the latest available version.

**Or downgrade the wrapper** (each wrapper release hardcodes which binary version it downloads):

pip install cloakbrowser==0.3.21              # Python
npm install cloakbrowser@0.3.21               # JavaScript
docker pull cloakhq/cloakbrowser:0.3.21       # Docker

* * *

Set a custom download URL or use a local binary:

export CLOAKBROWSER\_BINARY\_PATH=/path/to/your/chrome

### macOS: "App is damaged" or Gatekeeper blocks launch

The binary is ad-hoc signed. macOS quarantines downloaded files. Run once to clear it:

xattr -cr ~/.cloakbrowser/chromium-\*/Chromium.app

* * *

### "playwright install" vs CloakBrowser binary

You do NOT need `playwright install chromium`. CloakBrowser downloads its own binary. You only need Playwright's system deps:

playwright install-deps chromium

* * *

### Site detects incognito / private browsing mode

By default, `launch()` opens an incognito context. Some sites penalize this. Use `launch_persistent_context()` to get a real profile with cookie persistence:

from cloakbrowser import launch\_persistent\_context

ctx \= launch\_persistent\_context("./my-profile", headless\=False)

If the site still flags incognito, raise the storage quota to appear as a regular browsing session. See the storage quota tradeoff for details on how this affects different detection services.

* * *

### reCAPTCHA v3 scores are low (0.1–0.3)

Avoid `page.wait_for_timeout()` — it sends CDP protocol commands that reCAPTCHA detects. Use native sleep instead:

\# Bad — sends CDP commands, reCAPTCHA detects this
page.wait\_for\_timeout(3000)

\# Good — invisible to the browser
import time
time.sleep(3)

// Bad — sends CDP commands
await page.waitForTimeout(3000);

// Good — invisible to the browser
await new Promise(r \=> setTimeout(r, 3000));

Other tips for maximizing reCAPTCHA scores:

-   **Use Playwright, not Puppeteer** — Puppeteer sends more CDP protocol traffic that reCAPTCHA detects (details)
    
-   **Use residential proxies** — datacenter IPs are flagged by IP reputation, not browser fingerprint
    
-   **Spend 15+ seconds on the page** before triggering reCAPTCHA — short visits score lower
    
-   **Space out requests** — back-to-back `grecaptcha.execute()` calls from the same session get penalized. Wait 30+ seconds between pages with reCAPTCHA
    
-   **Use a fixed fingerprint seed** for consistent device identity across sessions (see Fingerprint Management)
    
-   **Use `page.type()` instead of `page.fill()`** for form filling — `fill()` sets values directly without keyboard events, which reCAPTCHA's behavioral analysis flags. `type()` with a delay simulates real keystrokes:
    
    page.type("#email", "user@example.com", delay\=50)
    
-   **Minimize `page.evaluate()` calls** before the reCAPTCHA check fires — each one sends CDP traffic
    

FAQ
---

**Q: Is this legal?** A: CloakBrowser is a browser built on open-source Chromium. We do not condone illegal use. Automating systems without authorization, credential stuffing, and account creation abuse are expressly prohibited. See BINARY-LICENSE.md for full terms.

**Q: Is CloakBrowser free?** A: The wrapper (Python + JS) is MIT and free forever. The binary uses a delayed free-release model: the previous Chromium major version (currently v146) is free on GitHub Releases with unlimited sessions; the latest major version is for Pro subscribers. Each new major release rolls the prior major version down to free.

**Q: Do I need a license key for the free version?** A: No. The free binary downloads automatically with no key. A license key only unlocks the latest (Pro) binary.

**Q: What happens if I cancel Pro?** A: Your subscription stays active until the end of the current billing period — cancelling doesn't cut you off immediately. After it ends, the wrapper stops pulling new Pro versions and falls back to the free binary on its next license check (cached ~24h). You just stop getting new versions.

**Q: How is this different from Camoufox?** A: Camoufox patches Firefox. We patch Chromium. Chromium means native Playwright support, larger ecosystem, and TLS fingerprints that match real Chrome. Camoufox returned in early 2026 but is in unstable beta — CloakBrowser is production-ready.

**Q: Will detection sites eventually catch this?** A: Possibly. Bot detection is an arms race. Source-level patches are harder to detect than config-level patches, but not impossible. We actively monitor and update when detection evolves.

**Q: Can I use my own proxy?** A: Yes. Pass `proxy="http://user:pass@host:port"` or `proxy="socks5://user:pass@host:port"` to `launch()`. Both HTTP and SOCKS5 proxies are supported natively.

Links
-----

-   📋 **Changelog** — CHANGELOG.md
-   🌐 **Website** — cloakbrowser.dev
-   🐛 **Bug reports & feature requests** — GitHub Issues
-   📦 **PyPI** — pypi.org/project/cloakbrowser
-   📦 **npm** — npmjs.com/package/cloakbrowser
-   ☕ **Support** — ko-fi.com/cloakhq
-   📧 **Contact** — cloakhq@pm.me

Security
--------

The wrapper automatically verifies every binary download against a pinned Ed25519 signature on the published checksums before extraction — a compromised mirror cannot serve a tampered or downgraded binary. Releases are additionally signed for manual supply chain verification:

# Verify GPG signature (binary release tag)
gpg --keyserver keyserver.ubuntu.com --recv-keys C60C0DDC9D0DE2DD
git verify-tag chromium-v146.0.7680.177.5

# Verify GitHub binary attestation (Sigstore)
gh attestation verify cloakbrowser-linux-x64.tar.gz --repo CloakHQ/cloakbrowser

# Verify Docker image signature (Cosign/Sigstore)
cosign verify \\
  --certificate-identity-regexp "https://github.com/CloakHQ/CloakBrowser/" \\
  --certificate-oidc-issuer "https://token.actions.githubusercontent.com" \\
  cloakhq/cloakbrowser:latest

License
-------

-   **Wrapper code** (this repository) — MIT. See LICENSE.
-   **CloakBrowser binary** (compiled Chromium):
    -   **v146 and earlier** — free for personal and commercial use, no redistribution (OEM/SaaS license required to serve third parties).
    -   **v148+ (latest)** — requires an active CloakBrowser Pro subscription to download.
    -   See BINARY-LICENSE.md for full terms.

Contributing
------------

Issues and PRs welcome. If something isn't working, open an issue — we respond fast.

Contributors
------------

-   @evelaa123 — humanize behavior, persistent contexts, Windows fix, .NET client
-   @yahooguntu — persistent contexts
-   @kitiho — null viewport fix
-   @eofreternal — humanConfig type fix, humanized method option types, iframe pointer-events fix
-   @manaskarra — iframe scope fix for humanized frame actions, GeoIP timeout guard
-   @Youhai020616 — SOCKS5 credential encoding logging
-   @AlexTech314 — AWS Lambda integration, cold-start hardening
-   @dgtlmoon — graceful pw.stop() cleanup
-   @zackycodes — Chrome extension loading
-   @aaronjmars — security fixes (shell injection, dep bumps)
-   @Seryiza — Nix/NixOS flake
-   @245678000000 — package-lock sync
-   @honor2030 — cloakserve WebSocket origin guard, CDP WebSocket URL rewrite, composable JS launch helpers
-   @sparanoid — Docker Xvfb lock cleanup
-   @Kumario1 — cloakserve idle cleanup for seeded profiles
-   @0xlally — security reports (cloakserve path traversal, WebSocket origin bypass)

Star History
------------
