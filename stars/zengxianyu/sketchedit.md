---
project: sketchedit
stars: 255
description: SketchEdit: Mask-Free Local Image Manipulation with Partial Sketches, CVPR2022
url: https://github.com/zengxianyu/sketchedit
---

SketchEdit: Mask-Free Local Image Manipulation with Partial Sketches
--------------------------------------------------------------------

\[Paper\]  \[Project Page\]  \[Interactive Demo\]  \[Supplementary Material\]

Update
------

Star this project to get notified.

-   🆕 Uploading custom photos are now enabled in the demo
-   🆕 Edit face in a fullbody/upper body photo

-   🆕 Enable general scenes editing in the demo
-   Exposing predicted mask & mask revising?

Usage
-----

### environment

The code only has been tested on Ubuntu 20.04.

GPU is required.

1.  Clone the repo:

```
git clone --single-branch https://github.com/zengxianyu/sketchedit
git submodule init
git submodule update
```

1.  Install using the provided docker file `Dockerfile` or

```
conda env create -f environment.yml
```

1.  Switch to the installed environment

```
conda activate editline
```

### Testing

1.  Download pretrained model

```
chmod +x download/*
./download/download_model.sh
```

1.  Use the model trained on CelebAHQ

```
./test_celeb.sh
```

1.  Use the model trained on Places

```
./test_places.sh
```

### Interactive demo

http://47.57.135.203:8001/

Training code and data
----------------------

Training code and data is coming soon. Star this project to get notified.

Citation
--------

```
@inproceedings{zeng2022sketchedit,
  title={SketchEdit: Mask-Free Local Image Manipulation with Partial Sketches},
  author={Zeng, Yu and Lin, Zhe and Patel, Vishal M.},
  booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},
  year={2022}
}
```

Acknowledgments
---------------

-   DeepFill https://github.com/jiahuiyu/generative\_inpainting
-   Pix2PixHD https://github.com/NVIDIA/pix2pixHD
-   SPADE https://github.com/NVlabs/SPADE
