---
project: ultralytics
stars: 48430
description: Ultralytics YOLO 🚀
url: https://github.com/ultralytics/ultralytics
---

中文 | 한국어 | 日本語 | Русский | Deutsch | Français | Español | Português | Türkçe | Tiếng Việt | العربية  

  

  

Ultralytics creates cutting-edge, state-of-the-art (SOTA) YOLO models built on years of foundational research in computer vision and AI. Constantly updated for performance and flexibility, our models are **fast**, **accurate**, and **easy to use**. They excel at object detection, tracking, instance segmentation, image classification, and pose estimation tasks.

Find detailed documentation in the Ultralytics Docs. Get support via GitHub Issues. Join discussions on Discord, Reddit, and the Ultralytics Community Forums!

Request an Enterprise License for commercial use at Ultralytics Licensing.

📄 Documentation
----------------

See below for quickstart installation and usage examples. For comprehensive guidance on training, validation, prediction, and deployment, refer to our full Ultralytics Docs.

Install

Install the `ultralytics` package, including all requirements, in a **Python>=3.8** environment with **PyTorch>=1.8**.

pip install ultralytics

For alternative installation methods, including Conda, Docker, and building from source via Git, please consult the Quickstart Guide.

Usage

### CLI

You can use Ultralytics YOLO directly from the Command Line Interface (CLI) with the `yolo` command:

# Predict using a pretrained YOLO model (e.g., YOLO11n) on an image
yolo predict model=yolo11n.pt source='https://ultralytics.com/images/bus.jpg'

The `yolo` command supports various tasks and modes, accepting additional arguments like `imgsz=640`. Explore the YOLO CLI Docs for more examples.

### Python

Ultralytics YOLO can also be integrated directly into your Python projects. It accepts the same configuration arguments as the CLI:

from ultralytics import YOLO

\# Load a pretrained YOLO11n model
model \= YOLO("yolo11n.pt")

\# Train the model on the COCO8 dataset for 100 epochs
train\_results \= model.train(
    data\="coco8.yaml",  \# Path to dataset configuration file
    epochs\=100,  \# Number of training epochs
    imgsz\=640,  \# Image size for training
    device\="cpu",  \# Device to run on (e.g., 'cpu', 0, \[0,1,2,3\])
)

\# Evaluate the model's performance on the validation set
metrics \= model.val()

\# Perform object detection on an image
results \= model("path/to/image.jpg")  \# Predict on an image
results\[0\].show()  \# Display results

\# Export the model to ONNX format for deployment
path \= model.export(format\="onnx")  \# Returns the path to the exported model

Discover more examples in the YOLO Python Docs.

✨ Models
--------

Ultralytics supports a wide range of YOLO models, from early versions like YOLOv3 to the latest YOLO11. The tables below showcase YOLO11 models pretrained on the COCO dataset for Detection, Segmentation, and Pose Estimation. Additionally, Classification models pretrained on the ImageNet dataset are available. Tracking mode is compatible with all Detection, Segmentation, and Pose models. All Models are automatically downloaded from the latest Ultralytics release upon first use.

  
  
Detection (COCO)

Explore the Detection Docs for usage examples. These models are trained on the COCO dataset, featuring 80 object classes.

Model

size  
(pixels)

mAPval  
50-95

Speed  
CPU ONNX  
(ms)

Speed  
T4 TensorRT10  
(ms)

params  
(M)

FLOPs  
(B)

YOLO11n

640

39.5

56.1 ± 0.8

1.5 ± 0.0

2.6

6.5

YOLO11s

640

47.0

90.0 ± 1.2

2.5 ± 0.0

9.4

21.5

YOLO11m

640

51.5

183.2 ± 2.0

4.7 ± 0.1

20.1

68.0

YOLO11l

640

53.4

238.6 ± 1.4

6.2 ± 0.1

25.3

86.9

YOLO11x

640

54.7

462.8 ± 6.7

11.3 ± 0.2

56.9

194.9

-   **mAPval** values refer to single-model single-scale performance on the COCO val2017 dataset. See YOLO Performance Metrics for details.  
    Reproduce with `yolo val detect data=coco.yaml device=0`
-   **Speed** metrics are averaged over COCO val images using an Amazon EC2 P4d instance. CPU speeds measured with ONNX export. GPU speeds measured with TensorRT export.  
    Reproduce with `yolo val detect data=coco.yaml batch=1 device=0|cpu`

Segmentation (COCO)

Refer to the Segmentation Docs for usage examples. These models are trained on COCO-Seg, including 80 classes.

Model

size  
(pixels)

mAPbox  
50-95

mAPmask  
50-95

Speed  
CPU ONNX  
(ms)

Speed  
T4 TensorRT10  
(ms)

params  
(M)

FLOPs  
(B)

YOLO11n-seg

640

38.9

32.0

65.9 ± 1.1

1.8 ± 0.0

2.9

9.7

YOLO11s-seg

640

46.6

37.8

117.6 ± 4.9

2.9 ± 0.0

10.1

33.0

YOLO11m-seg

640

51.5

41.5

281.6 ± 1.2

6.3 ± 0.1

22.4

113.2

YOLO11l-seg

640

53.4

42.9

344.2 ± 3.2

7.8 ± 0.2

27.6

132.2

YOLO11x-seg

640

54.7

43.8

664.5 ± 3.2

15.8 ± 0.7

62.1

296.4

-   **mAPval** values are for single-model single-scale on the COCO val2017 dataset. See YOLO Performance Metrics for details.  
    Reproduce with `yolo val segment data=coco.yaml device=0`
-   **Speed** metrics are averaged over COCO val images using an Amazon EC2 P4d instance. CPU speeds measured with ONNX export. GPU speeds measured with TensorRT export.  
    Reproduce with `yolo val segment data=coco.yaml batch=1 device=0|cpu`

Classification (ImageNet)

Consult the Classification Docs for usage examples. These models are trained on ImageNet, covering 1000 classes.

Model

size  
(pixels)

acc  
top1

acc  
top5

Speed  
CPU ONNX  
(ms)

Speed  
T4 TensorRT10  
(ms)

params  
(M)

FLOPs  
(B) at 224

YOLO11n-cls

224

70.0

89.4

5.0 ± 0.3

1.1 ± 0.0

2.8

0.5

YOLO11s-cls

224

75.4

92.7

7.9 ± 0.2

1.3 ± 0.0

6.7

1.6

YOLO11m-cls

224

77.3

93.9

17.2 ± 0.4

2.0 ± 0.0

11.6

4.9

YOLO11l-cls

224

78.3

94.3

23.2 ± 0.3

2.8 ± 0.0

14.1

6.2

YOLO11x-cls

224

79.5

94.9

41.4 ± 0.9

3.8 ± 0.0

29.6

13.6

-   **acc** values represent model accuracy on the ImageNet dataset validation set.  
    Reproduce with `yolo val classify data=path/to/ImageNet device=0`
-   **Speed** metrics are averaged over ImageNet val images using an Amazon EC2 P4d instance. CPU speeds measured with ONNX export. GPU speeds measured with TensorRT export.  
    Reproduce with `yolo val classify data=path/to/ImageNet batch=1 device=0|cpu`

Pose (COCO)

See the Pose Estimation Docs for usage examples. These models are trained on COCO-Pose, focusing on the 'person' class.

Model

size  
(pixels)

mAPpose  
50-95

mAPpose  
50

Speed  
CPU ONNX  
(ms)

Speed  
T4 TensorRT10  
(ms)

params  
(M)

FLOPs  
(B)

YOLO11n-pose

640

50.0

81.0

52.4 ± 0.5

1.7 ± 0.0

2.9

7.4

YOLO11s-pose

640

58.9

86.3

90.5 ± 0.6

2.6 ± 0.0

9.9

23.1

YOLO11m-pose

640

64.9

89.4

187.3 ± 0.8

4.9 ± 0.1

20.9

71.4

YOLO11l-pose

640

66.1

89.9

247.7 ± 1.1

6.4 ± 0.1

26.1

90.3

YOLO11x-pose

640

69.5

91.1

488.0 ± 13.9

12.1 ± 0.2

58.8

202.8

-   **mAPval** values are for single-model single-scale on the COCO Keypoints val2017 dataset. See YOLO Performance Metrics for details.  
    Reproduce with `yolo val pose data=coco-pose.yaml device=0`
-   **Speed** metrics are averaged over COCO val images using an Amazon EC2 P4d instance. CPU speeds measured with ONNX export. GPU speeds measured with TensorRT export.  
    Reproduce with `yolo val pose data=coco-pose.yaml batch=1 device=0|cpu`

Oriented Bounding Boxes (DOTAv1)

Check the OBB Docs for usage examples. These models are trained on DOTAv1, including 15 classes.

Model

size  
(pixels)

mAPtest  
50

Speed  
CPU ONNX  
(ms)

Speed  
T4 TensorRT10  
(ms)

params  
(M)

FLOPs  
(B)

YOLO11n-obb

1024

78.4

117.6 ± 0.8

4.4 ± 0.0

2.7

16.8

YOLO11s-obb

1024

79.5

219.4 ± 4.0

5.1 ± 0.0

9.7

57.1

YOLO11m-obb

1024

80.9

562.8 ± 2.9

10.1 ± 0.4

20.9

182.8

YOLO11l-obb

1024

81.0

712.5 ± 5.0

13.5 ± 0.6

26.1

231.2

YOLO11x-obb

1024

81.3

1408.6 ± 7.7

28.6 ± 1.0

58.8

519.1

-   **mAPtest** values are for single-model multiscale performance on the DOTAv1 test set.  
    Reproduce by `yolo val obb data=DOTAv1.yaml device=0 split=test` and submit merged results to the DOTA evaluation server.
-   **Speed** metrics are averaged over DOTAv1 val images using an Amazon EC2 P4d instance. CPU speeds measured with ONNX export. GPU speeds measured with TensorRT export.  
    Reproduce by `yolo val obb data=DOTAv1.yaml batch=1 device=0|cpu`

🧩 Integrations
---------------

Our key integrations with leading AI platforms extend the functionality of Ultralytics' offerings, enhancing tasks like dataset labeling, training, visualization, and model management. Discover how Ultralytics, in collaboration with partners like Weights & Biases, Comet ML, Roboflow, and Intel OpenVINO, can optimize your AI workflow. Explore more at Ultralytics Integrations.

  
  

Ultralytics HUB 🌟

Weights & Biases

Comet

Neural Magic

Streamline YOLO workflows: Label, train, and deploy effortlessly with Ultralytics HUB. Try now!

Track experiments, hyperparameters, and results with Weights & Biases.

Free forever, Comet ML lets you save YOLO models, resume training, and interactively visualize predictions.

Run YOLO inference up to 6x faster with Neural Magic DeepSparse.

🌟 Ultralytics HUB
------------------

Experience seamless AI with Ultralytics HUB, the all-in-one platform for data visualization, training YOLO models, and deployment—no coding required. Transform images into actionable insights and bring your AI visions to life effortlessly using our cutting-edge platform and user-friendly Ultralytics App. Start your journey for **Free** today!

🤝 Contribute
-------------

We thrive on community collaboration! Ultralytics YOLO wouldn't be the SOTA framework it is without contributions from developers like you. Please see our Contributing Guide to get started. We also welcome your feedback—share your experience by completing our Survey. A huge **Thank You** 🙏 to everyone who contributes!

We look forward to your contributions to help make the Ultralytics ecosystem even better!

📜 License
----------

Ultralytics offers two licensing options to suit different needs:

-   **AGPL-3.0 License**: This OSI-approved open-source license is perfect for students, researchers, and enthusiasts. It encourages open collaboration and knowledge sharing. See the LICENSE file for full details.
-   **Ultralytics Enterprise License**: Designed for commercial use, this license allows for the seamless integration of Ultralytics software and AI models into commercial products and services, bypassing the open-source requirements of AGPL-3.0. If your use case involves commercial deployment, please contact us via Ultralytics Licensing.

📞 Contact
----------

For bug reports and feature requests related to Ultralytics software, please visit GitHub Issues. For questions, discussions, and community support, join our active communities on Discord, Reddit, and the Ultralytics Community Forums. We're here to help with all things Ultralytics!
