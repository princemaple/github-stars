---
project: LLaMA-Factory
stars: 63917
description: Unified Efficient Fine-Tuning of 100+ LLMs & VLMs (ACL 2024)
url: https://github.com/hiyouga/LLaMA-Factory
---

### Used by Amazon, NVIDIA, Aliyun, etc.

### Supporters ❤️

  
Warp, the agentic terminal for developers  
Available for MacOS, Linux, & Windows

* * *

### Easily fine-tune 100+ large language models with zero-code CLI and Web UI

👋 Join our WeChat, NPU, Lab4AI, LLaMA Factory Online user group.

\[ English | 中文 \]

**Fine-tuning a large language model can be easy as...**

train\_en.mp4

Start local training:

-   Please refer to usage

Start cloud training:

-   **Colab (free)**: https://colab.research.google.com/drive/1eRTPn37ltBbYsISy9Aw2NuI2Aq5CQrD9?usp=sharing
-   **PAI-DSW (free trial)**: https://gallery.pai-ml.com/#/preview/deepLearning/nlp/llama\_factory
-   **LLaMA Factory Online**: https://www.llamafactory.com.cn/?utm\_source=LLaMA-Factory
-   **Alaya NeW (cloud GPU deal)**: https://docs.alayanew.com/docs/documents/useGuide/LLaMAFactory/mutiple/?utm\_source=LLaMA-Factory

Read technical notes:

-   **Documentation (WIP)**: https://llamafactory.readthedocs.io/en/latest/
-   **Documentation (AMD GPU)**: https://rocm.docs.amd.com/projects/ai-developer-hub/en/latest/notebooks/fine\_tune/llama\_factory\_llama3.html
-   **Official Blog**: https://blog.llamafactory.net/en/
-   **Official Course**: https://www.lab4ai.cn/course/detail?id=7c13e60f6137474eb40f6fd3983c0f46&utm\_source=LLaMA-Factory

Note

Except for the above links, all other websites are unauthorized third-party websites. Please carefully use them.

Table of Contents
-----------------

-   Features
-   Blogs
-   Changelog
-   Supported Models
-   Supported Training Approaches
-   Provided Datasets
-   Requirement
-   Getting Started
    -   Installation
    -   Data Preparation
    -   Quickstart
    -   Fine-Tuning with LLaMA Board GUI
    -   LLaMA Factory Online
    -   Build Docker
    -   Deploy with OpenAI-style API and vLLM
    -   Download from ModelScope Hub
    -   Download from Modelers Hub
    -   Use W&B Logger
    -   Use SwanLab Logger
-   Projects using LLaMA Factory
-   License
-   Citation
-   Acknowledgement

Features
--------

-   **Various models**: LLaMA, LLaVA, Mistral, Mixtral-MoE, Qwen, Qwen2-VL, DeepSeek, Yi, Gemma, ChatGLM, Phi, etc.
-   **Integrated methods**: (Continuous) pre-training, (multimodal) supervised fine-tuning, reward modeling, PPO, DPO, KTO, ORPO, etc.
-   **Scalable resources**: 16-bit full-tuning, freeze-tuning, LoRA and 2/3/4/5/6/8-bit QLoRA via AQLM/AWQ/GPTQ/LLM.int8/HQQ/EETQ.
-   **Advanced algorithms**: GaLore, BAdam, APOLLO, Adam-mini, Muon, OFT, DoRA, LongLoRA, LLaMA Pro, Mixture-of-Depths, LoRA+, LoftQ and PiSSA.
-   **Practical tricks**: FlashAttention-2, Unsloth, Liger Kernel, KTransformers, RoPE scaling, NEFTune and rsLoRA.
-   **Wide tasks**: Multi-turn dialogue, tool using, image understanding, visual grounding, video recognition, audio understanding, etc.
-   **Experiment monitors**: LlamaBoard, TensorBoard, Wandb, MLflow, SwanLab, etc.
-   **Faster inference**: OpenAI-style API, Gradio UI and CLI with vLLM worker or SGLang worker.

### Day-N Support for Fine-Tuning Cutting-Edge Models

Support Date

Model Name

Day 0

Qwen3 / Qwen2.5-VL / Gemma 3 / GLM-4.1V / InternLM 3 / MiniCPM-o-2.6

Day 1

Llama 3 / GLM-4 / Mistral Small / PaliGemma2 / Llama 4

Blogs
-----

Tip

Now we have a dedicated blog for LLaMA Factory!

Website: https://blog.llamafactory.net/en/

-   💡 KTransformers Fine-Tuning × LLaMA Factory: Fine-tuning 1000 Billion models with 2 4090-GPU + CPU (English)
-   💡 Easy Dataset × LLaMA Factory: Enabling LLMs to Efficiently Learn Domain Knowledge (English)
-   Fine-tune a mental health LLM using LLaMA-Factory (Chinese)
-   Fine-tune GPT-OSS for Role-Playing using LLaMA-Factory (Chinese)
-   A One-Stop Code-Free Model Reinforcement Learning and Deployment Platform based on LLaMA-Factory and EasyR1 (Chinese)
-   How Apoidea Group enhances visual information extraction from banking documents with multimodal models using LLaMA-Factory on Amazon SageMaker HyperPod (English)

All Blogs

-   Fine-tune Llama3.1-70B for Medical Diagnosis using LLaMA-Factory (Chinese)
-   Fine-tune Qwen2.5-VL for Autonomous Driving using LLaMA-Factory (Chinese)
-   LLaMA Factory: Fine-tuning the DeepSeek-R1-Distill-Qwen-7B Model for News Classifier (Chinese)
-   A One-Stop Code-Free Model Fine-Tuning & Deployment Platform based on SageMaker and LLaMA-Factory (Chinese)
-   LLaMA Factory Multi-Modal Fine-Tuning Practice: Fine-Tuning Qwen2-VL for Personal Tourist Guide (Chinese)
-   LLaMA Factory: Fine-tuning Llama3 for Role-Playing (Chinese)

Changelog
---------

\[25/10/26\] We support Megatron-core training backend with **mcore\_adapter**. See PR #9237 to get started.

\[25/08/22\] We supported **OFT** and **OFTv2**. See examples for usage.

\[25/08/20\] We supported fine-tuning the **Intern-S1-mini** models. See PR #8976 to get started.

\[25/08/06\] We supported fine-tuning the **GPT-OSS** models. See PR #8826 to get started.

Full Changelog

\[25/07/02\] We supported fine-tuning the **GLM-4.1V-9B-Thinking** model.

\[25/04/28\] We supported fine-tuning the **Qwen3** model family.

\[25/04/21\] We supported the **Muon** optimizer. See examples for usage. Thank @tianshijing's PR.

\[25/04/16\] We supported fine-tuning the **InternVL3** model. See PR #7258 to get started.

\[25/04/14\] We supported fine-tuning the **GLM-Z1** and **Kimi-VL** models.

\[25/04/06\] We supported fine-tuning the **Llama 4** model. See PR #7611 to get started.

\[25/03/31\] We supported fine-tuning the **Qwen2.5 Omni** model. See PR #7537 to get started.

\[25/03/15\] We supported **SGLang** as inference backend. Try `infer_backend: sglang` to accelerate inference.

\[25/03/12\] We supported fine-tuning the **Gemma 3** model.

\[25/02/24\] Announcing **EasyR1**, an efficient, scalable and multi-modality RL training framework for efficient GRPO training.

\[25/02/11\] We supported saving the **Ollama** modelfile when exporting the model checkpoints. See examples for usage.

\[25/02/05\] We supported fine-tuning the **Qwen2-Audio** and **MiniCPM-o-2.6** on audio understanding tasks.

\[25/01/31\] We supported fine-tuning the **DeepSeek-R1** and **Qwen2.5-VL** models.

\[25/01/15\] We supported **APOLLO** optimizer. See examples for usage.

\[25/01/14\] We supported fine-tuning the **MiniCPM-o-2.6** and **MiniCPM-V-2.6** models. Thank @BUAADreamer's PR.

\[25/01/14\] We supported fine-tuning the **InternLM 3** models. Thank @hhaAndroid's PR.

\[25/01/10\] We supported fine-tuning the **Phi-4** model.

\[24/12/21\] We supported using **SwanLab** for experiment tracking and visualization. See this section for details.

\[24/11/27\] We supported fine-tuning the **Skywork-o1** model and the **OpenO1** dataset.

\[24/10/09\] We supported downloading pre-trained models and datasets from the **Modelers Hub**. See this tutorial for usage.

\[24/09/19\] We supported fine-tuning the **Qwen2.5** models.

\[24/08/30\] We supported fine-tuning the **Qwen2-VL** models. Thank @simonJJJ's PR.

\[24/08/27\] We supported **Liger Kernel**. Try `enable_liger_kernel: true` for efficient training.

\[24/08/09\] We supported **Adam-mini** optimizer. See examples for usage. Thank @relic-yuexi's PR.

\[24/07/04\] We supported contamination-free packed training. Use `neat_packing: true` to activate it. Thank @chuan298's PR.

\[24/06/16\] We supported **PiSSA** algorithm. See examples for usage.

\[24/06/07\] We supported fine-tuning the **Qwen2** and **GLM-4** models.

\[24/05/26\] We supported **SimPO** algorithm for preference learning. See examples for usage.

\[24/05/20\] We supported fine-tuning the **PaliGemma** series models. Note that the PaliGemma models are pre-trained models, you need to fine-tune them with `paligemma` template for chat completion.

\[24/05/18\] We supported **KTO** algorithm for preference learning. See examples for usage.

\[24/05/14\] We supported training and inference on the Ascend NPU devices. Check installation section for details.

\[24/04/26\] We supported fine-tuning the **LLaVA-1.5** multimodal LLMs. See examples for usage.

\[24/04/22\] We provided a **Colab notebook** for fine-tuning the Llama-3 model on a free T4 GPU. Two Llama-3-derived models fine-tuned using LLaMA Factory are available at Hugging Face, check Llama3-8B-Chinese-Chat and Llama3-Chinese for details.

\[24/04/21\] We supported **Mixture-of-Depths** according to AstraMindAI's implementation. See examples for usage.

\[24/04/16\] We supported **BAdam** optimizer. See examples for usage.

\[24/04/16\] We supported **unsloth**'s long-sequence training (Llama-2-7B-56k within 24GB). It achieves **117%** speed and **50%** memory compared with FlashAttention-2, more benchmarks can be found in this page.

\[24/03/31\] We supported **ORPO**. See examples for usage.

\[24/03/21\] Our paper "LlamaFactory: Unified Efficient Fine-Tuning of 100+ Language Models" is available at arXiv!

\[24/03/20\] We supported **FSDP+QLoRA** that fine-tunes a 70B model on 2x24GB GPUs. See examples for usage.

\[24/03/13\] We supported **LoRA+**. See examples for usage.

\[24/03/07\] We supported **GaLore** optimizer. See examples for usage.

\[24/03/07\] We integrated **vLLM** for faster and concurrent inference. Try `infer_backend: vllm` to enjoy **270%** inference speed.

\[24/02/28\] We supported weight-decomposed LoRA (**DoRA**). Try `use_dora: true` to activate DoRA training.

\[24/02/15\] We supported **block expansion** proposed by LLaMA Pro. See examples for usage.

\[24/02/05\] Qwen1.5 (Qwen2 beta version) series models are supported in LLaMA-Factory. Check this blog post for details.

\[24/01/18\] We supported **agent tuning** for most models, equipping model with tool using abilities by fine-tuning with `dataset: glaive_toolcall_en`.

\[23/12/23\] We supported **unsloth**'s implementation to boost LoRA tuning for the LLaMA, Mistral and Yi models. Try `use_unsloth: true` argument to activate unsloth patch. It achieves **170%** speed in our benchmark, check this page for details.

\[23/12/12\] We supported fine-tuning the latest MoE model **Mixtral 8x7B** in our framework. See hardware requirement here.

\[23/12/01\] We supported downloading pre-trained models and datasets from the **ModelScope Hub**. See this tutorial for usage.

\[23/10/21\] We supported **NEFTune** trick for fine-tuning. Try `neftune_noise_alpha: 5` argument to activate NEFTune.

\[23/09/27\] We supported **$S^2$-Attn** proposed by LongLoRA for the LLaMA models. Try `shift_attn: true` argument to enable shift short attention.

\[23/09/23\] We integrated MMLU, C-Eval and CMMLU benchmarks in this repo. See examples for usage.

\[23/09/10\] We supported **FlashAttention-2**. Try `flash_attn: fa2` argument to enable FlashAttention-2 if you are using RTX4090, A100 or H100 GPUs.

\[23/08/12\] We supported **RoPE scaling** to extend the context length of the LLaMA models. Try `rope_scaling: linear` argument in training and `rope_scaling: dynamic` argument at inference to extrapolate the position embeddings.

\[23/08/11\] We supported **DPO training** for instruction-tuned models. See examples for usage.

\[23/07/31\] We supported **dataset streaming**. Try `streaming: true` and `max_steps: 10000` arguments to load your dataset in streaming mode.

\[23/07/29\] We released two instruction-tuned 13B models at Hugging Face. See these Hugging Face Repos (LLaMA-2 / Baichuan) for details.

\[23/07/18\] We developed an **all-in-one Web UI** for training, evaluation and inference. Try `train_web.py` to fine-tune models in your Web browser. Thank @KanadeSiina and @codemayq for their efforts in the development.

\[23/07/09\] We released **FastEdit** ⚡🩹, an easy-to-use package for editing the factual knowledge of large language models efficiently. Please follow FastEdit if you are interested.

\[23/06/29\] We provided a **reproducible example** of training a chat model using instruction-following datasets, see Baichuan-7B-sft for details.

\[23/06/22\] We aligned the demo API with the OpenAI's format where you can insert the fine-tuned model in **arbitrary ChatGPT-based applications**.

\[23/06/03\] We supported quantized training and inference (aka **QLoRA**). See examples for usage.

Tip

If you cannot use the latest feature, please pull the latest code and install LLaMA-Factory again.

Supported Models
----------------

Model

Model size

Template

Baichuan 2

7B/13B

baichuan2

BLOOM/BLOOMZ

560M/1.1B/1.7B/3B/7.1B/176B

\-

ChatGLM3

6B

chatglm3

Command R

35B/104B

cohere

DeepSeek (Code/MoE)

7B/16B/67B/236B

deepseek

DeepSeek 2.5/3

236B/671B

deepseek3

DeepSeek R1 (Distill)

1.5B/7B/8B/14B/32B/70B/671B

deepseekr1

ERNIE-4.5

0.3B/21B/300B

ernie/ernie\_nothink

Falcon

7B/11B/40B/180B

falcon

Falcon-H1

0.5B/1.5B/3B/7B/34B

falcon\_h1

Gemma/Gemma 2/CodeGemma

2B/7B/9B/27B

gemma/gemma2

Gemma 3/Gemma 3n

270M/1B/4B/6B/8B/12B/27B

gemma3/gemma3n

GLM-4/GLM-4-0414/GLM-Z1

9B/32B

glm4/glmz1

GLM-4.1V

9B

glm4v

GLM-4.5/GLM-4.5(6)V

9B/106B/355B

glm4\_moe/glm4\_5v

GPT-2

0.1B/0.4B/0.8B/1.5B

\-

GPT-OSS

20B/120B

gpt

Granite 3.0-3.3

1B/2B/3B/8B

granite3

Granite 4

7B

granite4

Hunyuan (MT)

7B

hunyuan

Index

1.9B

index

InternLM 2-3

7B/8B/20B

intern2

InternVL 2.5-3.5

1B/2B/4B/8B/14B/30B/38B/78B/241B

intern\_vl

InternLM/Intern-S1-mini

8B

intern\_s1

Kimi-VL

16B

kimi\_vl

Ling 2.0 (mini/flash)

16B/100B

bailing\_v2

Llama

7B/13B/33B/65B

\-

Llama 2

7B/13B/70B

llama2

Llama 3-3.3

1B/3B/8B/70B

llama3

Llama 4

109B/402B

llama4

Llama 3.2 Vision

11B/90B

mllama

LLaVA-1.5

7B/13B

llava

LLaVA-NeXT

7B/8B/13B/34B/72B/110B

llava\_next

LLaVA-NeXT-Video

7B/34B

llava\_next\_video

MiMo

7B

mimo

MiniCPM 1-4.1

0.5B/1B/2B/4B/8B

cpm/cpm3/cpm4

MiniCPM-o-2.6/MiniCPM-V-2.6

8B

minicpm\_o/minicpm\_v

Ministral(3)/Mistral-Nemo

3B/8B/12B/14B

ministral/ministral3

Mistral/Mixtral

7B/8x7B/8x22B

mistral

Mistral Small

24B

mistral\_small

OLMo

1B/7B

\-

PaliGemma/PaliGemma2

3B/10B/28B

paligemma

Phi-1.5/Phi-2

1.3B/2.7B

\-

Phi-3/Phi-3.5

4B/14B

phi

Phi-3-small

7B

phi\_small

Phi-4

14B

phi4

Pixtral

12B

pixtral

Qwen (1-2.5) (Code/Math/MoE/QwQ)

0.5B/1.5B/3B/7B/14B/32B/72B/110B

qwen

Qwen3 (MoE/Instruct/Thinking/Next)

0.6B/1.7B/4B/8B/14B/32B/80B/235B

qwen3/qwen3\_nothink

Qwen2-Audio

7B

qwen2\_audio

Qwen2.5-Omni

3B/7B

qwen2\_omni

Qwen3-Omni

30B

qwen3\_omni

Qwen2-VL/Qwen2.5-VL/QVQ

2B/3B/7B/32B/72B

qwen2\_vl

Qwen3-VL

2B/4B/8B/30B/32B/235B

qwen3\_vl

Seed (OSS/Coder)

8B/36B

seed\_oss/seed\_coder

Skywork o1

8B

skywork\_o1

StarCoder 2

3B/7B/15B

\-

TeleChat2

3B/7B/35B/115B

telechat2

XVERSE

7B/13B/65B

xverse

Yi/Yi-1.5 (Code)

1.5B/6B/9B/34B

yi

Yi-VL

6B/34B

yi\_vl

Yuan 2

2B/51B/102B

yuan

Note

For the "base" models, the `template` argument can be chosen from `default`, `alpaca`, `vicuna` etc. But make sure to use the **corresponding template** for the "instruct/chat" models.

If the model has both reasoning and non-reasoning versions, please use the `_nothink` suffix to distinguish between them. For example, `qwen3` and `qwen3_nothink`.

Remember to use the **SAME** template in training and inference.

\*: You should install the `transformers` from main branch and use `DISABLE_VERSION_CHECK=1` to skip version check.

\*\*: You need to install a specific version of `transformers` to use the corresponding model.

Please refer to constants.py for a full list of models we supported.

You also can add a custom chat template to template.py.

Supported Training Approaches
-----------------------------

Approach

Full-tuning

Freeze-tuning

LoRA

QLoRA

OFT

QOFT

Pre-Training

✅

✅

✅

✅

✅

✅

Supervised Fine-Tuning

✅

✅

✅

✅

✅

✅

Reward Modeling

✅

✅

✅

✅

✅

✅

PPO Training

✅

✅

✅

✅

✅

✅

DPO Training

✅

✅

✅

✅

✅

✅

KTO Training

✅

✅

✅

✅

✅

✅

ORPO Training

✅

✅

✅

✅

✅

✅

SimPO Training

✅

✅

✅

✅

✅

✅

Tip

The implementation details of PPO can be found in this blog.

Provided Datasets
-----------------

Pre-training datasets

-   Wiki Demo (en)
-   RefinedWeb (en)
-   RedPajama V2 (en)
-   Wikipedia (en)
-   Wikipedia (zh)
-   Pile (en)
-   SkyPile (zh)
-   FineWeb (en)
-   FineWeb-Edu (en)
-   CCI3-HQ (zh)
-   CCI3-Data (zh)
-   CCI4.0-M2-Base-v1 (en&zh)
-   CCI4.0-M2-CoT-v1 (en&zh)
-   CCI4.0-M2-Extra-v1 (en&zh)
-   The Stack (en)
-   StarCoder (en)

Supervised fine-tuning datasets

-   Identity (en&zh)
-   Stanford Alpaca (en)
-   Stanford Alpaca (zh)
-   Alpaca GPT4 (en&zh)
-   Glaive Function Calling V2 (en&zh)
-   LIMA (en)
-   Guanaco Dataset (multilingual)
-   BELLE 2M (zh)
-   BELLE 1M (zh)
-   BELLE 0.5M (zh)
-   BELLE Dialogue 0.4M (zh)
-   BELLE School Math 0.25M (zh)
-   BELLE Multiturn Chat 0.8M (zh)
-   UltraChat (en)
-   OpenPlatypus (en)
-   CodeAlpaca 20k (en)
-   Alpaca CoT (multilingual)
-   OpenOrca (en)
-   SlimOrca (en)
-   MathInstruct (en)
-   Firefly 1.1M (zh)
-   Wiki QA (en)
-   Web QA (zh)
-   WebNovel (zh)
-   Nectar (en)
-   deepctrl (en&zh)
-   Advertise Generating (zh)
-   ShareGPT Hyperfiltered (en)
-   ShareGPT4 (en&zh)
-   UltraChat 200k (en)
-   Infinity Instruct (zh)
-   AgentInstruct (en)
-   LMSYS Chat 1M (en)
-   Evol Instruct V2 (en)
-   Cosmopedia (en)
-   STEM (zh)
-   Ruozhiba (zh)
-   Neo-sft (zh)
-   Magpie-Pro-300K-Filtered (en)
-   Magpie-ultra-v0.1 (en)
-   WebInstructSub (en)
-   OpenO1-SFT (en&zh)
-   Open-Thoughts (en)
-   Open-R1-Math (en)
-   Chinese-DeepSeek-R1-Distill (zh)
-   LLaVA mixed (en&zh)
-   Pokemon-gpt4o-captions (en&zh)
-   Open Assistant (de)
-   Dolly 15k (de)
-   Alpaca GPT4 (de)
-   OpenSchnabeltier (de)
-   Evol Instruct (de)
-   Dolphin (de)
-   Booksum (de)
-   Airoboros (de)
-   Ultrachat (de)

Preference datasets

-   DPO mixed (en&zh)
-   UltraFeedback (en)
-   COIG-P (zh)
-   RLHF-V (en)
-   VLFeedback (en)
-   RLAIF-V (en)
-   Orca DPO Pairs (en)
-   HH-RLHF (en)
-   Nectar (en)
-   Orca DPO (de)
-   KTO mixed (en)

Some datasets require confirmation before using them, so we recommend logging in with your Hugging Face account using these commands.

pip install "huggingface\_hub<1.0.0"
huggingface-cli login

Requirement
-----------

Mandatory

Minimum

Recommend

python

3.9

3.10

torch

2.0.0

2.6.0

torchvision

0.15.0

0.21.0

transformers

4.49.0

4.50.0

datasets

2.16.0

3.2.0

accelerate

0.34.0

1.2.1

peft

0.14.0

0.15.1

trl

0.8.6

0.9.6

Optional

Minimum

Recommend

CUDA

11.6

12.2

deepspeed

0.10.0

0.16.4

bitsandbytes

0.39.0

0.43.1

vllm

0.4.3

0.8.2

flash-attn

2.5.6

2.7.2

### Hardware Requirement

\* _estimated_

Method

Bits

7B

14B

30B

70B

`x`B

Full (`bf16` or `fp16`)

32

120GB

240GB

600GB

1200GB

`18x`GB

Full (`pure_bf16`)

16

60GB

120GB

300GB

600GB

`8x`GB

Freeze/LoRA/GaLore/APOLLO/BAdam/OFT

16

16GB

32GB

64GB

160GB

`2x`GB

QLoRA / QOFT

8

10GB

20GB

40GB

80GB

`x`GB

QLoRA / QOFT

4

6GB

12GB

24GB

48GB

`x/2`GB

QLoRA / QOFT

2

4GB

8GB

16GB

24GB

`x/4`GB

Getting Started
---------------

### Installation

Important

Installation is mandatory.

#### Install from Source

git clone --depth 1 https://github.com/hiyouga/LLaMA-Factory.git
cd LLaMA-Factory
pip install -e ".\[torch,metrics\]" --no-build-isolation

Extra dependencies available: torch, torch-npu, metrics, deepspeed, liger-kernel, bitsandbytes, hqq, eetq, gptq, aqlm, vllm, sglang, galore, apollo, badam, adam-mini, qwen, minicpm\_v, openmind, swanlab, dev

#### Install from Docker Image

docker run -it --rm --gpus=all --ipc=host hiyouga/llamafactory:latest

This image is built on Ubuntu 22.04 (x86\_64), CUDA 12.4, Python 3.11, PyTorch 2.6.0, and Flash-attn 2.7.4.

Find the pre-built images: https://hub.docker.com/r/hiyouga/llamafactory/tags

Please refer to build docker to build the image yourself.

Setting up a virtual environment with **uv**

Create an isolated Python environment with uv:

uv sync --extra torch --extra metrics --prerelease=allow

Run LLaMA-Factory in the isolated environment:

uv run --prerelease=allow llamafactory-cli train examples/train\_lora/llama3\_lora\_pretrain.yaml

For Windows users

#### Install PyTorch

You need to manually install the GPU version of PyTorch on the Windows platform. Please refer to the official website and the following command to install PyTorch with CUDA support:

pip uninstall torch torchvision torchaudio
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126
python -c "import torch; print(torch.cuda.is\_available())"

If you see `True` then you have successfully installed PyTorch with CUDA support.

Try `dataloader_num_workers: 0` if you encounter `Can't pickle local object` error.

#### Install BitsAndBytes

If you want to enable the quantized LoRA (QLoRA) on the Windows platform, you need to install a pre-built version of `bitsandbytes` library, which supports CUDA 11.1 to 12.2, please select the appropriate release version based on your CUDA version.

pip install https://github.com/jllllll/bitsandbytes-windows-webui/releases/download/wheels/bitsandbytes-0.41.2.post2-py3-none-win\_amd64.whl

#### Install Flash Attention-2

To enable FlashAttention-2 on the Windows platform, please use the script from flash-attention-windows-wheel to compile and install it by yourself.

For Ascend NPU users

To install LLaMA Factory on Ascend NPU devices, please upgrade Python to version 3.10 or higher and specify extra dependencies: `pip install -e ".[torch-npu,metrics]"`. Additionally, you need to install the **Ascend CANN Toolkit and Kernels**. Please follow the installation tutorial or use the following commands:

# replace the url according to your CANN version and devices
# install CANN Toolkit
wget https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/Milan-ASL/Milan-ASL%20V100R001C20SPC702/Ascend-cann-toolkit\_8.0.0.alpha002\_linux-"$(uname -i)".run
bash Ascend-cann-toolkit\_8.0.0.alpha002\_linux-"$(uname -i)".run --install

# install CANN Kernels
wget https://ascend-repo.obs.cn-east-2.myhuaweicloud.com/Milan-ASL/Milan-ASL%20V100R001C20SPC702/Ascend-cann-kernels-910b\_8.0.0.alpha002\_linux-"$(uname -i)".run
bash Ascend-cann-kernels-910b\_8.0.0.alpha002\_linux-"$(uname -i)".run --install

# set env variables
source /usr/local/Ascend/ascend-toolkit/set\_env.sh

Requirement

Minimum

Recommend

CANN

8.0.RC1

8.0.0.alpha002

torch

2.1.0

2.4.0

torch-npu

2.1.0

2.4.0.post2

deepspeed

0.13.2

0.13.2

vllm-ascend

\-

0.7.3

Remember to use `ASCEND_RT_VISIBLE_DEVICES` instead of `CUDA_VISIBLE_DEVICES` to specify the device to use.

If you cannot infer model on NPU devices, try setting `do_sample: false` in the configurations.

Download the pre-built Docker images: 32GB | 64GB

#### Install BitsAndBytes

To use QLoRA based on bitsandbytes on Ascend NPU, please follow these 3 steps:

1.  Manually compile bitsandbytes: Refer to the installation documentation for the NPU version of bitsandbytes to complete the compilation and installation. The compilation requires a cmake version of at least 3.22.1 and a g++ version of at least 12.x.

# Install bitsandbytes from source
# Clone bitsandbytes repo, Ascend NPU backend is currently enabled on multi-backend-refactor branch
git clone -b multi-backend-refactor https://github.com/bitsandbytes-foundation/bitsandbytes.git
cd bitsandbytes/

# Install dependencies
pip install -r requirements-dev.txt

# Install the dependencies for the compilation tools. Note that the commands for this step may vary depending on the operating system. The following are provided for reference
apt-get install -y build-essential cmake

# Compile & install  
cmake -DCOMPUTE\_BACKEND=npu -S .
make
pip install .

1.  Install transformers from the main branch.

git clone -b main https://github.com/huggingface/transformers.git
cd transformers
pip install .

1.  Set `double_quantization: false` in the configuration. You can refer to the example.

### Data Preparation

Please refer to data/README.md for checking the details about the format of dataset files. You can use datasets on HuggingFace / ModelScope / Modelers hub, load the dataset in local disk, or specify a path to s3/gcs cloud storage.

Note

Please update `data/dataset_info.json` to use your custom dataset.

You can also use **Easy Dataset**, **DataFlow** and **GraphGen** to create synthetic data for fine-tuning.

### Quickstart

Use the following 3 commands to run LoRA **fine-tuning**, **inference** and **merging** of the Llama3-8B-Instruct model, respectively.

llamafactory-cli train examples/train\_lora/llama3\_lora\_sft.yaml
llamafactory-cli chat examples/inference/llama3\_lora\_sft.yaml
llamafactory-cli export examples/merge\_lora/llama3\_lora\_sft.yaml

See examples/README.md for advanced usage (including distributed training).

Tip

Use `llamafactory-cli help` to show help information.

Read FAQs first if you encounter any problems.

### Fine-Tuning with LLaMA Board GUI (powered by Gradio)

llamafactory-cli webui

### LLaMA Factory Online

Read our documentation.

### Build Docker

For CUDA users:

cd docker/docker-cuda/
docker compose up -d
docker compose exec llamafactory bash

For Ascend NPU users:

cd docker/docker-npu/
docker compose up -d
docker compose exec llamafactory bash

For AMD ROCm users:

cd docker/docker-rocm/
docker compose up -d
docker compose exec llamafactory bash

Build without Docker Compose

For CUDA users:

docker build -f ./docker/docker-cuda/Dockerfile \\
    --build-arg PIP\_INDEX=https://pypi.org/simple \\
    --build-arg EXTRAS=metrics \\
    -t llamafactory:latest .

docker run -dit --ipc=host --gpus=all \\
    -p 7860:7860 \\
    -p 8000:8000 \\
    --name llamafactory \\
    llamafactory:latest

docker exec -it llamafactory bash

For Ascend NPU users:

docker build -f ./docker/docker-npu/Dockerfile \\
    --build-arg PIP\_INDEX=https://pypi.org/simple \\
    --build-arg EXTRAS=torch-npu,metrics \\
    -t llamafactory:latest .

docker run -dit --ipc=host \\
    -v /usr/local/dcmi:/usr/local/dcmi \\
    -v /usr/local/bin/npu-smi:/usr/local/bin/npu-smi \\
    -v /usr/local/Ascend/driver:/usr/local/Ascend/driver \\
    -v /etc/ascend\_install.info:/etc/ascend\_install.info \\
    -p 7860:7860 \\
    -p 8000:8000 \\
    --device /dev/davinci0 \\
    --device /dev/davinci\_manager \\
    --device /dev/devmm\_svm \\
    --device /dev/hisi\_hdc \\
    --name llamafactory \\
    llamafactory:latest

docker exec -it llamafactory bash

For AMD ROCm users:

docker build -f ./docker/docker-rocm/Dockerfile \\
    --build-arg PIP\_INDEX=https://pypi.org/simple \\
    --build-arg EXTRAS=metrics \\
    -t llamafactory:latest .

docker run -dit --ipc=host \\
    -p 7860:7860 \\
    -p 8000:8000 \\
    --device /dev/kfd \\
    --device /dev/dri \\
    --name llamafactory \\
    llamafactory:latest

docker exec -it llamafactory bash

Use Docker volumes

You can uncomment `VOLUME [ "/root/.cache/huggingface", "/app/shared_data", "/app/output" ]` in the Dockerfile to use data volumes.

When building the Docker image, use `-v ./hf_cache:/root/.cache/huggingface` argument to mount the local directory to the container. The following data volumes are available.

-   `hf_cache`: Utilize Hugging Face cache on the host machine.
-   `shared_data`: The directionary to store datasets on the host machine.
-   `output`: Set export dir to this location so that the merged result can be accessed directly on the host machine.

### Deploy with OpenAI-style API and vLLM

API\_PORT=8000 llamafactory-cli api examples/inference/llama3.yaml infer\_backend=vllm vllm\_enforce\_eager=true

Tip

Visit this page for API document.

Examples: Image understanding | Function calling

### Download from ModelScope Hub

If you have trouble with downloading models and datasets from Hugging Face, you can use ModelScope.

export USE\_MODELSCOPE\_HUB=1 # \`set USE\_MODELSCOPE\_HUB=1\` for Windows

Train the model by specifying a model ID of the ModelScope Hub as the `model_name_or_path`. You can find a full list of model IDs at ModelScope Hub, e.g., `LLM-Research/Meta-Llama-3-8B-Instruct`.

### Download from Modelers Hub

You can also use Modelers Hub to download models and datasets.

export USE\_OPENMIND\_HUB=1 # \`set USE\_OPENMIND\_HUB=1\` for Windows

Train the model by specifying a model ID of the Modelers Hub as the `model_name_or_path`. You can find a full list of model IDs at Modelers Hub, e.g., `TeleAI/TeleChat-7B-pt`.

### Use W&B Logger

To use Weights & Biases for logging experimental results, you need to add the following arguments to yaml files.

report\_to: wandb
run\_name: test\_run # optional

Set `WANDB_API_KEY` to your key when launching training tasks to log in with your W&B account.

### Use SwanLab Logger

To use SwanLab for logging experimental results, you need to add the following arguments to yaml files.

use\_swanlab: true
swanlab\_run\_name: test\_run # optional

When launching training tasks, you can log in to SwanLab in three ways:

1.  Add `swanlab_api_key=<your_api_key>` to the yaml file, and set it to your API key.
2.  Set the environment variable `SWANLAB_API_KEY` to your API key.
3.  Use the `swanlab login` command to complete the login.

Projects using LLaMA Factory
----------------------------

If you have a project that should be incorporated, please contact via email or create a pull request.

Click to show

1.  Wang et al. ESRL: Efficient Sampling-based Reinforcement Learning for Sequence Generation. 2023. \[arxiv\]
2.  Yu et al. Open, Closed, or Small Language Models for Text Classification? 2023. \[arxiv\]
3.  Wang et al. UbiPhysio: Support Daily Functioning, Fitness, and Rehabilitation with Action Understanding and Feedback in Natural Language. 2023. \[arxiv\]
4.  Luceri et al. Leveraging Large Language Models to Detect Influence Campaigns in Social Media. 2023. \[arxiv\]
5.  Zhang et al. Alleviating Hallucinations of Large Language Models through Induced Hallucinations. 2023. \[arxiv\]
6.  Wang et al. Know Your Needs Better: Towards Structured Understanding of Marketer Demands with Analogical Reasoning Augmented LLMs. KDD 2024. \[arxiv\]
7.  Wang et al. CANDLE: Iterative Conceptualization and Instantiation Distillation from Large Language Models for Commonsense Reasoning. ACL 2024. \[arxiv\]
8.  Choi et al. FACT-GPT: Fact-Checking Augmentation via Claim Matching with LLMs. 2024. \[arxiv\]
9.  Zhang et al. AutoMathText: Autonomous Data Selection with Language Models for Mathematical Texts. 2024. \[arxiv\]
10.  Lyu et al. KnowTuning: Knowledge-aware Fine-tuning for Large Language Models. 2024. \[arxiv\]
11.  Yang et al. LaCo: Large Language Model Pruning via Layer Collaps. 2024. \[arxiv\]
12.  Bhardwaj et al. Language Models are Homer Simpson! Safety Re-Alignment of Fine-tuned Language Models through Task Arithmetic. 2024. \[arxiv\]
13.  Yang et al. Enhancing Empathetic Response Generation by Augmenting LLMs with Small-scale Empathetic Models. 2024. \[arxiv\]
14.  Yi et al. Generation Meets Verification: Accelerating Large Language Model Inference with Smart Parallel Auto-Correct Decoding. ACL 2024 Findings. \[arxiv\]
15.  Cao et al. Head-wise Shareable Attention for Large Language Models. 2024. \[arxiv\]
16.  Zhang et al. Enhancing Multilingual Capabilities of Large Language Models through Self-Distillation from Resource-Rich Languages. 2024. \[arxiv\]
17.  Kim et al. Efficient and Effective Vocabulary Expansion Towards Multilingual Large Language Models. 2024. \[arxiv\]
18.  Yu et al. KIEval: A Knowledge-grounded Interactive Evaluation Framework for Large Language Models. ACL 2024. \[arxiv\]
19.  Huang et al. Key-Point-Driven Data Synthesis with its Enhancement on Mathematical Reasoning. 2024. \[arxiv\]
20.  Duan et al. Negating Negatives: Alignment without Human Positive Samples via Distributional Dispreference Optimization. 2024. \[arxiv\]
21.  Xie and Schwertfeger. Empowering Robotics with Large Language Models: osmAG Map Comprehension with LLMs. 2024. \[arxiv\]
22.  Wu et al. Large Language Models are Parallel Multilingual Learners. 2024. \[arxiv\]
23.  Zhang et al. EDT: Improving Large Language Models' Generation by Entropy-based Dynamic Temperature Sampling. 2024. \[arxiv\]
24.  Weller et al. FollowIR: Evaluating and Teaching Information Retrieval Models to Follow Instructions. 2024. \[arxiv\]
25.  Hongbin Na. CBT-LLM: A Chinese Large Language Model for Cognitive Behavioral Therapy-based Mental Health Question Answering. COLING 2024. \[arxiv\]
26.  Zan et al. CodeS: Natural Language to Code Repository via Multi-Layer Sketch. 2024. \[arxiv\]
27.  Liu et al. Extensive Self-Contrast Enables Feedback-Free Language Model Alignment. 2024. \[arxiv\]
28.  Luo et al. BAdam: A Memory Efficient Full Parameter Training Method for Large Language Models. 2024. \[arxiv\]
29.  Du et al. Chinese Tiny LLM: Pretraining a Chinese-Centric Large Language Model. 2024. \[arxiv\]
30.  Ma et al. Parameter Efficient Quasi-Orthogonal Fine-Tuning via Givens Rotation. ICML 2024. \[arxiv\]
31.  Liu et al. Dynamic Generation of Personalities with Large Language Models. 2024. \[arxiv\]
32.  Shang et al. How Far Have We Gone in Stripped Binary Code Understanding Using Large Language Models. 2024. \[arxiv\]
33.  Huang et al. LLMTune: Accelerate Database Knob Tuning with Large Language Models. 2024. \[arxiv\]
34.  Deng et al. Text-Tuple-Table: Towards Information Integration in Text-to-Table Generation via Global Tuple Extraction. 2024. \[arxiv\]
35.  Acikgoz et al. Hippocrates: An Open-Source Framework for Advancing Large Language Models in Healthcare. 2024. \[arxiv\]
36.  Zhang et al. Small Language Models Need Strong Verifiers to Self-Correct Reasoning. ACL 2024 Findings. \[arxiv\]
37.  Zhou et al. FREB-TQA: A Fine-Grained Robustness Evaluation Benchmark for Table Question Answering. NAACL 2024. \[arxiv\]
38.  Xu et al. Large Language Models for Cyber Security: A Systematic Literature Review. 2024. \[arxiv\]
39.  Dammu et al. "They are uncultured": Unveiling Covert Harms and Social Threats in LLM Generated Conversations. 2024. \[arxiv\]
40.  Yi et al. A safety realignment framework via subspace-oriented model fusion for large language models. 2024. \[arxiv\]
41.  Lou et al. SPO: Multi-Dimensional Preference Sequential Alignment With Implicit Reward Modeling. 2024. \[arxiv\]
42.  Zhang et al. Getting More from Less: Large Language Models are Good Spontaneous Multilingual Learners. 2024. \[arxiv\]
43.  Zhang et al. TS-Align: A Teacher-Student Collaborative Framework for Scalable Iterative Finetuning of Large Language Models. 2024. \[arxiv\]
44.  Zihong Chen. Sentence Segmentation and Sentence Punctuation Based on XunziALLM. 2024. \[paper\]
45.  Gao et al. The Best of Both Worlds: Toward an Honest and Helpful Large Language Model. 2024. \[arxiv\]
46.  Wang and Song. MARS: Benchmarking the Metaphysical Reasoning Abilities of Language Models with a Multi-task Evaluation Dataset. 2024. \[arxiv\]
47.  Hu et al. Computational Limits of Low-Rank Adaptation (LoRA) for Transformer-Based Models. 2024. \[arxiv\]
48.  Ge et al. Time Sensitive Knowledge Editing through Efficient Finetuning. ACL 2024. \[arxiv\]
49.  Tan et al. Peer Review as A Multi-Turn and Long-Context Dialogue with Role-Based Interactions. 2024. \[arxiv\]
50.  Song et al. Turbo Sparse: Achieving LLM SOTA Performance with Minimal Activated Parameters. 2024. \[arxiv\]
51.  Gu et al. RWKV-CLIP: A Robust Vision-Language Representation Learner. 2024. \[arxiv\]
52.  Chen et al. Advancing Tool-Augmented Large Language Models: Integrating Insights from Errors in Inference Trees. 2024. \[arxiv\]
53.  Zhu et al. Are Large Language Models Good Statisticians?. 2024. \[arxiv\]
54.  Li et al. Know the Unknown: An Uncertainty-Sensitive Method for LLM Instruction Tuning. 2024. \[arxiv\]
55.  Ding et al. IntentionQA: A Benchmark for Evaluating Purchase Intention Comprehension Abilities of Language Models in E-commerce. 2024. \[arxiv\]
56.  He et al. COMMUNITY-CROSS-INSTRUCT: Unsupervised Instruction Generation for Aligning Large Language Models to Online Communities. 2024. \[arxiv\]
57.  Lin et al. FVEL: Interactive Formal Verification Environment with Large Language Models via Theorem Proving. 2024. \[arxiv\]
58.  Treutlein et al. Connecting the Dots: LLMs can Infer and Verbalize Latent Structure from Disparate Training Data. 2024. \[arxiv\]
59.  Feng et al. SS-Bench: A Benchmark for Social Story Generation and Evaluation. 2024. \[arxiv\]
60.  Feng et al. Self-Constructed Context Decompilation with Fined-grained Alignment Enhancement. 2024. \[arxiv\]
61.  Liu et al. Large Language Models for Cuffless Blood Pressure Measurement From Wearable Biosignals. 2024. \[arxiv\]
62.  Iyer et al. Exploring Very Low-Resource Translation with LLMs: The University of Edinburgh's Submission to AmericasNLP 2024 Translation Task. AmericasNLP 2024. \[paper\]
63.  Li et al. Calibrating LLMs with Preference Optimization on Thought Trees for Generating Rationale in Science Question Scoring. 2024. \[arxiv\]
64.  Yang et al. Financial Knowledge Large Language Model. 2024. \[arxiv\]
65.  Lin et al. DogeRM: Equipping Reward Models with Domain Knowledge through Model Merging. 2024. \[arxiv\]
66.  Bako et al. Evaluating the Semantic Profiling Abilities of LLMs for Natural Language Utterances in Data Visualization. 2024. \[arxiv\]
67.  Huang et al. RoLoRA: Fine-tuning Rotated Outlier-free LLMs for Effective Weight-Activation Quantization. 2024. \[arxiv\]
68.  Jiang et al. LLM-Collaboration on Automatic Science Journalism for the General Audience. 2024. \[arxiv\]
69.  Inouye et al. Applied Auto-tuning on LoRA Hyperparameters. 2024. \[paper\]
70.  Qi et al. Research on Tibetan Tourism Viewpoints information generation system based on LLM. 2024. \[arxiv\]
71.  Xu et al. Course-Correction: Safety Alignment Using Synthetic Preferences. 2024. \[arxiv\]
72.  Sun et al. LAMBDA: A Large Model Based Data Agent. 2024. \[arxiv\]
73.  Zhu et al. CollectiveSFT: Scaling Large Language Models for Chinese Medical Benchmark with Collective Instructions in Healthcare. 2024. \[arxiv\]
74.  Yu et al. Correcting Negative Bias in Large Language Models through Negative Attention Score Alignment. 2024. \[arxiv\]
75.  Xie et al. The Power of Personalized Datasets: Advancing Chinese Composition Writing for Elementary School through Targeted Model Fine-Tuning. IALP 2024. \[paper\]
76.  Liu et al. Instruct-Code-Llama: Improving Capabilities of Language Model in Competition Level Code Generation by Online Judge Feedback. ICIC 2024. \[paper\]
77.  Wang et al. Cybernetic Sentinels: Unveiling the Impact of Safety Data Selection on Model Security in Supervised Fine-Tuning. ICIC 2024. \[paper\]
78.  Xia et al. Understanding the Performance and Estimating the Cost of LLM Fine-Tuning. 2024. \[arxiv\]
79.  Zeng et al. Perceive, Reflect, and Plan: Designing LLM Agent for Goal-Directed City Navigation without Instructions. 2024. \[arxiv\]
80.  Xia et al. Using Pre-trained Language Model for Accurate ESG Prediction. FinNLP 2024. \[paper\]
81.  Liang et al. I-SHEEP: Self-Alignment of LLM from Scratch through an Iterative Self-Enhancement Paradigm. 2024. \[arxiv\]
82.  Bai et al. Aligning Large Language Model with Direct Multi-Preference Optimization for Recommendation. CIKM 2024. \[paper\]
83.  Zhang et al. CPsyCoun: A Report-based Multi-turn Dialogue Reconstruction and Evaluation Framework for Chinese Psychological Counseling. ACL 2024. \[paper\]
84.  **StarWhisper**: A large language model for Astronomy, based on ChatGLM2-6B and Qwen-14B.
85.  **DISC-LawLLM**: A large language model specialized in Chinese legal domain, based on Baichuan-13B, is capable of retrieving and reasoning on legal knowledge.
86.  **Sunsimiao**: A large language model specialized in Chinese medical domain, based on Baichuan-7B and ChatGLM-6B.
87.  **CareGPT**: A series of large language models for Chinese medical domain, based on LLaMA2-7B and Baichuan-13B.
88.  **MachineMindset**: A series of MBTI Personality large language models, capable of giving any LLM 16 different personality types based on different datasets and training methods.
89.  **Luminia-13B-v3**: A large language model specialized in generate metadata for stable diffusion. \[demo\]
90.  **Chinese-LLaVA-Med**: A multimodal large language model specialized in Chinese medical domain, based on LLaVA-1.5-7B.
91.  **AutoRE**: A document-level relation extraction system based on large language models.
92.  **NVIDIA RTX AI Toolkit**: SDKs for fine-tuning LLMs on Windows PC for NVIDIA RTX.
93.  **LazyLLM**: An easy and lazy way for building multi-agent LLMs applications and supports model fine-tuning via LLaMA Factory.
94.  **RAG-Retrieval**: A full pipeline for RAG retrieval model fine-tuning, inference, and distillation. \[blog\]
95.  **360-LLaMA-Factory**: A modified library that supports long sequence SFT & DPO using ring attention.
96.  **Sky-T1**: An o1-like model fine-tuned by NovaSky AI with very small cost.
97.  **WeClone**: One-stop solution for creating your digital avatar from chat logs.
98.  **EmoLLM**: A project about large language models (LLMs) and mental health.

License
-------

This repository is licensed under the Apache-2.0 License.

Please follow the model licenses to use the corresponding model weights: Baichuan 2 / BLOOM / ChatGLM3 / Command R / DeepSeek / Falcon / Gemma / GLM-4 / GPT-2 / Granite / Index / InternLM / Llama / Llama 2 / Llama 3 / Llama 4 / MiniCPM / Mistral/Mixtral/Pixtral / OLMo / Phi-1.5/Phi-2 / Phi-3/Phi-4 / Qwen / Skywork / StarCoder 2 / TeleChat2 / XVERSE / Yi / Yi-1.5 / Yuan 2

Citation
--------

If this work is helpful, please kindly cite as:

@inproceedings{zheng2024llamafactory,
  title\={LlamaFactory: Unified Efficient Fine-Tuning of 100+ Language Models},
  author\={Yaowei Zheng and Richong Zhang and Junhao Zhang and Yanhan Ye and Zheyan Luo and Zhangchi Feng and Yongqiang Ma},
  booktitle\={Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics (Volume 3: System Demonstrations)},
  address\={Bangkok, Thailand},
  publisher\={Association for Computational Linguistics},
  year\={2024},
  url\={http://arxiv.org/abs/2403.13372}
}

Acknowledgement
---------------

This repo benefits from PEFT, TRL, QLoRA and FastChat. Thanks for their wonderful works.

Star History
------------
