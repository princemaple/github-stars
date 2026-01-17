---
project: crush
stars: 18275
description: Glamourous agentic coding for all 💘
url: https://github.com/charmbracelet/crush
---

Crush
=====

  

Your new coding bestie, now available in your favourite terminal.  
Your tools, your code, and your workflows, wired into your LLM of choice.

你的新编程伙伴，现在就在你最爱的终端中。  
你的工具、代码和工作流，都与您选择的 LLM 模型紧密相连。

Features
--------

-   **Multi-Model:** choose from a wide range of LLMs or add your own via OpenAI- or Anthropic-compatible APIs
-   **Flexible:** switch LLMs mid-session while preserving context
-   **Session-Based:** maintain multiple work sessions and contexts per project
-   **LSP-Enhanced:** Crush uses LSPs for additional context, just like you do
-   **Extensible:** add capabilities via MCPs (`http`, `stdio`, and `sse`)
-   **Works Everywhere:** first-class support in every terminal on macOS, Linux, Windows (PowerShell and WSL), Android, FreeBSD, OpenBSD, and NetBSD
-   **Industrial Grade:** built on the Charm ecosystem, powering 25k+ applications, from leading open source projects to business-critical infrastructure

Installation
------------

Use a package manager:

# Homebrew
brew install charmbracelet/tap/crush

# NPM
npm install -g @charmland/crush

# Arch Linux (btw)
yay -S crush-bin

# Nix
nix run github:numtide/nix-ai-tools#crush

# FreeBSD
pkg install crush

Windows users:

# Winget
winget install charmbracelet.crush

# Scoop
scoop bucket add charm https://github.com/charmbracelet/scoop-bucket.git
scoop install crush

**Nix (NUR)**

Crush is available via the official Charm NUR in `nur.repos.charmbracelet.crush`, which is the most up-to-date way to get Crush in Nix.

You can also try out Crush via the NUR with `nix-shell`:

# Add the NUR channel.
nix-channel --add https://github.com/nix-community/NUR/archive/main.tar.gz nur
nix-channel --update

# Get Crush in a Nix shell.
nix-shell -p '(import <nur> { pkgs = import <nixpkgs> {}; }).repos.charmbracelet.crush'

### NixOS & Home Manager Module Usage via NUR

Crush provides NixOS and Home Manager modules via NUR. You can use these modules directly in your flake by importing them from NUR. Since it auto detects whether its a home manager or nixos context you can use the import the exact same way :)

{
  inputs \= {
    nixpkgs.url \= "github:NixOS/nixpkgs/nixos-unstable";
    nur.url \= "github:nix-community/NUR";
  };

  outputs \= { self, nixpkgs, nur, ... }: {
    nixosConfigurations.your-hostname \= nixpkgs.lib.nixosSystem {
      system \= "x86\_64-linux";
      modules \= \[
        nur.modules.nixos.default
        nur.repos.charmbracelet.modules.crush
        {
          programs.crush \= {
            enable \= true;
            settings \= {
              providers \= {
                openai \= {
                  id \= "openai";
                  name \= "OpenAI";
                  base\_url \= "https://api.openai.com/v1";
                  type \= "openai";
                  api\_key \= "sk-fake123456789abcdef...";
                  models \= \[
                    {
                      id \= "gpt-4";
                      name \= "GPT-4";
                    }
                  \];
                };
              };
              lsp \= {
                go \= { command \= "gopls"; enabled \= true; };
                nix \= { command \= "nil"; enabled \= true; };
              };
              options \= {
                context\_paths \= \[ "/etc/nixos/configuration.nix" \];
                tui \= { compact\_mode \= true; };
                debug \= false;
              };
            };
          };
        }
      \];
    };
  };
}

**Debian/Ubuntu**

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://repo.charm.sh/apt/gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/charm.gpg
echo "deb \[signed-by=/etc/apt/keyrings/charm.gpg\] https://repo.charm.sh/apt/ \* \*" | sudo tee /etc/apt/sources.list.d/charm.list
sudo apt update && sudo apt install crush

**Fedora/RHEL**

echo '\[charm\]
name=Charm
baseurl=https://repo.charm.sh/yum/
enabled=1
gpgcheck=1
gpgkey=https://repo.charm.sh/yum/gpg.key' | sudo tee /etc/yum.repos.d/charm.repo
sudo yum install crush

Or, download it:

-   Packages are available in Debian and RPM formats
-   Binaries are available for Linux, macOS, Windows, FreeBSD, OpenBSD, and NetBSD

Or just install it with Go:

```
go install github.com/charmbracelet/crush@latest
```

Warning

Productivity may increase when using Crush and you may find yourself nerd sniped when first using the application. If the symptoms persist, join the Discord and nerd snipe the rest of us.

Getting Started
---------------

The quickest way to get started is to grab an API key for your preferred provider such as Anthropic, OpenAI, Groq, or OpenRouter and just start Crush. You'll be prompted to enter your API key.

That said, you can also set environment variables for preferred providers.

Environment Variable

Provider

`ANTHROPIC_API_KEY`

Anthropic

`OPENAI_API_KEY`

OpenAI

`OPENROUTER_API_KEY`

OpenRouter

`GEMINI_API_KEY`

Google Gemini

`CEREBRAS_API_KEY`

Cerebras

`HF_TOKEN`

Huggingface Inference

`VERTEXAI_PROJECT`

Google Cloud VertexAI (Gemini)

`VERTEXAI_LOCATION`

Google Cloud VertexAI (Gemini)

`GROQ_API_KEY`

Groq

`AWS_ACCESS_KEY_ID`

Amazon Bedrock (Claude)

`AWS_SECRET_ACCESS_KEY`

Amazon Bedrock (Claude)

`AWS_REGION`

Amazon Bedrock (Claude)

`AWS_PROFILE`

Amazon Bedrock (Custom Profile)

`AWS_BEARER_TOKEN_BEDROCK`

Amazon Bedrock

`AZURE_OPENAI_API_ENDPOINT`

Azure OpenAI models

`AZURE_OPENAI_API_KEY`

Azure OpenAI models (optional when using Entra ID)

`AZURE_OPENAI_API_VERSION`

Azure OpenAI models

### By the Way

Is there a provider you’d like to see in Crush? Is there an existing model that needs an update?

Crush’s default model listing is managed in Catwalk, a community-supported, open source repository of Crush-compatible models, and you’re welcome to contribute.

Configuration
-------------

Crush runs great with no configuration. That said, if you do need or want to customize Crush, configuration can be added either local to the project itself, or globally, with the following priority:

1.  `.crush.json`
2.  `crush.json`
3.  `$HOME/.config/crush/crush.json`

Configuration itself is stored as a JSON object:

{
  "this-setting": { "this": "that" },
  "that-setting": \["ceci", "cela"\]
}

As an additional note, Crush also stores ephemeral data, such as application state, in one additional location:

# Unix
$HOME/.local/share/crush/crush.json

# Windows
%LOCALAPPDATA%\\crush\\crush.json

Tip

You can override the user and data config locations by setting:

-   `CRUSH_GLOBAL_CONFIG`
-   `CRUSH_GLOBAL_DATA`

### LSPs

Crush can use LSPs for additional context to help inform its decisions, just like you would. LSPs can be added manually like so:

{
  "$schema": "https://charm.land/crush.json",
  "lsp": {
    "go": {
      "command": "gopls",
      "env": {
        "GOTOOLCHAIN": "go1.24.5"
      }
    },
    "typescript": {
      "command": "typescript-language-server",
      "args": \["\--stdio"\]
    },
    "nix": {
      "command": "nil"
    }
  }
}

### MCPs

Crush also supports Model Context Protocol (MCP) servers through three transport types: `stdio` for command-line servers, `http` for HTTP endpoints, and `sse` for Server-Sent Events. Environment variable expansion is supported using `$(echo $VAR)` syntax.

{
  "$schema": "https://charm.land/crush.json",
  "mcp": {
    "filesystem": {
      "type": "stdio",
      "command": "node",
      "args": \["/path/to/mcp-server.js"\],
      "timeout": 120,
      "disabled": false,
      "disabled\_tools": \["some-tool-name"\],
      "env": {
        "NODE\_ENV": "production"
      }
    },
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/",
      "timeout": 120,
      "disabled": false,
      "disabled\_tools": \["create\_issue", "create\_pull\_request"\],
      "headers": {
        "Authorization": "Bearer $GH\_PAT"
      }
    },
    "streaming-service": {
      "type": "sse",
      "url": "https://example.com/mcp/sse",
      "timeout": 120,
      "disabled": false,
      "headers": {
        "API-Key": "$(echo $API\_KEY)"
      }
    }
  }
}

### Ignoring Files

Crush respects `.gitignore` files by default, but you can also create a `.crushignore` file to specify additional files and directories that Crush should ignore. This is useful for excluding files that you want in version control but don't want Crush to consider when providing context.

The `.crushignore` file uses the same syntax as `.gitignore` and can be placed in the root of your project or in subdirectories.

### Allowing Tools

By default, Crush will ask you for permission before running tool calls. If you'd like, you can allow tools to be executed without prompting you for permissions. Use this with care.

{
  "$schema": "https://charm.land/crush.json",
  "permissions": {
    "allowed\_tools": \[
      "view",
      "ls",
      "grep",
      "edit",
      "mcp\_context7\_get-library-doc"
    \]
  }
}

You can also skip all permission prompts entirely by running Crush with the `--yolo` flag. Be very, very careful with this feature.

### Disabling Built-In Tools

If you'd like to prevent Crush from using certain built-in tools entirely, you can disable them via the `options.disabled_tools` list. Disabled tools are completely hidden from the agent.

{
  "$schema": "https://charm.land/crush.json",
  "options": {
    "disabled\_tools": \[
      "bash",
      "sourcegraph"
    \]
  }
}

To disable tools from MCP servers, see the MCP config section.

### Agent Skills

Crush supports the Agent Skills open standard for extending agent capabilities with reusable skill packages. Skills are folders containing a `SKILL.md` file with instructions that Crush can discover and activate on demand.

Skills are discovered from:

-   `~/.config/crush/skills/` on Unix (default, can be overridden with `CRUSH_SKILLS_DIR`)
-   `%LOCALAPPDATA%\crush\skills\` on Windows (default, can be overridden with `CRUSH_SKILLS_DIR`)
-   Additional paths configured via `options.skills_paths`

{
  "$schema": "https://charm.land/crush.json",
  "options": {
    "skills\_paths": \[
      "~/.config/crush/skills", // Windows: "%LOCALAPPDATA%\\\\crush\\\\skills",
      "./project-skills"
    \]
  }
}

You can get started with example skills from anthropics/skills:

# Unix
mkdir -p ~/.config/crush/skills
cd ~/.config/crush/skills
git clone https://github.com/anthropics/skills.git \_temp
mv \_temp/skills/\* . && rm -rf \_temp

# Windows (PowerShell)
mkdir \-Force "$env:LOCALAPPDATA\\crush\\skills"
cd "$env:LOCALAPPDATA\\crush\\skills"
git clone https://github.com/anthropics/skills.git \_temp
mv \_temp/skills/\* . ; rm \-r \-force \_temp

### Initialization

When you initialize a project, Crush analyzes your codebase and creates a context file that helps it work more effectively in future sessions. By default, this file is named `AGENTS.md`, but you can customize the name and location with the `initialize_as` option:

{
  "$schema": "https://charm.land/crush.json",
  "options": {
    "initialize\_as": "AGENTS.md"
  }
}

This is useful if you prefer a different naming convention or want to place the file in a specific directory (e.g., `CRUSH.md` or `docs/LLMs.md`). Crush will fill the file with project-specific context like build commands, code patterns, and conventions it discovered during initialization.

### Attribution Settings

By default, Crush adds attribution information to Git commits and pull requests it creates. You can customize this behavior with the `attribution` option:

{
  "$schema": "https://charm.land/crush.json",
  "options": {
    "attribution": {
      "trailer\_style": "co-authored-by",
      "generated\_with": true
    }
  }
}

-   `trailer_style`: Controls the attribution trailer added to commit messages (default: `assisted-by`)
    -   `assisted-by`: Adds `Assisted-by: [Model Name] via Crush <crush@charm.land>` (includes the model name)
    -   `co-authored-by`: Adds `Co-Authored-By: Crush <crush@charm.land>`
    -   `none`: No attribution trailer
-   `generated_with`: When true (default), adds `💘 Generated with Crush` line to commit messages and PR descriptions

### Custom Providers

Crush supports custom provider configurations for both OpenAI-compatible and Anthropic-compatible APIs.

Note

Note that we support two "types" for OpenAI. Make sure to choose the right one to ensure the best experience!

-   `openai` should be used when proxying or routing requests through OpenAI.
-   `openai-compat` should be used when using non-OpenAI providers that have OpenAI-compatible APIs.

#### OpenAI-Compatible APIs

Here’s an example configuration for Deepseek, which uses an OpenAI-compatible API. Don't forget to set `DEEPSEEK_API_KEY` in your environment.

{
  "$schema": "https://charm.land/crush.json",
  "providers": {
    "deepseek": {
      "type": "openai-compat",
      "base\_url": "https://api.deepseek.com/v1",
      "api\_key": "$DEEPSEEK\_API\_KEY",
      "models": \[
        {
          "id": "deepseek-chat",
          "name": "Deepseek V3",
          "cost\_per\_1m\_in": 0.27,
          "cost\_per\_1m\_out": 1.1,
          "cost\_per\_1m\_in\_cached": 0.07,
          "cost\_per\_1m\_out\_cached": 1.1,
          "context\_window": 64000,
          "default\_max\_tokens": 5000
        }
      \]
    }
  }
}

#### Anthropic-Compatible APIs

Custom Anthropic-compatible providers follow this format:

{
  "$schema": "https://charm.land/crush.json",
  "providers": {
    "custom-anthropic": {
      "type": "anthropic",
      "base\_url": "https://api.anthropic.com/v1",
      "api\_key": "$ANTHROPIC\_API\_KEY",
      "extra\_headers": {
        "anthropic-version": "2023-06-01"
      },
      "models": \[
        {
          "id": "claude-sonnet-4-20250514",
          "name": "Claude Sonnet 4",
          "cost\_per\_1m\_in": 3,
          "cost\_per\_1m\_out": 15,
          "cost\_per\_1m\_in\_cached": 3.75,
          "cost\_per\_1m\_out\_cached": 0.3,
          "context\_window": 200000,
          "default\_max\_tokens": 50000,
          "can\_reason": true,
          "supports\_attachments": true
        }
      \]
    }
  }
}

### Amazon Bedrock

Crush currently supports running Anthropic models through Bedrock, with caching disabled.

-   A Bedrock provider will appear once you have AWS configured, i.e. `aws configure`
-   Crush also expects the `AWS_REGION` or `AWS_DEFAULT_REGION` to be set
-   To use a specific AWS profile set `AWS_PROFILE` in your environment, i.e. `AWS_PROFILE=myprofile crush`
-   Alternatively to `aws configure`, you can also just set `AWS_BEARER_TOKEN_BEDROCK`

### Vertex AI Platform

Vertex AI will appear in the list of available providers when `VERTEXAI_PROJECT` and `VERTEXAI_LOCATION` are set. You will also need to be authenticated:

gcloud auth application-default login

To add specific models to the configuration, configure as such:

{
  "$schema": "https://charm.land/crush.json",
  "providers": {
    "vertexai": {
      "models": \[
        {
          "id": "claude-sonnet-4@20250514",
          "name": "VertexAI Sonnet 4",
          "cost\_per\_1m\_in": 3,
          "cost\_per\_1m\_out": 15,
          "cost\_per\_1m\_in\_cached": 3.75,
          "cost\_per\_1m\_out\_cached": 0.3,
          "context\_window": 200000,
          "default\_max\_tokens": 50000,
          "can\_reason": true,
          "supports\_attachments": true
        }
      \]
    }
  }
}

### Local Models

Local models can also be configured via OpenAI-compatible API. Here are two common examples:

#### Ollama

{
  "providers": {
    "ollama": {
      "name": "Ollama",
      "base\_url": "http://localhost:11434/v1/",
      "type": "openai-compat",
      "models": \[
        {
          "name": "Qwen 3 30B",
          "id": "qwen3:30b",
          "context\_window": 256000,
          "default\_max\_tokens": 20000
        }
      \]
    }
  }
}

#### LM Studio

{
  "providers": {
    "lmstudio": {
      "name": "LM Studio",
      "base\_url": "http://localhost:1234/v1/",
      "type": "openai-compat",
      "models": \[
        {
          "name": "Qwen 3 30B",
          "id": "qwen/qwen3-30b-a3b-2507",
          "context\_window": 256000,
          "default\_max\_tokens": 20000
        }
      \]
    }
  }
}

Logging
-------

Sometimes you need to look at logs. Luckily, Crush logs all sorts of stuff. Logs are stored in `./.crush/logs/crush.log` relative to the project.

The CLI also contains some helper commands to make perusing recent logs easier:

# Print the last 1000 lines
crush logs

# Print the last 500 lines
crush logs --tail 500

# Follow logs in real time
crush logs --follow

Want more logging? Run `crush` with the `--debug` flag, or enable it in the config:

{
  "$schema": "https://charm.land/crush.json",
  "options": {
    "debug": true,
    "debug\_lsp": true
  }
}

Provider Auto-Updates
---------------------

By default, Crush automatically checks for the latest and greatest list of providers and models from Catwalk, the open source Crush provider database. This means that when new providers and models are available, or when model metadata changes, Crush automatically updates your local configuration.

### Disabling automatic provider updates

For those with restricted internet access, or those who prefer to work in air-gapped environments, this might not be want you want, and this feature can be disabled.

To disable automatic provider updates, set `disable_provider_auto_update` into your `crush.json` config:

{
  "$schema": "https://charm.land/crush.json",
  "options": {
    "disable\_provider\_auto\_update": true
  }
}

Or set the `CRUSH_DISABLE_PROVIDER_AUTO_UPDATE` environment variable:

export CRUSH\_DISABLE\_PROVIDER\_AUTO\_UPDATE=1

### Manually updating providers

Manually updating providers is possible with the `crush update-providers` command:

# Update providers remotely from Catwalk.
crush update-providers

# Update providers from a custom Catwalk base URL.
crush update-providers https://example.com/

# Update providers from a local file.
crush update-providers /path/to/local-providers.json

# Reset providers to the embedded version, embedded at crush at build time.
crush update-providers embedded

# For more info:
crush update-providers --help

Metrics
-------

Crush records pseudonymous usage metrics (tied to a device-specific hash), which maintainers rely on to inform development and support priorities. The metrics include solely usage metadata; prompts and responses are NEVER collected.

Details on exactly what’s collected are in the source code (here and here).

You can opt out of metrics collection at any time by setting the environment variable by setting the following in your environment:

export CRUSH\_DISABLE\_METRICS=1

Or by setting the following in your config:

{
  "options": {
    "disable\_metrics": true
  }
}

Crush also respects the `DO_NOT_TRACK` convention which can be enabled via `export DO_NOT_TRACK=1`.

Contributing
------------

See the contributing guide.

Whatcha think?
--------------

We’d love to hear your thoughts on this project. Need help? We gotchu. You can find us on:

-   Twitter
-   Slack
-   Discord
-   The Fediverse
-   Bluesky

License
-------

FSL-1.1-MIT

* * *

Part of Charm.

Charm热爱开源 • Charm loves open source
