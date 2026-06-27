---
project: higgs-audio
stars: 8246
description: Text-audio foundation model from Boson AI
url: https://github.com/boson-ai/higgs-audio
---

🎉 Higgs Audio v3 is here — you no longer need this repo!
=========================================================

### **👉 Don't clone this repository to use the latest model.**

**Higgs Audio v3** is a standalone release and does **not** depend on the code here. Just grab the weights or call the hosted API:

### 🤗 **Hugging Face — bosonai/higgs-audio-v3-tts-4b**

### 📖 **Boson AI API — docs.boson.ai/models/higgs-audio-tts**

_Conversational TTS across 100+ languages · zero-shot voice cloning · inline emotion / style / prosody control._

* * *

Use Higgs Audio v3
------------------

### Option 1 — Boson AI API (no setup, no GPU)

Free, rate-limited public preview. Get a key at boson.ai/workspace.

export BOSON\_API\_KEY=bai-xxxx

curl https://api.boson.ai/v1/audio/speech \\
  -H "Authorization: Bearer $BOSON\_API\_KEY" \\
  -H "Content-Type: application/json" \\
  -d '{"model": "higgs-audio-v3-tts", "input": "Hello, this is a test."}' \\
  --output out.mp3

OpenAI-compatible; supports preset voices, zero-shot cloning, and streaming. Full reference: **API docs**.

### Option 2 — Self-host the open weights

Weights: **bosonai/higgs-audio-v3-tts-4b**. We recommend serving with **SGLang-Omni**:

export HF\_TOKEN=hf\_xxxxxxxxxxxxxxxx
hf download bosonai/higgs-audio-v3-tts-4b

sgl-omni serve --model-path bosonai/higgs-audio-v3-tts-4b --port 8000

Serving, voice-cloning, and streaming recipes are in the model card and the SGLang-Omni cookbook.

Note

Higgs Audio v3 is released under the **Boson Higgs Audio v3 Research and Non-Commercial License**. Production / hosted / revenue-generating use requires a separate commercial license.

* * *

Looking for Higgs Audio v2 / v2.5?
----------------------------------

The full v2 / v2.5 documentation — installation, examples, technical details, and benchmarks — has moved to **README\_V2.md**. Those models remain available on Hugging Face: v2 (3B base) and the v2.5 blog.

Contribution and Support
------------------------

For contribution and support guidelines, please see SUPPORT\_GUIDELINES.md.

We Are Hiring!
--------------

If you are passionate about multimodal AI, speech/audio models, or large-scale systems, check out our open positions at Boson AI Careers.

Citation
--------

@misc{bosonai\_higgs\_audio\_tts\_v3\_2026,
  title  = {Higgs Audio v3 TTS: Conversational Speech for Voice AI from Boson AI},
  author = {Boson AI},
  year   = {2026},
  howpublished = {https://huggingface.co/bosonai/higgs-audio-v3-tts-4b},
}

Third-Party Licenses
--------------------

The `boson_multimodal/audio_processing/` directory contains code derived from third-party repositories, primarily from xcodec. See the `LICENSE` in that directory for attribution and licensing.
