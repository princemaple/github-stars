---
project: fireplexity
stars: 1758
description: 🔥 Open Source Perplexity like AI search engine with real-time citations, streaming responses, and live data powered by Firecrawl 
url: https://github.com/firecrawl/fireplexity
---

Fireplexity v2
==============

AI search engine with web, news, and images.

Setup
-----

git clone https://github.com/mendableai/fireplexity.git
cd fireplexity
npm install

Configure
---------

cp .env.example .env.local

Add your keys to `.env.local`:

```
FIRECRAWL_API_KEY=fc-your-api-key
GROQ_API_KEY=gsk_your-groq-api-key
```

Run
---

npm run dev

Open http://localhost:3000

Deploy
------

Get API Keys
------------

-   Firecrawl
-   Groq

MIT License
