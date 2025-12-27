---
project: flair
stars: 14338
description: A very simple framework for state-of-the-art Natural Language Processing (NLP)
url: https://github.com/flairNLP/flair
---

A very simple framework for **state-of-the-art NLP**. Developed by Humboldt University of Berlin and friends.

* * *

Flair is:

-   **A powerful NLP library.** Flair allows you to apply our state-of-the-art natural language processing (NLP) models to your text, such as named entity recognition (NER), sentiment analysis, part-of-speech tagging (PoS), special support for biomedical texts, sense disambiguation and classification, with support for a rapidly growing number of languages.
    
-   **A text embedding library.** Flair has simple interfaces that allow you to use and combine different word and document embeddings, including our proposed Flair embeddings and various transformers.
    
-   **A PyTorch NLP framework.** Our framework builds directly on PyTorch, making it easy to train your own models and experiment with new approaches using Flair embeddings and classes.
    

Now at version 0.15.1!

State-of-the-Art Models
-----------------------

Flair ships with state-of-the-art models for a range of NLP tasks. For instance, check out our latest NER models:

Language

Dataset

Flair

Best published

Model card & demo

English

Conll-03 (4-class)

**94.09**

_94.3 (Yamada et al., 2020)_

Flair English 4-class NER demo

English

Ontonotes (18-class)

**90.93**

_91.3 (Yu et al., 2020)_

Flair English 18-class NER demo

German

Conll-03 (4-class)

**92.31**

_90.3 (Yu et al., 2020)_

Flair German 4-class NER demo

Dutch

Conll-03 (4-class)

**95.25**

_93.7 (Yu et al., 2020)_

Flair Dutch 4-class NER demo

Spanish

Conll-03 (4-class)

**90.54**

_90.3 (Yu et al., 2020)_

Flair Spanish 4-class NER demo

Many Flair sequence tagging models (named entity recognition, part-of-speech tagging etc.) are also hosted on the **🤗 Hugging Face model hub**! You can browse models, check detailed information on how they were trained, and even try each model out online!

Quick Start
-----------

### Requirements and Installation

In your favorite virtual environment, simply do:

```
pip install flair
```

Flair requires Python 3.9+.

### Example 1: Tag Entities in Text

Let's run **named entity recognition** (NER) over an example sentence. All you need to do is make a `Sentence`, load a pre-trained model and use it to predict tags for the sentence:

from flair.data import Sentence
from flair.nn import Classifier

\# make a sentence
sentence \= Sentence('I love Berlin .')

\# load the NER tagger
tagger \= Classifier.load('ner')

\# run NER over sentence
tagger.predict(sentence)

\# print the sentence with all annotations
print(sentence)

This should print:

Sentence: "I love Berlin ." → \["Berlin"/LOC\]

This means that "Berlin" was tagged as a **location entity** in this sentence.

-   _to learn more about NER tagging in Flair, check out our NER tutorial!_

### Example 2: Detect Sentiment

Let's run **sentiment analysis** over an example sentence to determine whether it is POSITIVE or NEGATIVE. Same code as above, just a different model:

from flair.data import Sentence
from flair.nn import Classifier

\# make a sentence
sentence \= Sentence('I love Berlin .')

\# load the NER tagger
tagger \= Classifier.load('sentiment')

\# run NER over sentence
tagger.predict(sentence)

\# print the sentence with all annotations
print(sentence)

This should print:

Sentence\[4\]: "I love Berlin ." → POSITIVE (0.9983)

This means that the sentence "I love Berlin" was tagged as having **POSITIVE** sentiment.

-   _to learn more about sentiment analysis in Flair, check out our sentiment analysis tutorial!_

Tutorials
---------

On our new 🔥 **Flair documentation page** you will find many tutorials to get you started!

In particular:

-   Tutorial 1: Basic tagging → how to tag your text
-   Tutorial 2: Training models → how to train your own state-of-the-art NLP models
-   Tutorial 3: Embeddings → how to produce embeddings for words and documents
-   Tutorial 4: Biomedical text → how to analyse biomedical text data

There is also a dedicated landing page for our biomedical NER and datasets with installation instructions and tutorials.

More Documentation
------------------

Another great place to start is the book Natural Language Processing with Flair and its accompanying code repository, though it was written for an older version of Flair and some examples may no longer work.

There are also good third-party articles and posts that illustrate how to use Flair:

-   Training an NER model with Flair
-   Training a text classifier with Flair
-   Zero and few-shot learning
-   Visualisation tool for highlighting the extracted entities
-   Flair functionality and how to use in Colab
-   Benchmarking NER algorithms
-   Clinical NLP
-   How to build a microservice with Flair and Flask
-   A docker image for Flair
-   Practical approach of State-of-the-Art Flair in Named Entity Recognition
-   Training a Flair text classifier on Google Cloud Platform (GCP) and serving predictions on GCP
-   Model Interpretability for transformer-based Flair models

Citing Flair
------------

Please cite the following paper when using Flair embeddings:

```
@inproceedings{akbik2018coling,
  title={Contextual String Embeddings for Sequence Labeling},
  author={Akbik, Alan and Blythe, Duncan and Vollgraf, Roland},
  booktitle = {{COLING} 2018, 27th International Conference on Computational Linguistics},
  pages     = {1638--1649},
  year      = {2018}
}
```

If you use the Flair framework for your experiments, please cite this paper:

```
@inproceedings{akbik2019flair,
  title={{FLAIR}: An easy-to-use framework for state-of-the-art {NLP}},
  author={Akbik, Alan and Bergmann, Tanja and Blythe, Duncan and Rasul, Kashif and Schweter, Stefan and Vollgraf, Roland},
  booktitle={{NAACL} 2019, 2019 Annual Conference of the North American Chapter of the Association for Computational Linguistics (Demonstrations)},
  pages={54--59},
  year={2019}
}
```

If you use our new "FLERT" models or approach, please cite this paper:

```
@misc{schweter2020flert,
    title={{FLERT}: Document-Level Features for Named Entity Recognition},
    author={Stefan Schweter and Alan Akbik},
    year={2020},
    eprint={2011.06993},
    archivePrefix={arXiv},
    primaryClass={cs.CL}
}
```

If you use our TARS approach for few-shot and zero-shot learning, please cite this paper:

```
@inproceedings{halder2020coling,
  title={Task Aware Representation of Sentences for Generic Text Classification},
  author={Halder, Kishaloy and Akbik, Alan and Krapac, Josip and Vollgraf, Roland},
  booktitle = {{COLING} 2020, 28th International Conference on Computational Linguistics},
  year      = {2020}
}
```

Contact
-------

Please email your questions or comments to Alan Akbik.

Contributing
------------

Thanks for your interest in contributing! There are many ways to get involved; start with our contributor guidelines and then check these open issues for specific tasks.

License
-------

The MIT License (MIT)

Flair is licensed under the following MIT license: The MIT License (MIT) Copyright © 2018 Zalando SE, https://tech.zalando.com

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
