---
project: litgpt
stars: 13072
description: 20+ high-performance LLMs with recipes to pretrain, finetune and deploy at scale.
url: https://github.com/Lightning-AI/litgpt
---

⚡ LitGPT
========

**20+ high-performance LLMs with recipes to pretrain, finetune, and deploy at scale.**

✅ From scratch implementations      ✅ No abstractions         ✅ Beginner friendly
   ✅ Flash attention                   ✅ FSDP                    ✅ LoRA, QLoRA, Adapter
✅ Reduce GPU memory (fp4/8/16/32)   ✅ 1-1000+ GPUs/TPUs       ✅ 20+ LLMs         

* * *

Quick start • Models • Finetune • Deploy • All workflows • Features • Recipes (YAML) • Lightning AI • Tutorials

Looking for GPUs?
=================

Over 340,000 developers use Lightning Cloud - purpose-built for PyTorch and PyTorch Lightning.

-   GPUs from $0.19.
-   Clusters: frontier-grade training/inference clusters.
-   AI Studio (vibe train): workspaces where AI helps you debug, tune and vibe train.
-   AI Studio (vibe deploy): workspaces where AI helps you optimize, and deploy models.
-   Notebooks: Persistent GPU workspaces where AI helps you code and analyze.
-   Inference: Deploy models as inference APIs.

Finetune, pretrain, and inference LLMs Lightning fast ⚡⚡
========================================================

Every LLM is implemented from scratch with **no abstractions** and **full control**, making them blazing fast, minimal, and performant at enterprise scale.

✅ **Enterprise ready -** Apache 2.0 for unlimited enterprise use.  
✅ **Developer friendly -** Easy debugging with no abstraction layers and single file implementations.  
✅ **Optimized performance -** Models designed to maximize performance, reduce costs, and speed up training.  
✅ **Proven recipes -** Highly-optimized training/finetuning recipes tested at enterprise scale.  

Quick start
===========

Install LitGPT

```
pip install 'litgpt[extra]'
```

Load and use any of the 20+ LLMs:

from litgpt import LLM

llm \= LLM.load("microsoft/phi-2")
text \= llm.generate("Fix the spelling: Every fall, the family goes to the mountains.")
print(text)
\# Corrected Sentence: Every fall, the family goes to the mountains.

✅ Optimized for fast inference  
✅ Quantization  
✅ Runs on low-memory GPUs  
✅ No layers of internal abstractions  
✅ Optimized for production scale  

Advanced install options

Install from source:

git clone https://github.com/Lightning-AI/litgpt
cd litgpt
pip install -e '.\[all\]'

Explore the full Python API docs.

* * *

Choose from 20+ LLMs
====================

Every model is written from scratch to maximize performance and remove layers of abstraction:

Model

Model size

Author

Reference

Llama 3, 3.1, 3.2, 3.3

1B, 3B, 8B, 70B, 405B

Meta AI

Meta AI 2024

Code Llama

7B, 13B, 34B, 70B

Meta AI

Rozière et al. 2023

CodeGemma

7B

Google

Google Team, Google Deepmind

Gemma 2

2B, 9B, 27B

Google

Google Team, Google Deepmind

Phi 4

14B

Microsoft Research

Abdin et al. 2024

Qwen2.5

0.5B, 1.5B, 3B, 7B, 14B, 32B, 72B

Alibaba Group

Qwen Team 2024

Qwen2.5 Coder

0.5B, 1.5B, 3B, 7B, 14B, 32B

Alibaba Group

Hui, Binyuan et al. 2024

R1 Distill Llama

8B, 70B

DeepSeek AI

DeepSeek AI 2025

...

...

...

...

See full list of 20+ LLMs

#### All models

Model

Model size

Author

Reference

CodeGemma

7B

Google

Google Team, Google Deepmind

Code Llama

7B, 13B, 34B, 70B

Meta AI

Rozière et al. 2023

Falcon

7B, 40B, 180B

TII UAE

TII 2023

Falcon 3

1B, 3B, 7B, 10B

TII UAE

TII 2024

FreeWilly2 (Stable Beluga 2)

70B

Stability AI

Stability AI 2023

Function Calling Llama 2

7B

Trelis

Trelis et al. 2023

Gemma

2B, 7B

Google

Google Team, Google Deepmind

Gemma 2

9B, 27B

Google

Google Team, Google Deepmind

Gemma 3

1B, 4B, 12B, 27B

Google

Google Team, Google Deepmind

Llama 2

7B, 13B, 70B

Meta AI

Touvron et al. 2023

Llama 3.1

8B, 70B

Meta AI

Meta AI 2024

Llama 3.2

1B, 3B

Meta AI

Meta AI 2024

Llama 3.3

70B

Meta AI

Meta AI 2024

Mathstral

7B

Mistral AI

Mistral AI 2024

MicroLlama

300M

Ken Wang

MicroLlama repo

Mixtral MoE

8x7B

Mistral AI

Mistral AI 2023

Mistral

7B, 123B

Mistral AI

Mistral AI 2023

Mixtral MoE

8x22B

Mistral AI

Mistral AI 2024

OLMo

1B, 7B

Allen Institute for AI (AI2)

Groeneveld et al. 2024

OpenLLaMA

3B, 7B, 13B

OpenLM Research

Geng & Liu 2023

Phi 1.5 & 2

1.3B, 2.7B

Microsoft Research

Li et al. 2023

Phi 3

3.8B

Microsoft Research

Abdin et al. 2024

Phi 4

14B

Microsoft Research

Abdin et al. 2024

Phi 4 Mini Instruct

3.8B

Microsoft Research

Microsoft 2025

Phi 4 Mini Reasoning

3.8B

Microsoft Research

Xu, Peng et al. 2025

Phi 4 Reasoning

3.8B

Microsoft Research

Abdin et al. 2025

Phi 4 Reasoning Plus

3.8B

Microsoft Research

Abdin et al. 2025

Platypus

7B, 13B, 70B

Lee et al.

Lee, Hunter, and Ruiz 2023

Pythia

{14,31,70,160,410}M, {1,1.4,2.8,6.9,12}B

EleutherAI

Biderman et al. 2023

Qwen2.5

0.5B, 1.5B, 3B, 7B, 14B, 32B, 72B

Alibaba Group

Qwen Team 2024

Qwen2.5 Coder

0.5B, 1.5B, 3B, 7B, 14B, 32B

Alibaba Group

Hui, Binyuan et al. 2024

Qwen2.5 1M (Long Context)

7B, 14B

Alibaba Group

Qwen Team 2025

Qwen2.5 Math

1.5B, 7B, 72B

Alibaba Group

An, Yang et al. 2024

QwQ

32B

Alibaba Group

Qwen Team 2025

QwQ-Preview

32B

Alibaba Group

Qwen Team 2024

Qwen3

0.6B, 1.7B, 4B{Hybrid, Thinking-2507, Instruct-2507}, 8B, 14B, 32B

Alibaba Group

Qwen Team 2025

Qwen3 MoE

30B{Hybrid, Thinking-2507, Instruct-2507}, 235B{Hybrid, Thinking-2507, Instruct-2507}

Alibaba Group

Qwen Team 2025

R1 Distill Llama

8B, 70B

DeepSeek AI

DeepSeek AI 2025

SmolLM2

135M, 360M, 1.7B

Hugging Face

Hugging Face 2024

Salamandra

2B, 7B

Barcelona Supercomputing Centre

BSC-LTC 2024

StableCode

3B

Stability AI

Stability AI 2023

StableLM

3B, 7B

Stability AI

Stability AI 2023

StableLM Zephyr

3B

Stability AI

Stability AI 2023

TinyLlama

1.1B

Zhang et al.

Zhang et al. 2023

**Tip**: You can list all available models by running the `litgpt download list` command.

* * *

Workflows
=========

Finetune • Pretrain • Continued pretraining • Evaluate • Deploy • Test

Use the command line interface to run advanced workflows such as pretraining or finetuning on your own data.

All workflows
-------------

After installing LitGPT, select the model and workflow to run (finetune, pretrain, evaluate, deploy, etc...):

# litgpt \[action\] \[model\]
litgpt  serve     meta-llama/Llama-3.2-3B-Instruct
litgpt  finetune  meta-llama/Llama-3.2-3B-Instruct
litgpt  pretrain  meta-llama/Llama-3.2-3B-Instruct
litgpt  chat      meta-llama/Llama-3.2-3B-Instruct
litgpt  evaluate  meta-llama/Llama-3.2-3B-Instruct

* * *

Finetune an LLM
---------------

Finetuning is the process of taking a pretrained AI model and further training it on a smaller, specialized dataset tailored to a specific task or application.

# 0) setup your dataset
curl -L https://huggingface.co/datasets/ksaw008/finance\_alpaca/resolve/main/finance\_alpaca.json -o my\_custom\_dataset.json

# 1) Finetune a model (auto downloads weights)
litgpt finetune microsoft/phi-2 \\
  --data JSON \\
  --data.json\_path my\_custom\_dataset.json \\
  --data.val\_split\_fraction 0.1 \\
  --out\_dir out/custom-model

# 2) Test the model
litgpt chat out/custom-model/final

# 3) Deploy the model
litgpt serve out/custom-model/final

Read the full finetuning docs

* * *

Deploy an LLM
-------------

Deploy a pretrained or finetune LLM to use it in real-world applications. Deploy, automatically sets up a web server that can be accessed by a website or app.

# deploy an out-of-the-box LLM
litgpt serve microsoft/phi-2

# deploy your own trained model
litgpt serve path/to/microsoft/phi-2/checkpoint

Show code to query server:

Test the server in a separate terminal and integrate the model API into your AI product:

\# 3) Use the server (in a separate Python session)
import requests, json
response \= requests.post(
    "http://127.0.0.1:8000/predict",
    json\={"prompt": "Fix typos in the following sentence: Example input"}
)
print(response.json()\["output"\])

Read the full deploy docs.

* * *

Evaluate an LLM
---------------

Evaluate an LLM to test its performance on various tasks to see how well it understands and generates text. Simply put, we can evaluate things like how well would it do in college-level chemistry, coding, etc... (MMLU, Truthful QA, etc...)

litgpt evaluate microsoft/phi-2 --tasks 'truthfulqa\_mc2,mmlu'

Read the full evaluation docs.

* * *

Test an LLM
-----------

Test how well the model works via an interactive chat. Use the `chat` command to chat, extract embeddings, etc...

Here's an example showing how to use the Phi-2 LLM:

litgpt chat microsoft/phi-2

\>> Prompt: What do Llamas eat?

Full code:

# 1) List all supported LLMs
litgpt download list

# 2) Use a model (auto downloads weights)
litgpt chat microsoft/phi-2

\>> Prompt: What do Llamas eat?

The download of certain models requires an additional access token. You can read more about this in the download documentation.

Read the full chat docs.

* * *

Pretrain an LLM
---------------

Pretraining is the process of teaching an AI model by exposing it to a large amount of data before it is fine-tuned for specific tasks.

Show code:

mkdir -p custom\_texts
curl https://www.gutenberg.org/cache/epub/24440/pg24440.txt --output custom\_texts/book1.txt
curl https://www.gutenberg.org/cache/epub/26393/pg26393.txt --output custom\_texts/book2.txt

# 1) Download a tokenizer
litgpt download EleutherAI/pythia-160m \\
  --tokenizer\_only True

# 2) Pretrain the model
litgpt pretrain EleutherAI/pythia-160m \\
  --tokenizer\_dir EleutherAI/pythia-160m \\
  --data TextFiles \\
  --data.train\_data\_path "custom\_texts/" \\
  --train.max\_tokens 10\_000\_000 \\
  --out\_dir out/custom-model

# 3) Test the model
litgpt chat out/custom-model/final

Read the full pretraining docs

* * *

Continue pretraining an LLM
---------------------------

Continued pretraining is another way of finetuning that specializes an already pretrained model by training on custom data:

Show code:

mkdir -p custom\_texts
curl https://www.gutenberg.org/cache/epub/24440/pg24440.txt --output custom\_texts/book1.txt
curl https://www.gutenberg.org/cache/epub/26393/pg26393.txt --output custom\_texts/book2.txt

# 1) Continue pretraining a model (auto downloads weights)
litgpt pretrain EleutherAI/pythia-160m \\
  --tokenizer\_dir EleutherAI/pythia-160m \\
  --initial\_checkpoint\_dir EleutherAI/pythia-160m \\
  --data TextFiles \\
  --data.train\_data\_path "custom\_texts/" \\
  --train.max\_tokens 10\_000\_000 \\
  --out\_dir out/custom-model

# 2) Test the model
litgpt chat out/custom-model/final

Read the full continued pretraining docs

* * *

State-of-the-art features
=========================

✅ State-of-the-art optimizations: Flash Attention v2, multi-GPU support via fully-sharded data parallelism, optional CPU offloading, and TPU and XLA support.  
✅ Pretrain, finetune, and deploy  
✅ Reduce compute requirements with low-precision settings: FP16, BF16, and FP16/FP32 mixed.  
✅ Lower memory requirements with quantization: 4-bit floats, 8-bit integers, and double quantization.  
✅ Configuration files for great out-of-the-box performance.  
✅ Parameter-efficient finetuning: LoRA, QLoRA, Adapter, and Adapter v2.  
✅ Exporting to other popular model weight formats.  
✅ Many popular datasets for pretraining and finetuning, and support for custom datasets.  
✅ Readable and easy-to-modify code to experiment with the latest research ideas.  

* * *

Training recipes
================

LitGPT comes with validated recipes (YAML configs) to train models under different conditions. We've generated these recipes based on the parameters we found to perform the best for different training conditions.

Browse all training recipes here.

### Example

litgpt finetune \\
  --config https://raw.githubusercontent.com/Lightning-AI/litgpt/main/config\_hub/finetune/llama-2-7b/lora.yaml

✅ Use configs to customize training

Configs let you customize training for all granular parameters like:

# The path to the base model's checkpoint directory to load for finetuning. (type: <class 'Path'>, default: checkpoints/stabilityai/stablelm-base-alpha-3b)
checkpoint\_dir: checkpoints/meta-llama/Llama-2-7b-hf

# Directory in which to save checkpoints and logs. (type: <class 'Path'>, default: out/lora)
out\_dir: out/finetune/qlora-llama2-7b

# The precision to use for finetuning. Possible choices: "bf16-true", "bf16-mixed", "32-true". (type: Optional\[str\], default: null)
precision: bf16-true

...

✅ Example: LoRA finetuning config

# The path to the base model's checkpoint directory to load for finetuning. (type: <class 'Path'>, default: checkpoints/stabilityai/stablelm-base-alpha-3b)
checkpoint\_dir: checkpoints/meta-llama/Llama-2-7b-hf

# Directory in which to save checkpoints and logs. (type: <class 'Path'>, default: out/lora)
out\_dir: out/finetune/qlora-llama2-7b

# The precision to use for finetuning. Possible choices: "bf16-true", "bf16-mixed", "32-true". (type: Optional\[str\], default: null)
precision: bf16-true

# If set, quantize the model with this algorithm. See \`\`tutorials/quantize.md\`\` for more information. (type: Optional\[Literal\['nf4', 'nf4-dq', 'fp4', 'fp4-dq', 'int8-training'\]\], default: null)
quantize: bnb.nf4

# How many devices/GPUs to use. (type: Union\[int, str\], default: 1)
devices: 1

# How many nodes to use. (type: int, default: 1)
num\_nodes: 1

# The LoRA rank. (type: int, default: 8)
lora\_r: 32

# The LoRA alpha. (type: int, default: 16)
lora\_alpha: 16

# The LoRA dropout value. (type: float, default: 0.05)
lora\_dropout: 0.05

# Whether to apply LoRA to the query weights in attention. (type: bool, default: True)
lora\_query: true

# Whether to apply LoRA to the key weights in attention. (type: bool, default: False)
lora\_key: false

# Whether to apply LoRA to the value weights in attention. (type: bool, default: True)
lora\_value: true

# Whether to apply LoRA to the output projection in the attention block. (type: bool, default: False)
lora\_projection: false

# Whether to apply LoRA to the weights of the MLP in the attention block. (type: bool, default: False)
lora\_mlp: false

# Whether to apply LoRA to output head in GPT. (type: bool, default: False)
lora\_head: false

# Data-related arguments. If not provided, the default is \`\`litgpt.data.Alpaca\`\`.
data:
  class\_path: litgpt.data.Alpaca2k
  init\_args:
    mask\_prompt: false
    val\_split\_fraction: 0.05
    prompt\_style: alpaca
    ignore\_index: \-100
    seed: 42
    num\_workers: 4
    download\_dir: data/alpaca2k

# Training-related arguments. See \`\`litgpt.args.TrainArgs\`\` for details
train:

  # Number of optimizer steps between saving checkpoints (type: Optional\[int\], default: 1000)
  save\_interval: 200

  # Number of iterations between logging calls (type: int, default: 1)
  log\_interval: 1

  # Number of samples between optimizer steps across data-parallel ranks (type: int, default: 128)
  global\_batch\_size: 8

  # Number of samples per data-parallel rank (type: int, default: 4)
  micro\_batch\_size: 2

  # Number of iterations with learning rate warmup active (type: int, default: 100)
  lr\_warmup\_steps: 10

  # Number of epochs to train on (type: Optional\[int\], default: 5)
  epochs: 4

  # Total number of tokens to train on (type: Optional\[int\], default: null)
  max\_tokens:

  # Limits the number of optimizer steps to run (type: Optional\[int\], default: null)
  max\_steps:

  # Limits the length of samples (type: Optional\[int\], default: null)
  max\_seq\_length: 512

  # Whether to tie the embedding weights with the language modeling head weights (type: Optional\[bool\], default: null)
  tie\_embeddings:

  #   (type: float, default: 0.0003)
  learning\_rate: 0.0002

  #   (type: float, default: 0.02)
  weight\_decay: 0.0

  #   (type: float, default: 0.9)
  beta1: 0.9

  #   (type: float, default: 0.95)
  beta2: 0.95

  #   (type: Optional\[float\], default: null)
  max\_norm:

  #   (type: float, default: 6e-05)
  min\_lr: 6.0e-05

# Evaluation-related arguments. See \`\`litgpt.args.EvalArgs\`\` for details
eval:

  # Number of optimizer steps between evaluation calls (type: int, default: 100)
  interval: 100

  # Number of tokens to generate (type: Optional\[int\], default: 100)
  max\_new\_tokens: 100

  # Number of iterations (type: int, default: 100)
  max\_iters: 100

# The name of the logger to send metrics to. (type: Literal\['wandb', 'tensorboard', 'csv'\], default: csv)
logger\_name: csv

# The random seed to use for reproducibility. (type: int, default: 1337)
seed: 1337

✅ Override any parameter in the CLI:

litgpt finetune \\
  --config https://raw.githubusercontent.com/Lightning-AI/litgpt/main/config\_hub/finetune/llama-2-7b/lora.yaml \\
  --lora\_r 4

* * *

Project highlights
==================

LitGPT powers many great AI projects, initiatives, challenges and of course enterprises. Please submit a pull request to be considered for a feature.

📊 SAMBA: Simple Hybrid State Space Models for Efficient Unlimited Context Language Modeling

The Samba project by researchers at Microsoft is built on top of the LitGPT code base and combines state space models with sliding window attention, which outperforms pure state space models.

🏆 NeurIPS 2023 Large Language Model Efficiency Challenge: 1 LLM + 1 GPU + 1 Day

The LitGPT repository was the official starter kit for the NeurIPS 2023 LLM Efficiency Challenge, which is a competition focused on finetuning an existing non-instruction tuned LLM for 24 hours on a single GPU.

🦙 TinyLlama: An Open-Source Small Language Model

LitGPT powered the TinyLlama project and TinyLlama: An Open-Source Small Language Model research paper.

🍪 MicroLlama: MicroLlama-300M

MicroLlama is a 300M Llama model pretrained on 50B tokens powered by TinyLlama and LitGPT.

🔬 Pre-training Small Base LMs with Fewer Tokens

The research paper "Pre-training Small Base LMs with Fewer Tokens", which utilizes LitGPT, develops smaller base language models by inheriting a few transformer blocks from larger models and training on a tiny fraction of the data used by the larger models. It demonstrates that these smaller models can perform comparably to larger models despite using significantly less training data and resources.

* * *

Community
=========

We welcome all individual contributors, regardless of their level of experience or hardware. Your contributions are valuable, and we are excited to see what you can accomplish in this collaborative and supportive environment.

-   Request a feature
-   Submit your first contribution
-   Join our Discord

Tutorials
=========

🚀 Get started  
⚡️ Finetuning, incl. LoRA, QLoRA, and Adapters  
🤖 Pretraining  
💬 Model evaluation  
📘 Supported and custom datasets  
🧹 Quantization  
🤯 Tips for dealing with out-of-memory (OOM) errors  
🧑🏽‍💻 Using cloud TPUs  

* * *

### Acknowledgments

This implementation extends on Lit-LLaMA and nanoGPT, and it's **powered by Lightning Fabric ⚡**.

-   @karpathy for nanoGPT
-   @EleutherAI for GPT-NeoX and the Evaluation Harness
-   @TimDettmers for bitsandbytes
-   @Microsoft for LoRA
-   @tridao for Flash Attention 2

### License

LitGPT is released under the Apache 2.0 license.

### Citation

If you use LitGPT in your research, please cite the following work:

@misc{litgpt-2023,
  author       = {Lightning AI},
  title        = {LitGPT},
  howpublished = {\\url{https://github.com/Lightning-AI/litgpt}},
  year         = {2023},
}
