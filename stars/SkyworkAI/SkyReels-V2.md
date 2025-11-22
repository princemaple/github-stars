---
project: SkyReels-V2
stars: 5022
description: SkyReels-V2: Infinite-length Film Generative model
url: https://github.com/SkyworkAI/SkyReels-V2
---

SkyReels V2: Infinite-Length Film Generative Model
==================================================

📑 Technical Report · 👋 Playground · 💬 Discord · 🤗 Hugging Face · 🤖 ModelScope

* * *

Welcome to the **SkyReels V2** repository! Here, you'll find the model weights and inference code for our infinite-length film generative models. To the best of our knowledge, it represents the first open-source video generative model employing **AutoRegressive Diffusion-Forcing architecture** that achieves the **SOTA performance** among publicly available models.

🔥🔥🔥 News!!
-------------

-   Jun 1, 2025: 🎉 We published the technical report, SkyReels-Audio: Omni Audio-Conditioned Talking Portraits in Video Diffusion Transformers.
-   May 16, 2025: 🔥 We release the inference code for video extension and start/end frame control in diffusion forcing model.
-   Apr 24, 2025: 🔥 We release the 720P models, SkyReels-V2-DF-14B-720P and SkyReels-V2-I2V-14B-720P. The former facilitates infinite-length autoregressive video generation, and the latter focuses on Image2Video synthesis.
-   Apr 21, 2025: 👋 We release the inference code and model weights of SkyReels-V2 Series Models and the video captioning model SkyCaptioner-V1 .
-   Apr 3, 2025: 🔥 We also release SkyReels-A2. This is an open-sourced controllable video generation framework capable of assembling arbitrary visual elements.
-   Feb 18, 2025: 🔥 we released SkyReels-A1. This is an open-sourced and effective framework for portrait image animation.
-   Feb 18, 2025: 🔥 We released SkyReels-V1. This is the first and most advanced open-source human-centric video foundation model.

🎥 Demos
--------

compress\_demo1.mp4

compress\_demo2.mp4

compress\_demo3.mp4

The demos above showcase 30-second videos generated using our SkyReels-V2 Diffusion Forcing model.

📑 TODO List
------------

-   Technical Report
-   Checkpoints of the 14B and 1.3B Models Series
-   Single-GPU & Multi-GPU Inference Code
-   SkyCaptioner-V1: A Video Captioning Model
-   Prompt Enhancer
-   Diffusers integration
-   Checkpoints of the 5B Models Series
-   Checkpoints of the Camera Director Models
-   Checkpoints of the Step & Guidance Distill Model

🚀 Quickstart
-------------

#### Installation

# clone the repository.
git clone https://github.com/SkyworkAI/SkyReels-V2
cd SkyReels-V2
# Install dependencies. Test environment uses Python 3.10.12.
pip install -r requirements.txt

#### Model Download

You can download our models from Hugging Face:

Type

Model Variant

Recommended Height/Width/Frame

Link

Diffusion Forcing

1.3B-540P

544 \* 960 \* 97f

🤗 Huggingface 🤖 ModelScope

5B-540P

544 \* 960 \* 97f

Coming Soon

5B-720P

720 \* 1280 \* 121f

Coming Soon

14B-540P

544 \* 960 \* 97f

🤗 Huggingface 🤖 ModelScope

14B-720P

720 \* 1280 \* 121f

🤗 Huggingface 🤖 ModelScope

Text-to-Video

1.3B-540P

544 \* 960 \* 97f

Coming Soon

5B-540P

544 \* 960 \* 97f

Coming Soon

5B-720P

720 \* 1280 \* 121f

Coming Soon

14B-540P

544 \* 960 \* 97f

🤗 Huggingface 🤖 ModelScope

14B-720P

720 \* 1280 \* 121f

🤗 Huggingface 🤖 ModelScope

Image-to-Video

1.3B-540P

544 \* 960 \* 97f

🤗 Huggingface 🤖 ModelScope

5B-540P

544 \* 960 \* 97f

Coming Soon

5B-720P

720 \* 1280 \* 121f

Coming Soon

14B-540P

544 \* 960 \* 97f

🤗 Huggingface 🤖 ModelScope

14B-720P

720 \* 1280 \* 121f

🤗 Huggingface 🤖 ModelScope

Camera Director

5B-540P

544 \* 960 \* 97f

Coming Soon

5B-720P

720 \* 1280 \* 121f

Coming Soon

14B-720P

720 \* 1280 \* 121f

Coming Soon

After downloading, set the model path in your generation commands:

#### Single GPU Inference

-   **Diffusion Forcing for Long Video Generation**

The **Diffusion Forcing** version model allows us to generate Infinite-Length videos. This model supports both **text-to-video (T2V)** and **image-to-video (I2V)** tasks, and it can perform inference in both synchronous and asynchronous modes. Here we demonstrate 2 running scripts as examples for long video generation. If you want to adjust the inference parameters, e.g., the duration of video, inference mode, read the Note below first.

synchronous generation for 10s video

model\_id=Skywork/SkyReels-V2-DF-14B-540P
# synchronous inference
python3 generate\_video\_df.py \\
  --model\_id ${model\_id} \\
  --resolution 540P \\
  --ar\_step 0 \\
  --base\_num\_frames 97 \\
  --num\_frames 257 \\
  --overlap\_history 17 \\
  --prompt "A graceful white swan with a curved neck and delicate feathers swimming in a serene lake at dawn, its reflection perfectly mirrored in the still water as mist rises from the surface, with the swan occasionally dipping its head into the water to feed." \\
  --addnoise\_condition 20 \\
  --offload \\
  --teacache \\
  --use\_ret\_steps \\
  --teacache\_thresh 0.3

asynchronous generation for 30s video

model\_id=Skywork/SkyReels-V2-DF-14B-540P
# asynchronous inference
python3 generate\_video\_df.py \\
  --model\_id ${model\_id} \\
  --resolution 540P \\
  --ar\_step 5 \\
  --causal\_block\_size 5 \\
  --base\_num\_frames 97 \\
  --num\_frames 737 \\
  --overlap\_history 17 \\
  --prompt "A graceful white swan with a curved neck and delicate feathers swimming in a serene lake at dawn, its reflection perfectly mirrored in the still water as mist rises from the surface, with the swan occasionally dipping its head into the water to feed." \\
  --addnoise\_condition 20 \\
  --offload

Text-to-video with `diffusers`:

import torch
from diffusers import AutoModel, SkyReelsV2DiffusionForcingPipeline, UniPCMultistepScheduler
from diffusers.utils import export\_to\_video

vae \= AutoModel.from\_pretrained("Skywork/SkyReels-V2-DF-14B-540P-Diffusers", subfolder\="vae", torch\_dtype\=torch.float32)

pipeline \= SkyReelsV2DiffusionForcingPipeline.from\_pretrained(
    "Skywork/SkyReels-V2-DF-14B-540P-Diffusers",
    vae\=vae,
    torch\_dtype\=torch.bfloat16
)
flow\_shift \= 8.0  \# 8.0 for T2V, 5.0 for I2V
pipeline.scheduler \= UniPCMultistepScheduler.from\_config(pipeline.scheduler.config, flow\_shift\=flow\_shift)
pipeline \= pipeline.to("cuda")

prompt \= "A cat and a dog baking a cake together in a kitchen. The cat is carefully measuring flour, while the dog is stirring the batter with a wooden spoon. The kitchen is cozy, with sunlight streaming through the window."

output \= pipeline(
    prompt\=prompt,
    num\_inference\_steps\=30,
    height\=544,  \# 720 for 720P
    width\=960,   \# 1280 for 720P
    num\_frames\=97,
    base\_num\_frames\=97,  \# 121 for 720P
    ar\_step\=5,  \# Controls asynchronous inference (0 for synchronous mode)
    causal\_block\_size\=5,  \# Number of frames in each block for asynchronous processing
    overlap\_history\=None,  \# Number of frames to overlap for smooth transitions in long videos; 17 for long video generations
    addnoise\_condition\=20,  \# Improves consistency in long video generation
).frames\[0\]
export\_to\_video(output, "T2V.mp4", fps\=24, quality\=8)

Image-to-video with `diffusers`:

import numpy as np
import torch
import torchvision.transforms.functional as TF
from diffusers import AutoencoderKLWan, SkyReelsV2DiffusionForcingImageToVideoPipeline, UniPCMultistepScheduler
from diffusers.utils import export\_to\_video, load\_image

model\_id \= "Skywork/SkyReels-V2-DF-14B-720P-Diffusers"
vae \= AutoencoderKLWan.from\_pretrained(model\_id, subfolder\="vae", torch\_dtype\=torch.float32)
pipeline \= SkyReelsV2DiffusionForcingImageToVideoPipeline.from\_pretrained(
    model\_id, vae\=vae, torch\_dtype\=torch.bfloat16
)
flow\_shift \= 5.0  \# 8.0 for T2V, 5.0 for I2V
pipeline.scheduler \= UniPCMultistepScheduler.from\_config(pipeline.scheduler.config, flow\_shift\=flow\_shift)
pipeline.to("cuda")

first\_frame \= load\_image("https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/diffusers/flf2v\_input\_first\_frame.png")
last\_frame \= load\_image("https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/diffusers/flf2v\_input\_last\_frame.png")

def aspect\_ratio\_resize(image, pipeline, max\_area\=720 \* 1280):
    aspect\_ratio \= image.height / image.width
    mod\_value \= pipeline.vae\_scale\_factor\_spatial \* pipeline.transformer.config.patch\_size\[1\]
    height \= round(np.sqrt(max\_area \* aspect\_ratio)) // mod\_value \* mod\_value
    width \= round(np.sqrt(max\_area / aspect\_ratio)) // mod\_value \* mod\_value
    image \= image.resize((width, height))
    return image, height, width

def center\_crop\_resize(image, height, width):
    \# Calculate resize ratio to match first frame dimensions
    resize\_ratio \= max(width / image.width, height / image.height)

    \# Resize the image
    width \= round(image.width \* resize\_ratio)
    height \= round(image.height \* resize\_ratio)
    size \= \[width, height\]
    image \= TF.center\_crop(image, size)

    return image, height, width

first\_frame, height, width \= aspect\_ratio\_resize(first\_frame, pipeline)
if last\_frame.size != first\_frame.size:
    last\_frame, \_, \_ \= center\_crop\_resize(last\_frame, height, width)

prompt \= "CG animation style, a small blue bird takes off from the ground, flapping its wings. The bird's feathers are delicate, with a unique pattern on its chest. The background shows a blue sky with white clouds under bright sunshine. The camera follows the bird upward, capturing its flight and the vastness of the sky from a close-up, low-angle perspective."

output \= pipeline(
    image\=first\_frame, last\_image\=last\_frame, prompt\=prompt, height\=height, width\=width, guidance\_scale\=5.0
).frames\[0\]
export\_to\_video(output, "output.mp4", fps\=24, quality\=8)

> **Note**:
> 
> -   If you want to run the **image-to-video (I2V)** task, add `--image ${image_path}` to your command and it is also better to use **text-to-video (T2V)**\-like prompt which includes some descriptions of the first-frame image.
> -   For long video generation, you can just switch the `--num_frames`, e.g., `--num_frames 257` for 10s video, `--num_frames 377` for 15s video, `--num_frames 737` for 30s video, `--num_frames 1457` for 60s video. The number is not strictly aligned with the logical frame number for specified time duration, but it is aligned with some training parameters, which means it may perform better. When you use asynchronous inference with causal\_block\_size > 1, the `--num_frames` should be carefully set.
> -   You can use `--ar_step 5` to enable asynchronous inference. When asynchronous inference, `--causal_block_size 5` is recommended while it is not supposed to be set for synchronous generation. REMEMBER that the frame latent number inputted into the model in every iteration, e.g., base frame latent number (e.g., (97-1)//4+1=25 for base\_num\_frames=97) and (e.g., (237-97-(97-17)x1+17-1)//4+1=20 for base\_num\_frames=97, num\_frames=237, overlap\_history=17) for the last iteration, MUST be divided by causal\_block\_size. If you find it too hard to calculate and set proper values, just use our recommended setting above :). Asynchronous inference will take more steps to diffuse the whole sequence which means it will be SLOWER than synchronous mode. In our experiments, asynchronous inference may improve the instruction following and visual consistent performance.
> -   To reduce peak VRAM, just lower the `--base_num_frames`, e.g., to 77 or 57, while keeping the same generative length `--num_frames` you want to generate. This may slightly reduce video quality, and it should not be set too small.
> -   `--addnoise_condition` is used to help smooth the long video generation by adding some noise to the clean condition. Too large noise can cause the inconsistency as well. 20 is a recommended value, and you may try larger ones, but it is recommended to not exceed 50.
> -   Generating a 540P video using the 1.3B model requires approximately 14.7GB peak VRAM, while the same resolution video using the 14B model demands around 51.2GB peak VRAM.

-   **Video Extention**

model\_id=Skywork/SkyReels-V2-DF-14B-540P
# video extention
python3 generate\_video\_df.py \\
  --model\_id ${model\_id} \\
  --resolution 540P \\
  --ar\_step 0 \\
  --base\_num\_frames 97 \\
  --num\_frames 120 \\
  --overlap\_history 17 \\
  --prompt ${prompt} \\
  --addnoise\_condition 20 \\
  --offload \\
  --use\_ret\_steps \\
  --teacache \\
  --teacache\_thresh 0.3 \\
  --video\_path ${video\_path}

> **Note**:
> 
> -   When performing video extension, you need to pass the `--video_path ${video_path}` parameter to specify the video to be extended.

-   **Start/End Frame Control**

model\_id=Skywork/SkyReels-V2-DF-14B-540P
# start/end frame control
python3 generate\_video\_df.py \\
  --model\_id ${model\_id} \\
  --resolution 540P \\
  --ar\_step 0 \\
  --base\_num\_frames 97 \\
  --num\_frames 97 \\
  --overlap\_history 17 \\
  --prompt ${prompt} \\
  --addnoise\_condition 20 \\
  --offload \\
  --use\_ret\_steps \\
  --teacache \\
  --teacache\_thresh 0.3 \\
  --image ${image} \\
  --end\_image ${end\_image}

> **Note**:
> 
> -   When controlling the start and end frames, you need to pass the `--image ${image}` parameter to control the generation of the start frame and the `--end_image ${end_image}` parameter to control the generation of the end frame.

Video extension with `diffusers`:

import numpy as np
import torch
import torchvision.transforms.functional as TF
from diffusers import AutoencoderKLWan, SkyReelsV2DiffusionForcingVideoToVideoPipeline, UniPCMultistepScheduler
from diffusers.utils import export\_to\_video, load\_video

model\_id \= "Skywork/SkyReels-V2-DF-14B-540P-Diffusers"
vae \= AutoencoderKLWan.from\_pretrained(model\_id, subfolder\="vae", torch\_dtype\=torch.float32)
pipeline \= SkyReelsV2DiffusionForcingVideoToVideoPipeline.from\_pretrained(
    model\_id, vae\=vae, torch\_dtype\=torch.bfloat16
)
flow\_shift \= 5.0  \# 8.0 for T2V, 5.0 for I2V
pipeline.scheduler \= UniPCMultistepScheduler.from\_config(pipeline.scheduler.config, flow\_shift\=flow\_shift)
pipeline.to("cuda")

video \= load\_video("input\_video.mp4")

prompt \= "CG animation style, a small blue bird takes off from the ground, flapping its wings. The bird's feathers are delicate, with a unique pattern on its chest. The background shows a blue sky with white clouds under bright sunshine. The camera follows the bird upward, capturing its flight and the vastness of the sky from a close-up, low-angle perspective."

output \= pipeline(
    video\=video, prompt\=prompt, height\=544, width\=960, guidance\_scale\=5.0,
    num\_inference\_steps\=30, num\_frames\=257, base\_num\_frames\=97#, ar\_step=5, causal\_block\_size=5,
).frames\[0\]
export\_to\_video(output, "output.mp4", fps\=24, quality\=8)
\# Total frames will be the number of frames of given video + 257

-   **Text To Video & Image To Video**

# run Text-to-Video Generation
model\_id=Skywork/SkyReels-V2-T2V-14B-540P
python3 generate\_video.py \\
  --model\_id ${model\_id} \\
  --resolution 540P \\
  --num\_frames 97 \\
  --guidance\_scale 6.0 \\
  --shift 8.0 \\
  --fps 24 \\
  --prompt "A serene lake surrounded by towering mountains, with a few swans gracefully gliding across the water and sunlight dancing on the surface." \\
  --offload \\
  --teacache \\
  --use\_ret\_steps \\
  --teacache\_thresh 0.3

> **Note**:
> 
> -   When using an **image-to-video (I2V)** model, you must provide an input image using the `--image ${image_path}` parameter. The `--guidance_scale 5.0` and `--shift 3.0` is recommended for I2V model.
> -   Generating a 540P video using the 1.3B model requires approximately 14.7GB peak VRAM, while the same resolution video using the 14B model demands around 43.4GB peak VRAM.

T2V models with `diffusers`:

import torch
from diffusers import (
    SkyReelsV2Pipeline,
    UniPCMultistepScheduler,
    AutoencoderKLWan,
)
from diffusers.utils import export\_to\_video

\# Load the pipeline
\# Available models:
\# - Skywork/SkyReels-V2-T2V-14B-540P-Diffusers
\# - Skywork/SkyReels-V2-T2V-14B-720P-Diffusers
vae \= AutoencoderKLWan.from\_pretrained(
    "Skywork/SkyReels-V2-T2V-14B-720P-Diffusers",
    subfolder\="vae",
    torch\_dtype\=torch.float32,
)
pipe \= SkyReelsV2Pipeline.from\_pretrained(
    "Skywork/SkyReels-V2-T2V-14B-720P-Diffusers",
    vae\=vae,
    torch\_dtype\=torch.bfloat16,
)
flow\_shift \= 8.0  \# 8.0 for T2V, 5.0 for I2V
pipe.scheduler \= UniPCMultistepScheduler.from\_config(pipe.scheduler.config, flow\_shift\=flow\_shift)
pipe \= pipe.to("cuda")

prompt \= "A cat and a dog baking a cake together in a kitchen. The cat is carefully measuring flour, while the dog is stirring the batter with a wooden spoon. The kitchen is cozy, with sunlight streaming through the window."

output \= pipe(
    prompt\=prompt,
    num\_inference\_steps\=50,
    height\=544,
    width\=960,
    guidance\_scale\=6.0,  \# 6.0 for T2V, 5.0 for I2V
    num\_frames\=97,
).frames\[0\]
export\_to\_video(output, "video.mp4", fps\=24, quality\=8)

I2V models with `diffusers`:

import torch
from diffusers import (
    SkyReelsV2ImageToVideoPipeline,
    UniPCMultistepScheduler,
    AutoencoderKLWan,
)
from diffusers.utils import export\_to\_video
from PIL import Image

\# Load the pipeline
\# Available models:
\# - Skywork/SkyReels-V2-I2V-1.3B-540P-Diffusers
\# - Skywork/SkyReels-V2-I2V-14B-540P-Diffusers
\# - Skywork/SkyReels-V2-I2V-14B-720P-Diffusers
vae \= AutoencoderKLWan.from\_pretrained(
    "Skywork/SkyReels-V2-I2V-14B-720P-Diffusers",
    subfolder\="vae",
    torch\_dtype\=torch.float32,
)
pipe \= SkyReelsV2ImageToVideoPipeline.from\_pretrained(
    "Skywork/SkyReels-V2-I2V-14B-720P-Diffusers",
    vae\=vae,
    torch\_dtype\=torch.bfloat16,
)
flow\_shift \= 5.0  \# 8.0 for T2V, 5.0 for I2V
pipe.scheduler \= UniPCMultistepScheduler.from\_config(pipe.scheduler.config, flow\_shift\=flow\_shift)
pipe \= pipe.to("cuda")

prompt \= "A cat and a dog baking a cake together in a kitchen. The cat is carefully measuring flour, while the dog is stirring the batter with a wooden spoon. The kitchen is cozy, with sunlight streaming through the window."
image \= Image.open("path/to/image.png")

output \= pipe(
    image\=image,
    prompt\=prompt,
    num\_inference\_steps\=50,
    height\=544,
    width\=960,
    guidance\_scale\=5.0,  \# 6.0 for T2V, 5.0 for I2V
    num\_frames\=97,
).frames\[0\]
export\_to\_video(output, "video.mp4", fps\=24, quality\=8)

-   **Prompt Enhancer**

The prompt enhancer is implemented based on Qwen2.5-32B-Instruct and is utilized via the `--prompt_enhancer` parameter. It works ideally for short prompts, while for long prompts, it might generate an excessively lengthy prompt that could lead to over-saturation in the generative video. Note the peak memory of GPU is 64G+ if you use `--prompt_enhancer`. If you want to obtain the enhanced prompt separately, you can also run the prompt\_enhancer script separately for testing. The steps are as follows:

cd skyreels\_v2\_infer/pipelines
python3 prompt\_enhancer.py --prompt "A serene lake surrounded by towering mountains, with a few swans gracefully gliding across the water and sunlight dancing on the surface."

> **Note**:
> 
> -   `--prompt_enhancer` is not allowed if using `--use_usp`. We recommend running the skyreels\_v2\_infer/pipelines/prompt\_enhancer.py script first to generate enhanced prompt before enabling the `--use_usp` parameter.

**Advanced Configuration Options**

Below are the key parameters you can customize for video generation:

Parameter

Recommended Value

Description

\--prompt

Text description for generating your video

\--image

Path to input image for image-to-video generation

\--resolution

540P or 720P

Output video resolution (select based on model type)

\--num\_frames

97 or 121

Total frames to generate (**97 for 540P models**, **121 for 720P models**)

\--inference\_steps

50

Number of denoising steps

\--fps

24

Frames per second in the output video

\--shift

8.0 or 5.0

Flow matching scheduler parameter (**8.0 for T2V**, **5.0 for I2V**)

\--guidance\_scale

6.0 or 5.0

Controls text adherence strength (**6.0 for T2V**, **5.0 for I2V**)

\--seed

Fixed seed for reproducible results (omit for random generation)

\--offload

True

Offloads model components to CPU to reduce VRAM usage (recommended)

\--use\_usp

True

Enables multi-GPU acceleration with xDiT USP

\--outdir

./video\_out

Directory where generated videos will be saved

\--prompt\_enhancer

True

Expand the prompt into a more detailed description

\--teacache

False

Enables teacache for faster inference

\--teacache\_thresh

0.2

Higher speedup will cause to worse quality

\--use\_ret\_steps

False

Retention Steps for teacache

**Diffusion Forcing Additional Parameters**

Parameter

Recommended Value

Description

\--ar\_step

0

Controls asynchronous inference (0 for synchronous mode)

\--base\_num\_frames

97 or 121

Base frame count (**97 for 540P**, **121 for 720P**)

\--overlap\_history

17

Number of frames to overlap for smooth transitions in long videos

\--addnoise\_condition

20

Improves consistency in long video generation

\--causal\_block\_size

5

Recommended when using asynchronous inference (--ar\_step > 0)

\--video\_path

Path to input video for video extension

\--end\_image

Path to input image for end frame control

#### Multi-GPU inference using xDiT USP

We use xDiT USP to accelerate inference. For example, to generate a video with 2 GPUs, you can use the following command:

-   **Diffusion Forcing**

model\_id=Skywork/SkyReels-V2-DF-14B-540P
# diffusion forcing synchronous inference
torchrun --nproc\_per\_node=2 generate\_video\_df.py \\
  --model\_id ${model\_id} \\
  --resolution 540P \\
  --ar\_step 0 \\
  --base\_num\_frames 97 \\
  --num\_frames 257 \\
  --overlap\_history 17 \\
  --prompt "A graceful white swan with a curved neck and delicate feathers swimming in a serene lake at dawn, its reflection perfectly mirrored in the still water as mist rises from the surface, with the swan occasionally dipping its head into the water to feed." \\
  --addnoise\_condition 20 \\
  --use\_usp \\
  --offload \\
  --seed 42

-   **Text To Video & Image To Video**

# run Text-to-Video Generation
model\_id=Skywork/SkyReels-V2-T2V-14B-540P
torchrun --nproc\_per\_node=2 generate\_video.py \\
  --model\_id ${model\_id} \\
  --resolution 540P \\
  --num\_frames 97 \\
  --guidance\_scale 6.0 \\
  --shift 8.0 \\
  --fps 24 \\
  --offload \\
  --prompt "A serene lake surrounded by towering mountains, with a few swans gracefully gliding across the water and sunlight dancing on the surface." \\
  --use\_usp \\
  --seed 42

> **Note**:
> 
> -   When using an **image-to-video (I2V)** model, you must provide an input image using the `--image ${image_path}` parameter. The `--guidance_scale 5.0` and `--shift 3.0` is recommended for I2V model.

Contents
--------

-   Abstract
-   Methodology of SkyReels-V2
-   Key Contributions of SkyReels-V2
    -   Video Captioner
    -   Reinforcement Learning
    -   Diffusion Forcing
    -   High-Quality Supervised Fine-Tuning(SFT)
-   Performance
-   Acknowledgements
-   Citation

* * *

Abstract
--------

Recent advances in video generation have been driven by diffusion models and autoregressive frameworks, yet critical challenges persist in harmonizing prompt adherence, visual quality, motion dynamics, and duration: compromises in motion dynamics to enhance temporal visual quality, constrained video duration (5-10 seconds) to prioritize resolution, and inadequate shot-aware generation stemming from general-purpose MLLMs' inability to interpret cinematic grammar, such as shot composition, actor expressions, and camera motions. These intertwined limitations hinder realistic long-form synthesis and professional film-style generation.

To address these limitations, we introduce SkyReels-V2, the world's first infinite-length film generative model using a Diffusion Forcing framework. Our approach synergizes Multi-modal Large Language Models (MLLM), Multi-stage Pretraining, Reinforcement Learning, and Diffusion Forcing techniques to achieve comprehensive optimization. Beyond its technical innovations, SkyReels-V2 enables multiple practical applications, including Story Generation, Image-to-Video Synthesis, Camera Director functionality, and multi-subject consistent video generation through our Skyreels-A2 system.

Methodology of SkyReels-V2
--------------------------

The SkyReels-V2 methodology consists of several interconnected components. It starts with a comprehensive data processing pipeline that prepares various quality training data. At its core is the Video Captioner architecture, which provides detailed annotations for video content. The system employs a multi-task pretraining strategy to build fundamental video generation capabilities. Post-training optimization includes Reinforcement Learning to enhance motion quality, Diffusion Forcing Training for generating extended videos, and High-quality Supervised Fine-Tuning (SFT) stages for visual refinement. The model runs on optimized computational infrastructure for efficient training and inference. SkyReels-V2 supports multiple applications, including Story Generation, Image-to-Video Synthesis, Camera Director functionality, and Elements-to-Video Generation.

Key Contributions of SkyReels-V2
--------------------------------

#### Video Captioner

SkyCaptioner-V1 serves as our video captioning model for data annotation. This model is trained on the captioning result from the base model Qwen2.5-VL-72B-Instruct and the sub-expert captioners on a balanced video data. The balanced video data is a carefully curated dataset of approximately 2 million videos to ensure conceptual balance and annotation quality. Built upon the Qwen2.5-VL-7B-Instruct foundation model, SkyCaptioner-V1 is fine-tuned to enhance performance in domain-specific video captioning tasks. To compare the performance with the SOTA models, we conducted a manual assessment of accuracy across different captioning fields using a test set of 1,000 samples. The proposed SkyCaptioner-V1 achieves the highest average accuracy among the baseline models, and show a dramatic result in the shot related fields

model

Qwen2.5-VL-7B-Ins.

Qwen2.5-VL-72B-Ins.

Tarsier2-Recap-7b

SkyCaptioner-V1

Avg accuracy

51.4%

58.7%

49.4%

**76.3%**

shot type

76.8%

82.5%

60.2%

**93.7%**

shot angle

60.0%

73.7%

52.4%

**89.8%**

shot position

28.4%

32.7%

23.6%

**83.1%**

camera motion

62.0%

61.2%

45.3%

**85.3%**

expression

43.6%

51.5%

54.3%

**68.8%**

TYPES\_type

43.5%

49.7%

47.6%

**82.5%**

TYPES\_sub\_type

38.9%

44.9%

45.9%

**75.4%**

appearance

40.9%

52.0%

45.6%

**59.3%**

action

32.4%

52.0%

**69.8%**

68.8%

position

35.4%

48.6%

45.5%

**57.5%**

is\_main\_subject

58.5%

68.7%

69.7%

**80.9%**

environment

70.4%

**72.7%**

61.4%

70.5%

lighting

77.1%

**80.0%**

21.2%

76.5%

#### Reinforcement Learning

Inspired by the previous success in LLM, we propose to enhance the performance of the generative model by Reinforcement Learning. Specifically, we focus on the motion quality because we find that the main drawback of our generative model is:

-   the generative model does not handle well with large, deformable motions.
-   the generated videos may violate the physical law.

To avoid the degradation in other metrics, such as text alignment and video quality, we ensure the preference data pairs have comparable text alignment and video quality, while only the motion quality varies. This requirement poses greater challenges in obtaining preference annotations due to the inherently higher costs of human annotation. To address this challenge, we propose a semi-automatic pipeline that strategically combines automatically generated motion pairs and human annotation results. This hybrid approach not only enhances the data scale but also improves alignment with human preferences through curated quality control. Leveraging this enhanced dataset, we first train a specialized reward model to capture the generic motion quality differences between paired samples. This learned reward function subsequently guides the sample selection process for Direct Preference Optimization (DPO), enhancing the motion quality of the generative model.

#### Diffusion Forcing

We introduce the Diffusion Forcing Transformer to unlock our model’s ability to generate long videos. Diffusion Forcing is a training and sampling strategy where each token is assigned an independent noise level. This allows tokens to be denoised according to arbitrary, per-token schedules. Conceptually, this approach functions as a form of partial masking: a token with zero noise is fully unmasked, while complete noise fully masks it. Diffusion Forcing trains the model to "unmask" any combination of variably noised tokens, using the cleaner tokens as conditional information to guide the recovery of noisy ones. Building on this, our Diffusion Forcing Transformer can extend video generation indefinitely based on the last frames of the previous segment. Note that the synchronous full sequence diffusion is a special case of Diffusion Forcing, where all tokens share the same noise level. This relationship allows us to fine-tune the Diffusion Forcing Transformer from a full-sequence diffusion model.

#### High-Quality Supervised Fine-Tuning (SFT)

We implement two sequential high-quality supervised fine-tuning (SFT) stages at 540p and 720p resolutions respectively, with the initial SFT phase conducted immediately after pretraining but prior to reinforcement learning (RL) stage.This first-stage SFT serves as a conceptual equilibrium trainer, building upon the foundation model’s pretraining outcomes that utilized only fps24 video data, while strategically removing FPS embedding components to streamline thearchitecture. Trained with the high-quality concept-balanced samples, this phase establishes optimized initialization parameters for subsequent training processes. Following this, we execute a secondary high-resolution SFT at 720p after completing the diffusion forcing stage, incorporating identical loss formulations and the higher-quality concept-balanced datasets by the manually filter. This final refinement phase focuses on resolution increase such that the overall video quality will be further enhanced.

Performance
-----------

To comprehensively evaluate our proposed method, we construct the SkyReels-Bench for human assessment and leveraged the open-source V-Bench for automated evaluation. This allows us to compare our model with the state-of-the-art (SOTA) baselines, including both open-source and proprietary models.

#### Human Evaluation

For human evaluation, we design SkyReels-Bench with 1,020 text prompts, systematically assessing three dimensions: Instruction Adherence, Motion Quality, Consistency and Visual Quality. This benchmark is designed to evaluate both text-to-video (T2V) and image-to-video (I2V) generation models, providing comprehensive assessment across different generation paradigms. To ensure fairness, all models were evaluated under default settings with consistent resolutions, and no post-generation filtering was applied.

-   Text To Video Models

Model Name

Average

Instruction Adherence

Consistency

Visual Quality

Motion Quality

Runway-Gen3 Alpha

2.53

2.19

2.57

3.23

2.11

HunyuanVideo-13B

2.82

2.64

2.81

3.20

2.61

Kling-1.6 STD Mode

2.99

2.77

3.05

3.39

**2.76**

Hailuo-01

3.0

2.8

3.08

3.29

2.74

Wan2.1-14B

3.12

2.91

3.31

**3.54**

2.71

SkyReels-V2

**3.14**

**3.15**

**3.35**

3.34

2.74

The evaluation demonstrates that our model achieves significant advancements in **instruction adherence (3.15)** compared to baseline methods, while maintaining competitive performance in **motion quality (2.74)** without sacrificing the **consistency (3.35)**.

-   Image To Video Models

Model

Average

Instruction Adherence

Consistency

Visual Quality

Motion Quality

HunyuanVideo-13B

2.84

2.97

2.95

2.87

2.56

Wan2.1-14B

2.85

3.10

2.81

3.00

2.48

Hailuo-01

3.05

3.31

2.58

3.55

2.74

Kling-1.6 Pro Mode

3.4

3.56

3.03

3.58

3.41

Runway-Gen4

3.39

3.75

3.2

3.4

3.37

SkyReels-V2-DF

3.24

3.64

3.21

3.18

2.93

SkyReels-V2-I2V

3.29

3.42

3.18

3.56

3.01

Our results demonstrate that both **SkyReels-V2-I2V (3.29)** and **SkyReels-V2-DF (3.24)** achieve state-of-the-art performance among open-source models, significantly outperforming HunyuanVideo-13B (2.84) and Wan2.1-14B (2.85) across all quality dimensions. With an average score of 3.29, SkyReels-V2-I2V demonstrates comparable performance to proprietary models Kling-1.6 (3.4) and Runway-Gen4 (3.39).

#### VBench

To objectively compare SkyReels-V2 Model against other leading open-source Text-To-Video models, we conduct comprehensive evaluations using the public benchmark V-Bench. Our evaluation specifically leverages the benchmark’s longer version prompt. For fair comparison with baseline models, we strictly follow their recommended setting for inference.

Model

Total Score

Quality Score

Semantic Score

OpenSora 2.0

81.5 %

82.1 %

78.2 %

CogVideoX1.5-5B

80.3 %

80.9 %

77.9 %

HunyuanVideo-13B

82.7 %

84.4 %

76.2 %

Wan2.1-14B

83.7 %

84.2 %

**81.4 %**

SkyReels-V2

**83.9 %**

**84.7 %**

80.8 %

The VBench results demonstrate that SkyReels-V2 outperforms all compared models including HunyuanVideo-13B and Wan2.1-14B, With the highest **total score (83.9%)** and **quality score (84.7%)**. In this evaluation, the semantic score is slightly lower than Wan2.1-14B, while we outperform Wan2.1-14B in human evaluations, with the primary gap attributed to V-Bench’s insufficient evaluation of shot-scenario semantic adherence.

Acknowledgements
----------------

We would like to thank the contributors of Wan 2.1, XDit and Qwen 2.5 repositories, for their open research and contributions.

Citation
--------

@misc{chen2025skyreelsv2infinitelengthfilmgenerative,
      title\={SkyReels-V2: Infinite-length Film Generative Model}, 
      author\={Guibin Chen and Dixuan Lin and Jiangping Yang and Chunze Lin and Junchen Zhu and Mingyuan Fan and Hao Zhang and Sheng Chen and Zheng Chen and Chengcheng Ma and Weiming Xiong and Wei Wang and Nuo Pang and Kang Kang and Zhiheng Xu and Yuzhe Jin and Yupeng Liang and Yubing Song and Peng Zhao and Boyuan Xu and Di Qiu and Debang Li and Zhengcong Fei and Yang Li and Yahui Zhou},
      year\={2025},
      eprint\={2504.13074},
      archivePrefix\={arXiv},
      primaryClass\={cs.CV},
      url\={https://arxiv.org/abs/2504.13074}, 
}
