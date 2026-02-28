---
project: ex_vision
stars: 63
description: null
url: https://github.com/software-mansion-labs/ex_vision
---

ExVision
========

ExVision is the collection of AI models related to vision delivered with ready to use package and easy to understand API. ExVision will take care of all necessary input transformations internally and return the result in the sensible format.

ExVision models are powered by Ortex.

Usage
-----

In order to use the model, you need to first load it

alias ExVision.Classification.MobileNetV3Small

model \= MobileNetV3Small.load() #=> %MobileNetV3{}

After that, the model is available for inference. ExVision will take care of all necessary input transformations and covert output to a format that makes sense.

MobileNetV3Small.run(model, "example/files/cat.jpg") #=> %{cat: 0.98, dog: 0.01, car: 0.00, ...}

ExVision is also capable of accepting tensors and images on input:

cat \= Image.open!("example/files/cat.jpg")
{:ok, cat\_tensor} \= Image.to\_nx(cat)
MobileNetV3Small.run(model, cat) #=> %{cat: 0.98, dog: 0.01, car: 0.00, ...}
MobileNetV3Small.run(model, cat\_tensor) #=> %{cat: 0.98, dog: 0.01, car: 0.00, ...}

### Usage in process workflow

All ExVision models are implemented using `Nx.Serving`. They are therefore compatible with process workflow.

You can start a model's process:

{:ok, pid} \= MobileNetV3Small.start\_link(name: MyModel)

or start it under the supervision tree

{:ok, \_supervisor\_pid} \= Supervisor.start\_link(\[
  {MobileNetV3Small, name: MyModel}
\], strategy: :one\_for\_one)

After starting, it's immediatelly available for inference using `batched_run/2` function.

MobileNetV3Small.batched\_run(MyModel, cat) #=> %{cat: 0.98, dog: 0.01, car: 0.00, ...}

Installation
------------

The package can be installed by adding `ex_vision` to your list of dependencies in `mix.exs`:

def deps do
  \[
    {:ex\_vision, "~> 0.4.0"}
  \]
end

In order to compile, ExVision **requires Rust and Cargo** to be installed on your system.

Current Timeline
----------------

We have identified a set of models that we would like to support. If the model that you would like to use is missing, feel free to open the issue, express interest in an existing one or contribute the model directly.

-   Classification
    -   MobileNetV3 Small
    -   EfficientNetV2
    -   SqueezeNet
-   Object detection
    -   SSDLite320 - MobileNetV3 Large backbone
    -   FasterRCNN ResNet50 FPN
-   Semantic segmentation
    -   DeepLabV3 - MobileNetV3
-   Instance segmentation
    -   Mask R-CNN
-   Keypoint Detection
    -   Keypoint R-CNN

Copyright and License
---------------------

Copyright 2024, Software Mansion

Licensed under the Apache License, Version 2.0
