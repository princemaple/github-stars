---
project: pifuhd
stars: 9759
description: High-Resolution 3D Human Digitization from A Single Image.
url: https://github.com/facebookresearch/pifuhd
---

PIFuHD: Multi-Level Pixel-Aligned Implicit Function for High-Resolution 3D Human Digitization (CVPR 2020)
=========================================================================================================

News:

-   \[2020/06/15\] Demo with Google Colab (incl. visualization) is available! Please check out #pifuhd on Twitter for many results tested by users!

This repository contains a pytorch implementation of "Multi-Level Pixel-Aligned Implicit Function for High-Resolution 3D Human Digitization".

This codebase provides:

-   test code
-   visualization code

See our blog post to learn more about our work at CVPR2020!

Demo on Google Colab
--------------------

In case you don't have an environment with GPUs to run PIFuHD, we offer Google Colab demo. You can also upload your own images and reconstruct 3D geometry together with visualization. Try our Colab demo using the following notebook:  

Requirements
------------

-   Python 3
-   PyTorch tested on 1.4.0, 1.5.0
-   json
-   PIL
-   skimage
-   tqdm
-   cv2

For visualization

-   trimesh with pyembree
-   PyOpenGL
-   freeglut (use `sudo apt-get install freeglut3-dev` for ubuntu users)
-   ffmpeg

Note: At least 8GB GPU memory is recommended to run PIFuHD model.

Run the following code to install all pip packages:

pip install -r requirements.txt 

Download Pre-trained model
--------------------------

Run the following script to download the pretrained model. The checkpoint is saved under `./checkpoints/`.

```
sh ./scripts/download_trained_model.sh
```

A Quick Testing
---------------

To process images under `./sample_images`, run the following code:

```
sh ./scripts/demo.sh
```

The resulting obj files and rendering will be saved in `./results`. You may use meshlab (http://www.meshlab.net/) to visualize the 3D mesh output (obj file).

Testing
-------

1.  run the following script to get joints for each image for testing (joints are used for image cropping only.). Make sure you correctly set the location of OpenPose binary. Alternatively colab demo provides more light-weight cropping rectange estimation without requiring openpose.

```
python apps/batch_openpose.py -d {openpose_root_path} -i {path_of_images} -o {path_of_images}
```

1.  run the following script to run reconstruction code. Make sure to set `--input_path` to `path_of_images`, `--out_path` to where you want to dump out results, and `--ckpt_path` to the checkpoint. Note that unlike PIFu, PIFuHD doesn't require segmentation mask as input. But if you observe severe artifacts, you may try removing background with off-the-shelf tools such as removebg. If you have `{image_name}_rect.txt` instead of `{image_name}_keypoints.json`, add `--use_rect` flag. For reference, you can take a look at colab demo.

```
python -m apps.simple_test
```

1.  optionally, you can also remove artifacts by keeping only the biggest connected component from the mesh reconstruction with the following script. (Warning: the script will overwrite the original obj files.)

```
python apps/clean_mesh.py -f {path_of_objs}
```

Visualization
-------------

To render results with turn-table, run the following code. The rendered animation (.mp4) will be stored under `{path_of_objs}`.

```
python -m apps.render_turntable -f {path_of_objs} -ww {rendering_width} -hh {rendering_height} 
# add -g for geometry rendering. default is normal visualization.
```

Citation
--------

```
@inproceedings{saito2020pifuhd,
  title={PIFuHD: Multi-Level Pixel-Aligned Implicit Function for High-Resolution 3D Human Digitization},
  author={Saito, Shunsuke and Simon, Tomas and Saragih, Jason and Joo, Hanbyul},
  booktitle={CVPR},
  year={2020}
}
```

Relevant Projects
-----------------

**Monocular Real-Time Volumetric Performance Capture (ECCV 2020)**  
_Ruilong Li\*, Yuliang Xiu\*, Shunsuke Saito, Zeng Huang, Kyle Olszewski, Hao Li_

The first real-time PIFu by accelerating reconstruction and rendering!!

**PIFu: Pixel-Aligned Implicit Function for High-Resolution Clothed Human Digitization (ICCV 2019)**  
_Shunsuke Saito\*, Zeng Huang\*, Ryota Natsume\*, Shigeo Morishima, Angjoo Kanazawa, Hao Li_

The original work of Pixel-Aligned Implicit Function for geometry and texture reconstruction, unifying sigle-view and multi-view methods.

**Learning to Infer Implicit Surfaces without 3d Supervision (NeurIPS 2019)**  
_Shichen Liu, Shunsuke Saito, Weikai Chen, Hao Li_

We answer to the question of "how can we learn implicit function if we don't have 3D ground truth?"

**SiCloPe: Silhouette-Based Clothed People (CVPR 2019, best paper finalist)**  
_Ryota Natsume\*, Shunsuke Saito\*, Zeng Huang, Weikai Chen, Chongyang Ma, Hao Li, Shigeo Morishima_

Our first attempt to reconstruct 3D clothed human body with texture from a single image!

Other Relevant Works
--------------------

**ARCH: Animatable Reconstruction of Clothed Humans (CVPR 2020)**  
_Zeng Huang, Yuanlu Xu, Christoph Lassner, Hao Li, Tony Tung_

Learning PIFu in canonical space for animatable avatar generation!

**Robust 3D Self-portraits in Seconds (CVPR 2020)**  
_Zhe Li, Tao Yu, Chuanyu Pan, Zerong Zheng, Yebin Liu_

They extend PIFu to RGBD + introduce "PIFusion" utilizing PIFu reconstruction for non-rigid fusion.

**Deep Volumetric Video from Very Sparse Multi-view Performance Capture (ECCV 2018)**  
_Zeng Huang, Tianye Li, Weikai Chen, Yajie Zhao, Jun Xing, Chloe LeGendre, Linjie Luo, Chongyang Ma, Hao Li_

Implict surface learning for sparse view human performance capture!

License
-------

CC-BY-NC 4.0. See the LICENSE file.
