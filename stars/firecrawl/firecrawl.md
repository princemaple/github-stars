---
project: firecrawl
stars: 68792
description: 🔥 The Web Data API for AI - Turn entire websites into LLM-ready markdown or structured data
url: https://github.com/firecrawl/firecrawl
---

### 

🔥 Firecrawl
============

Empower your AI apps with clean data from any website. Featuring advanced scraping, crawling, and data extraction capabilities.

_This repository is in development, and we’re still integrating custom modules into the mono repo. It's not fully ready for self-hosted deployment yet, but you can run it locally._

What is Firecrawl?
------------------

Firecrawl is an API service that takes a URL, crawls it, and converts it into clean markdown or structured data. We crawl all accessible subpages and give you clean data for each. No sitemap required. Check out our documentation.

Looking for our MCP? Check out the repo here.

_Pst. hey, you, join our stargazers :)_

How to use it?
--------------

We provide an easy to use API with our hosted version. You can find the playground and documentation here. You can also self host the backend if you'd like.

Check out the following resources to get started:

-   **API**: Documentation
-   **SDKs**: Python, Node
-   **LLM Frameworks**: Langchain (python), Langchain (js), Llama Index, Crew.ai, Composio, PraisonAI, Superinterface, Vectorize
-   **Low-code Frameworks**: Dify, Langflow, Flowise AI, Cargo, Pipedream
-   **Community SDKs**: Go, Rust
-   **Others**: Zapier, Pabbly Connect
-   Want an SDK or Integration? Let us know by opening an issue.

To run locally, refer to guide here.

### API Key

To use the API, you need to sign up on Firecrawl and get an API key.

### Features

-   **Scrape**: scrapes a URL and get its content in LLM-ready format (markdown, structured data via LLM Extract, screenshot, html)
-   **Crawl**: scrapes all the URLs of a web page and return content in LLM-ready format
-   **Map**: input a website and get all the website urls - extremely fast
-   **Search**: search the web and get full content from results
-   **Extract**: get structured data from single page, multiple pages or entire websites with AI.

### Powerful Capabilities

-   **LLM-ready formats**: markdown, structured data, screenshot, HTML, links, metadata
-   **The hard stuff**: proxies, anti-bot mechanisms, dynamic content (js-rendered), output parsing, orchestration
-   **Customizability**: exclude tags, crawl behind auth walls with custom headers, max crawl depth, etc...
-   **Media parsing**: pdfs, docx, images
-   **Reliability first**: designed to get the data you need - no matter how hard it is
-   **Actions**: click, scroll, input, wait and more before extracting data
-   **Batching**: scrape thousands of URLs at the same time with a new async endpoint
-   **Change Tracking**: monitor and detect changes in website content over time

You can find all of Firecrawl's capabilities and how to use them in our documentation

### Crawling

Used to crawl a URL and all accessible subpages. This submits a crawl job and returns a job ID to check the status of the crawl.

curl -X POST https://api.firecrawl.dev/v2/crawl \\
    -H 'Content-Type: application/json' \\
    -H 'Authorization: Bearer fc-YOUR\_API\_KEY' \\
    -d '{
      "url": "https://docs.firecrawl.dev",
      "limit": 10,
      "scrapeOptions": {
        "formats": \["markdown", "html"\]
      }
    }'

Returns a crawl job id and the url to check the status of the crawl.

{
  "success": true,
  "id": "123-456-789",
  "url": "https://api.firecrawl.dev/v2/crawl/123-456-789"
}

### Check Crawl Job

Used to check the status of a crawl job and get its result.

curl -X GET https://api.firecrawl.dev/v2/crawl/123-456-789 \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer YOUR\_API\_KEY'

{
  "status": "completed",
  "total": 36,
  "creditsUsed": 36,
  "expiresAt": "2024-00-00T00:00:00.000Z",
  "data": \[
    {
      "markdown": "\[Firecrawl Docs home page!\[light logo\](https://mintlify.s3-us-west-1.amazonaws.com/firecrawl/logo/light.svg)!...",
      "html": "<!DOCTYPE html><html lang=\\"en\\" class=\\"js-focus-visible lg:\[--scroll-mt:9.5rem\]\\" data-js-focus-visible=\\"\\"\>...",
      "metadata": {
        "title": "Build a 'Chat with website' using Groq Llama 3 | Firecrawl",
        "language": "en",
        "sourceURL": "https://docs.firecrawl.dev/learn/rag-llama3",
        "description": "Learn how to use Firecrawl, Groq Llama 3, and Langchain to build a 'Chat with your website' bot.",
        "ogLocaleAlternate": \[\],
        "statusCode": 200
      }
    }
  \]
}

### Scraping

Used to scrape a URL and get its content in the specified formats.

curl -X POST https://api.firecrawl.dev/v2/scrape \\
    -H 'Content-Type: application/json' \\
    -H 'Authorization: Bearer YOUR\_API\_KEY' \\
    -d '{
      "url": "https://docs.firecrawl.dev",
      "formats" : \["markdown", "html"\]
    }'

Response:

{
  "success": true,
  "data": {
    "markdown": "Launch Week I is here! \[See our Day 2 Release 🚀\](https://www.firecrawl.dev/blog/launch-week-i-day-2-doubled-rate-limits)\[💥 Get 2 months free...",
    "html": "<!DOCTYPE html><html lang=\\"en\\" class=\\"light\\" style=\\"color-scheme: light;\\"\><body class=\\"\_\_variable\_36bd41 \_\_variable\_d7dc5d font-inter ...",
    "metadata": {
      "title": "Home - Firecrawl",
      "description": "Firecrawl crawls and converts any website into clean markdown.",
      "language": "en",
      "keywords": "Firecrawl,Markdown,Data,Mendable,Langchain",
      "robots": "follow, index",
      "ogTitle": "Firecrawl",
      "ogDescription": "Turn any website into LLM-ready data.",
      "ogUrl": "https://www.firecrawl.dev/",
      "ogImage": "https://www.firecrawl.dev/og.png?123",
      "ogLocaleAlternate": \[\],
      "ogSiteName": "Firecrawl",
      "sourceURL": "https://firecrawl.dev",
      "statusCode": 200
    }
  }
}

### Map

Used to map a URL and get urls of the website. This returns most links present on the website.

curl -X POST https://api.firecrawl.dev/v2/map \\
    -H 'Content-Type: application/json' \\
    -H 'Authorization: Bearer YOUR\_API\_KEY' \\
    -d '{
      "url": "https://firecrawl.dev"
    }'

Response:

{
  "success": true,
  "links": \[
    { "url": "https://firecrawl.dev", "title": "Firecrawl", "description": "Firecrawl is a tool that allows you to crawl a website and get the data you need." },
    { "url": "https://www.firecrawl.dev/pricing", "title": "Firecrawl Pricing", "description": "Firecrawl Pricing" },
    { "url": "https://www.firecrawl.dev/blog", "title": "Firecrawl Blog", "description": "Firecrawl Blog" },
    { "url": "https://www.firecrawl.dev/playground", "title": "Firecrawl Playground", "description": "Firecrawl Playground" },
    { "url": "https://www.firecrawl.dev/smart-crawl", "title": "Firecrawl Smart Crawl", "description": "Firecrawl Smart Crawl" }
  \]
}

#### Map with search

Map with `search` param allows you to search for specific urls inside a website.

curl -X POST https://api.firecrawl.dev/v2/map \\
    -H 'Content-Type: application/json' \\
    -H 'Authorization: Bearer YOUR\_API\_KEY' \\
    -d '{
      "url": "https://firecrawl.dev",
      "search": "docs"
    }'

Response will be an ordered list from the most relevant to the least relevant.

{
  "success": true,
  "links": \[
    { "url": "https://docs.firecrawl.dev", "title": "Firecrawl Docs", "description": "Firecrawl Docs" },
    { "url": "https://docs.firecrawl.dev/sdks/python", "title": "Firecrawl Python SDK", "description": "Firecrawl Python SDK" },
    { "url": "https://docs.firecrawl.dev/learn/rag-llama3", "title": "Firecrawl RAG Llama 3", "description": "Firecrawl RAG Llama 3" }
  \]
}

### Search

Search the web and get full content from results

Firecrawl’s search API allows you to perform web searches and optionally scrape the search results in one operation.

-   Choose specific output formats (markdown, HTML, links, screenshots)
-   Search the web with customizable parameters (language, country, etc.)
-   Optionally retrieve content from search results in various formats
-   Control the number of results and set timeouts

curl -X POST https://api.firecrawl.dev/v2/search \\
  -H "Content-Type: application/json" \\
  -H "Authorization: Bearer fc-YOUR\_API\_KEY" \\
  -d '{
    "query": "what is firecrawl?",
    "limit": 5
  }'

#### Response

{
  "success": true,
  "data": \[
    {
      "url": "https://firecrawl.dev",
      "title": "Firecrawl | Home Page",
      "description": "Turn websites into LLM-ready data with Firecrawl"
    },
    {
      "url": "https://docs.firecrawl.dev",
      "title": "Documentation | Firecrawl",
      "description": "Learn how to use Firecrawl in your own applications"
    }
  \]
}

#### With content scraping

curl -X POST https://api.firecrawl.dev/v2/search \\
  -H "Content-Type: application/json" \\
  -H "Authorization: Bearer fc-YOUR\_API\_KEY" \\
  -d '{
    "query": "what is firecrawl?",
    "limit": 5,
    "scrapeOptions": {
      "formats": \["markdown", "links"\]
    }
  }'

### Extract (Beta)

Get structured data from entire websites with a prompt and/or a schema.

You can extract structured data from one or multiple URLs, including wildcards:

Single Page: Example: https://firecrawl.dev/some-page

Multiple Pages / Full Domain Example: https://firecrawl.dev/\*

When you use /\*, Firecrawl will automatically crawl and parse all URLs it can discover in that domain, then extract the requested data.

curl -X POST https://api.firecrawl.dev/v2/extract \\
    -H 'Content-Type: application/json' \\
    -H 'Authorization: Bearer YOUR\_API\_KEY' \\
    -d '{
      "urls": \[
        "https://firecrawl.dev/\*", 
        "https://docs.firecrawl.dev/", 
        "https://www.ycombinator.com/companies"
      \],
      "prompt": "Extract the company mission, whether it is open source, and whether it is in Y Combinator from the page.",
      "schema": {
        "type": "object",
        "properties": {
          "company\_mission": {
            "type": "string"
          },
          "is\_open\_source": {
            "type": "boolean"
          },
          "is\_in\_yc": {
            "type": "boolean"
          }
        },
        "required": \[
          "company\_mission",
          "is\_open\_source",
          "is\_in\_yc"
        \]
      }
    }'

{
  "success": true,
  "id": "44aa536d-f1cb-4706-ab87-ed0386685740",
  "urlTrace": \[\]
}

If you are using the sdks, it will auto pull the response for you:

{
  "success": true,
  "data": {
    "company\_mission": "Firecrawl is the easiest way to extract data from the web. Developers use us to reliably convert URLs into LLM-ready markdown or structured data with a single API call.",
    "supports\_sso": false,
    "is\_open\_source": true,
    "is\_in\_yc": true
  }
}

### LLM Extraction (Beta)

Used to extract structured data from scraped pages.

curl -X POST https://api.firecrawl.dev/v2/scrape \\
  -H 'Content-Type: application/json' \\
  -H 'Authorization: Bearer YOUR\_API\_KEY' \\
  -d '{
    "url": "https://www.mendable.ai/",
    "formats": \[
      {
        "type": "json",
        "schema": {
          "type": "object",
          "properties": {
            "company\_mission": { "type": "string" },
            "supports\_sso": { "type": "boolean" },
            "is\_open\_source": { "type": "boolean" },
            "is\_in\_yc": { "type": "boolean" }
          }
        }
      }
    \]
  }'

{
  "success": true,
  "data": {
    "content": "Raw Content",
    "metadata": {
      "title": "Mendable",
      "description": "Mendable allows you to easily build AI chat applications. Ingest, customize, then deploy with one line of code anywhere you want. Brought to you by SideGuide",
      "robots": "follow, index",
      "ogTitle": "Mendable",
      "ogDescription": "Mendable allows you to easily build AI chat applications. Ingest, customize, then deploy with one line of code anywhere you want. Brought to you by SideGuide",
      "ogUrl": "https://mendable.ai/",
      "ogImage": "https://mendable.ai/mendable\_new\_og1.png",
      "ogLocaleAlternate": \[\],
      "ogSiteName": "Mendable",
      "sourceURL": "https://mendable.ai/"
    },
    "json": {
      "company\_mission": "Train a secure AI on your technical resources that answers customer and employee questions so your team doesn't have to",
      "supports\_sso": true,
      "is\_open\_source": false,
      "is\_in\_yc": true
    }
  }
}

### Extracting without a schema (New)

You can now extract without a schema by just passing a `prompt` to the endpoint. The llm chooses the structure of the data.

curl -X POST https://api.firecrawl.dev/v2/scrape \\
    -H 'Content-Type: application/json' \\
    -H 'Authorization: Bearer YOUR\_API\_KEY' \\
    -d '{
      "url": "https://docs.firecrawl.dev/",
      "formats": \[
        {
          "type": "json",
          "prompt": "Extract the company mission from the page."
        }
      \]
    }'

### Interacting with the page with Actions (Cloud-only)

Firecrawl allows you to perform various actions on a web page before scraping its content. This is particularly useful for interacting with dynamic content, navigating through pages, or accessing content that requires user interaction.

Here is an example of how to use actions to navigate to google.com, search for Firecrawl, click on the first result, and take a screenshot.

curl -X POST https://api.firecrawl.dev/v2/scrape \\
    -H 'Content-Type: application/json' \\
    -H 'Authorization: Bearer YOUR\_API\_KEY' \\
    -d '{
        "url": "google.com",
        "formats": \["markdown"\],
        "actions": \[
            {"type": "wait", "milliseconds": 2000},
            {"type": "click", "selector": "textarea\[title=\\"Search\\"\]"},
            {"type": "wait", "milliseconds": 2000},
            {"type": "write", "text": "firecrawl"},
            {"type": "wait", "milliseconds": 2000},
            {"type": "press", "key": "ENTER"},
            {"type": "wait", "milliseconds": 3000},
            {"type": "click", "selector": "h3"},
            {"type": "wait", "milliseconds": 3000},
            {"type": "screenshot"}
        \]
    }'

### Batch Scraping Multiple URLs (New)

You can now batch scrape multiple URLs at the same time. It is very similar to how the /crawl endpoint works. It submits a batch scrape job and returns a job ID to check the status of the batch scrape.

curl -X POST https://api.firecrawl.dev/v2/batch/scrape \\
    -H 'Content-Type: application/json' \\
    -H 'Authorization: Bearer YOUR\_API\_KEY' \\
    -d '{
      "urls": \["https://docs.firecrawl.dev", "https://docs.firecrawl.dev/sdks/overview"\],
      "formats" : \["markdown", "html"\]
    }'

Using Python SDK
----------------

### Installing Python SDK

pip install firecrawl-py

### Crawl a website

from firecrawl import Firecrawl

firecrawl \= Firecrawl(api\_key\="fc-YOUR\_API\_KEY")

\# Scrape a website (returns a Document)
doc \= firecrawl.scrape(
    "https://firecrawl.dev",
    formats\=\["markdown", "html"\],
)
print(doc.markdown)

\# Crawl a website
response \= firecrawl.crawl(
    "https://firecrawl.dev",
    limit\=100,
    scrape\_options\={"formats": \["markdown", "html"\]},
    poll\_interval\=30,
)
print(response)

### Extracting structured data from a URL

With LLM extraction, you can easily extract structured data from any URL. We support pydantic schemas to make it easier for you too. Here is how you to use it:

from pydantic import BaseModel, Field
from typing import List

class Article(BaseModel):
    title: str
    points: int
    by: str
    commentsURL: str

class TopArticles(BaseModel):
    top: List\[Article\] \= Field(..., description\="Top 5 stories")

\# Use JSON format with a Pydantic schema
doc \= firecrawl.scrape(
    "https://news.ycombinator.com",
    formats\=\[{"type": "json", "schema": TopArticles}\],
)
print(doc.json)

Using the Node SDK
------------------

### Installation

To install the Firecrawl Node SDK, you can use npm:

npm install @mendable/firecrawl-js

### Usage

1.  Get an API key from firecrawl.dev
2.  Set the API key as an environment variable named `FIRECRAWL_API_KEY` or pass it as a parameter to the `Firecrawl` class.

import Firecrawl from '@mendable/firecrawl-js';

const firecrawl \= new Firecrawl({ apiKey: 'fc-YOUR\_API\_KEY' });

// Scrape a website
const doc \= await firecrawl.scrape('https://firecrawl.dev', {
  formats: \['markdown', 'html'\],
});
console.log(doc);

// Crawl a website
const response \= await firecrawl.crawl('https://firecrawl.dev', {
  limit: 100,
  scrapeOptions: { formats: \['markdown', 'html'\] },
});
console.log(response);

### Extracting structured data from a URL

With LLM extraction, you can easily extract structured data from any URL. We support zod schema to make it easier for you too. Here is how to use it:

import Firecrawl from '@mendable/firecrawl-js';
import { z } from 'zod';

const firecrawl \= new Firecrawl({ apiKey: 'fc-YOUR\_API\_KEY' });

// Define schema to extract contents into
const schema \= z.object({
  top: z
    .array(
      z.object({
        title: z.string(),
        points: z.number(),
        by: z.string(),
        commentsURL: z.string(),
      })
    )
    .length(5)
    .describe('Top 5 stories on Hacker News'),
});

// Use the v2 extract API with direct Zod schema support
const extractRes \= await firecrawl.extract({
  urls: \['https://news.ycombinator.com'\],
  schema,
  prompt: 'Extract the top 5 stories',
});

console.log(extractRes);

Open Source vs Cloud Offering
-----------------------------

Firecrawl is open source available under the AGPL-3.0 license.

To deliver the best possible product, we offer a hosted version of Firecrawl alongside our open-source offering. The cloud solution allows us to continuously innovate and maintain a high-quality, sustainable service for all users.

Firecrawl Cloud is available at firecrawl.dev and offers a range of features that are not available in the open source version:

Contributing
------------

We love contributions! Please read our contributing guide before submitting a pull request. If you'd like to self-host, refer to the self-hosting guide.

_It is the sole responsibility of the end users to respect websites' policies when scraping, searching and crawling with Firecrawl. Users are advised to adhere to the applicable privacy policies and terms of use of the websites prior to initiating any scraping activities. By default, Firecrawl respects the directives specified in the websites' robots.txt files when crawling. By utilizing Firecrawl, you expressly agree to comply with these conditions._

Contributors
------------

License Disclaimer
------------------

This project is primarily licensed under the GNU Affero General Public License v3.0 (AGPL-3.0), as specified in the LICENSE file in the root directory of this repository. However, certain components of this project are licensed under the MIT License. Refer to the LICENSE files in these specific directories for details.

Please note:

-   The AGPL-3.0 license applies to all parts of the project unless otherwise specified.
-   The SDKs and some UI components are licensed under the MIT License. Refer to the LICENSE files in these specific directories for details.
-   When using or contributing to this project, ensure you comply with the appropriate license terms for the specific component you are working with.

For more details on the licensing of specific components, please refer to the LICENSE files in the respective directories or contact the project maintainers.

↑ Back to Top ↑
