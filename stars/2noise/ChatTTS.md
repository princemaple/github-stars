---
project: ChatTTS
stars: 38633
description: A generative speech model for daily dialogue.
url: https://github.com/2noise/ChatTTS
---

ChatTTS
=======

A generative speech model for daily dialogue.

**English** | **简体中文** | **日本語** | **Русский** | **Español** | **Français** | **한국어**

Introduction
------------

Note

This repo contains the algorithm infrastructure and some simple examples.

Tip

For the extended end-user products, please refer to the index repo Awesome-ChatTTS maintained by the community.  
You can find a diagram visualization of the codebase here.

ChatTTS is a text-to-speech model designed specifically for dialogue scenarios such as LLM assistant.

### Supported Languages

-   English
-   Chinese
-   Coming Soon...

### Highlights

> You can refer to **this video on Bilibili** for the detailed description.

1.  **Conversational TTS**: ChatTTS is optimized for dialogue-based tasks, enabling natural and expressive speech synthesis. It supports multiple speakers, facilitating interactive conversations.
2.  **Fine-grained Control**: The model could predict and control fine-grained prosodic features, including laughter, pauses, and interjections.
3.  **Better Prosody**: ChatTTS surpasses most of open-source TTS models in terms of prosody. We provide pretrained models to support further research and development.

### Dataset & Model

Important

The released model is for academic purposes only.

-   The main model is trained with Chinese and English audio data of 100,000+ hours.
-   The open-source version on **HuggingFace** is a 40,000 hours pre-trained model without SFT.

### Roadmap

-   Open-source the 40k-hours-base model and spk\_stats file.
-   Streaming audio generation.
-   Open-source DVAE encoder and zero shot inferring code.
-   Multi-emotion controlling.
-   ChatTTS.cpp (new repo in `2noise` org is welcomed)

### Licenses

#### The Code

The code is published under `AGPLv3+` license.

#### The model

The model is published under `CC BY-NC 4.0` license. It is intended for educational and research use, and should not be used for any commercial or illegal purposes. The authors do not guarantee the accuracy, completeness, or reliability of the information. The information and data used in this repo, are for academic and research purposes only. The data obtained from publicly available sources, and the authors do not claim any ownership or copyright over the data.

### Disclaimer

ChatTTS is a powerful text-to-speech system. However, it is very important to utilize this technology responsibly and ethically. To limit the use of ChatTTS, we added a small amount of high-frequency noise during the training of the 40,000-hour model, and compressed the audio quality as much as possible using MP3 format, to prevent malicious actors from potentially using it for criminal purposes. At the same time, we have internally trained a detection model and plan to open-source it in the future.

### Contact

> GitHub issues/PRs are always welcomed.

#### Formal Inquiries

For formal inquiries about the model and roadmap, please contact us at **open-source@2noise.com**.

#### Online Chat

##### 1\. QQ Group (Chinese Social APP)

-   **Group 1**, 808364215
-   **Group 2**, 230696694
-   **Group 3**, 933639842
-   **Group 4**, 608667975

##### 2\. Discord Server

Join by clicking here.

Get Started
-----------

### Clone Repo

git clone https://github.com/2noise/ChatTTS
cd ChatTTS

### Install requirements

#### 1\. Install Directly

pip install --upgrade -r requirements.txt

#### 2\. Install from conda

conda create -n chattts python=3.11
conda activate chattts
pip install -r requirements.txt

#### Optional: Install vLLM (Linux only)

pip install safetensors vllm==0.2.7 torchaudio

#### Unrecommended Optional: Install TransformerEngine if using NVIDIA GPU (Linux only)

Warning

DO NOT INSTALL! The adaptation of TransformerEngine is currently under development and CANNOT run properly now. Only install it on developing purpose. See more details on at #672 #676

Note

The installation process is very slow.

pip install git+https://github.com/NVIDIA/TransformerEngine.git@stable

#### Unrecommended Optional: Install FlashAttention-2 (mainly NVIDIA GPU)

Warning

DO NOT INSTALL! Currently the FlashAttention-2 will slow down the generating speed according to this issue. Only install it on developing purpose.

Note

See supported devices at the Hugging Face Doc.

pip install flash-attn --no-build-isolation

### Quick Start

> Make sure you are under the project root directory when you execute these commands below.

#### 1\. Launch WebUI

python examples/web/webui.py

#### 2\. Infer by Command Line

> It will save audio to `./output_audio_n.mp3`

python examples/cmd/run.py "Your text 1." "Your text 2."

Installation
------------

1.  Install the stable version from PyPI

pip install ChatTTS

1.  Install the latest version from GitHub

pip install git+https://github.com/2noise/ChatTTS

1.  Install from local directory in dev mode

pip install -e .

### Basic Usage

import ChatTTS
import torch
import torchaudio

chat \= ChatTTS.Chat()
chat.load(compile\=False) \# Set to True for better performance

texts \= \["PUT YOUR 1st TEXT HERE", "PUT YOUR 2nd TEXT HERE"\]

wavs \= chat.infer(texts)

for i in range(len(wavs)):
    """
    In some versions of torchaudio, the first line works but in other versions, so does the second line.
    """
    try:
        torchaudio.save(f"basic\_output{i}.wav", torch.from\_numpy(wavs\[i\]).unsqueeze(0), 24000)
    except:
        torchaudio.save(f"basic\_output{i}.wav", torch.from\_numpy(wavs\[i\]), 24000)

### Advanced Usage

###################################
\# Sample a speaker from Gaussian.

rand\_spk \= chat.sample\_random\_speaker()
print(rand\_spk) \# save it for later timbre recovery

params\_infer\_code \= ChatTTS.Chat.InferCodeParams(
    spk\_emb \= rand\_spk, \# add sampled speaker 
    temperature \= .3,   \# using custom temperature
    top\_P \= 0.7,        \# top P decode
    top\_K \= 20,         \# top K decode
)

###################################
\# For sentence level manual control.

\# use oral\_(0-9), laugh\_(0-2), break\_(0-7) 
\# to generate special token in text to synthesize.
params\_refine\_text \= ChatTTS.Chat.RefineTextParams(
    prompt\='\[oral\_2\]\[laugh\_0\]\[break\_6\]',
)

wavs \= chat.infer(
    texts,
    params\_refine\_text\=params\_refine\_text,
    params\_infer\_code\=params\_infer\_code,
)

###################################
\# For word level manual control.

text \= 'What is \[uv\_break\]your favorite english food?\[laugh\]\[lbreak\]'
wavs \= chat.infer(text, skip\_refine\_text\=True, params\_refine\_text\=params\_refine\_text,  params\_infer\_code\=params\_infer\_code)
"""
In some versions of torchaudio, the first line works but in other versions, so does the second line.
"""
try:
    torchaudio.save("word\_level\_output.wav", torch.from\_numpy(wavs\[0\]).unsqueeze(0), 24000)
except:
    torchaudio.save("word\_level\_output.wav", torch.from\_numpy(wavs\[0\]), 24000)

#### Example: self introduction

inputs\_en \= """
chat T T S is a text to speech model designed for dialogue applications. 
\[uv\_break\]it supports mixed language input \[uv\_break\]and offers multi speaker 
capabilities with precise control over prosodic elements like 
\[uv\_break\]laughter\[uv\_break\]\[laugh\], \[uv\_break\]pauses, \[uv\_break\]and intonation. 
\[uv\_break\]it delivers natural and expressive speech,\[uv\_break\]so please
\[uv\_break\] use the project responsibly at your own risk.\[uv\_break\]
""".replace('\\n', '') \# English is still experimental.

params\_refine\_text \= ChatTTS.Chat.RefineTextParams(
    prompt\='\[oral\_2\]\[laugh\_0\]\[break\_4\]',
)

audio\_array\_en \= chat.infer(inputs\_en, params\_refine\_text\=params\_refine\_text)
torchaudio.save("self\_introduction\_output.wav", torch.from\_numpy(audio\_array\_en\[0\]), 24000)

**male speaker**

**female speaker**

intro\_en\_m.webm

intro\_en\_f.webm

FAQ
---

#### 1\. How much VRAM do I need? How about infer speed?

For a 30-second audio clip, at least 4GB of GPU memory is required. For the 4090 GPU, it can generate audio corresponding to approximately 7 semantic tokens per second. The Real-Time Factor (RTF) is around 0.3.

#### 2\. Model stability is not good enough, with issues such as multi speakers or poor audio quality.

This is a problem that typically occurs with autoregressive models (for bark and valle). It's generally difficult to avoid. One can try multiple samples to find a suitable result.

#### 3\. Besides laughter, can we control anything else? Can we control other emotions?

In the current released model, the only token-level control units are `[laugh]`, `[uv_break]`, and `[lbreak]`. In future versions, we may open-source models with additional emotional control capabilities.

Acknowledgements
----------------

-   bark, XTTSv2 and valle demonstrate a remarkable TTS result by an autoregressive-style system.
-   fish-speech reveals capability of GVQ as audio tokenizer for LLM modeling.
-   vocos which is used as a pretrained vocoder.

Special Appreciation
--------------------

-   wlu-audio lab for early algorithm experiments.

Thanks to all contributors for their efforts
--------------------------------------------
