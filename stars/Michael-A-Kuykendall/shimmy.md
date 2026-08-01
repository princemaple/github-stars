---
project: shimmy
stars: 5728
description: ⚡ Pure-Rust WebGPU inference engine — OpenAI-API compatible, GGUF native, runs on any GPU. No Python. No llama.cpp. Single binary.
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

What Is Shimmy?
---------------

Shimmy is a **single-binary** that provides **100% OpenAI-compatible endpoints** for GGUF models. Point your existing AI tools to Shimmy and they just work — locally, privately, and free.

Under the hood it runs on **Airframe**, a pure-Rust WebGPU (WGSL) transformer engine built from scratch. No C++ toolchain, no backend flags, no compilation required. Version history lives in the CHANGELOG; see the Airframe CHANGELOG for engine release notes.

**Why this matters:**

-   No C++ toolchain required — Rust only, top to bottom
-   F32 precision throughout for deterministic, high-quality output
-   WGSL compute shaders work on any GPU via WebGPU (NVIDIA, AMD, Intel, integrated)
-   Model spec auto-derived from GGUF metadata — no hardcoded per-model constants
-   YaRN RoPE scaling for extended context via `SHIMMY_MAX_CTX` (see Extended Context)

* * *

🎯 Supported Models
-------------------

**11 model families · 25 certified model/quant combinations** — every model below passes Shimmy's 5-gate GPU math verification pipeline (dequant, structural peel, numerical, decode≡prefill, logits) against the certification ledger. GGUF files load as-is; no recompilation, no hardcoded per-model constants.

Family

Model

Quants

**Llama**

Llama-3.2-1B-Instruct

Q4\_K\_M · Q6\_K

Llama-3.2-3B-Instruct

Q4\_K\_M

TinyLlama-1.1B-Chat

Q4\_0 · Q5\_K\_M · Q6\_K

**Qwen3**

Qwen3-0.6B

Q4\_K\_M

Qwen3-1.7B

Q4\_K\_M

Qwen3-4B

Q4\_K\_M

Qwen3-4B-Thinking

Q4\_K\_M

Qwen3-8B

Q4\_K\_M

**Qwen2**

Qwen2-0.5B-Instruct

Q4\_K\_M

Qwen2-1.5B-Instruct

Q4\_K\_M

Qwen2-7B-Instruct

Q4\_K\_M

**Qwen3.5**

Qwen3.5-9B

Q4\_K\_M

**Phi-3**

Phi-3.5-mini-Instruct

Q4\_K\_M

Phi-3-mini-4k-Instruct

Q4\_0

**Phi-2**

Phi-2

Q4\_K\_M

**Gemma-2**

Gemma-2-2B-it

Q4\_K\_M

Gemma-2-9B-it

Q4\_K\_M

**Gemma-4**

Gemma-4-12B-coder

Q4\_K\_M

Gemma-4-E4B

Q4\_K\_M

**DeepSeek-R1**

DeepSeek-R1-0528-Qwen3-8B

Q4\_K\_M

**Ministral**

Ministral-3-14B-Reasoning

Q4\_K\_M

**StarCoder2**

StarCoder2-3B

Q4\_K\_M

Features at a Glance
--------------------

-   **⚡ TurboShimmy INT4 KV Cache** — ~7× less KV VRAM with one flag (`--kv-quant int4`). Run Llama-3.2-3B on 4 GB GPUs.
-   **🚀 OpenAI SDK Compatibility** — drop-in replacement; VSCode Copilot, Cursor, Continue.dev, any OpenAI SDK.
-   **🔧 Extended Context** — YaRN RoPE scaling via `SHIMMY_MAX_CTX`.
-   **📦 Migrating from v1.x** — the llama.cpp backend was removed in v2.0; see the migration guide.
-   **🧠 MOE support** — Mixture-of-Experts CPU offloading is on the Airframe roadmap.
-   **🏆 Certification** — Every model passes a 5-gate mathematical verification pipeline. See docs/CERTIFICATION.md for how it works.

* * *

Quick Start (30 seconds)
------------------------

# 1) Download pre-built binary (Windows example)
curl -L https://github.com/Michael-A-Kuykendall/shimmy/releases/latest/download/shimmy-windows-x86\_64.exe -o shimmy.exe

# 2) Point it at a GGUF model
set SHIMMY\_BASE\_GGUF=C:\\path\\to\\model.gguf && ./shimmy.exe serve &

# 3) See registered models
./shimmy list

# 4) Smoke test the OpenAI API
curl -s http://127.0.0.1:11435/v1/chat/completions \\
  -H 'Content-Type: application/json' \\
  -d '{"model":"tinyllama-1.1b","messages":\[{"role":"user","content":"Say hi in 5 words."}\],"max\_tokens":32}' \\
  | jq -r '.choices\[0\].message.content'

Full install, model acquisition, GPU, and VRAM sizing: **docs/quickstart.md**

* * *

Documentation Hub
-----------------

Full documentation lives in docs/. Use this table to find what you need:

### Getting Started

Document

Description

quickstart.md

Install, models, GPU, VRAM, extended context

MIGRATION\_v2.md

Migrating from Shimmy v1.x

CONFIGURATION.md

All environment variables and config options

WINDOWS\_GPU\_BUILD\_GUIDE.md

Windows-specific build instructions

### Models & Performance

Document

Description

SUPPORTED\_MODELS.md

Certified models and quantization support

turboshimmy.md

INT4 KV cache compression

EXTENDED\_CONTEXT.md

YaRN RoPE scaling, VRAM math

MODEL\_EXPANSION.md

Model onboarding protocol and acceptance gates

PERFORMANCE.md

Performance tuning and token/sec benchmarks

### API & Integration

Document

Description

API.md

Complete endpoint, CLI, and env-var reference

OPENAI\_COMPAT.md

OpenAI compatibility matrix — what's supported

INTEGRATION.md

LangChain, OpenAI SDKs, VSCode, etc.

EXAMPLES.md

Runnable code examples

CROSS\_COMPILATION.md

Building for other targets (ARM, Linux from Windows)

### Engine Deep Dives

Document

Description

ARCHITECTURE.md

System-level architecture and component map

GPU\_PIPELINE.md

Bindless GPU architecture, WGSL shaders, dispatch patterns

QUANTIZATION.md

Q4\_0, Q8\_0, K-quant formats — bit-level internals

CHAT\_TEMPLATES.md

Chat template auto-detection and format reference

### FAQ & Troubleshooting

Document

Description

FAQ.md

Frequently asked questions

TROUBLESHOOTING.md

GPU errors, model failures, port conflicts

FEATURES.md

Complete feature list

### Certification & Methodology

Document

Description

CERTIFICATION.md

How we mathematically prove every model is correct

METHODOLOGY.md

Engineering methodology and quality standards

REGRESSION\_TESTING.md

Regression testing approach

ppt-invariant-testing.md

Property-based and invariant testing details

METRICS.md

Observability and metrics reference

* * *

Development Testing
-------------------

Shimmy maintains high code quality through comprehensive testing:

# Full test suite (default features = GPU engine)
cargo test --features airframe,huggingface

# Quick CPU-only tests (no GPU required)
cargo test --lib --no-default-features --features huggingface -- --test-threads=1

See docs/ppt-invariant-testing.md for technical details.

* * *

Community & Support
-------------------

-   **🐛 Bug Reports**: GitHub Issues
-   **💬 Discussions**: GitHub Discussions
-   **💝 Sponsorship**: GitHub Sponsors

### Star History

### 🚀 Momentum Snapshot

🌟 **stars and climbing fast** ⏱ **<1s startup** 🦀 **100% Rust, no Python**

### 📰 As Featured On

🔥 **Hacker News** • **Front Page Again** • **IPE Newsletter**

**Companies**: Need invoicing? Email michaelallenkuykendall@gmail.com

* * *

Performance Comparison
----------------------

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

* * *

License & Philosophy
--------------------

MIT License - forever and always.

**Philosophy**: Infrastructure should be invisible. Shimmy is infrastructure.

**Testing Philosophy**: Reliability through comprehensive validation and property-based testing.

* * *

**Forever maintainer**: Michael A. Kuykendall **Promise**: This will never become a paid product **Mission**: Making local model inference simple and reliable
