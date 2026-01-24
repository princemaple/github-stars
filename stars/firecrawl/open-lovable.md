---
project: open-lovable
stars: 23620
description: 🔥 Clone and recreate any website as a modern React app in seconds
url: https://github.com/firecrawl/open-lovable
---

Open Lovable
============

Chat with AI to build React apps instantly. An example app made by the Firecrawl team. For a complete cloud solution, check out Lovable.dev ❤️.

Setup
-----

1.  **Clone & Install**

git clone https://github.com/firecrawl/open-lovable.git
cd open-lovable
pnpm install  # or npm install / yarn install

1.  **Add `.env.local`**

# =================================================================
# REQUIRED
# =================================================================
FIRECRAWL\_API\_KEY\=your\_firecrawl\_api\_key    # https://firecrawl.dev

# =================================================================
# AI PROVIDER - Choose your LLM
# =================================================================
GEMINI\_API\_KEY\=your\_gemini\_api\_key        # https://aistudio.google.com/app/apikey
ANTHROPIC\_API\_KEY\=your\_anthropic\_api\_key  # https://console.anthropic.com
OPENAI\_API\_KEY\=your\_openai\_api\_key        # https://platform.openai.com
GROQ\_API\_KEY\=your\_groq\_api\_key            # https://console.groq.com

# =================================================================
# FAST APPLY (Optional - for faster edits)
# =================================================================
MORPH\_API\_KEY\=your\_morphllm\_api\_key    # https://morphllm.com/dashboard

# =================================================================
# SANDBOX PROVIDER - Choose ONE: Vercel (default) or E2B
# =================================================================
SANDBOX\_PROVIDER\=vercel  # or 'e2b'

# Option 1: Vercel Sandbox (default)
# Choose one authentication method:

# Method A: OIDC Token (recommended for development)
# Run \`vercel link\` then \`vercel env pull\` to get VERCEL\_OIDC\_TOKEN automatically
VERCEL\_OIDC\_TOKEN\=auto\_generated\_by\_vercel\_env\_pull

# Method B: Personal Access Token (for production or when OIDC unavailable)
# VERCEL\_TEAM\_ID=team\_xxxxxxxxx      # Your Vercel team ID 
# VERCEL\_PROJECT\_ID=prj\_xxxxxxxxx    # Your Vercel project ID
# VERCEL\_TOKEN=vercel\_xxxxxxxxxxxx   # Personal access token from Vercel dashboard

# Option 2: E2B Sandbox
# E2B\_API\_KEY=your\_e2b\_api\_key      # https://e2b.dev

1.  **Run**

pnpm dev  # or npm run dev / yarn dev

Open http://localhost:3000

License
-------

MIT
