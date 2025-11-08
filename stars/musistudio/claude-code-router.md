---
project: claude-code-router
stars: 21168
description: Use Claude Code as the foundation for coding infrastructure, allowing you to decide how to interact with the model while enjoying updates from Anthropic.
url: https://github.com/musistudio/claude-code-router
---

* * *

> This project is sponsored by Z.ai, supporting us with their GLM CODING PLAN.  
> GLM CODING PLAN is a subscription service designed for AI coding, starting at just $3/month. It provides access to their flagship GLM-4.6 model across 10+ popular AI coding tools (Claude Code, Cline, Roo Code, etc.), offering developers top-tier, fast, and stable coding experiences.  
> Get 10% OFF GLM CODING PLAN：https://z.ai/subscribe?ic=8JVLJQFSKB

> A powerful tool to route Claude Code requests to different models and customize any request.

✨ Features
----------

-   **Model Routing**: Route requests to different models based on your needs (e.g., background tasks, thinking, long context).
-   **Multi-Provider Support**: Supports various model providers like OpenRouter, DeepSeek, Ollama, Gemini, Volcengine, and SiliconFlow.
-   **Request/Response Transformation**: Customize requests and responses for different providers using transformers.
-   **Dynamic Model Switching**: Switch models on-the-fly within Claude Code using the `/model` command.
-   **CLI Model Management**: Manage models and providers directly from the terminal with `ccr model`.
-   **GitHub Actions Integration**: Trigger Claude Code tasks in your GitHub workflows.
-   **Plugin System**: Extend functionality with custom transformers.

🚀 Getting Started
------------------

### 1\. Installation

First, ensure you have Claude Code installed:

npm install -g @anthropic-ai/claude-code

Then, install Claude Code Router:

npm install -g @musistudio/claude-code-router

### 2\. Configuration

Create and configure your `~/.claude-code-router/config.json` file. For more details, you can refer to `config.example.json`.

The `config.json` file has several key sections:

-   **`PROXY_URL`** (optional): You can set a proxy for API requests, for example: `"PROXY_URL": "http://127.0.0.1:7890"`.
    
-   **`LOG`** (optional): You can enable logging by setting it to `true`. When set to `false`, no log files will be created. Default is `true`.
    
-   **`LOG_LEVEL`** (optional): Set the logging level. Available options are: `"fatal"`, `"error"`, `"warn"`, `"info"`, `"debug"`, `"trace"`. Default is `"debug"`.
    
-   **Logging Systems**: The Claude Code Router uses two separate logging systems:
    
    -   **Server-level logs**: HTTP requests, API calls, and server events are logged using pino in the `~/.claude-code-router/logs/` directory with filenames like `ccr-*.log`
    -   **Application-level logs**: Routing decisions and business logic events are logged in `~/.claude-code-router/claude-code-router.log`
-   **`APIKEY`** (optional): You can set a secret key to authenticate requests. When set, clients must provide this key in the `Authorization` header (e.g., `Bearer your-secret-key`) or the `x-api-key` header. Example: `"APIKEY": "your-secret-key"`.
    
-   **`HOST`** (optional): You can set the host address for the server. If `APIKEY` is not set, the host will be forced to `127.0.0.1` for security reasons to prevent unauthorized access. Example: `"HOST": "0.0.0.0"`.
    
-   **`NON_INTERACTIVE_MODE`** (optional): When set to `true`, enables compatibility with non-interactive environments like GitHub Actions, Docker containers, or other CI/CD systems. This sets appropriate environment variables (`CI=true`, `FORCE_COLOR=0`, etc.) and configures stdin handling to prevent the process from hanging in automated environments. Example: `"NON_INTERACTIVE_MODE": true`.
    
-   **`Providers`**: Used to configure different model providers.
    
-   **`Router`**: Used to set up routing rules. `default` specifies the default model, which will be used for all requests if no other route is configured.
    
-   **`API_TIMEOUT_MS`**: Specifies the timeout for API calls in milliseconds.
    

#### Environment Variable Interpolation

Claude Code Router supports environment variable interpolation for secure API key management. You can reference environment variables in your `config.json` using either `$VAR_NAME` or `${VAR_NAME}` syntax:

{
  "OPENAI\_API\_KEY": "$OPENAI\_API\_KEY",
  "GEMINI\_API\_KEY": "${GEMINI\_API\_KEY}",
  "Providers": \[
    {
      "name": "openai",
      "api\_base\_url": "https://api.openai.com/v1/chat/completions",
      "api\_key": "$OPENAI\_API\_KEY",
      "models": \["gpt-5", "gpt-5-mini"\]
    }
  \]
}

This allows you to keep sensitive API keys in environment variables instead of hardcoding them in configuration files. The interpolation works recursively through nested objects and arrays.

Here is a comprehensive example:

{
  "APIKEY": "your-secret-key",
  "PROXY\_URL": "http://127.0.0.1:7890",
  "LOG": true,
  "API\_TIMEOUT\_MS": 600000,
  "NON\_INTERACTIVE\_MODE": false,
  "Providers": \[
    {
      "name": "openrouter",
      "api\_base\_url": "https://openrouter.ai/api/v1/chat/completions",
      "api\_key": "sk-xxx",
      "models": \[
        "google/gemini-2.5-pro-preview",
        "anthropic/claude-sonnet-4",
        "anthropic/claude-3.5-sonnet",
        "anthropic/claude-3.7-sonnet:thinking"
      \],
      "transformer": {
        "use": \["openrouter"\]
      }
    },
    {
      "name": "deepseek",
      "api\_base\_url": "https://api.deepseek.com/chat/completions",
      "api\_key": "sk-xxx",
      "models": \["deepseek-chat", "deepseek-reasoner"\],
      "transformer": {
        "use": \["deepseek"\],
        "deepseek-chat": {
          "use": \["tooluse"\]
        }
      }
    },
    {
      "name": "ollama",
      "api\_base\_url": "http://localhost:11434/v1/chat/completions",
      "api\_key": "ollama",
      "models": \["qwen2.5-coder:latest"\]
    },
    {
      "name": "gemini",
      "api\_base\_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api\_key": "sk-xxx",
      "models": \["gemini-2.5-flash", "gemini-2.5-pro"\],
      "transformer": {
        "use": \["gemini"\]
      }
    },
    {
      "name": "volcengine",
      "api\_base\_url": "https://ark.cn-beijing.volces.com/api/v3/chat/completions",
      "api\_key": "sk-xxx",
      "models": \["deepseek-v3-250324", "deepseek-r1-250528"\],
      "transformer": {
        "use": \["deepseek"\]
      }
    },
    {
      "name": "modelscope",
      "api\_base\_url": "https://api-inference.modelscope.cn/v1/chat/completions",
      "api\_key": "",
      "models": \["Qwen/Qwen3-Coder-480B-A35B-Instruct", "Qwen/Qwen3-235B-A22B-Thinking-2507"\],
      "transformer": {
        "use": \[
          \[
            "maxtoken",
            {
              "max\_tokens": 65536
            }
          \],
          "enhancetool"
        \],
        "Qwen/Qwen3-235B-A22B-Thinking-2507": {
          "use": \["reasoning"\]
        }
      }
    },
    {
      "name": "dashscope",
      "api\_base\_url": "https://dashscope.aliyuncs.com/compatible-mode/v1/chat/completions",
      "api\_key": "",
      "models": \["qwen3-coder-plus"\],
      "transformer": {
        "use": \[
          \[
            "maxtoken",
            {
              "max\_tokens": 65536
            }
          \],
          "enhancetool"
        \]
      }
    },
    {
      "name": "aihubmix",
      "api\_base\_url": "https://aihubmix.com/v1/chat/completions",
      "api\_key": "sk-",
      "models": \[
        "Z/glm-4.5",
        "claude-opus-4-20250514",
        "gemini-2.5-pro"
      \]
    }
  \],
  "Router": {
    "default": "deepseek,deepseek-chat",
    "background": "ollama,qwen2.5-coder:latest",
    "think": "deepseek,deepseek-reasoner",
    "longContext": "openrouter,google/gemini-2.5-pro-preview",
    "longContextThreshold": 60000,
    "webSearch": "gemini,gemini-2.5-flash"
  }
}

### 3\. Running Claude Code with the Router

Start Claude Code using the router:

ccr code

> **Note**: After modifying the configuration file, you need to restart the service for the changes to take effect:
> 
> ccr restart

### 4\. UI Mode

For a more intuitive experience, you can use the UI mode to manage your configuration:

ccr ui

This will open a web-based interface where you can easily view and edit your `config.json` file.

### 5\. CLI Model Management

For users who prefer terminal-based workflows, you can use the interactive CLI model selector:

ccr model

This command provides an interactive interface to:

-   View current configuration:
-   See all configured models (default, background, think, longContext, webSearch, image)
-   Switch models: Quickly change which model is used for each router type
-   Add new models: Add models to existing providers
-   Create new providers: Set up complete provider configurations including:
    -   Provider name and API endpoint
    -   API key
    -   Available models
    -   Transformer configuration with support for:
        -   Multiple transformers (openrouter, deepseek, gemini, etc.)
        -   Transformer options (e.g., maxtoken with custom limits)
        -   Provider-specific routing (e.g., OpenRouter provider preferences)

The CLI tool validates all inputs and provides helpful prompts to guide you through the configuration process, making it easy to manage complex setups without editing JSON files manually.

#### Providers

The `Providers` array is where you define the different model providers you want to use. Each provider object requires:

-   `name`: A unique name for the provider.
-   `api_base_url`: The full API endpoint for chat completions.
-   `api_key`: Your API key for the provider.
-   `models`: A list of model names available from this provider.
-   `transformer` (optional): Specifies transformers to process requests and responses.

#### Transformers

Transformers allow you to modify the request and response payloads to ensure compatibility with different provider APIs.

-   **Global Transformer**: Apply a transformer to all models from a provider. In this example, the `openrouter` transformer is applied to all models under the `openrouter` provider.
    
    {
      "name": "openrouter",
      "api\_base\_url": "https://openrouter.ai/api/v1/chat/completions",
      "api\_key": "sk-xxx",
      "models": \[
        "google/gemini-2.5-pro-preview",
        "anthropic/claude-sonnet-4",
        "anthropic/claude-3.5-sonnet"
      \],
      "transformer": { "use": \["openrouter"\] }
    }
    
-   **Model-Specific Transformer**: Apply a transformer to a specific model. In this example, the `deepseek` transformer is applied to all models, and an additional `tooluse` transformer is applied only to the `deepseek-chat` model.
    
    {
      "name": "deepseek",
      "api\_base\_url": "https://api.deepseek.com/chat/completions",
      "api\_key": "sk-xxx",
      "models": \["deepseek-chat", "deepseek-reasoner"\],
      "transformer": {
        "use": \["deepseek"\],
        "deepseek-chat": { "use": \["tooluse"\] }
      }
    }
    
-   **Passing Options to a Transformer**: Some transformers, like `maxtoken`, accept options. To pass options, use a nested array where the first element is the transformer name and the second is an options object.
    
    {
      "name": "siliconflow",
      "api\_base\_url": "https://api.siliconflow.cn/v1/chat/completions",
      "api\_key": "sk-xxx",
      "models": \["moonshotai/Kimi-K2-Instruct"\],
      "transformer": {
        "use": \[
          \[
            "maxtoken",
            {
              "max\_tokens": 16384
            }
          \]
        \]
      }
    }
    

**Available Built-in Transformers:**

-   `Anthropic`:If you use only the `Anthropic` transformer, it will preserve the original request and response parameters(you can use it to connect directly to an Anthropic endpoint).
-   `deepseek`: Adapts requests/responses for DeepSeek API.
-   `gemini`: Adapts requests/responses for Gemini API.
-   `openrouter`: Adapts requests/responses for OpenRouter API. It can also accept a `provider` routing parameter to specify which underlying providers OpenRouter should use. For more details, refer to the OpenRouter documentation. See an example below:
    
      "transformer": {
        "use": \["openrouter"\],
        "moonshotai/kimi-k2": {
          "use": \[
            \[
              "openrouter",
              {
                "provider": {
                  "only": \["moonshotai/fp8"\]
                }
              }
            \]
          \]
        }
      }
    
-   `groq`: Adapts requests/responses for groq API.
-   `maxtoken`: Sets a specific `max_tokens` value.
-   `tooluse`: Optimizes tool usage for certain models via `tool_choice`.
-   `gemini-cli` (experimental): Unofficial support for Gemini via Gemini CLI gemini-cli.js.
-   `reasoning`: Used to process the `reasoning_content` field.
-   `sampling`: Used to process sampling information fields such as `temperature`, `top_p`, `top_k`, and `repetition_penalty`.
-   `enhancetool`: Adds a layer of error tolerance to the tool call parameters returned by the LLM (this will cause the tool call information to no longer be streamed).
-   `cleancache`: Clears the `cache_control` field from requests.
-   `vertex-gemini`: Handles the Gemini API using Vertex authentication.
-   `chutes-glm` Unofficial support for GLM 4.5 model via Chutes chutes-glm-transformer.js.
-   `qwen-cli` (experimental): Unofficial support for qwen3-coder-plus model via Qwen CLI qwen-cli.js.
-   `rovo-cli` (experimental): Unofficial support for gpt-5 via Atlassian Rovo Dev CLI rovo-cli.js.

**Custom Transformers:**

You can also create your own transformers and load them via the `transformers` field in `config.json`.

{
  "transformers": \[
    {
      "path": "/User/xxx/.claude-code-router/plugins/gemini-cli.js",
      "options": {
        "project": "xxx"
      }
    }
  \]
}

#### Router

The `Router` object defines which model to use for different scenarios:

-   `default`: The default model for general tasks.
    
-   `background`: A model for background tasks. This can be a smaller, local model to save costs.
    
-   `think`: A model for reasoning-heavy tasks, like Plan Mode.
    
-   `longContext`: A model for handling long contexts (e.g., > 60K tokens).
    
-   `longContextThreshold` (optional): The token count threshold for triggering the long context model. Defaults to 60000 if not specified.
    
-   `webSearch`: Used for handling web search tasks and this requires the model itself to support the feature. If you're using openrouter, you need to add the `:online` suffix after the model name.
    
-   `image` (beta): Used for handling image-related tasks (supported by CCR’s built-in agent). If the model does not support tool calling, you need to set the `config.forceUseImageAgent` property to `true`.
    
-   You can also switch models dynamically in Claude Code with the `/model` command: `/model provider_name,model_name` Example: `/model openrouter,anthropic/claude-3.5-sonnet`
    

#### Custom Router

For more advanced routing logic, you can specify a custom router script via the `CUSTOM_ROUTER_PATH` in your `config.json`. This allows you to implement complex routing rules beyond the default scenarios.

In your `config.json`:

{
  "CUSTOM\_ROUTER\_PATH": "/User/xxx/.claude-code-router/custom-router.js"
}

The custom router file must be a JavaScript module that exports an `async` function. This function receives the request object and the config object as arguments and should return the provider and model name as a string (e.g., `"provider_name,model_name"`), or `null` to fall back to the default router.

Here is an example of a `custom-router.js` based on `custom-router.example.js`:

// /User/xxx/.claude-code-router/custom-router.js

/\*\*
 \* A custom router function to determine which model to use based on the request.
 \*
 \* @param {object} req - The request object from Claude Code, containing the request body.
 \* @param {object} config - The application's config object.
 \* @returns {Promise<string|null>} - A promise that resolves to the "provider,model\_name" string, or null to use the default router.
 \*/
module.exports \= async function router(req, config) {
  const userMessage \= req.body.messages.find((m) \=> m.role \=== "user")?.content;

  if (userMessage && userMessage.includes("explain this code")) {
    // Use a powerful model for code explanation
    return "openrouter,anthropic/claude-3.5-sonnet";
  }

  // Fallback to the default router configuration
  return null;
};

##### Subagent Routing

For routing within subagents, you must specify a particular provider and model by including `<CCR-SUBAGENT-MODEL>provider,model</CCR-SUBAGENT-MODEL>` at the **beginning** of the subagent's prompt. This allows you to direct specific subagent tasks to designated models.

**Example:**

```
<CCR-SUBAGENT-MODEL>openrouter,anthropic/claude-3.5-sonnet</CCR-SUBAGENT-MODEL>
Please help me analyze this code snippet for potential optimizations...
```

Status Line (Beta)
------------------

To better monitor the status of claude-code-router at runtime, version v1.0.40 includes a built-in statusline tool, which you can enable in the UI.

The effect is as follows:

🤖 GitHub Actions
-----------------

Integrate Claude Code Router into your CI/CD pipeline. After setting up Claude Code Actions, modify your `.github/workflows/claude.yaml` to use the router:

name: Claude Code

on:
  issue\_comment:
    types: \[created\]
  # ... other triggers

jobs:
  claude:
    if: |
      (github.event\_name == 'issue\_comment' && contains(github.event.comment.body, '@claude')) ||
      # ... other conditions
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: read
      issues: read
      id-token: write
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 1

      - name: Prepare Environment
        run: |
          curl -fsSL https://bun.sh/install | bash
          mkdir -p $HOME/.claude-code-router
          cat << 'EOF' > $HOME/.claude-code-router/config.json
          {
            "log": true,
            "NON\_INTERACTIVE\_MODE": true,
            "OPENAI\_API\_KEY": "${{ secrets.OPENAI\_API\_KEY }}",
            "OPENAI\_BASE\_URL": "https://api.deepseek.com",
            "OPENAI\_MODEL": "deepseek-chat"
          }
          EOF
        shell: bash

      - name: Start Claude Code Router
        run: |
          nohup ~/.bun/bin/bunx @musistudio/claude-code-router@1.0.8 start &
        shell: bash

      - name: Run Claude Code
        id: claude
        uses: anthropics/claude-code-action@beta
        env:
          ANTHROPIC\_BASE\_URL: http://localhost:3456
        with:
          anthropic\_api\_key: "any-string-is-ok"

> **Note**: When running in GitHub Actions or other automation environments, make sure to set `"NON_INTERACTIVE_MODE": true` in your configuration to prevent the process from hanging due to stdin handling issues.

This setup allows for interesting automations, like running tasks during off-peak hours to reduce API costs.

📝 Further Reading
------------------

-   Project Motivation and How It Works
-   Maybe We Can Do More with the Router

❤️ Support & Sponsoring
-----------------------

If you find this project helpful, please consider sponsoring its development. Your support is greatly appreciated!

Paypal

### Our Sponsors

A huge thank you to all our sponsors for their generous support!

-   AIHubmix
-   BurnCloud
-   302.AI
-   Z智谱
-   @Simon Leischnig
-   @duanshuaimin
-   @vrgitadmin
-   @\*o
-   @ceilwoo
-   @\*说
-   @\*更
-   @K\*g
-   @R\*R
-   @bobleer
-   @\*苗
-   @\*划
-   @Clarence-pan
-   @carter003
-   @S\*r
-   @\*晖
-   @\*敏
-   @Z\*z
-   @\*然
-   @cluic
-   @\*苗
-   @PromptExpert
-   @\*应
-   @yusnake
-   @\*飞
-   @董\*
-   @\*汀
-   @\*涯
-   @\*:-）
-   @\*\*磊
-   @\*琢
-   @\*成
-   @Z\*o
-   @\*琨
-   @congzhangzh
-   @\*\_
-   @Z\*m
-   @\*鑫
-   @c\*y
-   @\*昕
-   @witsice
-   @b\*g
-   @\*亿
-   @\*辉
-   @JACK
-   @\*光
-   @W\*l
-   @kesku
-   @biguncle
-   @二吉吉
-   @a\*g
-   @\*林
-   @\*咸
-   @\*明
-   @S\*y
-   @f\*o
-   @\*智
-   @F\*t
-   @r\*c
-   @qierkang
-   @\*军
-   @snrise-z
-   @\*王
-   @greatheart1000
-   @\*王
-   @zcutlip
-   @Peng-YM
-   @\*更
-   @\*.
-   @F\*t
-   @\*政
-   @\*铭
-   @\*叶
-   @七\*o
-   @\*青
-   @\*\*晨
-   @\*远
-   @\*霄
-   @\*\*吉
-   @\*\*飞
-   @\*\*驰
-   @x\*g
-   @\*\*东
-   @\*落
-   @哆\*k
-   @\*涛
-   @苗大
-   @\*呢
-   @\\d\*u
-   @crizcraig

(If your name is masked, please contact me via my homepage email to update it with your GitHub username.)
