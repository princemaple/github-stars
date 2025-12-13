---
project: PaddleOCR
stars: 66227
description: Turn any PDF or image document into structured data for your AI. A powerful, lightweight OCR toolkit that bridges the gap between images/PDFs and LLMs. Supports 100+ languages.
url: https://github.com/PaddlePaddle/PaddleOCR
---

English | 简体中文 | 繁體中文 | 日本語 | 한국어 | Français | Русский | Español | العربية

**PaddleOCR is an industry-leading, production-ready OCR and document AI engine, offering end-to-end solutions from text extraction to intelligent document understanding**

PaddleOCR
=========

Tip

PaddleOCR now provides an MCP server that supports integration with Agent applications like Claude Desktop. For details, please refer to PaddleOCR MCP Server.

The PaddleOCR 3.0 Technical Report is now available. See details at: PaddleOCR 3.0 Technical Report.

The PaddleOCR-VL Technical Report is now available. See details at PaddleOCR-VL Technical Report.

The Beta version of the PaddleOCR official website is now live, offering a more convenient online experience and large-scale PDF file parsing, as well as free API and MCP services. For more details, please visit the PaddleOCR official website.

**PaddleOCR** converts documents and images into **structured, AI-friendly data** (like JSON and Markdown) with **industry-leading accuracy**—powering AI applications for everyone from indie developers and startups to large enterprises worldwide. With over **60,000 stars** and deep integration into leading projects like **MinerU, RAGFlow, pathway and cherry-studio**, PaddleOCR has become the **premier solution** for developers building intelligent document applications in the **AI era**.

### PaddleOCR 3.0 Core Features

-   **PaddleOCR-VL - Multilingual Document Parsing via a 0.9B VLM**  
    **The SOTA and resource-efficient model tailored for document parsing**, that supports 109 languages and excels in recognizing complex elements (e.g., text, tables, formulas, and charts), while maintaining minimal resource consumption.
    
-   **PP-OCRv5 — Universal Scene Text Recognition**  
    **Single model supports five text types** (Simplified Chinese, Traditional Chinese, English, Japanese, and Pinyin) with **13% accuracy improvement**. Solves multilingual mixed document recognition challenges.
    
-   **PP-StructureV3 — Complex Document Parsing**  
    Intelligently converts complex PDFs and document images into **Markdown and JSON files that preserve original structure**. **Outperforms** numerous commercial solutions in public benchmarks. **Perfectly maintains document layout and hierarchical structure**.
    
-   **PP-ChatOCRv4 — Intelligent Information Extraction**  
    Natively integrates ERNIE 4.5 to **precisely extract key information** from massive documents, with 15% accuracy improvement over previous generation. Makes documents "**understand**" your questions and provide accurate answers.
    

In addition to providing an outstanding model library, PaddleOCR 3.0 also offers user-friendly tools covering model training, inference, and service deployment, so developers can rapidly bring AI applications to production.

**Special Note**: PaddleOCR 3.x introduces several significant interface changes. **Old code written based on PaddleOCR 2.x is likely incompatible with PaddleOCR 3.x**. Please ensure that the documentation you are reading matches the version of PaddleOCR you are using. This document explains the reasons for the upgrade and the major changes from PaddleOCR 2.x to 3.x.

📣 Recent updates
-----------------

### 🔥🔥 2025.10.16: PaddleOCR 3.3.0 released, includes:

-   Released PaddleOCR-VL:
    
    -   **Model Introduction**:
        
        -   **PaddleOCR-VL** is a SOTA and resource-efficient model tailored for document parsing. Its core component is PaddleOCR-VL-0.9B, a compact yet powerful vision-language model (VLM) that integrates a NaViT-style dynamic resolution visual encoder with the ERNIE-4.5-0.3B language model to enable accurate element recognition. **This innovative model efficiently supports 109 languages and excels in recognizing complex elements (e.g., text, tables, formulas, and charts), while maintaining minimal resource consumption**. Through comprehensive evaluations on widely used public benchmarks and in-house benchmarks, PaddleOCR-VL achieves SOTA performance in both page-level document parsing and element-level recognition. It significantly outperforms existing solutions, exhibits strong competitiveness against top-tier VLMs, and delivers fast inference speeds. These strengths make it highly suitable for practical deployment in real-world scenarios. The model has been released on HuggingFace. Everyone is welcome to download and use it! More introduction infomation can be found in PaddleOCR-VL.
    -   **Core Features**:
        
        -   **Compact yet Powerful VLM Architecture**: We present a novel vision-language model that is specifically designed for resource-efficient inference, achieving outstanding performance in element recognition. By integrating a NaViT-style dynamic high-resolution visual encoder with the lightweight ERNIE-4.5-0.3B language model, we significantly enhance the model’s recognition capabilities and decoding efficiency. This integration maintains high accuracy while reducing computational demands, making it well-suited for efficient and practical document processing applications.
        -   **SOTA Performance on Document Parsing**: PaddleOCR-VL achieves state-of-the-art performance in both page-level document parsing and element-level recognition. It significantly outperforms existing pipeline-based solutions and exhibiting strong competitiveness against leading vision-language models (VLMs) in document parsing. Moreover, it excels in recognizing complex document elements, such as text, tables, formulas, and charts, making it suitable for a wide range of challenging content types, including handwritten text and historical documents. This makes it highly versatile and suitable for a wide range of document types and scenarios.
        -   **Multilingual Support**: PaddleOCR-VL Supports 109 languages, covering major global languages, including but not limited to Chinese, English, Japanese, Latin, and Korean, as well as languages with different scripts and structures, such as Russian (Cyrillic script), Arabic, Hindi (Devanagari script), and Thai. This broad language coverage substantially enhances the applicability of our system to multilingual and globalized document processing scenarios.
-   Released PP-OCRv5 Multilingual Recognition Model:
    
    -   Improved the accuracy and coverage of Latin script recognition; added support for Cyrillic, Arabic, Devanagari, Telugu, Tamil, and other language systems, covering recognition of 109 languages. The model has only 2M parameters, and the accuracy of some models has increased by over 40% compared to the previous generation.

**2025.08.21: Release of PaddleOCR 3.2.0**

-   **Significant Model Additions:**
    
    -   Introduced training, inference, and deployment for PP-OCRv5 recognition models in English, Thai, and Greek. **The PP-OCRv5 English model delivers an 11% improvement in English scenarios compared to the main PP-OCRv5 model, with the Thai and Greek recognition models achieving accuracies of 82.68% and 89.28%, respectively.**
-   **Deployment Capability Upgrades:**
    
    -   **Full support for PaddlePaddle framework versions 3.1.0 and 3.1.1.**
    -   **Comprehensive upgrade of the PP-OCRv5 C++ local deployment solution, now supporting both Linux and Windows, with feature parity and identical accuracy to the Python implementation.**
    -   **High-performance inference now supports CUDA 12, and inference can be performed using either the Paddle Inference or ONNX Runtime backends.**
    -   **The high-stability service-oriented deployment solution is now fully open-sourced, allowing users to customize Docker images and SDKs as required.**
    -   The high-stability service-oriented deployment solution also supports invocation via manually constructed HTTP requests, enabling client-side code development in any programming language.
-   **Benchmark Support:**
    
    -   **All production lines now support fine-grained benchmarking, enabling measurement of end-to-end inference time as well as per-layer and per-module latency data to assist with performance analysis. Here's how to set up and use the benchmark feature.**
    -   **Documentation has been updated to include key metrics for commonly used configurations on mainstream hardware, such as inference latency and memory usage, providing deployment references for users.**
-   **Bug Fixes:**
    
    -   Resolved the issue of failed log saving during model training.
    -   Upgraded the data augmentation component for formula models for compatibility with newer versions of the albumentations dependency, and fixed deadlock warnings when using the tokenizers package in multi-process scenarios.
    -   Fixed inconsistencies in switch behaviors (e.g., `use_chart_parsing`) in the PP-StructureV3 configuration files compared to other pipelines.
-   **Other Enhancements:**
    
    -   **Separated core and optional dependencies. Only minimal core dependencies are required for basic text recognition; additional dependencies for document parsing and information extraction can be installed as needed.**
    -   **Enabled support for NVIDIA RTX 50 series graphics cards on Windows; users can refer to the installation guide for the corresponding PaddlePaddle framework versions.**
    -   **PP-OCR series models now support returning single-character coordinates.**
    -   Added AIStudio, ModelScope, and other model download sources, allowing users to specify the source for model downloads.
    -   Added support for chart-to-table conversion via the PP-Chart2Table module.
    -   Optimized documentation descriptions to improve usability.

**2025.08.15: PaddleOCR 3.1.1 Released**

-   **Bug Fixes:**
    
    -   Added the missing methods `save_vector`, `save_visual_info_list`, `load_vector`, and `load_visual_info_list` in the `PP-ChatOCRv4` class.
    -   Added the missing parameters `glossary` and `llm_request_interval` to the `translate` method in the `PPDocTranslation` class.
-   **Documentation Improvements:**
    
    -   Added a demo to the MCP documentation.
    -   Added information about the PaddlePaddle and PaddleOCR version used for performance metrics testing in the documentation.
    -   Fixed errors and omissions in the production line document translation.
-   **Others:**
    
    -   Changed the MCP server dependency to use the pure Python library `puremagic` instead of `python-magic` to reduce installation issues.
    -   Retested PP-OCRv5 performance metrics with PaddleOCR version 3.1.0 and updated the documentation.

**2025.06.29: PaddleOCR 3.1.0 Released**

-   **Key Models and Pipelines:**
    
    -   **Added PP-OCRv5 Multilingual Text Recognition Model**, which supports the training and inference process for text recognition models in 37 languages, including French, Spanish, Portuguese, Russian, Korean, etc. **Average accuracy improved by over 30%.** Details
    -   Upgraded the **PP-Chart2Table model** in PP-StructureV3, further enhancing the capability of converting charts to tables. On internal custom evaluation sets, the metric (RMS-F1) **increased by 9.36 percentage points (71.24% -> 80.60%).**
    -   Newly launched **document translation pipeline, PP-DocTranslation, based on PP-StructureV3 and ERNIE 4.5**, which supports the translation of Markdown format documents, various complex-layout PDF documents, and document images, with the results saved as Markdown format documents. Details
-   **New MCP server:** Details
    
    -   **Supports both OCR and PP-StructureV3 pipelines.**
    -   Supports three working modes: local Python library, AIStudio Community Cloud Service, and self-hosted service.
    -   Supports invoking local services via stdio and remote services via Streamable HTTP.
-   **Documentation Optimization:** Improved the descriptions in some user guides for a smoother reading experience.
    

**2025.06.26: PaddleOCR 3.0.3 Released** - Bug Fix: Resolved the issue where the \`enable\_mkldnn\` parameter was not effective, restoring the default behavior of using MKL-DNN for CPU inference. **2025.06.19: PaddleOCR 3.0.2 Released** - \*\*New Features:\*\*

-   The default download source has been changed from `BOS` to `HuggingFace`. Users can also change the environment variable `PADDLE_PDX_MODEL_SOURCE` to `BOS` to set the model download source back to Baidu Object Storage (BOS).
    
-   Added service invocation examples for six languages—C++, Java, Go, C#, Node.js, and PHP—for pipelines like PP-OCRv5, PP-StructureV3, and PP-ChatOCRv4.
    
-   Improved the layout partition sorting algorithm in the PP-StructureV3 pipeline, enhancing the sorting logic for complex vertical layouts to deliver better results.
    
-   Enhanced model selection logic: when a language is specified but a model version is not, the system will automatically select the latest model version supporting that language.
    
-   Set a default upper limit for MKL-DNN cache size to prevent unlimited growth, while also allowing users to configure cache capacity.
    
-   Updated default configurations for high-performance inference to support Paddle MKL-DNN acceleration and optimized the logic for automatic configuration selection for smarter choices.
    
-   Adjusted the logic for obtaining the default device to consider the actual support for computing devices by the installed Paddle framework, making program behavior more intuitive.
    
-   Added Android example for PP-OCRv5. Details.
    
-   **Bug Fixes:**
    
    -   Fixed an issue with some CLI parameters in PP-StructureV3 not taking effect.
    -   Resolved an issue where `export_paddlex_config_to_yaml` would not function correctly in certain cases.
    -   Corrected the discrepancy between the actual behavior of `save_path` and its documentation description.
    -   Fixed potential multithreading errors when using MKL-DNN in basic service deployment.
    -   Corrected channel order errors in image preprocessing for the Latex-OCR model.
    -   Fixed channel order errors in saving visualized images within the text recognition module.
    -   Resolved channel order errors in visualized table results within PP-StructureV3 pipeline.
    -   Fixed an overflow issue in the calculation of `overlap_ratio` under extremely special circumstances in the PP-StructureV3 pipeline.
-   **Documentation Improvements:**
    
    -   Updated the description of the `enable_mkldnn` parameter in the documentation to accurately reflect the program's actual behavior.
    -   Fixed errors in the documentation regarding the `lang` and `ocr_version` parameters.
    -   Added instructions for exporting pipeline configuration files via CLI.
    -   Fixed missing columns in the performance data table for PP-OCRv5.
    -   Refined benchmark metrics for PP-StructureV3 across different configurations.
-   **Others:**
    
    -   Relaxed version restrictions on dependencies like numpy and pandas, restoring support for Python 3.12.

**History Log**

2025.06.05: **PaddleOCR 3.0.1 Released**, includes:

-   **Optimisation of certain models and model configurations:**
    -   Updated the default model configuration for PP-OCRv5, changing both detection and recognition from mobile to server models. To improve default performance in most scenarios, the parameter `limit_side_len` in the configuration has been changed from 736 to 64.
    -   Added a new text line orientation classification model `PP-LCNet_x1_0_textline_ori` with an accuracy of 99.42%. The default text line orientation classifier for OCR, PP-StructureV3, and PP-ChatOCRv4 pipelines has been updated to this model.
    -   Optimized the text line orientation classification model `PP-LCNet_x0_25_textline_ori`, improving accuracy by 3.3 percentage points to a current accuracy of 98.85%.
-   **Optimizations and fixes for some issues in version 3.0.0, details**

🔥🔥2025.05.20: Official Release of **PaddleOCR v3.0**, including:

-   **PP-OCRv5**: High-Accuracy Text Recognition Model for All Scenarios - Instant Text from Images/PDFs.
    
    1.  🌐 Single-model support for **five** text types - Seamlessly process **Simplified Chinese, Traditional Chinese, Simplified Chinese Pinyin, English** and **Japanese** within a single model.
    2.  ✍️ Improved **handwriting recognition**: Significantly better at complex cursive scripts and non-standard handwriting.
    3.  🎯 **13-point accuracy gain** over PP-OCRv4, achieving state-of-the-art performance across a variety of real-world scenarios.
-   **PP-StructureV3**: General-Purpose Document Parsing – Unleash SOTA Images/PDFs Parsing for Real-World Scenarios!
    
    1.  🧮 **High-Accuracy multi-scene PDF parsing**, leading both open- and closed-source solutions on the OmniDocBench benchmark.
    2.  🧠 Specialized capabilities include **seal recognition**, **chart-to-table conversion**, **table recognition with nested formulas/images**, **vertical text document parsing**, and **complex table structure analysis**.
-   **PP-ChatOCRv4**: Intelligent Document Understanding – Extract Key Information, not just text from Images/PDFs.
    
    1.  🔥 **15-point accuracy gain** in key-information extraction on PDF/PNG/JPG files over the previous generation.
    2.  💻 Native support for **ERNIE 4.5**, with compatibility for large-model deployments via PaddleNLP, Ollama, vLLM, and more.
    3.  🤝 Integrated PP-DocBee2, enabling extraction and understanding of printed text, handwriting, seals, tables, charts, and other common elements in complex documents.

History Log

⚡ Quick Start
-------------

### 1\. Run online demo

### 2\. Installation

Install PaddlePaddle refer to Installation Guide, after then, install the PaddleOCR toolkit.

# If you only want to use the basic text recognition feature (returns text position coordinates and content), including the PP-OCR series
python -m pip install paddleocr
# If you want to use all features such as document parsing, document understanding, document translation, key information extraction, etc.
# python -m pip install "paddleocr\[all\]"

Starting from version 3.2.0, in addition to the `all` dependency group demonstrated above, PaddleOCR also supports installing partial optional features by specifying other dependency groups. All dependency groups provided by PaddleOCR are as follows:

Dependency Group Name

Corresponding Functionality

`doc-parser`

Document parsing: can be used to extract layout elements such as tables, formulas, stamps, images, etc. from documents; includes models like PP-StructureV3, PaddleOCR-VL

`ie`

Information extraction: can be used to extract key information from documents, such as names, dates, addresses, amounts, etc.; includes models like PP-ChatOCRv4

`trans`

Document translation: can be used to translate documents from one language to another; includes models like PP-DocTranslation

`all`

Complete functionality

### 3\. Run inference by CLI

# Run PP-OCRv5 inference
paddleocr ocr -i https://paddle-model-ecology.bj.bcebos.com/paddlex/imgs/demo\_image/general\_ocr\_002.png --use\_doc\_orientation\_classify False --use\_doc\_unwarping False --use\_textline\_orientation False  

# Run PP-StructureV3 inference
paddleocr pp\_structurev3 -i https://paddle-model-ecology.bj.bcebos.com/paddlex/imgs/demo\_image/pp\_structure\_v3\_demo.png --use\_doc\_orientation\_classify False --use\_doc\_unwarping False

# Get the Qianfan API Key at first, and then run PP-ChatOCRv4 inference
paddleocr pp\_chatocrv4\_doc -i https://paddle-model-ecology.bj.bcebos.com/paddlex/imgs/demo\_image/vehicle\_certificate-1.png -k 驾驶室准乘人数 --qianfan\_api\_key your\_api\_key --use\_doc\_orientation\_classify False --use\_doc\_unwarping False 

# Run PaddleOCR-VL inference
paddleocr doc\_parser -i https://paddle-model-ecology.bj.bcebos.com/paddlex/imgs/demo\_image/paddleocr\_vl\_demo.png

# Get more information about "paddleocr ocr"
paddleocr ocr --help

### 4\. Run inference by API

**4.1 PP-OCRv5 Example**

\# Initialize PaddleOCR instance
from paddleocr import PaddleOCR
ocr \= PaddleOCR(
    use\_doc\_orientation\_classify\=False,
    use\_doc\_unwarping\=False,
    use\_textline\_orientation\=False)

\# Run OCR inference on a sample image 
result \= ocr.predict(
    input\="https://paddle-model-ecology.bj.bcebos.com/paddlex/imgs/demo\_image/general\_ocr\_002.png")

\# Visualize the results and save the JSON results
for res in result:
    res.print()
    res.save\_to\_img("output")
    res.save\_to\_json("output")

**4.2 PP-StructureV3 Example**

from pathlib import Path
from paddleocr import PPStructureV3

pipeline \= PPStructureV3(
    use\_doc\_orientation\_classify\=False,
    use\_doc\_unwarping\=False
)

\# For Image
output \= pipeline.predict(
    input\="https://paddle-model-ecology.bj.bcebos.com/paddlex/imgs/demo\_image/pp\_structure\_v3\_demo.png",
)

\# Visualize the results and save the JSON results
for res in output:
    res.print() 
    res.save\_to\_json(save\_path\="output") 
    res.save\_to\_markdown(save\_path\="output")           **4.3 PP-ChatOCRv4 Example**

from paddleocr import PPChatOCRv4Doc

chat\_bot\_config \= {
    "module\_name": "chat\_bot",
    "model\_name": "ernie-3.5-8k",
    "base\_url": "https://qianfan.baidubce.com/v2",
    "api\_type": "openai",
    "api\_key": "api\_key",  \# your api\_key
}

retriever\_config \= {
    "module\_name": "retriever",
    "model\_name": "embedding-v1",
    "base\_url": "https://qianfan.baidubce.com/v2",
    "api\_type": "qianfan",
    "api\_key": "api\_key",  \# your api\_key
}

pipeline \= PPChatOCRv4Doc(
    use\_doc\_orientation\_classify\=False,
    use\_doc\_unwarping\=False
)

visual\_predict\_res \= pipeline.visual\_predict(
    input\="https://paddle-model-ecology.bj.bcebos.com/paddlex/imgs/demo\_image/vehicle\_certificate-1.png",
    use\_common\_ocr\=True,
    use\_seal\_recognition\=True,
    use\_table\_recognition\=True,
)

mllm\_predict\_info \= None
use\_mllm \= False
\# If a multimodal large model is used, the local mllm service needs to be started. You can refer to the documentation: https://github.com/PaddlePaddle/PaddleX/blob/release/3.0/docs/pipeline\_usage/tutorials/vlm\_pipelines/doc\_understanding.en.md performs deployment and updates the mllm\_chat\_bot\_config configuration.
if use\_mllm:
    mllm\_chat\_bot\_config \= {
        "module\_name": "chat\_bot",
        "model\_name": "PP-DocBee",
        "base\_url": "http://127.0.0.1:8080/",  \# your local mllm service url
        "api\_type": "openai",
        "api\_key": "api\_key",  \# your api\_key
    }

    mllm\_predict\_res \= pipeline.mllm\_pred(
        input\="https://paddle-model-ecology.bj.bcebos.com/paddlex/imgs/demo\_image/vehicle\_certificate-1.png",
        key\_list\=\["驾驶室准乘人数"\],
        mllm\_chat\_bot\_config\=mllm\_chat\_bot\_config,
    )
    mllm\_predict\_info \= mllm\_predict\_res\["mllm\_res"\]

visual\_info\_list \= \[\]
for res in visual\_predict\_res:
    visual\_info\_list.append(res\["visual\_info"\])
    layout\_parsing\_result \= res\["layout\_parsing\_result"\]

vector\_info \= pipeline.build\_vector(
    visual\_info\_list, flag\_save\_bytes\_vector\=True, retriever\_config\=retriever\_config
)
chat\_result \= pipeline.chat(
    key\_list\=\["驾驶室准乘人数"\],
    visual\_info\=visual\_info\_list,
    vector\_info\=vector\_info,
    mllm\_predict\_info\=mllm\_predict\_info,
    chat\_bot\_config\=chat\_bot\_config,
    retriever\_config\=retriever\_config,
)
print(chat\_result)

**4.4 PaddleOCR-VL Example**

from paddleocr import PaddleOCRVL

pipeline \= PaddleOCRVL()
output \= pipeline.predict("https://paddle-model-ecology.bj.bcebos.com/paddlex/imgs/demo\_image/paddleocr\_vl\_demo.png")
for res in output:
    res.print()
    res.save\_to\_json(save\_path\="output")
    res.save\_to\_markdown(save\_path\="output")

### 5\. Chinese Heterogeneous AI Accelerators

-   Huawei Ascend
-   KUNLUNXIN

🧩 More Features
----------------

-   Convert models to ONNX format: Obtaining ONNX Models.
-   Accelerate inference using engines like OpenVINO, ONNX Runtime, TensorRT, or perform inference using ONNX format models: High-Performance Inference.
-   Accelerate inference using multi-GPU and multi-process: Parallel Inference for Pipelines.
-   Integrate PaddleOCR into applications written in C++, C#, Java, etc.: Serving.

⛰️ Advanced Tutorials
---------------------

-   PP-OCRv5 Tutorial
-   PP-StructureV3 Tutorial
-   PP-ChatOCRv4 Tutorial
-   PaddleOCR-VL Tutorial

🔄 Quick Overview of Execution Results
--------------------------------------

### PP-OCRv5

### PP-StructureV3

### PaddleOCR-VL

✨ Stay Tuned
------------

⭐ **Star this repository to keep up with exciting updates and new releases, including powerful OCR and document parsing capabilities!** ⭐

👩‍👩‍👧‍👦 Community
---------------------

PaddlePaddle WeChat official account

Join the tech discussion group

😃 Awesome Projects Leveraging PaddleOCR
----------------------------------------

PaddleOCR wouldn't be where it is today without its incredible community! 💗 A massive thank you to all our longtime partners, new collaborators, and everyone who's poured their passion into PaddleOCR — whether we've named you or not. Your support fuels our fire!

Project Name

Description

RAGFlow

RAG engine based on deep document understanding.

pathway

Python ETL framework for stream processing, real-time analytics, LLM pipelines, and RAG.

MinerU

Multi-type Document to Markdown Conversion Tool

Umi-OCR

Free, Open-source, Batch Offline OCR Software.

cherry-studio

A desktop client that supports for multiple LLM providers.

OmniParser

OmniParser: Screen Parsing tool for Pure Vision Based GUI Agent.

QAnything

Question and Answer based on Anything.

PDF-Extract-Kit

A powerful open-source toolkit designed to efficiently extract high-quality content from complex and diverse PDF documents.

Dango-Translator

Recognize text on the screen, translate it and show the translation results in real time.

Learn more projects

More projects based on PaddleOCR

👩‍👩‍👧‍👦 Contributors
------------------------

🌟 Star
-------

📄 License
----------

This project is released under the Apache 2.0 license.

🎓 Citation
-----------

@misc{cui2025paddleocr30technicalreport,
      title\={PaddleOCR 3.0 Technical Report}, 
      author\={Cheng Cui and Ting Sun and Manhui Lin and Tingquan Gao and Yubo Zhang and Jiaxuan Liu and Xueqing Wang and Zelun Zhang and Changda Zhou and Hongen Liu and Yue Zhang and Wenyu Lv and Kui Huang and Yichao Zhang and Jing Zhang and Jun Zhang and Yi Liu and Dianhai Yu and Yanjun Ma},
      year\={2025},
      eprint\={2507.05595},
      archivePrefix\={arXiv},
      primaryClass\={cs.CV},
      url\={https://arxiv.org/abs/2507.05595}, 
}

@misc{cui2025paddleocrvlboostingmultilingualdocument,
      title\={PaddleOCR-VL: Boosting Multilingual Document Parsing via a 0.9B Ultra-Compact Vision-Language Model}, 
      author\={Cheng Cui and Ting Sun and Suyin Liang and Tingquan Gao and Zelun Zhang and Jiaxuan Liu and Xueqing Wang and Changda Zhou and Hongen Liu and Manhui Lin and Yue Zhang and Yubo Zhang and Handong Zheng and Jing Zhang and Jun Zhang and Yi Liu and Dianhai Yu and Yanjun Ma},
      year\={2025},
      eprint\={2510.14528},
      archivePrefix\={arXiv},
      primaryClass\={cs.CV},
      url\={https://arxiv.org/abs/2510.14528}, 
}
