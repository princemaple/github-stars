---
project: higgs-audio
stars: 7589
description: Text-audio foundation model from Boson AI
url: https://github.com/boson-ai/higgs-audio
---

Higgs Audio V2: Redefining Expressiveness in Audio Generation
=============================================================

We are open-sourcing Higgs Audio v2, a powerful audio foundation model pretrained on over 10 million hours of audio data and a diverse set of text data. Despite having no post-training or fine-tuning, Higgs Audio v2 excels in expressive audio generation, thanks to its deep language and acoustic understanding.

On EmergentTTS-Eval, it achieves win rates of **75.7%** and **55.7%** over "gpt-4o-mini-tts" on the "Emotions" and "Questions" categories, respectively. It also obtains state-of-the-art performance on traditional TTS benchmarks like Seed-TTS Eval and Emotional Speech Dataset (ESD). Moreover, the model demonstrates capabilities rarely seen in previous systems, including generating natural multi-speaker dialogues in multiple languages, automatic prosody adaptation during narration, melodic humming with the cloned voice, and simultaneous generation of speech and background music.

Here's the demo video that shows some of its emergent capabilities (remember to unmute):

open\_source\_repo\_demo.mp4

Here's another demo video that show-cases the model's multilingual capability and how it enabled live translation (remember to unmute):

live\_translation\_v4\_compressed.mp4

Installation
------------

We recommend to use NVIDIA Deep Learning Container to manage the CUDA environment. Following are two docker images that we have verified:

-   nvcr.io/nvidia/pytorch:25.02-py3
-   nvcr.io/nvidia/pytorch:25.01-py3

Here's an example command for launching a docker container environment. Please also check the official NVIDIA documentations.

docker run --gpus all --ipc=host --net=host --ulimit memlock=-1 --ulimit stack=67108864 -it --rm nvcr.io/nvidia/pytorch:25.02-py3 bash

### Option 1: Direct installation

git clone https://github.com/boson-ai/higgs-audio.git
cd higgs-audio

pip install -r requirements.txt
pip install -e .

### Option 2: Using venv

git clone https://github.com/boson-ai/higgs-audio.git
cd higgs-audio

python3 -m venv higgs\_audio\_env
source higgs\_audio\_env/bin/activate
pip install -r requirements.txt
pip install -e .

### Option 3: Using conda

git clone https://github.com/boson-ai/higgs-audio.git
cd higgs-audio

conda create -y --prefix ./conda\_env --override-channels --strict-channel-priority --channel "conda-forge" "python==3.10.\*"
conda activate ./conda\_env
pip install -r requirements.txt
pip install -e .

# Uninstalling environment:
conda deactivate
conda remove -y --prefix ./conda\_env --all

### Option 4: Using uv

git clone https://github.com/boson-ai/higgs-audio.git
cd higgs-audio

uv venv --python 3.10
source .venv/bin/activate
uv pip install -r requirements.txt
uv pip install -e .

### Option 5: Using vllm

For advanced usage with higher throughput, we also built OpenAI compatible API server backed by vLLM engine for you to use. Please refer to examples/vllm for more details.

Usage
-----

Tip

For optimal performance, run the generation examples on a machine equipped with GPU with at least 24GB memory!

### Get Started

Here's a basic python snippet to help you get started.

from boson\_multimodal.serve.serve\_engine import HiggsAudioServeEngine, HiggsAudioResponse
from boson\_multimodal.data\_types import ChatMLSample, Message, AudioContent

import torch
import torchaudio
import time
import click

MODEL\_PATH \= "bosonai/higgs-audio-v2-generation-3B-base"
AUDIO\_TOKENIZER\_PATH \= "bosonai/higgs-audio-v2-tokenizer"

system\_prompt \= (
    "Generate audio following instruction.\\n\\n<|scene\_desc\_start|>\\nAudio is recorded from a quiet room.\\n<|scene\_desc\_end|>"
)

messages \= \[
    Message(
        role\="system",
        content\=system\_prompt,
    ),
    Message(
        role\="user",
        content\="The sun rises in the east and sets in the west. This simple fact has been observed by humans for thousands of years.",
    ),
\]
device \= "cuda" if torch.cuda.is\_available() else "cpu"

serve\_engine \= HiggsAudioServeEngine(MODEL\_PATH, AUDIO\_TOKENIZER\_PATH, device\=device)

output: HiggsAudioResponse \= serve\_engine.generate(
    chat\_ml\_sample\=ChatMLSample(messages\=messages),
    max\_new\_tokens\=1024,
    temperature\=0.3,
    top\_p\=0.95,
    top\_k\=50,
    stop\_strings\=\["<|end\_of\_text|>", "<|eot\_id|>"\],
)
torchaudio.save(f"output.wav", torch.from\_numpy(output.audio)\[None, :\], output.sampling\_rate)

We also provide a list of examples under examples. In the following we highlight a few examples to help you use Higgs Audio v2.

### Zero-Shot Voice Cloning

Generate audio that sounds similar as the provided reference audio.

python3 examples/generation.py \\
--transcript "The sun rises in the east and sets in the west. This simple fact has been observed by humans for thousands of years." \\
--ref\_audio belinda \\
--temperature 0.3 \\
--out\_path generation.wav

The generation script will automatically use `cuda:0` if it founds cuda is available. To change the device id, specify `--device_id`:

python3 examples/generation.py \\
--transcript "The sun rises in the east and sets in the west. This simple fact has been observed by humans for thousands of years." \\
--ref\_audio belinda \\
--temperature 0.3 \\
--device\_id 0 \\
--out\_path generation.wav

You can also try other voices. Check more example voices in examples/voice\_prompts. You can also add your own voice to the folder.

python3 examples/generation.py \\
--transcript "The sun rises in the east and sets in the west. This simple fact has been observed by humans for thousands of years." \\
--ref\_audio broom\_salesman \\
--temperature 0.3 \\
--out\_path generation.wav

### Single-speaker Generation with Smart Voice

If you do not specify reference voice, the model will decide the voice based on the transcript it sees.

python3 examples/generation.py \\
--transcript "The sun rises in the east and sets in the west. This simple fact has been observed by humans for thousands of years." \\
--temperature 0.3 \\
--out\_path generation.wav

### Multi-speaker Dialog with Smart Voice

Generate multi-speaker dialog. The model will decide the voices based on the transcript it sees.

python3 examples/generation.py \\
--transcript examples/transcript/multi\_speaker/en\_argument.txt \\
--seed 12345 \\
--out\_path generation.wav

### Multi-speaker Dialog with Voice Clone

Generate multi-speaker dialog with the voices you picked.

python3 examples/generation.py \\
--transcript examples/transcript/multi\_speaker/en\_argument.txt \\
--ref\_audio belinda,broom\_salesman \\
--ref\_audio\_in\_system\_message \\
--chunk\_method speaker \\
--seed 12345 \\
--out\_path generation.wav

Technical Details
-----------------

Higgs Audio v2 adopts the "generation variant" depicted in the architecture figure above. Its strong performance is driven by three key technical innovations:

-   We developed an automated annotation pipeline that leverages multiple ASR models, sound event classification models, and our in-house audio understanding model. Using this pipeline, we cleaned and annotated 10 million hours audio data, which we refer to as **AudioVerse**. The in-house understanding model is finetuned on top of Higgs Audio v1 Understanding, which adopts the "understanding variant" shown in the architecture figure.
-   We trained a unified audio tokenizer from scratch that captures both semantic and acoustic features. We also open-sourced our evaluation set on HuggingFace. Learn more in the tokenizer blog.
-   We proposed the DualFFN architecture, which enhances the LLM’s ability to model acoustics tokens with minimal computational overhead. See the architecture blog.

Evaluation
----------

Here's the performance of Higgs Audio v2 on four benchmarks, Seed-TTS Eval, Emotional Speech Dataset (ESD), EmergentTTS-Eval, and Multi-speaker Eval:

#### Seed-TTS Eval & ESD

We prompt Higgs Audio v2 with the reference text, reference audio, and target text for zero-shot TTS. We use the standard evaluation metrics from Seed-TTS Eval and ESD.

SeedTTS-Eval

ESD

WER ↓

SIM ↑

WER ↓

SIM (emo2vec) ↑

Cosyvoice2

2.28

65.49

2.71

80.48

Qwen2.5-omni†

2.33

64.10

\-

\-

ElevenLabs Multilingual V2

**1.43**

50.00

1.66

65.87

Higgs Audio v1

2.18

66.27

**1.49**

82.84

Higgs Audio v2 (base)

2.44

**67.70**

1.78

**86.13**

#### EmergentTTS-Eval ("Emotions" and "Questions")

Following the EmergentTTS-Eval Paper, we report the win-rate over "gpt-4o-mini-tts" with the "alloy" voice. The judge model is Gemini 2.5 Pro.

Model

Emotions (%) ↑

Questions (%) ↑

Higgs Audio v2 (base)

**75.71%**

**55.71%**

gpt-4o-audio-preview†

61.64%

47.85%

Hume.AI

61.60%

43.21%

**BASELINE:** gpt-4o-mini-tts

50.00%

50.00%

Qwen 2.5 Omni†

41.60%

51.78%

minimax/speech-02-hd

40.86%

47.32%

ElevenLabs Multilingual v2

30.35%

39.46%

DeepGram Aura-2

29.28%

48.21%

Sesame csm-1B

15.96%

31.78%

'†' means using the strong-prompting method described in the paper.

#### Multi-speaker Eval

We also designed a multi-speaker evaluation benchmark to evaluate the capability of Higgs Audio v2 for multi-speaker dialog generation. The benchmark contains three subsets

-   `two-speaker-conversation`: 1000 synthetic dialogues involving two speakers. We fix two reference audio clips to evaluate the model's ability in double voice cloning for utterances ranging from 4 to 10 dialogues between two randomly chosen persona.
-   `small talk (no ref)`: 250 synthetic dialogues curated in the same way as above, but are characterized by short utterances and a limited number of turns (4–6), we do not fix reference audios in this case and this set is designed to evaluate the model's ability to automatically assign appropriate voices to speakers.
-   `small talk (ref)`: 250 synthetic dialogues similar to above, but contains even shorter utterances as this set is meant to include reference clips in it's context, similar to `two-speaker-conversation`.

We report the word-error-rate (WER) and the geometric mean between intra-speaker similarity and inter-speaker dis-similarity on these three subsets. Other than Higgs Audio v2, we also evaluated MoonCast and nari-labs/Dia-1.6B-0626, two of the most popular open-source models capable of multi-speaker dialog generation. Results are summarized in the following table. We are not able to run nari-labs/Dia-1.6B-0626 on our "two-speaker-conversation" subset due to its strict limitation on the length of the utterances and output audio.

two-speaker-conversation

small talk

small talk (no ref)

WER ↓

Mean Sim & Dis-sim ↑

WER ↓

Mean Sim & Dis-sim ↑

WER ↓

Mean Sim & Dis-sim ↑

MoonCast

38.77

46.02

**8.33**

63.68

24.65

53.94

nari-labs/Dia-1.6B-0626

\-

\-

17.62

63.15

19.46

**61.14**

Higgs Audio v2 (base)

**18.88**

**51.95**

11.89

**67.92**

**14.65**

55.28

Contribution and Support
------------------------

For contribution and support guidelines, please see the support guidelines at SUPPORT\_GUIDELINES.md.

Citation
--------

If you feel the repository is helpful, please kindly cite as:

```
@misc{higgsaudio2025,
  author       = {{Boson AI}},
  title        = {{Higgs Audio V2: Redefining Expressiveness in Audio Generation}},
  year         = {2025},
  howpublished = {\url{https://github.com/boson-ai/higgs-audio}},
  note         = {GitHub repository. Release blog available at \url{https://www.boson.ai/blog/higgs-audio-v2}},
}
```

Third-Party Licenses
--------------------

The `boson_multimodal/audio_processing/` directory contains code derived from third-party repositories, primarily from xcodec. Please see the `LICENSE` in that directory for complete attribution and licensing information.

We Are Hiring!
--------------

If you are passionate about multimodal AI, speech/audio models, or large-scale systems, check out our open positions at Boson AI Careers.
