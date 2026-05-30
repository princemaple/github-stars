---
project: shimmy
stars: 5294
description: ⚡ Python-free Rust inference server — OpenAI-API compatible. GGUF + SafeTensors, hot model swap, auto-discovery, single binary. FREE now, FREE forever.
url: https://github.com/Michael-A-Kuykendall/shimmy
---

The Lightweight OpenAI API Server
=================================

### 🔒 Local Inference Without Dependencies 🚀

**Languages:** 简体中文 · 繁體中文

**Shimmy will be free forever.** No asterisks. No "free for now." No pivot to paid.

### 💝 Support Shimmy's Growth

🚀 **If Shimmy helps you, consider sponsoring — 100% of support goes to keeping it free forever.**

-   **$5/month**: Coffee tier ☕ - Eternal gratitude + sponsor badge
-   **$25/month**: Bug prioritizer 🐛 - Priority support + name in SPONSORS.md
-   **$100/month**: Corporate backer 🏢 - Logo placement + monthly office hours
-   **$500/month**: Infrastructure partner 🚀 - Direct support + roadmap input

**🎯 Become a Sponsor** | See our amazing sponsors 🙏

* * *

Table of Contents
-----------------

-   What Is Shimmy?
-   🔥 Airframe Engine (v2.0)
-   🎯 Supported Models
-   📦 Migrating from v1.x
-   ⚡ Quick Start (30 seconds)
-   🚀 OpenAI SDK Compatibility
-   🔧 Extended Context
-   📥 Download & Install
-   🔗 Integration Examples
-   📖 API Reference
-   ❓ FAQ
-   🏛️ Technical Architecture
-   📚 Documentation Hub
-   🌍 Community & Support
-   ⚡ Performance
-   License

* * *

Drop-in OpenAI API Replacement for Local LLMs
---------------------------------------------

Shimmy is a **single-binary** that provides **100% OpenAI-compatible endpoints** for GGUF models. Point your existing AI tools to Shimmy and they just work — locally, privately, and free.

**🎉 NEW in v2.0.0**: Shimmy now runs on Airframe, a pure-Rust WGSL GPU engine. No C++ toolchain, no backend flags, no compilation required.

🔥 Airframe Engine
------------------

Starting in v2.0.0, Shimmy's default inference engine is **Airframe** — a pure-Rust WebGPU (WGSL) transformer runtime built from scratch.

**Why this matters:**

-   No C++ toolchain required — Rust only, top to bottom
-   F32 precision throughout for deterministic, high-quality output
-   WGSL compute shaders work on any GPU via WebGPU (NVIDIA, AMD, Intel, integrated)
-   Model spec auto-derived from GGUF metadata — no hardcoded per-model constants
-   YaRN RoPE scaling for extended context via `SHIMMY_MAX_CTX` — engine allocates KV cache and sets RoPE scale automatically (see Extended Context below)

**Quick start with Airframe (v2.0.0+):**

# Default: 2048-token context
SHIMMY\_BASE\_GGUF=/path/to/TinyLlama-1.1B-Chat-v1.0.Q4\_0.gguf ./shimmy serve

# Extended context (4096 tokens — YaRN RoPE enabled automatically, KV cache resized)
SHIMMY\_BASE\_GGUF=/path/to/model.gguf SHIMMY\_MAX\_CTX=4096 ./shimmy serve

🎯 Supported Models
-------------------

Airframe v2.0 ships with GPU-verified support across **7 model architectures** and **5 quantization types**, covering the models most commonly run on consumer hardware. Context window is read directly from each model's GGUF metadata — no hardcoded limits.

### ✅ Locally Validated (GPU Math Verified)

Model

Architecture

Quant

Size

Context

Min VRAM

TinyLlama-1.1B-Chat-v1.0

Llama

Q4\_0

638 MB

2048

~800 MB

Llama-3.2-1B-Instruct

Llama

Q4\_K\_M

770 MB

131072\*

~1 GB

Llama-3.2-3B-Instruct

Llama

Q4\_K\_M

1.9 GB

131072\*

~2.5 GB

phi-2

Phi-2

Q4\_K\_M

1.7 GB

2048

~2.2 GB

gemma-2-2b-it

Gemma-2

Q4\_K\_M

1.6 GB

8192

~2 GB

starcoder2-3b

StarCoder2

Q4\_K\_M

1.8 GB

16384

~2.3 GB

gpt2

GPT-2

Q4\_K\_M

107 MB

1024

~200 MB

> \* Llama-3.2's native context is 131072 tokens. Airframe reads this from GGUF and allocates KV cache accordingly. Use `SHIMMY_MAX_CTX=8192` for a practical 8K window on consumer hardware (~256 MB KV cache for the 1B model).

**GPU Math Verified** means the Airframe GPU dequantization shader produces results matching the CPU reference implementation, independently confirmed for every tensor type in each model. This is done via `quant_verify`, which tests 512 elements per quantization type per model.

### ⏳ Roadmap — Larger Models (Require ≥16 GB VRAM)

Model

Architecture

Quant

Size

Status

deepseek-coder-6.7b-instruct

Llama

Q4\_K\_M

3.9 GB

Pending remote GPU validation

deepseek-llm-7b-chat

Llama

Q4\_K\_M

4.0 GB

Pending remote GPU validation

qwen2-7b-instruct

Qwen2

Q4\_K\_M

4.5 GB

Pending remote GPU validation

Phi-3.5-mini-instruct

Phi-3

Q4\_K\_M

2.3 GB

Requires fused QKV support (planned)

### ✅ Supported Quantization Types

Type

GGML ID

Notes

`F32`

0

Raw floats — maximum precision

`F16`

1

Half-precision floats

`Q4_0`

2

4-bit, 32-element blocks

`Q8_0`

8

8-bit, 32-element blocks

`Q4_K`

12

4-bit K-quant superblocks (256 elements) — used in Q4\_K\_M GGUFs

`Q5_K`

13

5-bit K-quant superblocks — used alongside Q4\_K in mixed-precision models

`Q6_K`

14

6-bit K-quant superblocks — typically used for output/embedding layers

All types are implemented in both the GPU inference shader and a CPU reference implementation. GPU vs CPU agreement is validated for every type.

**Auto-discovery is enabled.** If Shimmy finds GGUF models in your HuggingFace cache, Ollama directory, LM Studio cache (`~/.cache/lm-studio/models`), or local `./models/` folder, it will register and serve them automatically. See docs/MODEL\_EXPANSION.md for the full compatibility matrix.

📦 Migrating from v1.x
----------------------

The llama.cpp backend is **removed in v2.0.0**. The Airframe engine is the only inference path. See docs/MIGRATION\_v2.md for the step-by-step migration guide.

Developer Tools
---------------

Whether you're forking Shimmy or integrating it as a service, we provide complete documentation and integration templates.

### Try it in 30 seconds

# 1) Download pre-built binary
# Windows:
curl -L https://github.com/Michael-A-Kuykendall/shimmy/releases/latest/download/shimmy-windows-x86\_64.exe -o shimmy.exe
set SHIMMY\_BASE\_GGUF=C:\\path\\to\\model.gguf && ./shimmy.exe serve &

# Linux / macOS:
curl -L https://github.com/Michael-A-Kuykendall/shimmy/releases/latest/download/shimmy-linux-x86\_64 -o shimmy && chmod +x shimmy
SHIMMY\_BASE\_GGUF=/path/to/model.gguf ./shimmy serve &

# 2) See registered models
./shimmy list

# 3) Smoke test the OpenAI API
curl -s http://127.0.0.1:11435/v1/chat/completions \\
  -H 'Content-Type: application/json' \\
  -d '{
        "model":"tinyllama-1.1b",
        "messages":\[{"role":"user","content":"Say hi in 5 words."}\],
        "max\_tokens":32
      }' | jq -r '.choices\[0\].message.content'

🚀 Compatible with OpenAI SDKs and Tools
----------------------------------------

**No code changes needed** - just change the API endpoint:

-   **Any OpenAI client**: Python, Node.js, curl, etc.
-   **Development applications**: Compatible with standard SDKs
-   **VSCode Extensions**: Point to `http://localhost:11435`
-   **Cursor Editor**: Built-in OpenAI compatibility
-   **Continue.dev**: Drop-in model provider

### Use with OpenAI SDKs

-   Node.js (openai v4)

import OpenAI from "openai";

const openai \= new OpenAI({
  baseURL: "http://127.0.0.1:11435/v1",
  apiKey: "sk-local", // placeholder, Shimmy ignores it
});

const resp \= await openai.chat.completions.create({
  model: "REPLACE\_WITH\_MODEL",
  messages: \[{ role: "user", content: "Say hi in 5 words." }\],
  max\_tokens: 32,
});

console.log(resp.choices\[0\].message?.content);

-   Python (openai>=1.0.0)

from openai import OpenAI

client \= OpenAI(base\_url\="http://127.0.0.1:11435/v1", api\_key\="sk-local")

resp \= client.chat.completions.create(
    model\="REPLACE\_WITH\_MODEL",
    messages\=\[{"role": "user", "content": "Say hi in 5 words."}\],
    max\_tokens\=32,
)

print(resp.choices\[0\].message.content)

⚡ Zero Configuration Required
-----------------------------

-   **Automatically finds models** from Hugging Face cache, Ollama, LM Studio (`~/.cache/lm-studio/models`), and local dirs
-   **Auto-allocates ports** to avoid conflicts
-   **Auto-detects LoRA adapters** for specialized models
-   **Just works** - no config files, no setup wizards

🧠 Advanced MOE (Mixture of Experts) Support
--------------------------------------------

> **Note**: MoE (Mixture of Experts) CPU offloading is on the Airframe roadmap. See docs/AIRFRAME\_MOE\_ROADMAP.md for the implementation plan.

**Run 70B+ models on consumer hardware** — coming to the Airframe engine. Track progress on the roadmap.

**Perfect for**: Large models (70B+), limited VRAM systems, cost-effective inference

🎯 Perfect for Local Development
--------------------------------

-   **Privacy**: Your code never leaves your machine
-   **Cost**: No API keys, no per-token billing
-   **Speed**: Local inference, sub-second responses
-   **Reliability**: No rate limits, no downtime

Quick Start (30 seconds)
------------------------

### Installation

**v2.0.0**: Download pre-built binaries with Airframe WebGPU engine included!

#### **📥 Pre-Built Binaries (Recommended — Zero Dependencies)**

Pick your platform and download — no compilation needed, GPU acceleration included:

# Windows x64 (Airframe WebGPU engine)
curl -L https://github.com/Michael-A-Kuykendall/shimmy/releases/latest/download/shimmy-windows-x86\_64.exe -o shimmy.exe

# Linux x86\_64 (Airframe WebGPU engine)
curl -L https://github.com/Michael-A-Kuykendall/shimmy/releases/latest/download/shimmy-linux-x86\_64 -o shimmy && chmod +x shimmy

# macOS ARM64 (Airframe with Metal backend via wgpu)
curl -L https://github.com/Michael-A-Kuykendall/shimmy/releases/latest/download/shimmy-macos-arm64 -o shimmy && chmod +x shimmy

# macOS Intel
curl -L https://github.com/Michael-A-Kuykendall/shimmy/releases/latest/download/shimmy-macos-intel -o shimmy && chmod +x shimmy

# Linux ARM64 (huggingface engine; Airframe cross-compilation not yet supported)
curl -L https://github.com/Michael-A-Kuykendall/shimmy/releases/latest/download/shimmy-linux-aarch64 -o shimmy && chmod +x shimmy

**That's it!** The Airframe WebGPU adapter is selected automatically at runtime.

#### **🛠️ Build from Source / cargo install**

# Install from crates.io
cargo install shimmy

# Build from source (huggingface engine, no GPU)
git clone https://github.com/Michael-A-Kuykendall/shimmy
cd shimmy
cargo build --release

> **Note**: The Airframe GPU engine is a private dependency and **cannot be built from source** by public users. The pre-built release binaries already include Airframe compiled in — download those to get full GPU acceleration. `cargo install shimmy` installs the huggingface engine variant from crates.io.

### GPU Acceleration

**v2.0.0**: Airframe uses **WebGPU (wgpu)** for GPU acceleration. No backend flags, no driver installation beyond standard OS graphics drivers.

#### **📥 Download Pre-Built Binaries (Recommended)**

Release binaries include the Airframe engine with WebGPU support compiled in:

Platform

Download

GPU Backend

Notes

**Windows x64**

shimmy-windows-x86\_64.exe

WebGPU (wgpu)

NVIDIA, AMD, Intel

**Linux x86\_64**

shimmy-linux-x86\_64

WebGPU (wgpu)

NVIDIA, AMD, Intel

**macOS ARM64**

shimmy-macos-arm64

Metal (via wgpu)

Apple Silicon

**macOS Intel**

shimmy-macos-intel

Metal (via wgpu)

Intel Mac

**Linux ARM64**

shimmy-linux-aarch64

huggingface only

ARM cross-build

#### **🎯 How GPU Selection Works**

Airframe uses wgpu's adapter enumeration. On first launch it selects the best available GPU adapter for your system — discrete GPU preferred over integrated, integrated over CPU fallback. No configuration needed.

# Check selected adapter
shimmy gpu-info

# Start serving (GPU adapter auto-selected)
shimmy serve

#### **🔧 Extended Context**

`SHIMMY_MAX_CTX` overrides the context window at the engine level. When set above the model's native window, Airframe automatically engages YaRN RoPE scaling and resizes the KV cache accordingly.

# 4096-token context with YaRN (2x native window for TinyLlama)
SHIMMY\_BASE\_GGUF=/path/to/model.gguf SHIMMY\_MAX\_CTX=4096 shimmy serve

# 8192 tokens (4x native, higher RoPE compression)
SHIMMY\_BASE\_GGUF=/path/to/model.gguf SHIMMY\_MAX\_CTX=8192 shimmy serve

> **Note:** Extended context beyond 4096 is functional but not yet as deeply validated as the native 2048-token window. Accepted range is 512–131072. Values outside that range are silently ignored and 2048 is used.

#### **💾 VRAM Sizing Reference**

Airframe allocates VRAM at load time: **weights** + **KV cache**. The KV cache is F32 and scales linearly with context length (`n_layers × n_kv_heads × head_dim × ctx × 2 × 4 bytes`).

**TinyLlama 1.1B Q4\_0 — the v2.0 validated path:**

Context (`SHIMMY_MAX_CTX`)

KV cache

Weights

Total

Min VRAM

2048 (default)

~88 MB

~638 MB

~726 MB

**~800 MB**

4096

~176 MB

~638 MB

~814 MB

**~900 MB**

8192

~352 MB

~638 MB

~990 MB

**~1.1 GB**

16384

~704 MB

~638 MB

~1.3 GB

**~1.5 GB**

> Integrated graphics (Intel Iris, Apple M-series unified memory, AMD Vega) running at 2048 context is ~800 MB — comfortably inside the 2 GB allocation most integrated GPUs share with system RAM.

**Scaling up to larger models** (architecture and quant support required — see docs/MODEL\_EXPANSION.md):

Model

Quant

Weights

KV @ 2048 ctx

Min VRAM

Llama 3.2 1B

Q4\_0

~636 MB

~128 MB

~900 MB

Llama 3.2 3B

Q4\_0

~1.9 GB

~448 MB

~2.5 GB

Mistral 7B

Q4\_K\_M

~4.1 GB

~512 MB

~5 GB

Llama 3 8B

Q4\_K\_M

~4.7 GB

~512 MB

~5.5 GB

The KV cache formula for any model: `n_layers × n_kv_heads × head_dim × ctx × 2 × 4 bytes`. Multiply the 2048 baseline by your `SHIMMY_MAX_CTX` multiplier to get the extended context allocation.

### Get Models

Shimmy auto-discovers models from:

-   **Hugging Face cache**: `~/.cache/huggingface/hub/`
-   **Ollama models**: `~/.ollama/models/`
-   **Local directory**: `./models/`
-   **Environment**: `SHIMMY_BASE_GGUF=path/to/model.gguf`

# Primary validated model for Airframe v2.0
huggingface-cli download TheBloke/TinyLlama-1.1B-Chat-v1.0-GGUF \\
  --include "tinyllama-1.1b-chat-v1.0.Q4\_0.gguf" --local-dir ./models/

# Alternative 1B — also fits in the same hardware envelope
huggingface-cli download bartowski/Llama-3.2-1B-Instruct-GGUF \\
  --include "\*Q4\_K\_M\*" --local-dir ./models/

### Start Server

# Auto-allocates port to avoid conflicts
shimmy serve

# Or use manual port
shimmy serve --bind 127.0.0.1:11435

Point your development tools to the displayed port — VSCode Copilot, Cursor, Continue.dev all work instantly.

📦 Download & Install
---------------------

### Package Managers

-   **Rust**: `cargo install shimmy` _(installs huggingface engine; for Airframe GPU, use GitHub Releases binaries)_
-   **VS Code**: Shimmy Extension
-   **npm**: `npm install -g shimmy-js` _(planned)_
-   **Python**: `pip install shimmy` _(planned)_

### Direct Downloads

-   **GitHub Releases**: Latest binaries
-   **Docker**: `docker pull shimmy/shimmy:latest` _(coming soon)_

### 🍎 macOS Support

**Full compatibility confirmed!** Shimmy works on macOS with Metal GPU acceleration via wgpu.

# Install from crates.io (huggingface engine)
cargo install shimmy

# For Airframe GPU engine, download the macOS binary from GitHub Releases:
curl -L https://github.com/Michael-A-Kuykendall/shimmy/releases/latest/download/shimmy-macos-arm64 -o shimmy && chmod +x shimmy

**✅ Verified working:**

-   Intel and Apple Silicon Macs
-   Metal GPU acceleration via wgpu (automatic on Apple Silicon)
-   Xcode 17+ compatibility

Integration Examples
--------------------

### VSCode Copilot

{
  "github.copilot.advanced": {
    "serverUrl": "http://localhost:11435"
  }
}

### Continue.dev

{
  "models": \[{
    "title": "Local Shimmy",
    "provider": "openai",
    "model": "your-model-name",
    "apiBase": "http://localhost:11435/v1"
  }\]
}

### Cursor IDE

Works out of the box - just point to `http://localhost:11435/v1`

Why Shimmy Will Always Be Free
------------------------------

I built Shimmy to retain privacy-first control on my AI development and keep things local and lean.

**This is my commitment**: Shimmy stays MIT licensed, forever. If you want to support development, sponsor it. If you don't, just build something cool with it.

> 💡 **Shimmy saves you time and money. If it's useful, consider sponsoring for $5/month — less than your Netflix subscription, infinitely more useful for developers.**

API Reference
-------------

### Endpoints

-   `GET /health` - Health check
-   `POST /v1/chat/completions` - OpenAI-compatible chat (streaming supported)
-   `POST /v1/completions` - OpenAI-compatible text completions
-   `GET /v1/models` - List available models
-   `POST /api/generate` - Shimmy native API
-   `GET /ws/generate` - WebSocket streaming

### Environment Variables

Variable

Default

Description

`SHIMMY_BASE_GGUF`

_(auto-discover)_

Path to GGUF model file loaded as the default model

`SHIMMY_PORT`

`8080`

Port to listen on (Airframe server binary)

`SHIMMY_BIND_ADDRESS`

`0.0.0.0:8080`

Full bind address (overrides port)

`SHIMMY_MAX_CTX`

_(from GGUF)_

Override context window; activates YaRN RoPE scaling when above model native

`SHIMMY_MODEL_PATHS`

_(see Zero Config)_

Colon-separated extra model search paths

`SHIMMY_ENGINE_BACKEND`

`airframe`

`airframe` (default) or `llama` (legacy path)

`SHIMMY_ROPE_SCALE`

_(auto)_

Override computed YaRN scale factor

`RUST_BACKTRACE`

_(off)_

Set to `1` to print crash backtraces

### CLI Commands

shimmy serve                              # Start server (auto port allocation)
shimmy serve --bind 127.0.0.1:8080        # Manual port binding
shimmy serve --gpu-backend auto           # WebGPU adapter auto-select (default)
shimmy serve --gpu-backend cpu            # Force CPU (disable GPU)
shimmy list                               # Show available models
shimmy discover                           # Refresh model discovery
shimmy generate --name X --prompt "Hi"   # Test generation
shimmy probe model-name                   # Verify model loads
shimmy gpu-info                           # Show selected WebGPU adapter

Technical Architecture
----------------------

-   **Rust + Tokio**: Memory-safe, async performance
-   **Airframe engine**: Pure-Rust WGSL GPU inference — no C++ toolchain, deterministic output, GGUF-native
-   **OpenAI API compatibility**: Drop-in replacement
-   **Dynamic port management**: Zero conflicts, auto-allocation
-   **Zero-config auto-discovery**: Just works™

### 🚀 Advanced Features

-   **🧠 MOE CPU Offloading**: Hybrid GPU/CPU processing for large models (70B+)
-   **🎯 Smart Model Filtering**: Automatically excludes non-language models (Stable Diffusion, Whisper, CLIP)
-   **🛡️ 6-Gate Release Validation**: Constitutional quality limits ensure reliability
-   **⚡ Smart Model Preloading**: Background loading with usage tracking for instant model switching
-   **💾 Response Caching**: LRU + TTL cache delivering 20-40% performance gains on repeat queries
-   **🚀 Integration Templates**: One-command deployment for Docker, Kubernetes, Railway, Fly.io, FastAPI, Express
-   **🔄 Request Routing**: Multi-instance support with health checking and load balancing
-   **📊 Advanced Observability**: Real-time metrics with self-optimization and Prometheus integration
-   **🔗 RustChain Integration**: Universal workflow transpilation with workflow orchestration

* * *

❓ FAQ
-----

**Does Shimmy work on my GPU?** Shimmy uses WebGPU (via the Airframe engine) which runs on Vulkan, D3D12, and Metal — covering NVIDIA, AMD, Intel, and Apple Silicon. No CUDA required. See GPU requirements in TROUBLESHOOTING.md if you hit adapter errors.

**What's the difference between Shimmy and llama.cpp / Ollama?** Shimmy is written in pure Rust with no C++ toolchain dependency. The Airframe engine runs WGSL compute shaders compiled at startup — no pre-built binaries, no driver version pinning. The result is faster startup, lower memory overhead, and deterministic output. See the GPU Pipeline doc for internals.

**Why do I need `SHIMMY_BASE_GGUF` or `LIBSHIMMY_MODEL_PATH`?** If you don't set these, Shimmy auto-discovers models in standard directories (`~/.cache/huggingface`, `~/.ollama`, `~/lm-studio/models`, `~/.cache/lm-studio/models`, `~/Library/Application Support/LMStudio`). Set `SHIMMY_BASE_GGUF` to override and point directly at a specific GGUF file.

**Can I run multiple models at once?** Not currently — Shimmy loads one model per server instance. To serve multiple models, run multiple server instances on different ports. Hot-swapping models (reload without restart) is on the roadmap.

**Why does generation stop before `max_tokens`?** The model reached a natural end-of-sequence token. For chat models this is expected behavior — the model signals it's done. If you want to force longer output, increase `max_tokens` and set `temperature > 0`. If generation stops on the wrong token, the model may be using the wrong chat template — see CHAT\_TEMPLATES.md.

**Is there streaming support?** Set `"stream": true` in your request. Shimmy returns Server-Sent Events in the standard OpenAI streaming format.

**Q4\_K\_M vs Q4\_0 — which should I use?** `Q4_K_M` (K-quant) is consistently better quality than `Q4_0` for the same file size. Use `Q4_0` only when you need maximum compatibility or the model isn't available in K-quant. See QUANTIZATION.md for the full analysis.

**Can I extend the context window beyond what the model was trained on?** Yes — set `SHIMMY_MAX_CTX` to any value. Airframe applies YaRN scaling automatically when the requested context exceeds the model's native context. Quality degrades gradually beyond 2× the native context. See EXTENDED\_CONTEXT.md.

* * *

📚 Documentation Hub
--------------------

Full documentation lives in docs/. Use this table to find what you need:

### Getting Started

Document

Description

docs/quickstart.md

5-minute getting started guide

docs/MIGRATION\_v2.md

Migrating from Shimmy v1.x

docs/CONFIGURATION.md

All environment variables and config options

docs/WINDOWS\_GPU\_BUILD\_GUIDE.md

Windows-specific build instructions

### API & Integration

Document

Description

docs/API.md

Complete API endpoint reference

docs/OPENAI\_COMPAT.md

OpenAI compatibility matrix — what's supported

docs/INTEGRATION.md

Integrating with LangChain, OpenAI SDKs, etc.

docs/EXAMPLES.md

Runnable code examples

docs/CROSS\_COMPILATION.md

Building for other targets (ARM, Linux from Windows)

### Engine Deep Dives

Document

Description

docs/ARCHITECTURE.md

System-level architecture and component map

docs/GPU\_PIPELINE.md

Bindless GPU architecture, WGSL shaders, dispatch patterns

docs/QUANTIZATION.md

Q4\_0, Q8\_0, K-quant formats — bit-level internals

docs/EXTENDED\_CONTEXT.md

YaRN RoPE scaling, VRAM math, context extension

docs/CHAT\_TEMPLATES.md

Chat template auto-detection and format reference

docs/MODEL\_EXPANSION.md

Model onboarding protocol and acceptance gates

### Troubleshooting & Reference

Document

Description

docs/TROUBLESHOOTING.md

Diagnostic guide for GPU errors, model failures, port conflicts

docs/PERFORMANCE.md

Performance tuning and token/sec benchmarks

docs/FEATURES.md

Complete feature list

### Development & Methodology

Document

Description

docs/METHODOLOGY.md

Engineering methodology and quality standards

docs/REGRESSION\_TESTING.md

Regression testing approach

docs/ppt-invariant-testing.md

Property-based and invariant testing details

docs/METRICS.md

Observability and metrics reference

* * *

Community & Support
-------------------

-   **🐛 Bug Reports**: GitHub Issues
-   **💬 Discussions**: GitHub Discussions
-   **📖 Documentation**: Full Documentation Hub • Migration Guide v1→v2 • Engineering Methodology • OpenAI Compatibility Matrix • Architecture • GPU Pipeline • Troubleshooting
-   **💝 Sponsorship**: GitHub Sponsors

### Star History

### 🚀 Momentum Snapshot

🌟 **stars and climbing fast** ⏱ **<1s startup** 🦀 **100% Rust, no Python**

### 📰 As Featured On

🔥 **Hacker News** • **Front Page Again** • **IPE Newsletter**

**Companies**: Need invoicing? Email michaelallenkuykendall@gmail.com

⚡ Performance Comparison
------------------------

Tool

Startup Time

Memory Usage

OpenAI API

**Shimmy**

**<100ms**

**50MB**

**100%**

Ollama

5-10s

200MB+

Partial

Quality & Reliability
---------------------

Shimmy maintains high code quality through comprehensive testing:

-   **Comprehensive test suite** with property-based testing
-   **Automated CI/CD pipeline** with quality gates
-   **Runtime invariant checking** for critical operations
-   **Cross-platform compatibility testing**

### Development Testing

Run the complete test suite:

# Using cargo aliases
cargo test-quick           # Quick development tests

# Using Makefile  
make test                  # Full test suite
make test-quick            # Quick development tests

See our testing approach for technical details.

* * *

License & Philosophy
--------------------

MIT License - forever and always.

**Philosophy**: Infrastructure should be invisible. Shimmy is infrastructure.

**Testing Philosophy**: Reliability through comprehensive validation and property-based testing.

* * *

**Forever maintainer**: Michael A. Kuykendall **Promise**: This will never become a paid product **Mission**: Making local model inference simple and reliable
