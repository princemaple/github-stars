---
project: crush
stars: 27584
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

On illumos (OpenIndiana, OmniOS), the command above works as-is. Only native OS notifications are unavailable there; terminal-based notifications (OSC) and the terminal bell still work. On Oracle Solaris, add `-tags sqlite3_dotlk` so the local database uses dot-file locking:

```
go install -tags sqlite3_dotlk github.com/charmbracelet/crush@latest
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

Crush ships with a builtin skill for configuring itself. Most of the time you can just tell what you want it to configure and it will get the job done.

Crush runs great with no configuration. That said, if you do need or want to customize Crush, you can, with a `crushrc`.

A `crushrc` is just Bash with some Crush-specific builtins. It’s a lot like a `.bashrc`, just for your Crush. Because Crush has a native, built-in Bash interpreter, Bash-based config works identically across all platforms, including Windows.

For example:

# Add Ollama.
provider add ollama --type ollama --base-url "http://localhost:11434/v1"

# Register a model on Ollama.
model add ollama/llama3.3 --name "Llama 3.3" --context-window 128000

# Auto-approve some tools.
permissions allow view edit

# Include some other file on a specific machine.
if \[\[ $HOSTNAME \== "babysquid" \]\]; then
    source ~/my-stuff/babysquid.sh
fi

# Add an MCP server, with a GitHub API token stored in 1password.
mcp add github \\
  --type http \\
  --url "https://api.githubcopilot.com/mcp/" \\
  --header Authorization "Bearer $(op read 'op://my-secret-key')"

Configuration can be added either local to the project itself, or globally, with the following priority:

Priority

Unix-like

Windows

1

`./.crushrc`

`.\.crushrc`

2

`./crushrc`

`.\crushrc`

3

`~/.config/crush/crushrc`

`%USERPROFILE%\.config\crush\crushrc`

(Crush respects the XDG Base Directory Specification, so your paths may differ depending on your `XDG_CONFIG_HOME` value. Data directories such as `~/.local/share/crush` and `%LOCALAPPDATA%\crush` contain JSON state only; Crush does not execute a `crushrc` from them.)

What about the old JSON format? It’s still supported, but it should be consdiered deprecated. See: the config docs for details.

Tip

You can override the user and data config locations by setting:

-   `CRUSH_GLOBAL_CONFIG`
-   `CRUSH_GLOBAL_DATA`

As an additional note, Crush also stores ephemeral data, such as application state, in one additional location. This is state and should not be edited by hand, nor should it be considered configuration.

# Unix
$HOME/.local/share/crush/crush.json

# Windows
%LOCALAPPDATA%\\crush\\crush.json

#### A note on security

Both `crushrc` and `crush.json` are trusted code; `crushrc` runs in a full shell, and any `$(...)` in `crush.json` runs at load time. Don't launch Crush in a directory whose config you haven't reviewed, and don't randomly `source` files from the internet into your config.

### Environment Variables

The top-level `env` field sets environment variables at startup, before providers are configured. This is useful for variables that affect provider authentication (e.g. the AWS SDK credential chain) without wrapping the `crush` command in a shell script or exporting them in your shell profile:

{
  "$schema": "https://charm.land/crush.json",
  "env": {
    "AWS\_PROFILE": "my-sso-profile"
  }
}

Values support the same `$VAR` and `$(command)` expansion as other config fields, so you can reference existing environment variables or shell out for a value.

### LSPs

Crush can use LSPs for additional context to help inform its decisions, just like you would. LSPs can be added manually like so:

# crushrc

lsp add go --command "gopls" --env "GOTOOLCHAIN go1.24.5"
lsp add typescript --command "typescript-language-server" --args --stdio
lsp add nix --command "nil"

### MCPs

Crush also supports Model Context Protocol (MCP) servers through three transport types: `stdio` for command-line servers, `http` for HTTP endpoints, and `sse` for Server-Sent Events.

# crushrc

# Add a local MCP server that runs a Node.js script.
mcp add filesystem --command node --args /path/to/mcp-server.js \\
  --timeout 10 --disabled-tools some-tool-name --env NODE\_ENV production

# Add a GitHub MCP server that uses an API token.
mcp add github --type http --url "https://api.githubcopilot.com/mcp/" \\
  --timeout 10 --header Authorization "Bearer $GH\_PAT" \\
  --disabled-tools create\_issue --disabled-tools create\_pull\_request

# Add a streaming MCP server that uses SSE.
mcp add streaming-service --type sse --url "https://example.com/mcp/sse" \\
  --timeout 10 --header API-Key "$API\_KEY"

#### MCP OAuth

HTTP and SSE MCP servers that require OAuth can use Crush's built-in authorization-code flow instead of a static `Authorization` header. Set `"oauth": true` to enable it:

{
  "mcp": {
    "linear": {
      "type": "http",
      "url": "https://mcp.linear.app/mcp",
      "oauth": true
    }
  }
}

##### Pre-registered clients

Some servers (GitHub, Slack) don't support dynamic client registration. For those, register an OAuth app with the provider and supply the credentials directly. All values support shell expansion:

{
  "mcp": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/",
      "oauth": true,
      "oauth\_client\_id": "Iv1.abc123def456",
      "oauth\_client\_secret": "$GITHUB\_MCP\_SECRET",
      "oauth\_callback\_port": 40704
    }
  }
}

When `oauth_client_id` is set, Crush skips dynamic client registration and authenticates as the specified client. When omitted, Crush attempts dynamic registration automatically (works with Linear, Notion, and other servers that support RFC 7591).

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

Crush automatically includes two files for cross-project instructions. Think of these are personal additions to the system prompt.

-   `~/.config/crush/CRUSH.md`: Crush-specific rules that would confuse other agentic coding tools. If you only use Crush, this is the only one you need to edit.
-   `~/.config/AGENTS.md`: generic instructions that other coding tools might read. Avoid referring to Crush-specific features or workflows here. You probably only care about this if you use multiple agentic coding tools and want to share instructions between them.

You can customize these paths with `option global-context-path`. Repeat the command to add multiple paths:

# Load a single markdown file.
option global-context-path "~/path/to/custom/context/file.md"

# Recursively load all Markdown files in the folder.
option global-context-path "/full/path/to/folder/of/files/"

### Ignoring Files

Crush respects `.gitignore` files by default, but you can also create a `.crushignore` file to specify additional files and directories that Crush should ignore. This is useful for excluding files that you want in version control but don't want Crush to consider when providing context.

The `.crushignore` file uses the same syntax as `.gitignore` and can be placed in the root of your project or in subdirectories.

### Allowing Tools

By default, Crush will ask you for permission before running tool calls. If you'd like, you can allow tools to be executed without prompting you for permissions. Use this with care.

permissions allow view ls grep edit mcp\_context7\_get-library-doc

### Disabling Built-In Tools

You can also deny tools, hiding then from the agent entirely:

permissions deny bash sourcegraph

To disable tools from MCP servers, see the MCP config section.

### You only live once

You can also skip all permission prompts completely by running Crush with the `--yolo` flag. Be very, very careful with this feature.

### Disabling Skills

You can prevent Crush from using certain skills entirely. Disabled skills are hidden from the agent, including builtin skills and skills discovered from disk.

option disable-skill crush-config

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

Or load directories of skills specifically in your config:

option skill-path "$HOME/squid-skills" "./other-skills"

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

Skills can be made invocable as commands from the commands palette (ctrl+p). Add `user-invocable: true` to the skill's YAML frontmatter:

\---
name: my-hot-skill
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

# Choose auto, native, osc, bell, or disabled.
option notifications disabled

`auto` uses native notifications locally and OSC notifications over SSH when supported.

### Initialization

When you initialize a project, Crush analyzes your codebase and creates a context file that helps it work more effectively in future sessions. By default, this file is named `AGENTS.md`, but you can customize the name and location with the `initialize-as` option:

# crushrc
option initialize-as AGENTS.md

This is useful if you prefer a different naming convention or want to place the file in a specific directory (e.g., `CRUSH.md` or `docs/LLMs.md`). Crush will fill the file with project-specific context like build commands, code patterns, and conventions it discovered during initialization.

### Attribution Settings

By default, Crush adds attribution information to Git commits and pull requests it creates. You can customize this behavior with `option` commands:

option attribution-trailer-style co-authored-by
option attribution-generated-with true

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

provider add deepseek --type openai-compat \\
  --base-url "https://api.deepseek.com/v1" \\
  --api-key "$DEEPSEEK\_API\_KEY"

model add deepseek/deepseek-chat \\
  --name "Deepseek V3" \\
  --context-window 64000 \\
  --default-max-tokens 5000 \\
  --price-input 0.27 \\
  --price-output 1.1 \\
  --price-cache-create 1.1 \\
  --price-cache-hit 0.07

#### Anthropic-Compatible APIs

Custom Anthropic-compatible providers follow this format:

provider add custom-anthropic \\
  --type anthropic \\
  --base-url "https://api.anthropic.com/v1" \\
  --api-key "$ANTHROPIC\_API\_KEY" \\
  --extra-header anthropic-version 2023-06-01

model add custom-anthropic/claude-sonnet-4-20250514 \\
  --name "Claude Sonnet 4" \\
  --context-window 200000 \\
  --default-max-tokens 50000 \\
  --can-reason true \\
  --supports-images true \\
  --price-input 3 \\
  --price-output 15 \\
  --price-cache-create 3.75 \\
  --price-cache-hit 0.3

### Amazon Bedrock

Crush currently supports running Anthropic models through Bedrock, with caching disabled.

A Bedrock provider appears once Crush can find AWS credentials. You can authenticate in one of two ways:

**API key.** Set `AWS_BEARER_TOKEN_BEDROCK` to a Bedrock API key. This is the simplest option and never expires mid-session.

**AWS credential chain (SSO, profiles, access keys).** Configure AWS the usual way with `aws configure` or `aws configure sso`. Crush picks up whatever the AWS SDK credential chain resolves, including `AWS_PROFILE`, `AWS_ACCESS_KEY_ID` / `AWS_SECRET_ACCESS_KEY`, or an SSO session. To select a specific profile, set `AWS_PROFILE` in your shell (`AWS_PROFILE=myprofile crush`) or in the top-level `env` config.

If you authenticate via AWS SSO, your session expires periodically. Set `aws_auth_refresh` to a command that refreshes it. When Bedrock returns a credential error, Crush runs the command, then retries the request in place (no duplicate messages, no manual restart):

{
  "$schema": "https://charm.land/crush.json",
  "env": {
    "AWS\_PROFILE": "my-sso-profile"
  },
  "providers": {
    "bedrock": {
      "aws\_auth\_refresh": "aws sso login --profile my-sso-profile"
    },
    "bedrock-europe": {
      "aws\_auth\_refresh": "aws sso login --profile my-eu-sso-profile"
    }
  }
}

-   `aws_auth_refresh` — shell command run when AWS credentials expire (e.g. `aws sso login`)

### Vertex AI Platform

Vertex AI will appear in the list of available providers when `VERTEXAI_PROJECT` and `VERTEXAI_LOCATION` are set. You will also need to be authenticated:

$ gcloud auth application-default login

To add specific models to the configuration, configure as such:

# crushrc — authentication still comes from gcloud and the VERTEXAI\_\* env vars.
provider add vertexai --type google-vertex

model add vertexai/claude-sonnet-4@20250514 \\
  --name "VertexAI Sonnet 4" \\
  --context-window 200000 \\
  --default-max-tokens 50000 \\
  --can-reason true \\
  --supports-images true \\
  --price-input 3 \\
  --price-output 15 \\
  --price-cache-create 3.75 \\
  --price-cache-hit 0.3

### Local Models

Crush can auto-discovers models from local providers. Add a custom provider with `type` set to `llamacpp`, `omlx`, `lmstudio`, `litellm`, or `ollama` and leave out the models list. Crush will populate the model list automatically.

# Piece of cake.
provider add ollama \\
  --name Ollama \\
  --type ollama \\
  --base-url "http://localhost:11434/v1/"

For llama.cpp (`llama-server`), point at the server's base URL:

provider add llamacpp \\
  --name "llama.cpp" \\
  --type llamacpp \\
  --base-url "http://localhost:2222"

#### Manual Model Configuration

You can still list models explicitly. User-defined models always take precedence over discovered ones, and any fields you set won't be overwritten by auto-discovery. Auto discovery will run if the model list is empty for any `openai-compat` provider or if you pass `"discover_models": true` it will merge the found models with your hand configured ones.

# crushrc
provider add ollama \\
  --name Ollama \\
  --type ollama \\
  --base-url "http://localhost:11434/v1/" \\
  --discover-models true

model add ollama/qwen3:30b \\
  --name "Qwen 3 30B" \\
  --context-window 256000 \\
  --default-max-tokens 20000

The `--discover-models true` flag merges discovered models with the one above; your explicit model fields win on conflicts.

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

Want more logging? Run `crush` with the `--debug` flag, or enable it in your `crushrc`:

# crushrc
option debug true
option debug-lsp true

Provider Auto-Updates
---------------------

By default, Crush automatically checks for the latest and greatest list of providers and models from Catwalk, the open source Crush provider database. This means that when new providers and models are available, or when model metadata changes, Crush automatically updates your local configuration.

### Disabling automatic provider updates

For those with restricted internet access, or those who prefer to work in air-gapped environments, this might not be want you want, and this feature can be disabled.

To disable automatic provider updates in your `crushrc`:

option provider-auto-update false

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
