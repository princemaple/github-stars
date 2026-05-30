---
project: ludwig
stars: 11708
description: Low-code framework for building custom LLMs, neural networks, and other AI models
url: https://github.com/ludwig-ai/ludwig
---

**Declarative deep learning framework for LLMs, multimodal models, and tabular AI.**

**Docs** · **Getting Started** · **Examples** · **Discord**

* * *

What is Ludwig?
---------------

Ludwig is a **declarative deep learning framework** that lets you train, fine-tune, and deploy AI models — from LLM fine-tuning to tabular classification — using a YAML config file and zero boilerplate Python.

# Fine-tune Llama-3.1 with LoRA in one config file
model\_type: llm
base\_model: meta-llama/Llama-3.1-8B
adapter:
  type: lora
trainer:
  type: finetune
  epochs: 3
input\_features:
  - name: instruction
    type: text
output\_features:
  - name: response
    type: text

ludwig train --config model.yaml --dataset my\_data.csv

**Tech stack:** Python 3.12 · PyTorch 2.7+ · Pydantic 2 · Transformers 5 · Ray 2.54

Ludwig is hosted by the Linux Foundation AI & Data.

* * *

What's New in Ludwig 0.16
-------------------------

Feature

Description

**PatchTST & N-BEATS encoders**

State-of-the-art timeseries forecasting encoders with MASE/sMAPE metrics

**Advanced PEFT adapters**

PiSSA, EVA, CorDA/LoftQ initializers; TinyLoRA, OFT, HRA, WaveFT, LN-Tuning, VBLoRA, C3A adapter types

**VLM fine-tuning**

Train LLaVA, Qwen2-VL, InternVL via `is_multimodal: true` with gated cross-attention

**HyperNetwork combiner**

Conditioning-based feature fusion — one feature generates weights for others

**Nash-MTL & Pareto-MTL**

Game-theoretic and preference-based multi-task loss balancing

**LLM config generation**

`ludwig generate_config "describe your task"` — LLM writes the YAML for you

**ModelInspector**

Architecture analysis, weight collection, feature importance proxy

**Ray Serve & KServe**

Distributed and Kubernetes-native model deployment shims

**GRPO alignment**

Reward-model-free RLHF via Group Relative Policy Optimization

**torchao quantization + QAT**

PyTorch-native `int4/int8/float8` with Quantization-Aware Training

**Multi-adapter PEFT**

Multiple named LoRA adapters with weighted merging (TIES, DARE, SVD)

**Native Optuna executor**

GPT/TPE/CMA-ES samplers, pruning, resumable SQLite/PostgreSQL storage

**Timeseries forecasting**

`model.forecast(dataset, horizon=N)` API with `TimeseriesOutputFeature`

**Muon & ScheduleFreeAdamW**

New optimizers for large-scale pretraining and fine-tuning

**Image segmentation decoders**

UNet, SegFormer, FPN decoders for semantic segmentation

* * *

Installation
------------

pip install ludwig           # core
pip install ludwig\[full\]     # all optional dependencies
pip install ludwig\[llm\]      # LLM fine-tuning only

Requires Python 3.12+. See contributing for a full dependency matrix.

* * *

Quick Start
-----------

### Fine-tune an LLM (instruction tuning)

Ludwig supports the full LLM fine-tuning spectrum:

Technique

Config key

Supervised fine-tuning (SFT)

`trainer.type: finetune`

DPO / KTO / ORPO / GRPO alignment

`trainer.type: dpo` (or `kto`, `orpo`, `grpo`)

LoRA / DoRA / VeRA / PiSSA

`adapter.type: lora` (or `dora`, `vera`, `lora` + `init_weights: pissa`)

4-bit QLoRA (bitsandbytes)

`quantization.bits: 4`

torchao + QAT

`quantization.backend: torchao`

Multi-adapter with merging

`adapters:` dict + `merge:` block

VLM (vision-language)

`is_multimodal: true`

model\_type: llm
base\_model: meta-llama/Llama-3.1-8B

quantization:
  bits: 4

adapter:
  type: lora

prompt:
  template: |
    ### Instruction: {instruction}
    ### Input: {input}
    ### Response:
input\_features:
  - name: prompt
    type: text

output\_features:
  - name: output
    type: text

trainer:
  type: finetune
  learning\_rate: 0.0001
  batch\_size: 1
  gradient\_accumulation\_steps: 16
  epochs: 3
  learning\_rate\_scheduler:
    decay: cosine
    warmup\_fraction: 0.01

backend:
  type: local

export HUGGING\_FACE\_HUB\_TOKEN="<your\_token>"
ludwig train --config model.yaml --dataset "ludwig://alpaca"

### Train a multimodal classifier

input\_features:
  - name: review\_text
    type: text
    encoder:
      type: bert
  - name: star\_rating
    type: number
  - name: product\_image
    type: image
    encoder:
      type: dinov2

output\_features:
  - name: recommended
    type: binary

ludwig train --config model.yaml --dataset reviews.csv

### Generate a config from natural language

ludwig generate\_config "I have a CSV with age, income, education level, and I want to predict loan default"

### Make predictions

ludwig predict --model\_path results/experiment\_run/model --dataset new\_data.csv

### Launch a REST API

ludwig serve --model\_path results/experiment\_run/model
# POST http://localhost:8000/predict

* * *

Capabilities
------------

**LLM Fine-Tuning**

-   **Supervised fine-tuning (SFT)** on instruction/response pairs
-   **Alignment training**: DPO, KTO, ORPO, GRPO (reward-model-free RLHF)
-   **PEFT adapters**: LoRA, DoRA, VeRA, LoRA+, TinyLoRA, OFT, HRA, WaveFT, LN-Tuning, VBLoRA, C3A
-   **LoRA initializers**: PiSSA, EVA, CorDA, LoftQ for improved convergence
-   **Multi-adapter PEFT**: multiple named adapters on one base model, switchable at runtime; merge with TIES, DARE, SVD, magnitude pruning
-   **Quantization**: 4-bit/8-bit QLoRA (bitsandbytes), torchao int4/int8/float8 with QAT
-   **VLM fine-tuning**: LLaVA, Qwen2-VL, InternVL via `is_multimodal: true`
-   **Sequence packing** for efficient training on variable-length inputs
-   **Paged and 8-bit optimizers** for memory-efficient training

**Multimodal & Tabular Models**

-   **Input modalities**: text, numbers, categories, binary, sets, bags, sequences, images, audio, timeseries, vectors, dates
-   **Text encoders**: any HuggingFace Transformer (BERT, RoBERTa, ModernBERT, Qwen3, Llama-3.1, etc.), plus Mamba-2, Jamba
-   **Image encoders**: DINOv2, ConvNeXt, EfficientNet, ViT, CAFormer, ConvFormer, PoolFormer, TIMM (1000+ models)
-   **Timeseries encoders**: PatchTST, N-BEATS, CNN, RNN, Transformer; MASE and sMAPE metrics; `model.forecast()` API
-   **Combiners**: concat, transformer, tab\_transformer, FT-Transformer, TabNet, TabPFN v2, HyperNetwork, ProjectAggregate, GatedFusion, Perceiver
-   **Multi-task learning**: multiple output features in a single model; Nash-MTL, Pareto-MTL, FAMO, GradNorm, uncertainty loss balancing
-   **Image segmentation**: UNet, SegFormer, FPN decoders

**Training Infrastructure**

-   **Distributed training**: HuggingFace Accelerate with DDP, FSDP, DeepSpeed (zero-code changes)
-   **Ray backend**: training across a Ray cluster, larger-than-memory datasets via Ray Data
-   **Automatic batch size selection** and learning rate range test
-   **Mixed precision** (fp16/bf16), gradient checkpointing, gradient accumulation
-   **Optimizers**: AdamW, Adafactor, SGD, Muon, ScheduleFreeAdamW, Lion, paged/8-bit variants
-   **Learning rate schedulers**: cosine, linear, polynomial, reduce-on-plateau, OneCycleLR
-   **Model Soup**: uniform and greedy checkpoint averaging for better generalization at zero inference cost
-   **Modality dropout** for robust multimodal models

**Hyperparameter Optimization**

-   **Executors**: Ray Tune (ASHA, PBT, Bayesian) and native Optuna (auto/GP/TPE/CMA-ES)
-   **Optuna persistence**: SQLite or PostgreSQL for resumable HPO runs
-   **Pruning** with Optuna's MedianPruner and HyperbandPruner
-   **Search spaces**: uniform, log-uniform, choice, randint, quantized
-   **Full Ludwig config** is searchable — any nested parameter can be a hyperparameter

**Production & Deployment**

-   **REST API**: FastAPI server with Prometheus metrics and structured logging (`ludwig serve`)
-   **vLLM serving**: OpenAI-compatible API with PagedAttention and continuous batching
-   **Ray Serve**: distributed deployment with auto-scaling and traffic splitting
-   **KServe**: Kubernetes-native deployment with Open Inference Protocol v2
-   **Model export**: SafeTensors (default), `torch.export` `.pt2` bundles, ONNX
-   **HuggingFace Hub**: `ludwig upload hf_hub` — push model + auto-generated model card
-   **Docker**: prebuilt containers at ludwigai/ludwig

**Tooling & Integrations**

-   **Experiment tracking**: TensorBoard, Weights & Biases, Comet ML, MLflow, Aim Stack
-   **Model inspection**: `ModelInspector` — weight enumeration, architecture summary, feature importance proxy
-   **Visualizations**: learning curves, confusion matrices, calibration plots, ROC curves, hyperopt analysis
-   **AutoML**: `ludwig.automl.auto_train()` — give it a dataset and a time budget; the YAML-driven search space samples encoder/combiner/decoder combinations and validates them before training
-   **Dataset quality checks**: `from ludwig.utils.dataset_quality import check_dataset_quality` — validates a DataFrame before training (missing values, class imbalance, near-duplicate columns, ID leakage, …)
-   **OpenML integration**: load any OpenML task directly — `OpenMLLoader` fetches by task ID and caches locally as Parquet
-   **LLM config generation**: `ludwig generate_config "describe your task"` — LLM writes the YAML
-   **K-fold cross-validation**: `ludwig experiment --k_fold N`
-   **Dataset Zoo**: 70+ built-in benchmark datasets (`ludwig://mnist`, `ludwig://alpaca`, …)

* * *

Examples
--------

### LLM & Alignment

Use Case

Link

LLM instruction tuning (LoRA + QLoRA)

examples/llm

DPO / GRPO alignment

examples/llm/alignment

Advanced PEFT (PiSSA, OFT, VBLoRA, …)

examples/llms/peft\_advanced

VLM fine-tuning (LLaVA, Qwen2-VL)

examples/vlm

### Tabular & Multimodal

Use Case

Link

Binary classification (Titanic)

examples/titanic

Tabular classification (census income)

examples/adult\_census\_income

Multimodal classification

examples/multimodal\_classification

Multi-task learning

examples/multi\_task

### Timeseries & Vision

Use Case

Link

Timeseries forecasting (PatchTST, N-BEATS)

examples/forecasting

Weather forecasting

examples/weather

Image classification (MNIST)

examples/mnist

Semantic segmentation

examples/semantic\_segmentation

### NLP & Audio

Use Case

Link

Text classification

examples/text\_classification

Named entity recognition

examples/ner\_tagging

Machine translation

examples/machine\_translation

Speech recognition

examples/speech\_recognition

Speaker verification

examples/speaker\_verification

* * *

Why Ludwig?
-----------

-   **Zero boilerplate** — no training loop, no data pipeline, no evaluation code. The YAML config is the entire program.
-   **Best-in-class LLM support** — full spectrum from LoRA to GRPO alignment, torchao QAT, and VLM fine-tuning, all in config.
-   **Multimodal out of the box** — mix text, images, numbers, audio, and timeseries with one config change.
-   **Scale without code changes** — go from laptop → multi-GPU → Ray cluster by changing `backend.type`.
-   **Expert control when you need it** — every activation function, scheduler, and optimizer is configurable.
-   **Reproducible research** — every run is logged and the full config is saved. Compare experiments with `ludwig visualize`.

* * *

Publications
------------

-   Ludwig: A Type-Based Declarative Deep Learning Toolbox (2019)
-   Declarative Machine Learning Systems (2021)
-   Ludwig's State-of-the-Art Benchmarks

* * *

Community
---------

-   Discord — ask questions, share what you've built
-   GitHub Issues — bugs and feature requests
-   X / Twitter — announcements
-   Medium — tutorials and deep-dives
