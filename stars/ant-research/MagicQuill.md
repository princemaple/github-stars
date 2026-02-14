---
project: MagicQuill
stars: 3667
description: [CVPR'25] Official Implementations for Paper - MagicQuill: An Intelligent Interactive Image Editing System
url: https://github.com/ant-research/MagicQuill
---

🪶 MagicQuill: An Intelligent Interactive Image Editing System (_CVPR 2025_)
============================================================================

demo480p.mp4

There is an HD video on Youtube.

Zichen Liu\*,1,2, Yue Yu\*,1,2, Hao Ouyang2, Qiuyu Wang2, Ka Leong Cheng1,2, Wen Wang3,2, Zhiheng Liu4, Qifeng Chen†,1, Yujun Shen†,2  
1HKUST 2Ant Group 3ZJU 4HKU \*equal contribution †corresponding author

> TLDR: MagicQuill is an intelligent and interactive system achieving precise image editing.
> 
> Key Features: 😎 User-friendly interface / 🤖 AI-powered suggestions / 🎨 Precise local editing

-   🪶 MagicQuill: An Intelligent Interactive Image Editing System
    -   TODO List
    -   Update Log
    -   Hardware Requirements
    -   Docker Container
    -   Setup
    -   Tutorial
    -   Citation
    -   Acknowledgement
    -   Note

MagicQuillV2 has been released!!! Check it out ;)
-------------------------------------------------

TODO List
---------

-   Release the paper and demo page. Visit magicquill.art 🪩
-   Release the code and checkpoints.
-   Release gradio demo.
-   Release ComfyUI MagicQuill custom node.

Update Log
----------

-   \[2024.11.21\] 📢 Update the save button; Fix path bug on Windows; Add `.bat` and `.sh` files for convenient environment install on Windows and Linux. Thanks lior007 and JamesIV4.
-   \[2024.11.25\] 📢 New UI Updates: Drag & Drop Images + Download Button: We've enhanced our interface with two exciting features! Now you can easily upload images with drag & drop functionality, and quickly save your work using our new download button. Try it out and let us know what you think!
-   \[2024.12.06\] 📢 New Feature Updates: Auto-save and Resolution Adjustment are now enabled in the parameter settings. Thanks Furkan Gözükara for his brilliant suggestions.
-   \[2024.12.07\] 🎉 Exciting News: ComfyUI MagicQuill Node has been released! Check the repository https://github.com/magic-quill/ComfyUI\_MagicQuill for more details.
-   \[2024.12.16\] 🎉 Exciting News: MagicQuill is also available at Modelscope. Thanks for their amazing support and infrastructure.
-   \[2025.01.02\] 🎉 Exciting News: MagicQuill docker container is now available. You can now build & run your own image in a cleaner, isolated environment. Thanks gbudge for his contribution.
-   \[2025.02.27\] 🎉 Exciting News: MagicQuill has been accepted to CVPR 2025! Looking forward to meeting everyone in Tennessee!
-   \[2025.12.03\] 🎉 Exciting News: MagicQuillV2 has been released! Check it out ;), give us a star if you are interested.

To update the latest features, pull the latest code and re-install the gradio\_magicquill:

```
pip uninstall -y gradio_magicquill-0.0.1-py3-none-any.whl
pip install gradio_magicquill-0.0.1-py3-none-any.whl
```

Hardware Requirements
---------------------

-   GPU is required to run MagicQuill. **Through our testing, we have confirmed that the model can run on GPUs with 8GB VRAM (RTX4070 Laptop).**

For users with limited GPU resources, please try our Huggingface Demo and Modelscope Demo. Also, consider disabling the DrawNGuess automatic prompt filling by clicking the wand icon above if it takes too long time on your machine.

Setup
-----

Follow the following guide to set up the environment.

1.  git clone repo. **Please don't forget the `--recursive` flag.** Otherwise, you will find `LLaVA` submodule missing.
    
    ```
    git clone --recursive https://github.com/magic-quill/MagicQuill.git
    cd MagicQuill
    ```
    
2.  download and unzip checkpoints
    
    ```
    wget -O models.zip "https://hkustconnect-my.sharepoint.com/:u:/g/personal/zliucz_connect_ust_hk/EWlGF0WfawJIrJ1Hn85_-3gB0MtwImAnYeWXuleVQcukMg?e=Gcjugg&download=1"
    unzip models.zip
    ```
    
    If the .zip file is not accessible, download it via browser. All checkpoints are about 25 GB in total. It may take some time to download. Alternatively, check our checkpoints at huggingface.

* * *

If you are a Windows user, you may try to use `windows_setup.bat` to conveniently install environments, just enter `windows_setup.bat` in your Python shell. For Linux user, check `linux_setup.sh`.

Alternatively, follow the step-by-step installation guide.

1.  create environment
    
    ```
    conda create -n MagicQuill python=3.10 -y
    conda activate MagicQuill
    ```
    
2.  install torch with GPU support
    
    ```
    pip install torch==2.1.2 torchvision==0.16.2 torchaudio==2.1.2 --index-url https://download.pytorch.org/whl/cu118
    ```
    
3.  install the interface
    
    ```
    pip install gradio_magicquill-0.0.1-py3-none-any.whl
    ```
    
4.  install llava environment
    
    ```
    (For Linux)
    cp -f pyproject.toml MagicQuill/LLaVA/
    pip install -e MagicQuill/LLaVA/
    ```
    
    or
    
    ```
    (For Windows)
    copy /Y pyproject.toml MagicQuill\LLaVA\
    pip install -e MagicQuill\LLaVA\
    ```
    
    (For Windows PowerShell, the first line should be `Copy-Item -Path pyproject.toml -Destination "MagicQuill\LLaVA" -Force`)
    
5.  install the remaining environment
    
    ```
    pip install -r requirements.txt
    ```
    
6.  run magicquill
    
    ```
    python gradio_run.py
    ```
    
    If you are mainland user, you may try `export HF_ENDPOINT=https://hf-mirror.com` to use huggingface mirror to facilitate the download of some necessary checkpoints to run our system.
    

Docker Container
----------------

You can build a docker container with MagicQuill as follows:

1.  git clone repo. **Please don't forget the `--recursive` flag.** Otherwise, you will find `LLaVA` submodule missing.
    
    ```
    git clone --recursive https://github.com/magic-quill/MagicQuill.git
    cd MagicQuill
    ```
    
2.  download and unzip checkpoints
    
    ```
    wget -O models.zip "https://hkustconnect-my.sharepoint.com/:u:/g/personal/zliucz_connect_ust_hk/EWlGF0WfawJIrJ1Hn85_-3gB0MtwImAnYeWXuleVQcukMg?e=Gcjugg&download=1"
    unzip models.zip
    ```
    
    If the .zip file is not accessible, download it via browser. All checkpoints are about 25 GB in total. It may take some time to download. Alternatively, check our checkpoints at huggingface.
    
    Note: these can be located anywhere on the host computer, but Docker Compose expects them to be in `/data/magicquill/models` by default. Update `docker-compose.yaml` if you unzip them to another location.
    
3.  build the image
    
    ```
    docker compose build
    ```
    
4.  run the image
    
    ```
    docker compose up -d
    ```
    

Tutorial
--------

Please read before you try!

### I. Three type of magic quills

  
Use the **add brush** to add details and elements guided by prompts - express your ideas with your own lively strokes!  

  

"With just a few strokes, a vivid little deer comes to life"  

  

"Adorn the beautiful lady with a necklace"  

  

  
The **subtract brush** can remove excess details or redraw areas based on prompts. If there's anything you're not satisfied with, just subtract it away!  

  

"A dolphin with two tail fins? Let's give it a quick 'treatment'!"  

  

"Let's take off Mr. Skeleton's hat and help him cool down."  
  

  
&

  
Combine the **add and subtract brushes** to create amazing combo effects!  

  

"Let's give Mona Lisa a pet cat~"  

  

"Let's give this handsome fellow a new tie!"  
  

  
The **color brush** can precisely color the image, matching the color of your brush~  

  

"Precise color highlighting - paint exactly where you want to color"  

  

"Don't you think the blue flowers look more dreamy than the pink ones?"  
  

\*Please note the color brush and add&subtract brush are mutually exclusive - you can only use one at a time!  
  

* * *

### II. Draw and Guess

Our brush is super smart! Look at the examples above - as soon as you finish drawing, it quickly guesses what you want to create and fills in the prompts for you~ Sometimes it might guess wrong though, so feel free to tell it what you actually want to draw~  

  

"Oops! I don't want to draw a vine, I want to create a path!"  
  

* * *

### III. Super useful canvas tools!

  

Click this button to upload the photo you want to edit~  

  

Made a mistake with the brush? Just erase it with the rubber tool!  

  

Drag, rotate, and resize your strokes with the cursor - just like when you're working in PowerPoint!  

  

&

Left is ctrl+z, right is ctrl+y - you know what that means! 😊  
And for Mac users, left is command+z, right is command+shift+z! 😝  

  

Oops! That doesn't look right 😵 - click this trash bin to delete the stroke  

  

The brush strokes are in my way, how can I see the image😡?! Try clicking this button to temporarily hide your strokes  

  

&

These two icons will appear after the image is generated...  
I love this generated image 😍, I want to keep editing! ➡️ Click ✅ to continue editing  
What is this thing 😡, I don't want to see it! ➡️ Click ❎ to discard the result  
  

* * *

### IV. Notes

  

When you see the spinning icon in the bottom left corner, it means the magicquill is still charging up 💪 Wait for it to disappear before clicking the Run button!  

  

When the magic wand is flashing, our brush is working hard to guess what you're trying to draw 🤔 Please be patient! 🙏  
  

* * *

### V. Parameters

If you've made it here, you must really love our work! 😍  
If you want to learn how to better control the generation results, don't miss this section! 😘  
Next to the Run button, you can select parameters to modify advanced settings 🧐  
  

-   Base Model Name: Users can adjust this to select appropriate base models for different editing styles
    -   SD1.5/realisticVisionV60B1\_v51VAE.safetensors: This generates realistic style images! Use this most of the time.
    -   SD1.5/DreamShaper.safetensors: This one is for generating fantasy style images
    -   SD1.5/majicMIX\_realistic: This one is good at generating portraits 👩
    -   SD1.5/MeinaMix.safetensors: This one is good at generating anime images.
    -   SD1.5/ghostmix\_v20Bakedvae.safetensors: Another model for anime image generation.
    -   If there are any models you'd like to add, contact us!
-   Negative Prompt: Users can input content they want the model to avoid generating. Whatever you don't want to generate, put it here.
-   Fine Edge: Users can enable this option to activate fine edge control.
-   Grow Size: Adjust this parameter to set the pixel range affected around brush strokes when editing images, to expand/reduce the brush stroke influence area.
-   Edge Strength: Parameter for adjusting the add/subtract brush control strength. Simply put, if you're confident in your drawing skills, you can increase strength. If you're a bad drawer like us 🤦, please keep the parameter as is, or reduce the strength a bit.
-   Color Strength: Parameter for adjusting the color brush control strength, can adjust the image's coloring effects.
-   The remaining parameters are just some common parameters for diffusion models! You basically don't need to manage these, but if you're in the industry/AI art expert, feel free to try adjusting them.

Citation
--------

Don't forget to cite this source if it proves useful in your research!

@article{liu2024magicquill, 
	title\={MagicQuill: An Intelligent Interactive Image Editing System}, 
	author\={Zichen Liu and Yue Yu and Hao Ouyang and Qiuyu Wang and Ka Leong Cheng and Wen Wang and Zhiheng Liu and Qifeng Chen and Yujun Shen}, 
	year\={2024}, 
	eprint\={2411.09703}, 
	archivePrefix\={arXiv}, 
	primaryClass\={cs.CV}}

Acknowledgement
---------------

Our implementation is based on

-   ComfyUI-BrushNet
-   ComfyUI
-   LLaVA
-   comfyui\_controlnet\_aux
-   ComfyUI\_Custom\_Nodes\_AlekPet
-   fabric.js

Thanks for their remarkable contribution and released code!

Note
----

Note: This repo is governed by the license of CC BY-NC 4.0 We strongly advise users not to knowingly generate or allow others to knowingly generate harmful content, including hate speech, violence, pornography, deception, etc.

(注：本仓库受CC BY-NC的许可协议限制。我们强烈建议，用户不应传播及不应允许他人传播以下内容，包括但不限于仇恨言论、暴力、色情、欺诈相关的有害信息。)
