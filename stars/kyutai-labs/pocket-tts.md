---
project: pocket-tts
stars: 9372
description: A TTS that fits in your CPU (and pocket)
url: https://github.com/kyutai-labs/pocket-tts
---

Pocket TTS
==========

A lightweight text-to-speech (TTS) application designed to run efficiently on CPUs. Forget about the hassle of using GPUs and web APIs serving TTS models. With Kyutai's Pocket TTS, generating audio is just a pip install and a function call away.

Supports Python 3.10, 3.11, 3.12, 3.13 and 3.14. Requires PyTorch 2.5+. Does not require the gpu version of PyTorch.

🔊 Demo | 🐱‍💻GitHub Repository | 🤗 Hugging Face Model Card | ⚙️ Tech report | 📄 Paper | 📚 Documentation

Note

**New (August 2026):** We've released the training code! Check out `training/` to start training your own models. Open a PR to add your model to the Models trained by the community section.

Main takeaways
--------------

-   Runs on CPU
-   Small model size, 100M parameters
-   Audio streaming
-   Low latency, ~200ms to get the first audio chunk
-   Faster than real-time, ~6x real-time on a CPU of MacBook Air M4
-   Uses only 2 CPU cores
-   Python API and CLI
-   Voice cloning
-   Multi-language support: english, french, german, portuguese, italian, spanish
-   Can handle infinitely long text inputs
-   Can run on client-side in the browser

Additional languages may be added in the future.

Trying it from the website, without installing anything
-------------------------------------------------------

Navigate to the Kyutai website to try it out directly in your browser. You can input text, select different voices, and generate speech without any installation.

Trying it with the CLI
----------------------

### The `generate` command

You can use pocket-tts directly from the command line. We recommend using `uv` as it installs any dependencies on the fly in an isolated environment (uv installation instructions here). You can also use `pip install pocket-tts` to install it manually. On Linux, see CPU-only installation to avoid pulling in the CUDA build of PyTorch.

This will generate a wav file `./tts_output.wav` saying the default text with the default voice, and display some speed statistics.

uvx pocket-tts generate
# or if you installed it manually with pip:
pocket-tts generate

Modify the voice with `--voice` and the text with `--text`. We provide a small catalog of voices. Choose a pretrained language model with `--language` when running `generate`, `export-voice`, or `serve` (default: `english`). Non-english languages have also biggers 24 layers variants that are higher quality but slower. You can select them by using for example `--language italian_24l`. The `--config` option accepts a local YAML path, an `https://` URL, or an `hf://` path (e.g. `hf://<repo_id>/<path>[@revision]`) for custom weights.

You can take a look at this page which details the licenses for each voice.

-   alba (en)
-   giovanni (it)
-   lola (es)
-   juergen (de)
-   rafael (pt)
-   estelle (fr)
-   anna (en)
-   azelma (en)
-   bill\_boerst (en)
-   caro\_davy (en)
-   charles (en)
-   cosette (en)
-   eponine (en)
-   eve (en)
-   fantine (en)
-   george (en)
-   jane (en)
-   jean (en)
-   javert (en)
-   marius (en)
-   mary (en)
-   michael (en)
-   paul (en)
-   peter\_yearsley (en)
-   stuart\_bell (en)
-   vera (en)

The `--voice` argument can also take a plain wav file as input for voice cloning. You can use your own or check out our voice repository. We recommend cleaning the sample before using it with Pocket TTS, because the audio quality of the sample is also reproduced.

Feel free to check out the generate documentation for more details and examples. For trying multiple voices and prompts quickly, prefer using the `serve` command.

### The `serve` command

You can also run a local server to generate audio via HTTP requests.

uvx pocket-tts serve
# or if you installed it manually with pip:
pocket-tts serve

Navigate to `http://localhost:8000` to try the web interface, it's faster than the command line as the model is kept in memory between requests.

You can check out the serve documentation for more details and examples.

### The `export-voice` command

Processing an audio file (e.g., a .wav or .mp3) for voice cloning is relatively slow, but loading a safetensors file -- a voice embedding converted from an audio file -- is very fast. You can use the `export-voice` command to do this conversion. See the export-voice documentation for more details and examples.

Using it as a Python library
----------------------------

You can try out the Python library on Colab here.

Install the package with

pip install pocket-tts
# or
uv add pocket-tts

### CPU-only installation

On Linux, PyPI serves the CUDA build of PyTorch by default, so `pip install pocket-tts` also downloads the `nvidia-*` CUDA runtime wheels, even though pocket-tts runs on CPU. This adds several gigabytes to the install (with torch 2.13, roughly 3 GB instead of 200 MB). Installing from the PyTorch CPU index pulls the CPU build and no NVIDIA packages:

pip install pocket-tts --extra-index-url https://download.pytorch.org/whl/cpu

To run the CLI without installing, pass the same index to `uvx`:

uvx --index https://download.pytorch.org/whl/cpu pocket-tts generate

With `uv`, declare the index explicitly in your project:

\[\[tool.uv.index\]\]
name = "pytorch-cpu"
url = "https://download.pytorch.org/whl/cpu"
explicit = true

\[tool.uv.sources\]
torch = \[{ index = "pytorch-cpu" }\]

This is not needed on macOS or Windows, where the default PyTorch wheels are already CPU-only.

You can use this package as a simple Python library to generate audio from text.

from pocket\_tts import TTSModel
import scipy.io.wavfile

tts\_model \= TTSModel.load\_model()
voice\_state \= tts\_model.get\_state\_for\_audio\_prompt(
    "alba"  \# One of the pre-made voices, see above
    \# You can also use any voice file you have locally or from Hugging Face:
    \# "./some\_audio.wav"
    \# or "hf://kyutai/tts-voices/expresso/ex01-ex02\_default\_001\_channel2\_198s.wav"
)
audio \= tts\_model.generate\_audio(voice\_state, "Hello world, this is a test.")
\# Audio is a 1D torch tensor containing PCM data.
scipy.io.wavfile.write("output.wav", tts\_model.sample\_rate, audio.numpy())

You can have multiple voice states around if you have multiple voices you want to use. `load_model()` and `get_state_for_audio_prompt()` are relatively slow operations, so we recommend to keep the model and voice states in memory if you can.

For faster voice loading, you can export voice states to safetensors files:

from pocket\_tts import TTSModel, export\_model\_state

model \= TTSModel.load\_model()

\# Export a voice state for fast loading later
model\_state \= model.get\_state\_for\_audio\_prompt("some\_voice.wav")
export\_model\_state(model\_state, "./some\_voice.safetensors")

\# Later, load it quickly, this is quite fast as it's just reading the kvcache
\# from disk and doesn't do any others computations.
model\_state\_copy \= model.get\_state\_for\_audio\_prompt("./some\_voice.safetensors")

audio \= model.generate\_audio(model\_state\_copy, "Hello world!")

You can check out the Python API documentation for more details and examples.

Running on GPU
--------------

Pocket TTS is designed to run on CPU, and on hardware with strong single-thread CPU performance (e.g. Apple Silicon) we did not observe a GPU speedup, notably because we use a batch size of 1 and a very small model. However, this turns out to be hardware-dependent: measured on a cloud x86 VM (4 vCPUs) with a Tesla T4, moving the model to GPU gave a consistent ~2.6x speedup over CPU (RTF ~2.3-2.5x on CPU vs. ~6.28x on GPU, for both short and long input text). If your CPU is thread-limited or otherwise weaker than a modern laptop chip, it's worth trying the GPU.

This is not officially supported (there is no `device` argument on `TTSModel.load_model()`), but since `TTSModel` is a regular `nn.Module` you can move it yourself:

tts\_model \= TTSModel.load\_model()
tts\_model.to("cuda")
...
audio \= tts\_model.generate\_audio(voice\_state, "Hello world, this is a test.")
\# generate\_audio() returns a tensor on the same device as the model, so on GPU you need
\# to move it back to CPU before calling .numpy():
scipy.io.wavfile.write("output.wav", tts\_model.sample\_rate, audio.detach().cpu().numpy())

A few things to be aware of if you want to use the GPU:

-   The `generate` CLI command has a `--device` option (defaults to `cpu`, documented in the CLI reference — note that page's own description ("you may not get a speedup by using a gpu since it's a small model") is what this section is correcting, based on the T4 measurements above); the `serve` command and the Docker image do not expose any device option and will always run on CPU.
-   `pip install pocket-tts` / `uv add pocket-tts` install whatever `torch` build is current on PyPI, which may require a newer CUDA version than your driver supports. In that case `torch.cuda.is_available()` silently returns `False` (you'll only see a `UserWarning` about an outdated driver, not an error). If this happens, install a `torch` build matching your driver's CUDA version explicitly, e.g. `pip install torch --index-url https://download.pytorch.org/whl/cu121`.
-   `quantize=True` (int8 dynamic quantization) only works on CPU; calling it on a model moved to CUDA raises `NotImplementedError: Could not run 'quantized::linear_dynamic' ... 'CUDA' backend`. Separately, the optional `torchao` backend (`pip install pocket-tts[quantize]`) declares `torch>=2.11` — fine with a fresh install (torch 2.11+ is on PyPI as of this writing), but if you've pinned an older `torch` (e.g. to match an older GPU driver's CUDA build, per the point above), adding this extra can pull in a `torchao` that's incompatible with your pinned `torch` and break `quantize=True` even on CPU. Match `torchao`'s `torch` requirement to whatever `torch` you actually have installed.

Unsupported features
--------------------

At the moment, we do not support (but would love pull requests adding):

-   Adding silence in the text input to generate pauses.

We tried running this TTS model on the GPU but did not observe a speedup compared to CPU execution on hardware with very strong single-thread CPU performance, notably because we use a batch size of 1 and a very small model. See the "Running on GPU" section above for measurements on other hardware and caveats if you want to try it yourself.

Development and local setup
---------------------------

We accept contributions! Feel free to open issues or pull requests on GitHub.

You can find development instructions in the CONTRIBUTING.md file. You'll also find there how to have an editable install of the package for local development.

In-browser implementations
--------------------------

Pocket TTS is small enough to run directly in your browser in WebAssembly/JavaScript. We don't have official support for this yet, but you can try out one of these community implementations:

-   wasm-pocket-tts by @LaurentMazare: Rust port of pocket TTS with XN. Demo here
-   pocket-tts-onnx-export by @KevinAHM: Model exported to .onnx and run using ONNX Runtime Web. Demo here
-   pocket-tts by @babybirdprd: Candle version (Rust) with WebAssembly and PyO3 bindings, meaning it can run on the web too.
-   jax-js by @ekzhang: Using jax-js, a ML library for the web. Demo here

Alterative implementations
--------------------------

-   pocket-tts-mlx by @jishnuvenugopal - MLX backend optimized for Apple Silicon
-   pocket-tts-xn by @LaurentMazare - A Rust port of Pocket TTS implemented with XN.
-   pocket-tts-candle by @babybirdprd - Candle version (Rust) with WebAssembly and PyO3 bindings.
-   PocketTTS.cpp by @VolgaGerm - Single-file C++ runtime using ONNX Runtime, with CLI, HTTP server, and FFI C API.
-   sherpa-onnx by @csukuangfj - Run PocketTTS on **Windows, macOS, Linux**, and embedded boards (Raspberry Pi, Jetson, RK3588, etc.) with bindings for 12 programming languages: **C++, C, Python, JavaScript, Java, C#, Kotlin, Swift, Go, Dart, Rust, Pascal**, plus WebAssembly.
-   pocket-tts-csharp by @TheAjaykrishnanR - A C# port of Pocket TTS implemented using TorchSharp and TorchSharp.PyBridge for ease of use as a library in .NET projects.
-   pocket-tts-timestamped by @dpm63 - A fork that adds support for word-level timestamps.
-   Pocket-TTS-LiteRT by @john-rocky - LiteRT (.tflite) graphs that run on Android phone GPUs through the LiteRT CompiledModel API, ~1x real-time on a Pixel 8a, with Python and Kotlin usage snippets.

Models trained by the community
-------------------------------

To use a community model, just use the `--config` argument and point it to the url of the model's yaml file. For example:

uvx pocket-tts generate --config https://raw.githubusercontent.com/kyutai-labs/pocket-tts/refs/heads/main/pocket\_tts/config/english\_2026-04.yaml

It also works with huggingface urls like `hf://kyutai/pocket-tts/config/english_2026-04.yaml` or local paths like `./english_2026-04.yaml`.

The pre-made voices listed above are embeddings precomputed with our released weights, so they are not available for community models. With `--config`, `--voice` defaults to alba's audio file, which any model can clone. Pass your own audio file to `--voice` to use another voice.

We recommend inserting the commit hash somehow in the url to avoid breaking changes by the model authors. For example:

uvx pocket-tts generate --config https://raw.githubusercontent.com/kyutai-labs/pocket-tts/891886a61a1ed45fd429a0a63bd96181e6cff637/pocket\_tts/config/english\_2026-04.yaml

or with `hf://...`

uvx pocket-tts generate --config hf://user/repo/config\_file.yaml@commit\_hash

### List of community-trained models

-   pocket-tts-czech by @vvolhejn (trained internally at Kyutai):

uvx pocket-tts generate \\
  --config hf://vvolhejn/pocket-tts-czech/czech.yaml@7b7760dd0fe994a0800f2fdbc837dc4b8f219d1c \\
  --text "Dnešek je velmi dobrý den"

-   Pocket TTS Hindi by Saryps Labs (community research release):

uvx pocket-tts generate \\
  --config hf://saryps-labs/pocket-tts-hindi/config.yaml@dbaa326069d20bfbdaeb625613736773741a24ea \\
  --text "आज का दिन बहुत अच्छा है"

-   Pocket TTS Korean 300M by @seastar105 (community research release):

uvx pocket-tts generate \\
  --config hf://seastar105/pocket-tts-korean-300m/korean.yaml@df328c817a02866f20a6f74e5183e0a1fc6f6435 \\
  --text "안녕하세요. 한국어 음성 합성 모델입니다."

Want your model here? Head to the training Readme to get started!

Projects using Pocket TTS
-------------------------

-   pocket-reader by @lukasmwerner- Browser screen reader
-   pocket-tts-wyoming by @ikidd - Docker container for pocket-tts using Wyoming protocol, ready for Home Assistant Voice use.
-   Sonorus by @KevinAHM - Talk to any named character in Hogwarts Legacy with their original voice.
-   Native macOS App by @slaughters85j - Native macOS app, Python-free. Runs Pocket-TTS via Core ML, fully on-device. Includes signed and notarized .app releases.
-   Electron macOS App by @slaughters85j - Electron Mac Desktop App + macOS Quick Action
-   pocket-tts-openai\_streaming\_server by @teddybear082 - OpenAI-compatible streaming server, dockerized and with an `.exe` release
-   pocket-tts-unity by @lookbe - A Unity 6 integration for Pocket-TTS.
-   ComfyUI-Pocket-TTS by @ai-joe-git Lightweight CPU-based Text-to-Speech for ComfyUI
-   pocket-tts-server by @ai-joe-git A lightweight, real-time voice cloning and chat server with OpenAI-compatible API. Clone any voice with just 20 seconds of audio and chat with AI using that voice instantly.
-   discord-tts by @alkmei - Multivoice Discord text-to-speech bot that uses Pocket TTS.
-   cursed-codex by @dooart - AI coding agent with unhinged live football commentary
-   pocket-tts-deno Port of pocket-tts-server as a wasm + onnx deno server with voice TTS API.
-   FrontPocket by @markd89 - Front-end for Pocket-TTS to speak text from clipboard, file, CLI (hotkeys) & GUI toolbar. Change playback speed, voice, and move forward/backward between sentences instantaneously.
-   openclaw-pockettts by @dodgyrabbit - A Docker container with the Python implementation but exposed as an OpenAI TTS API for easy integration with OpenClaw.
-   openclaw-pocketts.cpp by @dodgyrabbit - A Docker container with the PocketTTS.cpp version, packaged for easy integration with OpenClaw.
-   tts-audiobook-tool by @zeropointnine - Multi-model audiobook generator with automatic error detection, 48khz upscaling, synced browser reader, stand-alone server-mode.
-   seshat-tts by @scriptriva - Accessibility tool that provides real-time audio synthesis for games and apps. It also features a voice manager capable of cloning voices based on user presets.
-   LocalVocal.ai by @joshwhiton - Fully local conversational voice-harness for Macs with Apple Silicon. Includes voice-activity & turn detection, dictation, voice cloning, CLI to talk to Claude, Codex... and more.

Prohibited use
--------------

Use of our model must comply with all applicable laws and regulations and must not result in, involve, or facilitate any illegal, harmful, deceptive, fraudulent, or unauthorized activity. Prohibited uses include, without limitation, voice impersonation or cloning without explicit and lawful consent; misinformation, disinformation, or deception (including fake news, fraudulent calls, or presenting generated content as genuine recordings of real people or events); and the generation of unlawful, harmful, libelous, abusive, harassing, discriminatory, hateful, or privacy-invasive content. We disclaim all liability for any non-compliant use.

Authors
-------

Manu Orsini\*, Simon Rouard\*, Gabriel De Marmiesse\*, Václav Volhejn, Neil Zeghidour, Alexandre Défossez

\*equal contribution
