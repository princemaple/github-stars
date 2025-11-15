---
project: Auralis
stars: 567
description: A Fast TTS Engine
url: https://github.com/astramind-ai/Auralis
---

Auralis 🌌 (/auˈralis/)
=======================

Transform text into natural speech (with voice cloning) at warp speed. Process an entire novel in minutes, not hours.

What is Auralis? 🚀
-------------------

Auralis is a text-to-speech engine that makes voice generation practical for real-world use:

-   Convert the entire first Harry Potter book to speech in 10 minutes (**realtime factor of ≈ 0.02x!** )
-   Automatically enhance the reference quality, you can register them even with a low quality mic!
-   It can be configured to have a small memory footprint (scheduler\_max\_concurrency)
-   Process multiple requests simultaneously
-   Stream long texts piece by piece

Quick Start ⭐
-------------

1.  Create a new Conda environment:
    
    conda create -n auralis\_env python=3.10 -y
    
2.  Activate the environment:
    
    conda activate auralis\_env
    
3.  Install Auralis:
    
    pip install auralis
    

and then you can try it out via **python**

from auralis import TTS, TTSRequest

\# Initialize
tts \= TTS().from\_pretrained("AstraMindAI/xttsv2", gpt\_model\='AstraMindAI/xtts2-gpt')

\# Generate speech
request \= TTSRequest(
    text\="Hello Earth! This is Auralis speaking.",
    speaker\_files\=\['reference.wav'\]
)

output \= tts.generate\_speech(request)
output.save('hello.wav')

or via **cli** using the openai compatible server

```
auralis.openai --host 127.0.0.1 --port 8000 --model AstraMindAI/xttsv2 --gpt_model AstraMindAI/xtts2-gpt --max_concurrency 8 --vllm_logging_level warn  
```

You can see here for a more in-depth explanation or try it out with this example

Key Features 🛸
---------------

### Speed & Efficiency

-   Processes long texts rapidly using smart batching
-   Runs on consumer GPUs without memory issues
-   Handles multiple requests in parallel

### Easy Integration

-   Simple Python API
-   Streaming support for long texts
-   Built-in audio enhancement
-   Automatic language detection

### Audio Quality

-   Voice cloning from short samples
-   Background noise reduction
-   Speech clarity enhancement
-   Volume normalization

XTTSv2 Finetunes
----------------

You can use your own XTTSv2 finetunes by simply converting them from the standard coqui checkpoint format to our safetensor format. Use this script:

```
python checkpoint_converter.py path/to/checkpoint.pth --output_dir path/to/output
```

it will create two folders, one with the core xttsv2 checkpoint and one with the gtp2 component. Then create a TTS instance with

tts \= TTS().from\_pretrained("som/core-xttsv2\_model", gpt\_model\='some/xttsv2-gpt\_model')

Examples & Usage 🚀
-------------------

### Basic Examples ⭐

**Simple Text Generation**

from auralis import TTS, TTSRequest

\# Initialize
tts \= TTS().from\_pretrained("AstraMindAI/xttsv2", gpt\_model\='AstraMindAI/xtts2-gpt')
\# Basic generation
request \= TTSRequest(
    text\="Hello Earth! This is Auralis speaking.",
    speaker\_files\=\["speaker.wav"\]
)
output \= tts.generate\_speech(request)
output.save("hello.wav")

**Working with TTSRequest** 🎤

\# Basic request
request \= TTSRequest(
    text\="Hello world!",
    speaker\_files\=\["speaker.wav"\]
)

\# Enhanced audio processing
request \= TTSRequest(
    text\="Pristine audio quality",
    speaker\_files\=\["speaker.wav"\],
    audio\_config\=AudioPreprocessingConfig(
        normalize\=True,
        trim\_silence\=True,
        enhance\_speech\=True,
        enhance\_amount\=1.5
    )
)

\# Language-specific request
request \= TTSRequest(
    text\="Bonjour le monde!",
    speaker\_files\=\["speaker.wav"\],
    language\="fr"
)

\# Streaming configuration
request \= TTSRequest(
    text\="Very long text...",
    speaker\_files\=\["speaker.wav"\],
    stream\=True,
)

\# Generation parameters
request \= TTSRequest(
    text\="Creative variations",
    speaker\_files\=\["speaker.wav"\],
    temperature\=0.8,
    top\_p\=0.9,
    top\_k\=50
)

**Working with TTSOutput** 🎧

\# Load audio file
output \= TTSOutput.from\_file("input.wav")

\# Format conversion
output.bit\_depth \= 32
output.channel \= 2
tensor\_audio \= output.to\_tensor()
audio\_bytes \= output.to\_bytes()

\# Audio processing
resampled \= output.resample(target\_sr\=44100)
faster \= output.change\_speed(1.5)
num\_samples, sample\_rate, duration \= output.get\_info()

\# Combine multiple outputs
combined \= TTSOutput.combine\_outputs(\[output1, output2, output3\])

\# Playback and saving
output.play()  \# Play audio
output.preview()  \# Smart playback (Jupyter/system)
output.save("processed.wav", sample\_rate\=44100)

### Synchronous Advanced Examples 🌟

**Batch Text Processing**

\# Process multiple texts with same voice
texts \= \["First paragraph.", "Second paragraph.", "Third paragraph."\]
requests \= \[
    TTSRequest(
        text\=text,
        speaker\_files\=\["speaker.wav"\]
    ) for text in texts
\]

\# Sequential processing with progress
outputs \= \[\]
for i, req in enumerate(requests, 1):
    print(f"Processing text {i}/{len(requests)}")
    outputs.append(tts.generate\_speech(req))

\# Combine all outputs
combined \= TTSOutput.combine\_outputs(outputs)
combined.save("combined\_output.wav")

**Book Chapter Processing**

def process\_book(chapter\_file: str, speaker\_file: str):
    \# Read chapter
    with open(chapter\_file, 'r') as f:
        chapter \= f.read()
    
    \# You can pass the whole book, auralis will take care of splitting
    
    request \= TTSRequest(
            text\=chapter,
            speaker\_files\=\[speaker\_file\],
            audio\_config\=AudioPreprocessingConfig(
                enhance\_speech\=True,
                normalize\=True
            )
        )
        
    output \= tts.generate\_speech(request)
    
    output.play()
    output.save("chapter\_output.wav")

### Asynchronous Examples 🛸

**Basic Async Generation**

import asyncio
from auralis import TTS, TTSRequest

async def generate\_speech():
    tts \= TTS().from\_pretrained("AstraMindAI/xttsv2", gpt\_model\='AstraMindAI/xtts2-gpt')
    
    request \= TTSRequest(
        text\="Async generation example",
        speaker\_files\=\["speaker.wav"\]
    )
    
    output \= await tts.generate\_speech\_async(request)
    output.save("async\_output.wav")

asyncio.run(generate\_speech())

**Parallel Processing**

async def generate\_parallel():
    tts \= TTS().from\_pretrained("AstraMindAI/xttsv2", gpt\_model\='AstraMindAI/xtts2-gpt')
    
    \# Create multiple requests
    requests \= \[
        TTSRequest(
            text\=f"This is voice {i}",
            speaker\_files\=\[f"speaker\_{i}.wav"\]
        ) for i in range(3)
    \]
    
    \# Process in parallel
    coroutines \= \[tts.generate\_speech\_async(req) for req in requests\]
    outputs \= await asyncio.gather(\*coroutines, return\_exceptions\=True)
    
    \# Handle results
    valid\_outputs \= \[
        out for out in outputs 
        if not isinstance(out, Exception)
    \]
    
    combined \= TTSOutput.combine\_outputs(valid\_outputs)
    combined.save("parallel\_output.wav")

asyncio.run(generate\_parallel())

**Async Streaming with Multiple Requests**

async def stream\_multiple\_texts():
    tts \= TTS().from\_pretrained("AstraMindAI/xttsv2", gpt\_model\='AstraMindAI/xtts2-gpt')
    
    \# Prepare streaming requests
    texts \= \[
        "First long text...",
        "Second long text...",
        "Third long text..."
    \]
    
    requests \= \[
        TTSRequest(
            text\=text,
            speaker\_files\=\["speaker.wav"\],
            stream\=True,
        ) for text in texts
    \]
    
    \# Process streams in parallel
    coroutines \= \[tts.generate\_speech\_async(req) for req in requests\]
    streams \= await asyncio.gather(\*coroutines)
    
    \# Collect outputs
    output\_container \= {i: \[\] for i in range(len(requests))}
    
    async def process\_stream(idx, stream):
        async for chunk in stream:
            output\_container\[idx\].append(chunk)
            print(f"Processed chunk for text {idx+1}")
            
    \# Process all streams
    await asyncio.gather(
        \*(process\_stream(i, stream) 
          for i, stream in enumerate(streams))
    )
    
    \# Save results
    for idx, chunks in output\_container.items():
        TTSOutput.combine\_outputs(chunks).save(
            f"text\_{idx}\_output.wav"
        )

asyncio.run(stream\_multiple\_texts())

Core Classes 🌟
---------------

**TTSRequest** - Unified request container with audio enhancement 🎤

@dataclass
class TTSRequest:
    """Container for TTS inference request data"""
    \# Request metadata
    text: Union\[AsyncGenerator\[str, None\], str, List\[str\]\]

    speaker\_files: Union\[List\[str\], bytes\]  \# Path to the speaker audio file

    enhance\_speech: bool \= True
    audio\_config: AudioPreprocessingConfig \= field(default\_factory\=AudioPreprocessingConfig)
    language: SupportedLanguages \= "auto"
    request\_id: str \= field(default\_factory\=lambda: uuid.uuid4().hex)
    load\_sample\_rate: int \= 22050
    sound\_norm\_refs: bool \= False

    \# Voice conditioning parameters
    max\_ref\_length: int \= 60
    gpt\_cond\_len: int \= 30
    gpt\_cond\_chunk\_len: int \= 4

    \# Generation parameters
    stream: bool \= False
    temperature: float \= 0.75
    top\_p: float \= 0.85
    top\_k: int \= 50
    repetition\_penalty: float \= 5.0
    length\_penalty: float \= 1.0
    do\_sample: bool \= True

### Examples

\# Basic usage
request \= TTSRequest(
    text\="Hello world!",
    speaker\_files\=\["reference.wav"\]
)

\# With custom audio enhancement
request \= TTSRequest(
    text\="Hello world!",
    speaker\_files\=\["reference.wav"\],
    audio\_config\=AudioPreprocessingConfig(
        normalize\=True,
        trim\_silence\=True,
        enhance\_speech\=True,
        enhance\_amount\=1.5
    )
)

\# Streaming long text
request \= TTSRequest(
    text\="Very long text...",
    speaker\_files\=\["reference.wav"\],
    stream\=True,
)

### Features

-   Automatic language detection
-   Audio preprocessing & enhancement
-   Flexible input handling (strings, lists, generators)
-   Configurable generation parameters
-   Caching for efficient processing

**TTSOutput** - Unified output container for audio processing 🎧

@dataclass
class TTSOutput:
    array: np.ndarray
    sample\_rate: int

### Methods

#### Format Conversion

output.to\_tensor()      \# → torch.Tensor
output.to\_bytes()       \# → bytes (wav/raw)
output.from\_tensor()    \# → TTSOutput
output.from\_file()      \# → TTSOutput

#### Audio Processing

output.combine\_outputs()  \# Combine multiple outputs
output.resample()        \# Change sample rate
output.get\_info()        \# Get audio properties
output.change\_speed()    \# Modify playback speed

#### File & Playback

output.save()           \# Save to file
output.play()          \# Play audio
output.display()       \# Show in Jupyter
output.preview()       \# Smart playback

### Examples

\# Load and process
output \= TTSOutput.from\_file("input.wav")
output \= output.resample(target\_sr\=44100)
output.save("output.wav")

\# Combine multiple outputs
combined \= TTSOutput.combine\_outputs(\[output1, output2, output3\])

\# Change playback speed
faster \= output.change\_speed(1.5)

Languages 🌍
------------

XTTSv2 Supports: English, Spanish, French, German, Italian, Portuguese, Polish, Turkish, Russian, Dutch, Czech, Arabic, Chinese (Simplified), Hungarian, Korean, Japanese, Hindi

Performance Details 📊
----------------------

Processing speeds on NVIDIA 3090:

-   Short phrases (< 100 chars): ~1 second
-   Medium texts (< 1000 chars): ~5-10 seconds
-   Full books (~500K chars @ concurrency 36): ~10 minutes

Memory usage:

-   Base: ~2.5GB VRAM concurrency = 1
-   ~ 5.3GB VRAM concurrency = 20

Gradio
------

Gradio code

Contributions
-------------

**Join Our Community!**

We welcome and appreciate any contributions to our project! To ensure a smooth and efficient process, please take a moment to review our Contribution Guideline. By following these guidelines, you'll help us review and accept your contribution quickly. Thank you for your support!

Learn More 🔭
-------------

-   Technical Deep Dive
-   Adding Custom Models

License
-------

The codebase is released under Apache 2.0, feel free to use it in your projects.

The XTTSv2 model (and the files under auralis/models/xttsv2/components/tts) are licensed under the Coqui AI License.
