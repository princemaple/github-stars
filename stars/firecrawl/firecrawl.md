---
project: firecrawl
stars: 84495
description: 🔥 The Web Data API for AI - Turn entire websites into LLM-ready markdown or structured data
url: https://github.com/firecrawl/firecrawl
---

### 

* * *

**🔥 Firecrawl**
================

**Turn websites into LLM-ready data.**

**Firecrawl** is an API that scrapes, crawls, and extracts structured data from any website, powering AI agents and apps with real-time context from the web.

Looking for our MCP? Check out the repo here.

_This repository is in development, and we're still integrating custom modules into the mono repo. It's not fully ready for self-hosted deployment yet, but you can run it locally._

_Pst. Hey, you, join our stargazers :)_

* * *

Why Firecrawl?
--------------

-   **LLM-ready output**: Clean markdown, structured JSON, screenshots, HTML, and more
-   **Industry-leading reliability**: >80% coverage on benchmark evaluations, outperforming every other provider tested
-   **Handles the hard stuff**: Proxies, JavaScript rendering, and dynamic content that breaks other scrapers
-   **Customization**: Exclude tags, crawl behind auth walls, max depth, and more
-   **Media parsing**: Automatic text extraction from PDFs, DOCX, and images
-   **Actions**: Click, scroll, input, wait, and more before extracting
-   **Batch processing**: Scrape thousands of URLs asynchronously
-   **Change tracking**: Monitor website content changes over time

* * *

Quick Start
-----------

Sign up at firecrawl.dev to get your API key and start extracting data in seconds. Try the playground to test it out.

### Make Your First API Request

curl -X POST 'https://api.firecrawl.dev/v2/scrape' \\
  -H 'Authorization: Bearer fc-YOUR\_API\_KEY' \\
  -H 'Content-Type: application/json' \\
  -d '{"url": "https://example.com"}'

Response:

{
  "success": true,
  "data": {
    "markdown": "\# Example Domain\\n\\nThis domain is for use in illustrative examples...",
    "metadata": {
      "title": "Example Domain",
      "sourceURL": "https://example.com"
    }
  }
}

* * *

Feature Overview
----------------

Feature

Description

**Scrape**

Convert any URL to markdown, HTML, screenshots, or structured JSON

**Search**

Search the web and get full page content from results

**Agent**

Automated data gathering, just describe what you need

**Crawl**

Scrape all URLs of a website with a single request

**Map**

Discover all URLs on a website instantly

* * *

Scrape
------

Convert any URL to clean markdown, HTML, or structured data.

curl -X POST 'https://api.firecrawl.dev/v2/scrape' \\
  -H 'Authorization: Bearer fc-YOUR\_API\_KEY' \\
  -H 'Content-Type: application/json' \\
  -d '{
    "url": "https://docs.firecrawl.dev",
    "formats": \["markdown", "html"\]
  }'

Response:

{
  "success": true,
  "data": {
    "markdown": "\# Firecrawl Docs\\n\\nTurn websites into LLM-ready data...",
    "html": "<!DOCTYPE html><html>...",
    "metadata": {
      "title": "Quickstart | Firecrawl",
      "description": "Firecrawl allows you to turn entire websites into LLM-ready markdown",
      "sourceURL": "https://docs.firecrawl.dev",
      "statusCode": 200
    }
  }
}

### Extract Structured Data (JSON Mode)

Extract structured data using a schema:

from firecrawl import Firecrawl
from pydantic import BaseModel

app \= Firecrawl(api\_key\="fc-YOUR\_API\_KEY")

class CompanyInfo(BaseModel):
    company\_mission: str
    is\_open\_source: bool
    is\_in\_yc: bool

result \= app.scrape(
    'https://firecrawl.dev',
    formats\=\[{"type": "json", "schema": CompanyInfo.model\_json\_schema()}\]
)

print(result.json)

{"company\_mission": "Turn websites into LLM-ready data", "is\_open\_source": true, "is\_in\_yc": true}

Or extract with just a prompt (no schema):

result \= app.scrape(
    'https://firecrawl.dev',
    formats\=\[{"type": "json", "prompt": "Extract the company mission"}\]
)

### Scrape Formats

Available formats: `markdown`, `html`, `rawHtml`, `screenshot`, `links`, `json`, `branding`

**Get a screenshot**

doc \= app.scrape("https://firecrawl.dev", formats\=\["screenshot"\])
print(doc.screenshot)  \# Base64 encoded image

**Extract brand identity (colors, fonts, typography)**

doc \= app.scrape("https://firecrawl.dev", formats\=\["branding"\])
print(doc.branding)  \# {"colors": {...}, "fonts": \[...\], "typography": {...}}

### Actions (Interact Before Scraping)

Click, type, scroll, and more before extracting:

doc \= app.scrape(
    url\="https://example.com/login",
    formats\=\["markdown"\],
    actions\=\[
        {"type": "write", "text": "user@example.com"},
        {"type": "press", "key": "Tab"},
        {"type": "write", "text": "password"},
        {"type": "click", "selector": 'button\[type="submit"\]'},
        {"type": "wait", "milliseconds": 2000},
        {"type": "screenshot"}
    \]
)

* * *

Search
------

Search the web and optionally scrape the results.

curl -X POST 'https://api.firecrawl.dev/v2/search' \\
  -H 'Authorization: Bearer fc-YOUR\_API\_KEY' \\
  -H 'Content-Type: application/json' \\
  -d '{
    "query": "firecrawl web scraping",
    "limit": 5
  }'

Response:

{
  "success": true,
  "data": {
    "web": \[
      {
        "url": "https://www.firecrawl.dev/",
        "title": "Firecrawl - The Web Data API for AI",
        "description": "The web crawling, scraping, and search API for AI.",
        "position": 1
      }
    \],
    "images": \[...\],
    "news": \[...\]
  }
}

### Search with Content Scraping

Get the full content of search results:

from firecrawl import Firecrawl

firecrawl \= Firecrawl(api\_key\="fc-YOUR\_API\_KEY")

results \= firecrawl.search(
    "firecrawl web scraping",
    limit\=3,
    scrape\_options\={
        "formats": \["markdown", "links"\]
    }
)

* * *

Agent
-----

**The easiest way to get data from the web.** Describe what you need, and our AI agent searches, navigates, and extracts it. No URLs required.

Agent is the evolution of our `/extract` endpoint: faster, more reliable, and doesn't require you to know the URLs upfront.

curl -X POST 'https://api.firecrawl.dev/v2/agent' \\
  -H 'Authorization: Bearer fc-YOUR\_API\_KEY' \\
  -H 'Content-Type: application/json' \\
  -d '{
    "prompt": "Find the pricing plans for Notion"
  }'

Response:

{
  "success": true,
  "data": {
    "result": "Notion offers the following pricing plans:\\n\\n1\. Free - $0/month...\\n2\. Plus - $10/seat/month...\\n3\. Business - $18/seat/month...",
    "sources": \["https://www.notion.so/pricing"\]
  }
}

### Agent with Structured Output

Use a schema to get structured data:

from firecrawl import Firecrawl
from pydantic import BaseModel, Field
from typing import List, Optional

app \= Firecrawl(api\_key\="fc-YOUR\_API\_KEY")

class Founder(BaseModel):
    name: str \= Field(description\="Full name of the founder")
    role: Optional\[str\] \= Field(None, description\="Role or position")

class FoundersSchema(BaseModel):
    founders: List\[Founder\] \= Field(description\="List of founders")

result \= app.agent(
    prompt\="Find the founders of Firecrawl",
    schema\=FoundersSchema
)

print(result.data)

{
  "founders": \[
    {"name": "Eric Ciarla", "role": "Co-founder"},
    {"name": "Nicolas Camara", "role": "Co-founder"},
    {"name": "Caleb Peffer", "role": "Co-founder"}
  \]
}

### Agent with URLs (Optional)

Focus the agent on specific pages:

result \= app.agent(
    urls\=\["https://docs.firecrawl.dev", "https://firecrawl.dev/pricing"\],
    prompt\="Compare the features and pricing information"
)

### Model Selection

Choose between two models based on your needs:

Model

Cost

Best For

`spark-1-mini` (default)

60% cheaper

Most tasks

`spark-1-pro`

Standard

Complex research, critical extraction

result \= app.agent(
    prompt\="Compare enterprise features across Firecrawl, Apify, and ScrapingBee",
    model\="spark-1-pro"
)

**When to use Pro:**

-   Comparing data across multiple websites
-   Extracting from sites with complex navigation or auth
-   Research tasks where the agent needs to explore multiple paths
-   Critical data where accuracy is paramount

Learn more about Spark models in our Agent documentation.

### Using Firecrawl with AI agents

Install the Firecrawl skill to let AI agents like Claude Code, Codex, and OpenCode use Firecrawl automatically:

npx skills add firecrawl/cli

Restart your agent after installing. See the Skill + CLI docs for full setup.

* * *

Crawling
--------

Crawl an entire website and get content from all pages.

curl -X POST 'https://api.firecrawl.dev/v2/crawl' \\
  -H 'Authorization: Bearer fc-YOUR\_API\_KEY' \\
  -H 'Content-Type: application/json' \\
  -d '{
    "url": "https://docs.firecrawl.dev",
    "limit": 100,
    "scrapeOptions": {
      "formats": \["markdown"\]
    }
  }'

Returns a job ID:

{
  "success": true,
  "id": "123-456-789",
  "url": "https://api.firecrawl.dev/v2/crawl/123-456-789"
}

### Check Crawl Status

curl -X GET 'https://api.firecrawl.dev/v2/crawl/123-456-789' \\
  -H 'Authorization: Bearer fc-YOUR\_API\_KEY'

{
  "status": "completed",
  "total": 50,
  "completed": 50,
  "creditsUsed": 50,
  "data": \[
    {
      "markdown": "\# Page Title\\n\\nContent...",
      "metadata": {"title": "Page Title", "sourceURL": "https://..."}
    }
  \]
}

**Note:** The SDKs handle polling automatically for a better developer experience.

* * *

Map
---

Discover all URLs on a website instantly.

curl -X POST 'https://api.firecrawl.dev/v2/map' \\
  -H 'Authorization: Bearer fc-YOUR\_API\_KEY' \\
  -H 'Content-Type: application/json' \\
  -d '{"url": "https://firecrawl.dev"}'

Response:

{
  "success": true,
  "links": \[
    {"url": "https://firecrawl.dev", "title": "Firecrawl", "description": "Turn websites into LLM-ready data"},
    {"url": "https://firecrawl.dev/pricing", "title": "Pricing", "description": "Firecrawl pricing plans"},
    {"url": "https://firecrawl.dev/blog", "title": "Blog", "description": "Firecrawl blog"}
  \]
}

### Map with Search

Find specific URLs within a site:

from firecrawl import Firecrawl

app \= Firecrawl(api\_key\="fc-YOUR\_API\_KEY")

result \= app.map("https://firecrawl.dev", search\="pricing")
\# Returns URLs ordered by relevance to "pricing"

* * *

Batch Scraping
--------------

Scrape multiple URLs at once:

from firecrawl import Firecrawl

app \= Firecrawl(api\_key\="fc-YOUR\_API\_KEY")

job \= app.batch\_scrape(\[
    "https://firecrawl.dev",
    "https://docs.firecrawl.dev",
    "https://firecrawl.dev/pricing"
\], formats\=\["markdown"\])

for doc in job.data:
    print(doc.metadata.source\_url)

* * *

SDKs
----

Our SDKs provide a convenient way to interact with all Firecrawl features and automatically handle polling for async operations like crawling and batch scraping.

### Python

Install the SDK:

pip install firecrawl-py

from firecrawl import Firecrawl

app \= Firecrawl(api\_key\="fc-YOUR\_API\_KEY")

\# Scrape a single URL
doc \= app.scrape("https://firecrawl.dev", formats\=\["markdown"\])
print(doc.markdown)

\# Use the Agent for autonomous data gathering
result \= app.agent(prompt\="Find the founders of Stripe")
print(result.data)

\# Crawl a website (automatically waits for completion)
docs \= app.crawl("https://docs.firecrawl.dev", limit\=50)
for doc in docs.data:
    print(doc.metadata.source\_url, doc.markdown\[:100\])

\# Search the web
results \= app.search("best web scraping tools 2024", limit\=10)
print(results)

### Node.js

Install the SDK:

npm install @mendable/firecrawl-js

import Firecrawl from '@mendable/firecrawl-js';

const app \= new Firecrawl({ apiKey: 'fc-YOUR\_API\_KEY' });

// Scrape a single URL
const doc \= await app.scrape('https://firecrawl.dev', { formats: \['markdown'\] });
console.log(doc.markdown);

// Use the Agent for autonomous data gathering
const result \= await app.agent({ prompt: 'Find the founders of Stripe' });
console.log(result.data);

// Crawl a website (automatically waits for completion)
const docs \= await app.crawl('https://docs.firecrawl.dev', { limit: 50 });
docs.data.forEach(doc \=> {
    console.log(doc.metadata.sourceURL, doc.markdown.substring(0, 100));
});

// Search the web
const results \= await app.search('best web scraping tools 2024', { limit: 10 });
results.data.web.forEach(result \=> {
    console.log(\`${result.title}: ${result.url}\`);
});

### Community SDKs

-   Go SDK
-   Rust SDK

* * *

Integrations
------------

**Agents & AI Tools**

-   Firecrawl Skill
-   Firecrawl MCP

**Platforms**

-   Lovable
-   Zapier
-   n8n

View all integrations →

**Missing your favorite tool?** Open an issue and let us know!

* * *

Resources
---------

-   Documentation
-   API Reference
-   Playground
-   Changelog

* * *

Open Source vs Cloud
--------------------

Firecrawl is open source under the AGPL-3.0 license. The cloud version at firecrawl.dev includes additional features:

To run locally, see the Contributing Guide. To self-host, see Self-Hosting Guide.

* * *

Contributing
------------

We love contributions! Please read our Contributing Guide before submitting a pull request.

### Contributors

* * *

License
-------

This project is primarily licensed under the GNU Affero General Public License v3.0 (AGPL-3.0). The SDKs and some UI components are licensed under the MIT License. See the LICENSE files in specific directories for details.

* * *

**It is the sole responsibility of end users to respect websites' policies when scraping.** Users are advised to adhere to applicable privacy policies and terms of use. By default, Firecrawl respects robots.txt directives. By using Firecrawl, you agree to comply with these conditions.

↑ Back to Top ↑
