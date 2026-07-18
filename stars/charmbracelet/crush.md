---
project: crush
stars: 26605
description: Glamourous agentic coding for all 💘
url: https://github.com/charmbracelet/crush
---

Crush
=====

  

Your new coding bestie, now available in your favourite terminal.  
Your tools, your code, and your workflows, wired into your LLM of choice.

终端里的编程新搭档，  
无缝接入你的工具、代码与工作流，全面兼容主流 LLM 模型。

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

Productivity may increase when using Crush and you may find yourself nerd sniped when first using the application. If the symptoms persist, join the Slack or Discord and nerd snipe the rest of us.

Getting Started
---------------

The quickest way to get started is to choose a Hyper model from model picker. Follow the steps to authenticate and you'll be good to go.

Hyper, from Charm, is the official Crush provider. It’s subscription-based, with a free tier, and optimized for Crush. It’s privacy focused, with zero data retention (ZDR) is and designed to comply with GDPR. More on Hyper.

API Keys
--------

You can also use Crush with many other providers such as Anthopic, OpenAI, Gemini, OpenRouter and so on. Press ctrl+l to open the model picker, choose the provider of your choice, and paste your API key.

That said, you can also set environment variables for preferred providers:

Environment Variable

Provider

`HYPER_API_KEY`

Charm Hyper

`ANTHROPIC_API_KEY`

Anthropic

`OPENAI_API_KEY`

OpenAI

`VERCEL_API_KEY`

Vercel AI Gateway

`GEMINI_API_KEY`

Google Gemini

`ZAI_API_KEY`

Z.ai

`MINIMAX_API_KEY`

MiniMax

`SYNTHETIC_API_KEY`

Synthetic

`HF_TOKEN`

Hugging Face Inference

`CEREBRAS_API_KEY`

Cerebras

`OPENROUTER_API_KEY`

OpenRouter

`IONET_API_KEY`

io.net

`ALIBABA_SINGAPORE_API_KEY`

Alibaba (Singapore)

`ALIBABA_US_API_KEY`

Alibaba (United States)

`GROQ_API_KEY`

Groq

`AVIAN_API_KEY`

Avian

`OPENCODE_API_KEY`

OpenCode Zen & Go

`VERTEXAI_PROJECT`

Google Cloud VertexAI (Gemini)

`VERTEXAI_LOCATION`

Google Cloud VertexAI (Gemini)

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

`MOONSHOT_API_KEY`

Moonshot

Also note that Crush can support nearly any provider, including Local Models. For more info see Custom Providers below.

### By the Way

Is there a provider you’d like to see in Crush? Is there an existing model that needs an update?

Crush’s default model listing is managed in Catwalk, a community-supported, open source repository of Crush-compatible models, and you’re welcome to contribute.

Configuration
-------------

Tip

Crush ships with a builtin `crush-config` skill for configuring itself. In many cases you can simply ask Crush to configure itself.

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

Crush also supports Model Context Protocol (MCP) servers through three transport types: `stdio` for command-line servers, `http` for HTTP endpoints, and `sse` for Server-Sent Events.

Shell-style value expansion (`$VAR`, `${VAR:-default}`, `$(command)`, quoting, nesting) works in `command`, `args`, `env`, `headers`, and `url`, so file-based secrets work out of the box. You can use values like `"$TOKEN"` or `"$(cat /path/to/secret/token)"`. Expansion runs through Crush's embedded shell, so the same syntax works on every supported system, Windows included.

Unset variables expand to the empty string by default, matching bash. For required credentials, use `${VAR:?message}` so an unset variable fails loudly at load time with `message` instead of silently resolving to empty:

{ "api\_key": "${CODEBERG\_TOKEN:?set CODEBERG\_TOKEN}" }

Headers (both MCP `headers` and provider `extra_headers`) whose value resolves to the empty string are dropped from the outgoing request rather than sent as `Header:`. That keeps optional env-gated headers like `"OpenAI-Organization": "$OPENAI_ORG_ID"` clean when the variable is unset.

Provider `extra_body` is a non-expanding JSON passthrough; put env-driven values in `extra_headers` or the provider's `api_key` / `base_url`, all of which do expand.

> **Security note:** `crush.json` is trusted code. Any `$(...)` in it runs at load time with your shell's privileges, before the UI appears. Don't launch Crush in a directory whose `crush.json` you haven't reviewed.

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

### Hooks

Crush has preliminary support for hooks. For details, see the hook guide.

### Sharing a workspace across clients

When Crush is run against a shared backend (for example two TUIs talking to the same `crush serve`), clients are grouped into **workspaces** keyed by their resolved `--cwd`. Two clients with the same `--cwd` join the same underlying workspace, so they share the session list, message history, permission queue, LSP, and MCP state.

Joining is implicit: pointing a second client at the same working directory attaches it to the existing workspace. Each new invocation, however, starts in its own fresh session by default. To pick up the conversation another client already has open, use the session manager (the session picker) and select it. Sessions surface two signals there:

-   `IsBusy` is set while an agent turn is in flight for that session.
-   `AttachedClients` reports how many clients are currently viewing it.

A non-zero `AttachedClients` (often combined with `IsBusy`) is the cue that a session is "in progress" on another client and joining it will mirror that view live.

The first client to create a workspace fixes its process-wide flags. In particular, `--yolo` and `--debug` follow a **first-wins** rule: later clients that arrive at the same `--cwd` with different values for those flags do not change the running workspace. A debug log line is emitted recording the mismatch, and the workspace keeps the flags it was created with.

A workspace lives as long as at least one client has an SSE event stream open against it. When the last stream disconnects, the workspace is torn down. There is a short grace window right after `POST /v1/workspaces` so a client that has created the workspace but not yet opened its event stream does not get reaped before it can attach.

### Global context files

Crush automatically includes two files for cross-project instructions.

-   `~/.config/crush/CRUSH.md`: Crush-specific rules that would confuse other agentic coding tools. If you only use Crush, this is the only one you need to edit.
-   `~/.config/AGENTS.md`: generic instructions that other coding tools might read. Avoid referring to Crush-specific features or workflows here. You probably only care about this if you use multiple agentic coding tools and want to share instructions between them.

You can customize these paths using the `global_context_paths` option in your configuration:

{
  "$schema": "https://charm.land/crush.json",
  "options": {
    "global\_context\_paths": \[
      "~/path/to/custom/context/file.md",
      "/full/path/to/folder/of/files/" // recursively load all .md files in folder
    \]
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
    "disabled\_tools": \["bash", "sourcegraph"\]
  }
}

To disable tools from MCP servers, see the MCP config section.

### Disabling Skills

If you'd like to prevent Crush from using certain skills entirely, you can disable them via the `options.disabled_skills` list. Disabled skills are hidden from the agent, including builtin skills and skills discovered from disk.

{
  "$schema": "https://charm.land/crush.json",
  "options": {
    "disabled\_skills": \["crush-config"\]
  }
}

### Agent Skills

Crush supports the Agent Skills open standard for extending agent capabilities with reusable skill packages. Skills are folders containing a `SKILL.md` file with instructions that Crush can discover and activate on demand.

The global paths we looks for skills are:

-   `$CRUSH_SKILLS_DIR`
-   `$XDG_CONFIG_HOME/agents/skills` or `~/.config/agents/skills/`
-   `$XDG_CONFIG_HOME/crush/skills` or `~/.config/crush/skills/`
-   `~/.agents/skills/`
-   `~/.claude/skills/`
-   On Windows, we _also_ look at
    -   `%LOCALAPPDATA%\agents\skills\` or `%USERPROFILE%\AppData\Local\agents\skills\`
    -   `%LOCALAPPDATA%\crush\skills\` or `%USERPROFILE%\AppData\Local\crush\skills\`
-   Additional paths configured via `options.skills_paths`

On top of that, we _also_ load skills in your project from the following relative paths:

-   `.agents/skills`
-   `.crush/skills`
-   `.claude/skills`
-   `.cursor/skills`

{
  "$schema": "https://charm.land/crush.json",
  "options": {
    "skills\_paths": \[
      "~/.config/crush/skills", // Windows: "%LOCALAPPDATA%\\\\crush\\\\skills",
      "./project-skills",
    \],
  },
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

#### User-Invocable Skills

Skills can be made invocable as commands from the commands palette (Ctrl+P). Add `user-invocable: true` to the skill's YAML frontmatter:

\---
name: my-skill
description: A skill that can be invoked as a command.
user-invocable: true
---

User-invocable skills appear in the commands palette with a `user:` or `project:` prefix:

-   Skills from global directories show as `user:skill-name`
-   Skills from project directories show as `project:skill-name`

When invoked, the skill's instructions are loaded into the conversation context.

To prevent the model from auto-triggering a skill (while still allowing user invocation), add `disable-model-invocation: true`:

\---
name: my-skill
description: Only invocable by users, not the model.
user-invocable: true
disable-model-invocation: true
---

Skills with `disable-model-invocation` won't appear in the model's available skills list but can still be invoked manually by users.

### Desktop notifications

Crush sends desktop notifications when a tool call requires permission and when the agent finishes its turn. They're only sent when the terminal window isn't focused _and_ your terminal supports reporting the focus state.

{
  "$schema": "https://charm.land/crush.json",
  "options": {
    "disable\_notifications": false, // default
  },
}

To disable desktop notifications, set `disable_notifications` to `true` in your configuration. On macOS, notifications currently lack icons due to platform limitations.

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
    -   `assisted-by`: Adds `Assisted-by: Crush:[ModelID]` as specified in the convention
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

Crush can auto-discovers models from local providers. Add a custom provider with `type` set to `llamacpp`, `omlx`, `lmstudio`, `litellm`, or `ollama` and leave out the models list. Crush will populate the model list automatically.

{
  "providers": {
    "ollama": {
      "name": "Ollama",
      "base\_url": "http://localhost:11434/v1/",
      "type": "ollama"
    }
  }
}

For llama.cpp (`llama-server`), point at the server's base URL:

{
  "providers": {
    "llamacpp": {
      "name": "llama.cpp",
      "base\_url": "http://localhost:2222",
      "type": "llamacpp"
    }
  }
}

#### Manual Model Configuration

You can still list models explicitly. User-defined models always take precedence over discovered ones, and any fields you set won't be overwritten by auto-discovery. Auto discovery will run if the model list is empty for any `openai-compat` provider or if you pass `"discover_models": true` it will merge the found models with your hand configured ones.

{
  "providers": {
    "ollama": {
      "name": "Ollama",
      "base\_url": "http://localhost:11434/v1/",
      "type": "ollama",
      "models": \[
        {
          "name": "Qwen 3 30B",
          "id": "qwen3:30b",
          "context\_window": 256000,
          "default\_max\_tokens": 20000
        }
      \],
      "discover\_models": true
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

Q&A
---

### Why is clipboard copy and paste not working?

Installing an extra tool might be needed on Unix-like environments.

Environment

Tool

Windows

Native support

macOS

Native support

Linux/BSD + Wayland

`wl-copy` and `wl-paste`

Linux/BSD + X11

`xclip` or `xsel`

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
