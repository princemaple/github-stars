---
project: MimicBrush
stars: 1305
description: Official implementations for paper: Zero-shot Image Editing with Reference Imitation
url: https://github.com/ali-vilab/MimicBrush
---

Zero-shot Image Editing with Reference Imitation
------------------------------------------------

**Xi Chen** · **Yutong Feng** · **Mengting Chen** · **Yiyang Wang** · **Shilong Zhang** · **Yu Liu** · **Yujun Shen** · **Hengshuang Zhao**  
  
  
**The University of Hong Kong   |   Alibaba Group |   Ant Group**

News
----

-   **\[2024.06.12\]** Release inference code, local gradio demo, online demo.
-   **\[Todo\]** Release our benchmark.

Community Contributions
-----------------------

ComfyUI version by @AIFSH

Installation
------------

Install with `conda`:

conda env create -f environment.yaml
conda activate mimicbrush

or `pip`:

#Python==3.8.5
pip install -r requirements.txt

Download Checkpoints
--------------------

Download SD-1.5 and SD-1.5-inpainting checkpoint:

-   You could download them from HuggingFace stable-diffusion-v1-5 and stable-diffusion-inpainting
-   However, the repo above contains many models that would not be used, we provide a clean version at cleansd

Download MimicBrush checkpoint, along with a VAE, a CLIP encoder, and a depth model

-   Download the weights on ModelScope xichen/MimicBrush
-   The model is big because it contains two U-Nets.

You could use the following code to download them from modelscope

from modelscope.hub.snapshot\_download import snapshot\_download as ms\_snapshot\_download

sd\_dir \= ms\_snapshot\_download('xichen/cleansd', cache\_dir\='./modelscope')
print('=== Pretrained SD weights downloaded ===')
model\_dir \= ms\_snapshot\_download('xichen/MimicBrush', cache\_dir\='./modelscope')
print('=== MimicBrush weights downloaded ===')

or from Huggingface

from huggingface\_hub import snapshot\_download
snapshot\_download(repo\_id\="xichenhku/cleansd", local\_dir\="./cleansd")
print('=== Pretrained SD weights downloaded ===')
snapshot\_download(repo\_id\="xichenhku/MimicBrush", local\_dir\="./MimicBrush")
print('=== MimicBrush weights downloaded ===')

Gradio Demo
-----------

First, modify `./configs/inference.yaml` to set the path of model weight. Afterwards, run the script:

python run\_gradio3\_demo.py

The gradio demo would look like the UI shown below.

\*Please do not forget to click ''keep the original shape'' if you want condut texture transfer like the third case.  

A biref tutorial:

-   Upload/select a source image to edit.
-   Draw the to-edit regionon the source image.
-   Upload/select a reference image.
-   Run.

Inference
---------

1.  Dowload our evaluation benchmark at Google Drive:
    
    -   URL: \[to be released\]
2.  Set the path to each dataset and checkpoints in `./config/inference.yaml` :
    
3.  Run inference with
    
    python run\_inference\_benchmark.py
    

Acknowledgements
----------------

This project is developped on the codebase of IP-Adapter and MagicAnimate . We appreciate this great work!

Citation
--------

If you find this codebase useful for your research, please use the following entry.

@article{chen2024mimicbrush,
  title\={Zero-shot Image Editing with Reference Imitation},
  author\={Chen, Xi and Feng, Yutong and Chen, Mengting and Wang, Yiyang, and Zhang, Shilong and Yu, Liu and Shen, Yujun and Zhao, Hengshuang},
  journal\={arXiv preprint arXiv:2406.07547},
  year\={2024}
}

Star History
------------
