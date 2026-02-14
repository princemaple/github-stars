---
project: DragGAN
stars: 35972
description: Official Code for DragGAN (SIGGRAPH 2023)
url: https://github.com/XingangPan/DragGAN
---

Drag Your GAN: Interactive Point-based Manipulation on the Generative Image Manifold
====================================================================================

**Xingang Pan** · **Ayush Tewari** · **Thomas Leimkühler** · **Lingjie Liu** · **Abhimitra Meka** · **Christian Theobalt**

SIGGRAPH 2023 Conference Proceedings
------------------------------------

  

Web Demos
---------

Requirements
------------

If you have CUDA graphic card, please follow the requirements of NVlabs/stylegan3.

The usual installation steps involve the following commands, they should set up the correct CUDA version and all the python packages

```
conda env create -f environment.yml
conda activate stylegan3
```

Then install the additional requirements

```
pip install -r requirements.txt
```

Otherwise (for GPU acceleration on MacOS with Silicon Mac M1/M2, or just CPU) try the following:

cat environment.yml | \\
  grep -v -E 'nvidia|cuda' \> environment-no-nvidia.yml && \\
    conda env create -f environment-no-nvidia.yml
conda activate stylegan3

# On MacOS
export PYTORCH\_ENABLE\_MPS\_FALLBACK=1

Run Gradio visualizer in Docker
-------------------------------

Provided docker image is based on NGC PyTorch repository. To quickly try out visualizer in Docker, run the following:

# before you build the docker container, make sure you have cloned this repo, and downloaded the pretrained model by \`python scripts/download\_model.py\`.
docker build . -t draggan:latest  
docker run -p 7860:7860 -v "$PWD":/workspace/src -it draggan:latest bash
# (Use GPU)if you want to utilize your Nvidia gpu to accelerate in docker, please add command tag \`--gpus all\`, like:
#   docker run --gpus all  -p 7860:7860 -v "$PWD":/workspace/src -it draggan:latest bash

cd src && python visualizer\_drag\_gradio.py --listen

Now you can open a shared link from Gradio (printed in the terminal console).  
Beware the Docker image takes about 25GB of disk space!

Download pre-trained StyleGAN2 weights
--------------------------------------

To download pre-trained weights, simply run:

```
python scripts/download_model.py
```

If you want to try StyleGAN-Human and the Landscapes HQ (LHQ) dataset, please download weights from these links: StyleGAN-Human, LHQ, and put them under `./checkpoints`.

Feel free to try other pretrained StyleGAN.

Run DragGAN GUI
---------------

To start the DragGAN GUI, simply run:

sh scripts/gui.sh

If you are using windows, you can run:

```
.\scripts\gui.bat
```

This GUI supports editing GAN-generated images. To edit a real image, you need to first perform GAN inversion using tools like PTI. Then load the new latent code and model weights to the GUI.

You can run DragGAN Gradio demo as well, this is universal for both windows and linux:

python visualizer\_drag\_gradio.py

Acknowledgement
---------------

This code is developed based on StyleGAN3. Part of the code is borrowed from StyleGAN-Human.

(cheers to the community as well)

License
-------

The code related to the DragGAN algorithm is licensed under CC-BY-NC. However, most of this project are available under a separate license terms: all codes used or modified from StyleGAN3 is under the Nvidia Source Code License.

Any form of use and derivative of this code must preserve the watermarking functionality showing "AI Generated".

BibTeX
------

@inproceedings{pan2023draggan,
    title\={Drag Your GAN: Interactive Point-based Manipulation on the Generative Image Manifold},
    author\={Pan, Xingang and Tewari, Ayush, and Leimk{\\"u}hler, Thomas and Liu, Lingjie and Meka, Abhimitra and Theobalt, Christian},
    booktitle = {ACM SIGGRAPH 2023 Conference Proceedings},
    year\={2023}
}
