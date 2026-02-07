---
project: chatterbox
stars: 22418
description: SoTA open-source TTS
url: https://github.com/resemble-ai/chatterbox
---

Chatterbox TTS
==============

\_Made with ♥️ by

**Chatterbox** is a family of three state-of-the-art, open-source text-to-speech models by Resemble AI.

We are excited to introduce **Chatterbox-Turbo**, our most efficient model yet. Built on a streamlined 350M parameter architecture, **Turbo** delivers high-quality speech with less compute and VRAM than our previous models. We have also distilled the speech-token-to-mel decoder, previously a bottleneck, reducing generation from 10 steps to just **one**, while retaining high-fidelity audio output.

**Paralinguistic tags** are now native to the Turbo model, allowing you to use `[cough]`, `[laugh]`, `[chuckle]`, and more to add distinct realism. While Turbo was built primarily for low-latency voice agents, it excels at narration and creative workflows.

If you like the model but need to scale or tune it for higher accuracy, check out our competitively priced TTS service (link). It delivers reliable performance with ultra-low latency of sub 200ms—ideal for production use in agents, applications, or interactive media.

### ⚡ Model Zoo

Choose the right model for your application.

Model

Size

Languages

Key Features

Best For

🤗

Examples

**Chatterbox-Turbo**

**350M**

**English**

Paralinguistic Tags (`[laugh]`), Lower Compute and VRAM

Zero-shot voice agents, Production

Demo

Listen

Chatterbox-Multilingual (Language list)

500M

23+

Zero-shot cloning, Multiple Languages

Global applications, Localization

Demo

Listen

Chatterbox (Tips and Tricks)

500M

English

CFG & Exaggeration tuning

General zero-shot TTS with creative controls

Demo

Listen

Installation
------------

pip install chatterbox-tts

Alternatively, you can install from source:

# conda create -yn chatterbox python=3.11
# conda activate chatterbox

git clone https://github.com/resemble-ai/chatterbox.git
cd chatterbox
pip install -e .

We developed and tested Chatterbox on Python 3.11 on Debian 11 OS; the versions of the dependencies are pinned in `pyproject.toml` to ensure consistency. You can modify the code or dependencies in this installation mode.

Usage
-----

##### Chatterbox-Turbo

import torchaudio as ta
import torch
from chatterbox.tts\_turbo import ChatterboxTurboTTS

\# Load the Turbo model
model \= ChatterboxTurboTTS.from\_pretrained(device\="cuda")

\# Generate with Paralinguistic Tags
text \= "Hi there, Sarah here from MochaFone calling you back \[chuckle\], have you got one minute to chat about the billing issue?"

\# Generate audio (requires a reference clip for voice cloning)
wav \= model.generate(text, audio\_prompt\_path\="your\_10s\_ref\_clip.wav")

ta.save("test-turbo.wav", wav, model.sr)

##### Chatterbox and Chatterbox-Multilingual

import torchaudio as ta
from chatterbox.tts import ChatterboxTTS
from chatterbox.mtl\_tts import ChatterboxMultilingualTTS

\# English example
model \= ChatterboxTTS.from\_pretrained(device\="cuda")

text \= "Ezreal and Jinx teamed up with Ahri, Yasuo, and Teemo to take down the enemy's Nexus in an epic late-game pentakill."
wav \= model.generate(text)
ta.save("test-english.wav", wav, model.sr)

\# Multilingual examples
multilingual\_model \= ChatterboxMultilingualTTS.from\_pretrained(device\=device)

french\_text \= "Bonjour, comment ça va? Ceci est le modèle de synthèse vocale multilingue Chatterbox, il prend en charge 23 langues."
wav\_french \= multilingual\_model.generate(spanish\_text, language\_id\="fr")
ta.save("test-french.wav", wav\_french, model.sr)

chinese\_text \= "你好，今天天气真不错，希望你有一个愉快的周末。"
wav\_chinese \= multilingual\_model.generate(chinese\_text, language\_id\="zh")
ta.save("test-chinese.wav", wav\_chinese, model.sr)

\# If you want to synthesize with a different voice, specify the audio prompt
AUDIO\_PROMPT\_PATH \= "YOUR\_FILE.wav"
wav \= model.generate(text, audio\_prompt\_path\=AUDIO\_PROMPT\_PATH)
ta.save("test-2.wav", wav, model.sr)

See `example_tts.py` and `example_vc.py` for more examples.

Supported Languages
-------------------

Arabic (ar) • Danish (da) • German (de) • Greek (el) • English (en) • Spanish (es) • Finnish (fi) • French (fr) • Hebrew (he) • Hindi (hi) • Italian (it) • Japanese (ja) • Korean (ko) • Malay (ms) • Dutch (nl) • Norwegian (no) • Polish (pl) • Portuguese (pt) • Russian (ru) • Swedish (sv) • Swahili (sw) • Turkish (tr) • Chinese (zh)

Original Chatterbox Tips
------------------------

-   **General Use (TTS and Voice Agents):**
    
    -   Ensure that the reference clip matches the specified language tag. Otherwise, language transfer outputs may inherit the accent of the reference clip’s language. To mitigate this, set `cfg_weight` to `0`.
    -   The default settings (`exaggeration=0.5`, `cfg_weight=0.5`) work well for most prompts across all languages.
    -   If the reference speaker has a fast speaking style, lowering `cfg_weight` to around `0.3` can improve pacing.
-   **Expressive or Dramatic Speech:**
    
    -   Try lower `cfg_weight` values (e.g. `~0.3`) and increase `exaggeration` to around `0.7` or higher.
    -   Higher `exaggeration` tends to speed up speech; reducing `cfg_weight` helps compensate with slower, more deliberate pacing.

Built-in PerTh Watermarking for Responsible AI
----------------------------------------------

Every audio file generated by Chatterbox includes Resemble AI's Perth (Perceptual Threshold) Watermarker - imperceptible neural watermarks that survive MP3 compression, audio editing, and common manipulations while maintaining nearly 100% detection accuracy.

Watermark extraction
--------------------

You can look for the watermark using the following script.

import perth
import librosa

AUDIO\_PATH \= "YOUR\_FILE.wav"

\# Load the watermarked audio
watermarked\_audio, sr \= librosa.load(AUDIO\_PATH, sr\=None)

\# Initialize watermarker (same as used for embedding)
watermarker \= perth.PerthImplicitWatermarker()

\# Extract watermark
watermark \= watermarker.get\_watermark(watermarked\_audio, sample\_rate\=sr)
print(f"Extracted watermark: {watermark}")
\# Output: 0.0 (no watermark) or 1.0 (watermarked)

Official Discord
----------------

👋 Join us on Discord and let's build something awesome together!

Evaluation
----------

Chatterbox Turbo was evaluated using Podonos, a platform for reproducible subjective speech evaluation.

We compared Chatterbox Turbo to competitive TTS systems using Podonos' standardized evaluation suite, focusing on overall preference, naturalness, and expressiveness.

Evaluation reports:

-   Chatterbox Turbo vs ElevenLabs Turbo v2.5
-   Chatterbox Turbo vs Cartesia Sonic 3
-   Chatterbox Turbo vs VibeVoice 7B

These evaluations were conducted under identical conditions and are publicly accessible via Podonos.

Acknowledgements
----------------

-   Podonos — for supporting reproducible subjective speech evaluation
-   Cosyvoice
-   Real-Time-Voice-Cloning
-   HiFT-GAN
-   Llama 3
-   S3Tokenizer

Citation
--------

If you find this model useful, please consider citing.

```
@misc{chatterboxtts2025,
  author       = {{Resemble AI}},
  title        = {{Chatterbox-TTS}},
  year         = {2025},
  howpublished = {\url{https://github.com/resemble-ai/chatterbox}},
  note         = {GitHub repository}
}
```

Disclaimer
----------

Don't use this model to do bad things. Prompts are sourced from freely available data on the internet.
