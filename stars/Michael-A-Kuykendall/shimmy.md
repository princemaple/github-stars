---
project: shimmy
stars: 5867
description: ⚡ Pure-Rust WebGPU inference engine — OpenAI-API compatible, GGUF native, runs on any GPU. No Python. No llama.cpp. Single binary.
url: https://github.com/Michael-A-Kuykendall/shimmy
---

Shimmy — Local Inference, OpenAI-Compatible
===========================================

### 🔒 The 5MB alternative to Ollama — 100% Rust, zero dependencies 🚀

**Languages:** 简体中文 · 繁體中文

Shimmy is independently maintained and free forever. Sponsorship funds certification, compatibility work, and releases.

**Shimmy will be free forever.** No asterisks. No "free for now." No pivot to paid.

* * *

What Is Shimmy?
---------------

Shimmy is a **single-binary** OpenAI-compatible inference server for GGUF models. Point your existing AI tools at Shimmy and they just work — locally, privately, and free.

**Shimmy is the server. Airframe is the engine.** Under the hood, Shimmy runs on **Airframe** (v0.4.0), a pure-Rust WebGPU (WGSL) transformer engine. No C++ toolchain, no Python runtime, no backend flags. 26 models certified across 12 families. Version history: CHANGELOG · Airframe CHANGELOG.

**Why this matters:**

-   No Python runtime or C++ toolchain — Rust only, top to bottom
-   F32 accumulation precision with deterministic output (same model + seed + params → same output)
-   WGSL compute shaders via WebGPU — NVIDIA, AMD, Intel, integrated GPUs, Apple Silicon
-   Model spec auto-derived from GGUF metadata — no hardcoded per-model constants
-   YaRN RoPE scaling for extended context via `SHIMMY_MAX_CTX` (see Extended Context)

* * *

🎯 Supported Models
-------------------

**12 model families · 26 certified model/quant combinations** — every model below passes Shimmy's 3-box certification regimen (MATH + INFERENCE + DETERMINISM) against the certification ledger. Certification applies to the named model/quant combination; architecture recognition does not automatically mean certification. GGUF files load as-is; no recompilation, no hardcoded per-model constants.

Family

Model

Quants

**Llama**

Llama-3.2-1B-Instruct

Q4\_K\_M · Q6\_K

Llama-3.2-3B-Instruct

Q4\_K\_M

Llama-3.1-8B-Instruct

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

Q4\_K\_M (supported; cert: see v2-roadmap)

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

**SafeTensors format** (`.safetensors`) is supported for model loading via `safetensors_native`. Full Airframe-native inference for SafeTensors remains roadmap work; see docs/v2-roadmap.md.

Features
--------

-   **⚡ TurboShimmy INT4 KV Cache** — About 7× lower KV-cache memory in tested configurations. Run Llama-3.2-3B on 4 GB GPUs.
-   **🚀 OpenAI SDK Compatibility** — Chat completions, text completions, streaming, and model endpoints. Works with OpenAI SDKs and tools using that surface.
-   **🔧 Extended Context** — YaRN RoPE scaling via `SHIMMY_MAX_CTX`.
-   **📦 Migrating from v1.x** — llama.cpp, MLX, HuggingFace, and RustChain backends removed in v2.0+. Shimmy is now a pure Airframe product.
-   **🏆 Certification** — Every model passes a 3-box certification regimen (MATH + INFERENCE + DETERMINISM). See docs/CERTIFICATION.md.
-   **🧠 MOE support** — Mixture-of-Experts CPU offloading is on the Airframe roadmap.

* * *

Quick Start
-----------

cargo install shimmy
shimmy serve --model-path /absolute/path/to/model.gguf --bind 127.0.0.1:11435

Then in another terminal:

shimmy list --short
curl -s http://127.0.0.1:11435/v1/chat/completions \\
  -H 'Content-Type: application/json' \\
  -d '{"model":"tinyllama-1.1b","messages":\[{"role":"user","content":"Say hi in 5 words."}\],"max\_tokens":32}'

Full install, model acquisition, GPU, VRAM sizing, platform-specific builds: **docs/quickstart.md**

* * *

Documentation
-------------

Start here

What you need

Quick Start

Install, models, GPU, VRAM

Supported Models

Certified models and quantization

API Compatibility

Endpoints, SDKs, integration

Configuration

Env vars and config options

Troubleshooting

GPU errors, model failures

Complete documentation index

Section

Documents

**Models & Performance**

TurboShimmy — INT4 KV cache compression · Extended Context — YaRN RoPE scaling, VRAM math · Performance — Tuning and token/sec · Model Expansion — Onboarding protocol

**API & Integration**

API Reference · OpenAPI / Swagger UI · Integration Guides · Examples · Cross-Compilation

**Engine**

Architecture · GPU Pipeline · Quantization · Chat Templates

**Certification**

Certification · Methodology · Regression Testing · PPT Testing · Metrics

**FAQ**

FAQ · Features · Migration · Windows GPU

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
-   **📖 Security**: Security Policy

### 🚀 Momentum Snapshot

🌟 **stars and climbing fast** ⏱ **<1s startup** 🦀 **100% Rust, no Python**

### 📰 As Featured On

🔥 **Hacker News** · **Front Page Again** · **IPE Newsletter**

**Companies**: Need invoicing? Email michaelallenkuykendall@gmail.com

* * *

Performance
-----------

Tool

Startup

Memory

API

**Shimmy**

**<1s**

**~50MB**

Chat, completions, streaming, models

Ollama

5-10s

200MB+

Partial

_Measured on RTX 3060, Shimmy v2.6.0, TinyLlama-1.1B. Your results vary by hardware._

* * *

Sponsor Shimmy
--------------

Shimmy is independently maintained. Sponsorship funds certification, compatibility work, and releases.

-   **$5/month**: Coffee tier ☕ — Sponsor badge + name in SPONSORS.md
-   **$25/month**: Supporter 🐛 — Priority support + name in SPONSORS.md
-   **$100/month**: Corporate backer 🏢 — Logo placement + release recognition
-   **$500/month**: Infrastructure partner 🚀 — Office hours + roadmap consultation

**Current sponsors:** ZephyrCloudIO · alistairheath

**🎯 Become a Sponsor** · Invoicing

* * *

License & Philosophy
--------------------

MIT License — see LICENSE. **Shimmy will be free forever.**

**Promise**: This will never become a paid product.

Shimmy is infrastructure: it should be invisible. Reliability through comprehensive validation and property-based testing.

* * *

**Maintainer**: Michael A. Kuykendall · **Mission**: Making local model inference simple and reliable

* * *

Support
-------

This project is a safe space. Trans rights are human rights.

If you or someone you love needs support:

-   The Trevor Project — 24/7 for LGBTQ+ young people. Call 1-866-488-7386 or text START to 678-678
-   Trans Lifeline — peer support run by and for trans people. US: 877-565-8860
-   988 Suicide & Crisis Lifeline — call or text 988
