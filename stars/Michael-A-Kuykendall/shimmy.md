---
project: shimmy
stars: 6012
description: ⚡ Pure-Rust WebGPU inference engine — OpenAI-API compatible, GGUF native, runs on any GPU. No Python. No llama.cpp. Single binary.
url: https://github.com/Michael-A-Kuykendall/shimmy
---

Shimmy — Local Inference, OpenAI-Compatible
===========================================

### 🔒 Local GPU inference — Rust/WGSL application 🚀

Shimmy 2.6.6
------------

Shimmy is a local inference server and CLI; **Airframe 0.4.5 is its engine**. This is a coordinated dense-text correctness, dependency-security and documentation release, not a new architecture or performance release. See CHANGELOG.

**Default dependency licensing:** Shimmy → Airframe → libfse. Shimmy is Apache-2.0; Airframe and airframe-observe are MIT; ShimmyTok is MIT OR Apache-2.0. The libfse 0.1.4 additional Apache-2.0 grant permits commercial use, modification, redistribution and incorporation into products without separate commercial permission. The original crates.io archive and metadata remain unchanged. Preserve component and third-party notices; see stack licensing.

Install and run
---------------

Verified native 2.6.6 archives and checksum instructions are available separately from crates.io, including the Windows executable and complete licensing bundles.

Install the versioned crate with a Rust toolchain:

cargo install shimmy --version 2.6.6 --locked
shimmy --version
shimmy --ctx 512 --kv-quant f32 serve --model-path /path/to/model.gguf --bind 127.0.0.1:11435

Use a verified admitted fixture in place of the path. A working Rust toolchain and GPU driver are required. The fast profile does not provide inference. The separately verified native downloads, Homebrew and Scoop installers and versioned GHCR image are now available for 2.6.6. A crates.io upload does not create those channels automatically. Docker latest is unchanged; npm is not included. Verify the exact installed version.

See quickstart for model hashes, listing, requests and network access. Unavailable translations are not linked as current guides.

Correctness and support
-----------------------

The exact fixture matrix covers selected Qwen3-0.6B/Qwen3-1.7B and Llama 3.2 3B Q4\_K\_M cases, with independent FP32 full logits, maximum absolute 0.1/RMS 0.03 gates and matching measured greedy decisions. These are bounded model/context/mode results, not universal family support.

F32 KV and reference kernels define the validated path. Parsing metadata, tokenizers or quantization is not certification. Gemma2, MoE, MLA, recurrent, state-space and multimodal executors are not enabled. INT4/TurboShimmy and experimental kernels remain excluded and rejected.

Executed full-logit GPU evidence is NVIDIA through WSL Dozen/Vulkan. **NOT\_RUN for full-logit certification:** Metal/M4, other unexecuted native GPU platforms, extended-context Llama, alternate prefill chunks and unlisted combinations. WSL device-destruction and active-generation device-loss investigations remain open. No universal determinism, startup, multi-GPU, memory or speed guarantee is made.

Server contract
---------------

Selected OpenAI-compatible endpoints provide model listing, JSON chat/text completions and explicit **chat-only SSE**. Chat defaults to JSON; text streaming rejects. Usage, stop/finish metadata and typed errors are part of the tested contract. This is not every OpenAI endpoint/SDK feature.

Loopback can run without a key. Non-loopback binds require SHIMMY\_API\_KEY; browser origins require SHIMMY\_ALLOWED\_ORIGINS. With a key, routes except GET /health require credentials; origin checks still apply to health. Use TLS and appropriate network access controls remotely. Lazy loading is the default; optional selected-model warm-up shifts cold work before readiness without eliminating it or guaranteeing stability.

Documentation
-------------

-   Quickstart and configuration
-   API, compatibility and integration
-   Model scope, certification and quantization
-   Context capacity and templates
-   Docker scope, Windows scope and troubleshooting
-   Security, release process and release gates
-   Developer guide, contribution policy and roadmap

Shimmy source is Apache-2.0. Airframe runtime and Observe are MIT; ShimmyTok is dual-licensed. libfse 0.1.4 is covered by the additional Apache-2.0 grant, permitting commercial use without separate permission. Preserve applicable component, dependency and model terms; see stack licensing.

Support
-------

This project is independently maintained. Component licensing terms described above apply. Sponsorship helps fund ongoing development, certification, compatibility work, and releases.

Sponsor on GitHub · Buy Me a Coffee

Any amount is appreciated. Suggested tiers:

-   **$5/month** — Thanks
-   **$15/month** — Supporter
-   **$50/month** — Backer
-   **Custom** — Email for invoicing

* * *

License & Philosophy
--------------------

Shimmy server code: Apache-2.0 — see LICENSE. The default dependency stack permits commercial use under its component terms, including the libfse additional grant. See stack licensing; original published archives remain unchanged.

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
