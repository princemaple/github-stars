---
project: crawl4ai
stars: 56532
description: 🚀🤖 Crawl4AI: Open-source LLM Friendly Web Crawler & Scraper. Don't be shy, join here: https://discord.gg/jP8KfhDhyN
url: https://github.com/unclecode/crawl4ai
---

🚀🤖 Crawl4AI: Open-source LLM Friendly Web Crawler & Scraper.
==============================================================

Crawl4AI turns the web into clean, LLM ready Markdown for RAG, agents, and data pipelines. Fast, controllable, battle tested by a 50k+ star community.

✨ Check out latest update v0.7.7

✨ **New in v0.7.7**: Complete Self-Hosting Platform with Real-time Monitoring! Enterprise-grade monitoring dashboard, comprehensive REST API, WebSocket streaming, smart browser pool management, and production-ready observability. Full visibility and control over your crawling infrastructure. Release notes →

✨ Recent v0.7.6: Complete Webhook Infrastructure for Docker Job Queue API! Real-time notifications for both `/crawl/job` and `/llm/job` endpoints with exponential backoff retry, custom headers, and flexible delivery modes. No more polling! Release notes →

✨ Previous v0.7.5: Docker Hooks System with function-based API for pipeline customization, Enhanced LLM Integration with custom providers, HTTPS Preservation, and multiple community-reported bug fixes. Release notes →

🤓 **My Personal Story**

I grew up on an Amstrad, thanks to my dad, and never stopped building. In grad school I specialized in NLP and built crawlers for research. That’s where I learned how much extraction matters.

In 2023, I needed web-to-Markdown. The “open source” option wanted an account, API token, and $16, and still under-delivered. I went turbo anger mode, built Crawl4AI in days, and it went viral. Now it’s the most-starred crawler on GitHub.

I made it open source for **availability**, anyone can use it without a gate. Now I’m building the platform for **affordability**, anyone can run serious crawls without breaking the bank. If that resonates, join in, send feedback, or just crawl something amazing.

Why developers pick Crawl4AI

-   **LLM ready output**, smart Markdown with headings, tables, code, citation hints
-   **Fast in practice**, async browser pool, caching, minimal hops
-   **Full control**, sessions, proxies, cookies, user scripts, hooks
-   **Adaptive intelligence**, learns site patterns, explores only what matters
-   **Deploy anywhere**, zero keys, CLI and Docker, cloud friendly

🚀 Quick Start
--------------

1.  Install Crawl4AI:

# Install the package
pip install -U crawl4ai

# For pre release versions
pip install crawl4ai --pre

# Run post-installation setup
crawl4ai-setup

# Verify your installation
crawl4ai-doctor

If you encounter any browser-related issues, you can install them manually:

python -m playwright install --with-deps chromium

1.  Run a simple web crawl with Python:

import asyncio
from crawl4ai import \*

async def main():
    async with AsyncWebCrawler() as crawler:
        result \= await crawler.arun(
            url\="https://www.nbcnews.com/business",
        )
        print(result.markdown)

if \_\_name\_\_ \== "\_\_main\_\_":
    asyncio.run(main())

1.  Or use the new command-line interface:

# Basic crawl with markdown output
crwl https://www.nbcnews.com/business -o markdown

# Deep crawl with BFS strategy, max 10 pages
crwl https://docs.crawl4ai.com --deep-crawl bfs --max-pages 10

# Use LLM extraction with a specific question
crwl https://www.example.com/products -q "Extract all product prices"

💖 Support Crawl4AI
-------------------

> 🎉 **Sponsorship Program Now Open!** After powering 51K+ developers and 1 year of growth, Crawl4AI is launching dedicated support for **startups** and **enterprises**. Be among the first 50 **Founding Sponsors** for permanent recognition in our Hall of Fame.

Crawl4AI is the #1 trending open-source web crawler on GitHub. Your support keeps it independent, innovative, and free for the community — while giving you direct access to premium benefits.

  

### 🤝 Sponsorship Tiers

-   **🌱 Believer ($5/mo)** — Join the movement for data democratization
-   **🚀 Builder ($50/mo)** — Priority support & early access to features
-   **💼 Growing Team ($500/mo)** — Bi-weekly syncs & optimization help
-   **🏢 Data Infrastructure Partner ($2000/mo)** — Full partnership with dedicated support  
    _Custom arrangements available - see SPONSORS.md for details & contact_

**Why sponsor?**  
No rate-limited APIs. No lock-in. Build and own your data pipeline with direct guidance from the creator of Crawl4AI.

See All Tiers & Benefits →

✨ Features
----------

📝 **Markdown Generation**

-   🧹 **Clean Markdown**: Generates clean, structured Markdown with accurate formatting.
-   🎯 **Fit Markdown**: Heuristic-based filtering to remove noise and irrelevant parts for AI-friendly processing.
-   🔗 **Citations and References**: Converts page links into a numbered reference list with clean citations.
-   🛠️ **Custom Strategies**: Users can create their own Markdown generation strategies tailored to specific needs.
-   📚 **BM25 Algorithm**: Employs BM25-based filtering for extracting core information and removing irrelevant content.

📊 **Structured Data Extraction**

-   🤖 **LLM-Driven Extraction**: Supports all LLMs (open-source and proprietary) for structured data extraction.
-   🧱 **Chunking Strategies**: Implements chunking (topic-based, regex, sentence-level) for targeted content processing.
-   🌌 **Cosine Similarity**: Find relevant content chunks based on user queries for semantic extraction.
-   🔎 **CSS-Based Extraction**: Fast schema-based data extraction using XPath and CSS selectors.
-   🔧 **Schema Definition**: Define custom schemas for extracting structured JSON from repetitive patterns.

🌐 **Browser Integration**

-   🖥️ **Managed Browser**: Use user-owned browsers with full control, avoiding bot detection.
-   🔄 **Remote Browser Control**: Connect to Chrome Developer Tools Protocol for remote, large-scale data extraction.
-   👤 **Browser Profiler**: Create and manage persistent profiles with saved authentication states, cookies, and settings.
-   🔒 **Session Management**: Preserve browser states and reuse them for multi-step crawling.
-   🧩 **Proxy Support**: Seamlessly connect to proxies with authentication for secure access.
-   ⚙️ **Full Browser Control**: Modify headers, cookies, user agents, and more for tailored crawling setups.
-   🌍 **Multi-Browser Support**: Compatible with Chromium, Firefox, and WebKit.
-   📐 **Dynamic Viewport Adjustment**: Automatically adjusts the browser viewport to match page content, ensuring complete rendering and capturing of all elements.

🔎 **Crawling & Scraping**

-   🖼️ **Media Support**: Extract images, audio, videos, and responsive image formats like `srcset` and `picture`.
-   🚀 **Dynamic Crawling**: Execute JS and wait for async or sync for dynamic content extraction.
-   📸 **Screenshots**: Capture page screenshots during crawling for debugging or analysis.
-   📂 **Raw Data Crawling**: Directly process raw HTML (`raw:`) or local files (`file://`).
-   🔗 **Comprehensive Link Extraction**: Extracts internal, external links, and embedded iframe content.
-   🛠️ **Customizable Hooks**: Define hooks at every step to customize crawling behavior (supports both string and function-based APIs).
-   💾 **Caching**: Cache data for improved speed and to avoid redundant fetches.
-   📄 **Metadata Extraction**: Retrieve structured metadata from web pages.
-   📡 **IFrame Content Extraction**: Seamless extraction from embedded iframe content.
-   🕵️ **Lazy Load Handling**: Waits for images to fully load, ensuring no content is missed due to lazy loading.
-   🔄 **Full-Page Scanning**: Simulates scrolling to load and capture all dynamic content, perfect for infinite scroll pages.

🚀 **Deployment**

-   🐳 **Dockerized Setup**: Optimized Docker image with FastAPI server for easy deployment.
-   🔑 **Secure Authentication**: Built-in JWT token authentication for API security.
-   🔄 **API Gateway**: One-click deployment with secure token authentication for API-based workflows.
-   🌐 **Scalable Architecture**: Designed for mass-scale production and optimized server performance.
-   ☁️ **Cloud Deployment**: Ready-to-deploy configurations for major cloud platforms.

🎯 **Additional Features**

-   🕶️ **Stealth Mode**: Avoid bot detection by mimicking real users.
-   🏷️ **Tag-Based Content Extraction**: Refine crawling based on custom tags, headers, or metadata.
-   🔗 **Link Analysis**: Extract and analyze all links for detailed data exploration.
-   🛡️ **Error Handling**: Robust error management for seamless execution.
-   🔐 **CORS & Static Serving**: Supports filesystem-based caching and cross-origin requests.
-   📖 **Clear Documentation**: Simplified and updated guides for onboarding and advanced usage.
-   🙌 **Community Recognition**: Acknowledges contributors and pull requests for transparency.

Try it Now!
-----------

✨ Play around with this

✨ Visit our Documentation Website

Installation 🛠️
----------------

Crawl4AI offers flexible installation options to suit various use cases. You can install it as a Python package or use Docker.

🐍 **Using pip**

Choose the installation option that best fits your needs:

### Basic Installation

For basic web crawling and scraping tasks:

pip install crawl4ai
crawl4ai-setup # Setup the browser

By default, this will install the asynchronous version of Crawl4AI, using Playwright for web crawling.

👉 **Note**: When you install Crawl4AI, the `crawl4ai-setup` should automatically install and set up Playwright. However, if you encounter any Playwright-related errors, you can manually install it using one of these methods:

1.  Through the command line:
    
    playwright install
    
2.  If the above doesn't work, try this more specific command:
    
    python -m playwright install chromium
    

This second method has proven to be more reliable in some cases.

* * *

### Installation with Synchronous Version

The sync version is deprecated and will be removed in future versions. If you need the synchronous version using Selenium:

pip install crawl4ai\[sync\]

* * *

### Development Installation

For contributors who plan to modify the source code:

git clone https://github.com/unclecode/crawl4ai.git
cd crawl4ai
pip install -e .                    # Basic installation in editable mode

Install optional features:

pip install -e ".\[torch\]"           # With PyTorch features
pip install -e ".\[transformer\]"     # With Transformer features
pip install -e ".\[cosine\]"          # With cosine similarity features
pip install -e ".\[sync\]"            # With synchronous crawling (Selenium)
pip install -e ".\[all\]"             # Install all optional features

🐳 **Docker Deployment**

> 🚀 **Now Available!** Our completely redesigned Docker implementation is here! This new solution makes deployment more efficient and seamless than ever.

### New Docker Features

The new Docker implementation includes:

-   **Real-time Monitoring Dashboard** with live system metrics and browser pool visibility
-   **Browser pooling** with page pre-warming for faster response times
-   **Interactive playground** to test and generate request code
-   **MCP integration** for direct connection to AI tools like Claude Code
-   **Comprehensive API endpoints** including HTML extraction, screenshots, PDF generation, and JavaScript execution
-   **Multi-architecture support** with automatic detection (AMD64/ARM64)
-   **Optimized resources** with improved memory management

### Getting Started

# Pull and run the latest release
docker pull unclecode/crawl4ai:latest
docker run -d -p 11235:11235 --name crawl4ai --shm-size=1g unclecode/crawl4ai:latest

# Visit the monitoring dashboard at http://localhost:11235/dashboard
# Or the playground at http://localhost:11235/playground

### Quick Test

Run a quick test (works for both Docker options):

import requests

\# Submit a crawl job
response \= requests.post(
    "http://localhost:11235/crawl",
    json\={"urls": \["https://example.com"\], "priority": 10}
)
if response.status\_code \== 200:
    print("Crawl job submitted successfully.")
    
if "results" in response.json():
    results \= response.json()\["results"\]
    print("Crawl job completed. Results:")
    for result in results:
        print(result)
else:
    task\_id \= response.json()\["task\_id"\]
    print(f"Crawl job submitted. Task ID:: {task\_id}")
    result \= requests.get(f"http://localhost:11235/task/{task\_id}")

For more examples, see our Docker Examples. For advanced configuration, monitoring features, and production deployment, see our Self-Hosting Guide.

* * *

🔬 Advanced Usage Examples 🔬
-----------------------------

You can check the project structure in the directory docs/examples. Over there, you can find a variety of examples; here, some popular examples are shared.

📝 **Heuristic Markdown Generation with Clean and Fit Markdown**

import asyncio
from crawl4ai import AsyncWebCrawler, BrowserConfig, CrawlerRunConfig, CacheMode
from crawl4ai.content\_filter\_strategy import PruningContentFilter, BM25ContentFilter
from crawl4ai.markdown\_generation\_strategy import DefaultMarkdownGenerator

async def main():
    browser\_config \= BrowserConfig(
        headless\=True,  
        verbose\=True,
    )
    run\_config \= CrawlerRunConfig(
        cache\_mode\=CacheMode.ENABLED,
        markdown\_generator\=DefaultMarkdownGenerator(
            content\_filter\=PruningContentFilter(threshold\=0.48, threshold\_type\="fixed", min\_word\_threshold\=0)
        ),
        \# markdown\_generator=DefaultMarkdownGenerator(
        \#     content\_filter=BM25ContentFilter(user\_query="WHEN\_WE\_FOCUS\_BASED\_ON\_A\_USER\_QUERY", bm25\_threshold=1.0)
        \# ),
    )
    
    async with AsyncWebCrawler(config\=browser\_config) as crawler:
        result \= await crawler.arun(
            url\="https://docs.micronaut.io/4.9.9/guide/",
            config\=run\_config
        )
        print(len(result.markdown.raw\_markdown))
        print(len(result.markdown.fit\_markdown))

if \_\_name\_\_ \== "\_\_main\_\_":
    asyncio.run(main())

🖥️ **Executing JavaScript & Extract Structured Data without LLMs**

import asyncio
from crawl4ai import AsyncWebCrawler, BrowserConfig, CrawlerRunConfig, CacheMode
from crawl4ai import JsonCssExtractionStrategy
import json

async def main():
    schema \= {
    "name": "KidoCode Courses",
    "baseSelector": "section.charge-methodology .w-tab-content > div",
    "fields": \[
        {
            "name": "section\_title",
            "selector": "h3.heading-50",
            "type": "text",
        },
        {
            "name": "section\_description",
            "selector": ".charge-content",
            "type": "text",
        },
        {
            "name": "course\_name",
            "selector": ".text-block-93",
            "type": "text",
        },
        {
            "name": "course\_description",
            "selector": ".course-content-text",
            "type": "text",
        },
        {
            "name": "course\_icon",
            "selector": ".image-92",
            "type": "attribute",
            "attribute": "src"
        }
    \]
}

    extraction\_strategy \= JsonCssExtractionStrategy(schema, verbose\=True)

    browser\_config \= BrowserConfig(
        headless\=False,
        verbose\=True
    )
    run\_config \= CrawlerRunConfig(
        extraction\_strategy\=extraction\_strategy,
        js\_code\=\["""(async () => {const tabs = document.querySelectorAll("section.charge-methodology .tabs-menu-3 > div");for(let tab of tabs) {tab.scrollIntoView();tab.click();await new Promise(r => setTimeout(r, 500));}})();"""\],
        cache\_mode\=CacheMode.BYPASS
    )
        
    async with AsyncWebCrawler(config\=browser\_config) as crawler:
        
        result \= await crawler.arun(
            url\="https://www.kidocode.com/degrees/technology",
            config\=run\_config
        )

        companies \= json.loads(result.extracted\_content)
        print(f"Successfully extracted {len(companies)} companies")
        print(json.dumps(companies\[0\], indent\=2))

if \_\_name\_\_ \== "\_\_main\_\_":
    asyncio.run(main())

📚 **Extracting Structured Data with LLMs**

import os
import asyncio
from crawl4ai import AsyncWebCrawler, BrowserConfig, CrawlerRunConfig, CacheMode, LLMConfig
from crawl4ai import LLMExtractionStrategy
from pydantic import BaseModel, Field

class OpenAIModelFee(BaseModel):
    model\_name: str \= Field(..., description\="Name of the OpenAI model.")
    input\_fee: str \= Field(..., description\="Fee for input token for the OpenAI model.")
    output\_fee: str \= Field(..., description\="Fee for output token for the OpenAI model.")

async def main():
    browser\_config \= BrowserConfig(verbose\=True)
    run\_config \= CrawlerRunConfig(
        word\_count\_threshold\=1,
        extraction\_strategy\=LLMExtractionStrategy(
            \# Here you can use any provider that Litellm library supports, for instance: ollama/qwen2
            \# provider="ollama/qwen2", api\_token="no-token", 
            llm\_config \= LLMConfig(provider\="openai/gpt-4o", api\_token\=os.getenv('OPENAI\_API\_KEY')), 
            schema\=OpenAIModelFee.schema(),
            extraction\_type\="schema",
            instruction\="""From the crawled content, extract all mentioned model names along with their fees for input and output tokens. 
            Do not miss any models in the entire content. One extracted model JSON format should look like this: 
            {"model\_name": "GPT-4", "input\_fee": "US$10.00 / 1M tokens", "output\_fee": "US$30.00 / 1M tokens"}."""
        ),            
        cache\_mode\=CacheMode.BYPASS,
    )
    
    async with AsyncWebCrawler(config\=browser\_config) as crawler:
        result \= await crawler.arun(
            url\='https://openai.com/api/pricing/',
            config\=run\_config
        )
        print(result.extracted\_content)

if \_\_name\_\_ \== "\_\_main\_\_":
    asyncio.run(main())

🤖 **Using Your own Browser with Custom User Profile**

import os, sys
from pathlib import Path
import asyncio, time
from crawl4ai import AsyncWebCrawler, BrowserConfig, CrawlerRunConfig, CacheMode

async def test\_news\_crawl():
    \# Create a persistent user data directory
    user\_data\_dir \= os.path.join(Path.home(), ".crawl4ai", "browser\_profile")
    os.makedirs(user\_data\_dir, exist\_ok\=True)

    browser\_config \= BrowserConfig(
        verbose\=True,
        headless\=True,
        user\_data\_dir\=user\_data\_dir,
        use\_persistent\_context\=True,
    )
    run\_config \= CrawlerRunConfig(
        cache\_mode\=CacheMode.BYPASS
    )
    
    async with AsyncWebCrawler(config\=browser\_config) as crawler:
        url \= "ADDRESS\_OF\_A\_CHALLENGING\_WEBSITE"
        
        result \= await crawler.arun(
            url,
            config\=run\_config,
            magic\=True,
        )
        
        print(f"Successfully crawled {url}")
        print(f"Content length: {len(result.markdown)}")

* * *

> **💡 Tip:** Some websites may use **CAPTCHA** based verification mechanisms to prevent automated access. If your workflow encounters such challenges, you may optionally integrate a third-party CAPTCHA-handling service such as **CapSolver**. They support reCAPTCHA v2/v3, Cloudflare Turnstile, Challenge, AWS WAF, and more. Please ensure that your usage complies with the target website’s terms of service and applicable laws.

✨ Recent Updates
----------------

**Version 0.7.7 Release Highlights - The Self-Hosting & Monitoring Update**

-   **📊 Real-time Monitoring Dashboard**: Interactive web UI with live system metrics and browser pool visibility
    
    \# Access the monitoring dashboard
    \# Visit: http://localhost:11235/dashboard
    
    \# Real-time metrics include:
    \# - System health (CPU, memory, network, uptime)
    \# - Active and completed request tracking
    \# - Browser pool management (permanent/hot/cold)
    \# - Janitor cleanup events
    \# - Error monitoring with full context
    
-   **🔌 Comprehensive Monitor API**: Complete REST API for programmatic access to all monitoring data
    
    import httpx
    
    async with httpx.AsyncClient() as client:
        \# System health
        health \= await client.get("http://localhost:11235/monitor/health")
    
        \# Request tracking
        requests \= await client.get("http://localhost:11235/monitor/requests")
    
        \# Browser pool status
        browsers \= await client.get("http://localhost:11235/monitor/browsers")
    
        \# Endpoint statistics
        stats \= await client.get("http://localhost:11235/monitor/endpoints/stats")
    
-   **⚡ WebSocket Streaming**: Real-time updates every 2 seconds for custom dashboards
    
-   **🔥 Smart Browser Pool**: 3-tier architecture (permanent/hot/cold) with automatic promotion and cleanup
    
-   **🧹 Janitor System**: Automatic resource management with event logging
    
-   **🎮 Control Actions**: Manual browser management (kill, restart, cleanup) via API
    
-   **📈 Production Metrics**: 6 critical metrics for operational excellence with Prometheus integration
    
-   **🐛 Critical Bug Fixes**:
    
    -   Fixed async LLM extraction blocking issue (#1055)
    -   Enhanced DFS deep crawl strategy (#1607)
    -   Fixed sitemap parsing in AsyncUrlSeeder (#1598)
    -   Resolved browser viewport configuration (#1495)
    -   Fixed CDP timing with exponential backoff (#1528)
    -   Security update for pyOpenSSL (>=25.3.0)

Full v0.7.7 Release Notes →

**Version 0.7.5 Release Highlights - The Docker Hooks & Security Update**

-   **🔧 Docker Hooks System**: Complete pipeline customization with user-provided Python functions at 8 key points
    
-   **✨ Function-Based Hooks API (NEW)**: Write hooks as regular Python functions with full IDE support:
    
    from crawl4ai import hooks\_to\_string
    from crawl4ai.docker\_client import Crawl4aiDockerClient
    
    \# Define hooks as regular Python functions
    async def on\_page\_context\_created(page, context, \*\*kwargs):
        """Block images to speed up crawling"""
        await context.route("\*\*/\*.{png,jpg,jpeg,gif,webp}", lambda route: route.abort())
        await page.set\_viewport\_size({"width": 1920, "height": 1080})
        return page
    
    async def before\_goto(page, context, url, \*\*kwargs):
        """Add custom headers"""
        await page.set\_extra\_http\_headers({'X-Crawl4AI': 'v0.7.5'})
        return page
    
    \# Option 1: Use hooks\_to\_string() utility for REST API
    hooks\_code \= hooks\_to\_string({
        "on\_page\_context\_created": on\_page\_context\_created,
        "before\_goto": before\_goto
    })
    
    \# Option 2: Docker client with automatic conversion (Recommended)
    client \= Crawl4aiDockerClient(base\_url\="http://localhost:11235")
    results \= await client.crawl(
        urls\=\["https://httpbin.org/html"\],
        hooks\={
            "on\_page\_context\_created": on\_page\_context\_created,
            "before\_goto": before\_goto
        }
    )
    \# ✓ Full IDE support, type checking, and reusability!
    
-   **🤖 Enhanced LLM Integration**: Custom providers with temperature control and base\_url configuration
    
-   **🔒 HTTPS Preservation**: Secure internal link handling with `preserve_https_for_internal_links=True`
    
-   **🐍 Python 3.10+ Support**: Modern language features and enhanced performance
    
-   **🛠️ Bug Fixes**: Resolved multiple community-reported issues including URL processing, JWT authentication, and proxy configuration
    

Full v0.7.5 Release Notes →

**Version 0.7.4 Release Highlights - The Intelligent Table Extraction & Performance Update**

-   **🚀 LLMTableExtraction**: Revolutionary table extraction with intelligent chunking for massive tables:
    
    from crawl4ai import LLMTableExtraction, LLMConfig
    
    \# Configure intelligent table extraction
    table\_strategy \= LLMTableExtraction(
        llm\_config\=LLMConfig(provider\="openai/gpt-4.1-mini"),
        enable\_chunking\=True,           \# Handle massive tables
        chunk\_token\_threshold\=5000,     \# Smart chunking threshold
        overlap\_threshold\=100,          \# Maintain context between chunks
        extraction\_type\="structured"    \# Get structured data output
    )
    
    config \= CrawlerRunConfig(table\_extraction\_strategy\=table\_strategy)
    result \= await crawler.arun("https://complex-tables-site.com", config\=config)
    
    \# Tables are automatically chunked, processed, and merged
    for table in result.tables:
        print(f"Extracted table: {len(table\['data'\])} rows")
    
-   **⚡ Dispatcher Bug Fix**: Fixed sequential processing bottleneck in arun\_many for fast-completing tasks
    
-   **🧹 Memory Management Refactor**: Consolidated memory utilities into main utils module for cleaner architecture
    
-   **🔧 Browser Manager Fixes**: Resolved race conditions in concurrent page creation with thread-safe locking
    
-   **🔗 Advanced URL Processing**: Better handling of raw:// URLs and base tag link resolution
    
-   **🛡️ Enhanced Proxy Support**: Flexible proxy configuration supporting both dict and string formats
    

Full v0.7.4 Release Notes →

**Version 0.7.3 Release Highlights - The Multi-Config Intelligence Update**

-   **🕵️ Undetected Browser Support**: Bypass sophisticated bot detection systems:
    
    from crawl4ai import AsyncWebCrawler, BrowserConfig
    
    browser\_config \= BrowserConfig(
        browser\_type\="undetected",  \# Use undetected Chrome
        headless\=True,              \# Can run headless with stealth
        extra\_args\=\[
            "--disable-blink-features=AutomationControlled",
            "--disable-web-security"
        \]
    )
    
    async with AsyncWebCrawler(config\=browser\_config) as crawler:
        result \= await crawler.arun("https://protected-site.com")
    \# Successfully bypass Cloudflare, Akamai, and custom bot detection
    
-   **🎨 Multi-URL Configuration**: Different strategies for different URL patterns in one batch:
    
    from crawl4ai import CrawlerRunConfig, MatchMode
    
    configs \= \[
        \# Documentation sites - aggressive caching
        CrawlerRunConfig(
            url\_matcher\=\["\*docs\*", "\*documentation\*"\],
            cache\_mode\="write",
            markdown\_generator\_options\={"include\_links": True}
        ),
        
        \# News/blog sites - fresh content
        CrawlerRunConfig(
            url\_matcher\=lambda url: 'blog' in url or 'news' in url,
            cache\_mode\="bypass"
        ),
        
        \# Fallback for everything else
        CrawlerRunConfig()
    \]
    
    results \= await crawler.arun\_many(urls, config\=configs)
    \# Each URL gets the perfect configuration automatically
    
-   **🧠 Memory Monitoring**: Track and optimize memory usage during crawling:
    
    from crawl4ai.memory\_utils import MemoryMonitor
    
    monitor \= MemoryMonitor()
    monitor.start\_monitoring()
    
    results \= await crawler.arun\_many(large\_url\_list)
    
    report \= monitor.get\_report()
    print(f"Peak memory: {report\['peak\_mb'\]:.1f} MB")
    print(f"Efficiency: {report\['efficiency'\]:.1f}%")
    \# Get optimization recommendations
    
-   **📊 Enhanced Table Extraction**: Direct DataFrame conversion from web tables:
    
    result \= await crawler.arun("https://site-with-tables.com")
    
    \# New way - direct table access
    if result.tables:
        import pandas as pd
        for table in result.tables:
            df \= pd.DataFrame(table\['data'\])
            print(f"Table: {df.shape\[0\]} rows × {df.shape\[1\]} columns")
    
-   **💰 GitHub Sponsors**: 4-tier sponsorship system for project sustainability
    
-   **🐳 Docker LLM Flexibility**: Configure providers via environment variables
    

Full v0.7.3 Release Notes →

**Version 0.7.0 Release Highlights - The Adaptive Intelligence Update**

-   **🧠 Adaptive Crawling**: Your crawler now learns and adapts to website patterns automatically:
    
    config \= AdaptiveConfig(
        confidence\_threshold\=0.7, \# Min confidence to stop crawling
        max\_depth\=5, \# Maximum crawl depth
        max\_pages\=20, \# Maximum number of pages to crawl
        strategy\="statistical"
    )
    
    async with AsyncWebCrawler() as crawler:
        adaptive\_crawler \= AdaptiveCrawler(crawler, config)
        state \= await adaptive\_crawler.digest(
            start\_url\="https://news.example.com",
            query\="latest news content"
        )
    \# Crawler learns patterns and improves extraction over time
    
-   **🌊 Virtual Scroll Support**: Complete content extraction from infinite scroll pages:
    
    scroll\_config \= VirtualScrollConfig(
        container\_selector\="\[data-testid='feed'\]",
        scroll\_count\=20,
        scroll\_by\="container\_height",
        wait\_after\_scroll\=1.0
    )
    
    result \= await crawler.arun(url, config\=CrawlerRunConfig(
        virtual\_scroll\_config\=scroll\_config
    ))
    
-   **🔗 Intelligent Link Analysis**: 3-layer scoring system for smart link prioritization:
    
    link\_config \= LinkPreviewConfig(
        query\="machine learning tutorials",
        score\_threshold\=0.3,
        concurrent\_requests\=10
    )
    
    result \= await crawler.arun(url, config\=CrawlerRunConfig(
        link\_preview\_config\=link\_config,
        score\_links\=True
    ))
    \# Links ranked by relevance and quality
    
-   **🎣 Async URL Seeder**: Discover thousands of URLs in seconds:
    
    seeder \= AsyncUrlSeeder(SeedingConfig(
        source\="sitemap+cc",
        pattern\="\*/blog/\*",
        query\="python tutorials",
        score\_threshold\=0.4
    ))
    
    urls \= await seeder.discover("https://example.com")
    
-   **⚡ Performance Boost**: Up to 3x faster with optimized resource handling and memory efficiency
    

Read the full details in our 0.7.0 Release Notes or check the CHANGELOG.

Version Numbering in Crawl4AI
-----------------------------

Crawl4AI follows standard Python version numbering conventions (PEP 440) to help users understand the stability and features of each release.

📈 **Version Numbers Explained**

Our version numbers follow this pattern: `MAJOR.MINOR.PATCH` (e.g., 0.4.3)

#### Pre-release Versions

We use different suffixes to indicate development stages:

-   `dev` (0.4.3dev1): Development versions, unstable
-   `a` (0.4.3a1): Alpha releases, experimental features
-   `b` (0.4.3b1): Beta releases, feature complete but needs testing
-   `rc` (0.4.3): Release candidates, potential final version

#### Installation

-   Regular installation (stable version):
    
    pip install -U crawl4ai
    
-   Install pre-release versions:
    
    pip install crawl4ai --pre
    
-   Install specific version:
    
    pip install crawl4ai==0.4.3b1
    

#### Why Pre-releases?

We use pre-releases to:

-   Test new features in real-world scenarios
-   Gather feedback before final releases
-   Ensure stability for production users
-   Allow early adopters to try new features

For production environments, we recommend using the stable version. For testing new features, you can opt-in to pre-releases using the `--pre` flag.

📖 Documentation & Roadmap
--------------------------

> 🚨 **Documentation Update Alert**: We're undertaking a major documentation overhaul next week to reflect recent updates and improvements. Stay tuned for a more comprehensive and up-to-date guide!

For current documentation, including installation instructions, advanced features, and API reference, visit our Documentation Website.

To check our development plans and upcoming features, visit our Roadmap.

📈 **Development TODOs**

-   0\. Graph Crawler: Smart website traversal using graph search algorithms for comprehensive nested page extraction
-   1\. Question-Based Crawler: Natural language driven web discovery and content extraction
-   2\. Knowledge-Optimal Crawler: Smart crawling that maximizes knowledge while minimizing data extraction
-   3\. Agentic Crawler: Autonomous system for complex multi-step crawling operations
-   4\. Automated Schema Generator: Convert natural language to extraction schemas
-   5\. Domain-Specific Scrapers: Pre-configured extractors for common platforms (academic, e-commerce)
-   6\. Web Embedding Index: Semantic search infrastructure for crawled content
-   7\. Interactive Playground: Web UI for testing, comparing strategies with AI assistance
-   8\. Performance Monitor: Real-time insights into crawler operations
-   9\. Cloud Integration: One-click deployment solutions across cloud providers
-   10\. Sponsorship Program: Structured support system with tiered benefits
-   11\. Educational Content: "How to Crawl" video series and interactive tutorials

🤝 Contributing
---------------

We welcome contributions from the open-source community. Check out our contribution guidelines for more information.

I'll help modify the license section with badges. For the halftone effect, here's a version with it:

Here's the updated license section:

📄 License & Attribution
------------------------

This project is licensed under the Apache License 2.0, attribution is recommended via the badges below. See the Apache 2.0 License file for details.

### Attribution Requirements

When using Crawl4AI, you must include one of the following attribution methods:

📈 **1\. Badge Attribution (Recommended)** Add one of these badges to your README, documentation, or website:

Theme

Badge

**Disco Theme (Animated)**

**Night Theme (Dark with Neon)**

**Dark Theme (Classic)**

**Light Theme (Classic)**

HTML code for adding the badges:

<!-- Disco Theme (Animated) -->
<a href\="https://github.com/unclecode/crawl4ai"\>
  <img src\="https://raw.githubusercontent.com/unclecode/crawl4ai/main/docs/assets/powered-by-disco.svg" alt\="Powered by Crawl4AI" width\="200"/>
</a\>

<!-- Night Theme (Dark with Neon) -->
<a href\="https://github.com/unclecode/crawl4ai"\>
  <img src\="https://raw.githubusercontent.com/unclecode/crawl4ai/main/docs/assets/powered-by-night.svg" alt\="Powered by Crawl4AI" width\="200"/>
</a\>

<!-- Dark Theme (Classic) -->
<a href\="https://github.com/unclecode/crawl4ai"\>
  <img src\="https://raw.githubusercontent.com/unclecode/crawl4ai/main/docs/assets/powered-by-dark.svg" alt\="Powered by Crawl4AI" width\="200"/>
</a\>

<!-- Light Theme (Classic) -->
<a href\="https://github.com/unclecode/crawl4ai"\>
  <img src\="https://raw.githubusercontent.com/unclecode/crawl4ai/main/docs/assets/powered-by-light.svg" alt\="Powered by Crawl4AI" width\="200"/>
</a\>

<!-- Simple Shield Badge -->
<a href\="https://github.com/unclecode/crawl4ai"\>
  <img src\="https://img.shields.io/badge/Powered%20by-Crawl4AI-blue?style=flat-square" alt\="Powered by Crawl4AI"/>
</a\>

📖 **2\. Text Attribution** Add this line to your documentation: \`\`\` This project uses Crawl4AI (https://github.com/unclecode/crawl4ai) for web data extraction. \`\`\`

📚 Citation
-----------

If you use Crawl4AI in your research or project, please cite:

@software{crawl4ai2024,
  author = {UncleCode},
  title = {Crawl4AI: Open-source LLM Friendly Web Crawler & Scraper},
  year = {2024},
  publisher = {GitHub},
  journal = {GitHub Repository},
  howpublished = {\\url{https://github.com/unclecode/crawl4ai}},
  commit = {Please use the commit hash you're working with}
}

Text citation format:

```
UncleCode. (2024). Crawl4AI: Open-source LLM Friendly Web Crawler & Scraper [Computer software]. 
GitHub. https://github.com/unclecode/crawl4ai
```

📧 Contact
----------

For questions, suggestions, or feedback, feel free to reach out:

-   GitHub: unclecode
-   Twitter: @unclecode
-   Website: crawl4ai.com

Happy Crawling! 🕸️🚀

🗾 Mission
----------

Our mission is to unlock the value of personal and enterprise data by transforming digital footprints into structured, tradeable assets. Crawl4AI empowers individuals and organizations with open-source tools to extract and structure data, fostering a shared data economy.

We envision a future where AI is powered by real human knowledge, ensuring data creators directly benefit from their contributions. By democratizing data and enabling ethical sharing, we are laying the foundation for authentic AI advancement.

🔑 **Key Opportunities**

-   **Data Capitalization**: Transform digital footprints into measurable, valuable assets.
-   **Authentic AI Data**: Provide AI systems with real human insights.
-   **Shared Economy**: Create a fair data marketplace that benefits data creators.

🚀 **Development Pathway**

1.  **Open-Source Tools**: Community-driven platforms for transparent data extraction.
2.  **Digital Asset Structuring**: Tools to organize and value digital knowledge.
3.  **Ethical Data Marketplace**: A secure, fair platform for exchanging structured data.

For more details, see our full mission statement.

🌟 Current Sponsors
-------------------

### 🏢 Enterprise Sponsors & Partners

Our enterprise sponsors and technology partners help scale Crawl4AI to power production-grade data pipelines.

Company

About

Sponsorship Tier

Scrapeless provides production-grade infrastructure for Crawling, Automation, and AI Agents, offering Scraping Browser, 4 Proxy Types and Universal Scraping API.

🥈 Silver

AI-powered Captcha solving service. Supports all major Captcha types, including reCAPTCHA, Cloudflare, and more

🥉 Bronze

Helps engineers and buyers find, compare, and source electronic & industrial parts in seconds, with specs, pricing, lead times & alternatives.

🥇 Gold

KidoCode

Kidocode is a hybrid technology and entrepreneurship school for kids aged 5–18, offering both online and on-campus education.

🥇 Gold

Singapore-based Aleph Null is Asia’s leading edtech hub, dedicated to student-centric, AI-driven education—empowering learners with the tools to thrive in a fast-changing world.

🥇 Gold

### 🧑‍🤝 Individual Sponsors

A heartfelt thanks to our individual supporters! Every contribution helps us keep our opensource mission alive and thriving!

> Want to join them? Sponsor Crawl4AI →

Star History
------------
