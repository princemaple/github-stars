---
project: texthero
stars: 2916
description: Text preprocessing, representation and visualization from zero to hero.
url: https://github.com/jbesomi/texthero
---

Text preprocessing, representation and visualization from zero to hero.

From zero to hero • Installation • Getting Started • Examples • API • FAQ • Contributions

From zero to hero
-----------------

Texthero is a python toolkit to work with text-based dataset quickly and effortlessly. Texthero is very simple to learn and designed to be used on top of Pandas. Texthero has the same expressiveness and power of Pandas and is extensively documented. Texthero is modern and conceived for programmers of the 2020 decade with little knowledge if any in linguistic.

You can think of Texthero as a tool to help you _understand_ and work with text-based dataset. Given a tabular dataset, it's easy to _grasp the main concept_. Instead, given a text dataset, it's harder to have quick insights into the underline data. With Texthero, preprocessing text data, mapping it into vectors, and visualizing the obtained vector space takes just a couple of lines.

Texthero include tools for:

-   Preprocess text data: it offers both out-of-the-box solutions but it's also flexible for custom-solutions.
-   Natural Language Processing: keyphrases and keywords extraction, and named entity recognition.
-   Text representation: TF-IDF, term frequency, and custom word-embeddings (wip)
-   Vector space analysis: clustering (K-means, Meanshift, DBSCAN and Hierarchical), topic modeling (wip) and interpretation.
-   Text visualization: vector space visualization, place localization on maps (wip).

Texthero is free, open-source and well documented (and that's what we love most by the way!).

We hope you will find pleasure working with Texthero as we had during his development.

Hablas español? क्या आप हिंदी बोलते हैं? 日本語が話せるのか？
---------------------------------------------------

Texthero has been developed for the whole NLP community. We know how hard it is to deal with different NLP tools (NLTK, SpaCy, Gensim, TextBlob, Sklearn): that's why we developed Texthero, to simplify things.

Now, the next main milestone is to provide _multilingual support_ and for this big step, we need the help of all of you. ¿Hablas español? Sie sprechen Deutsch? 你会说中文？ 日本語が話せるのか？ Fala português? Parli Italiano? Вы говорите по-русски? If yes or you speak another language not mentioned here, then you might help us develop multilingual support! Even if you haven't contributed before or you just started with NLP, contact us or open a Github issue, there is always a first time :) We promise you will learn a lot, and, ... who knows? It might help you find your new job as an NLP-developer!

For improving the python toolkit and provide an even better experience, your aid and feedback are crucial. If you have any problem or suggestion please open a Github issue, we will be glad to support you and help you.

Beta version
------------

Texthero's community is growing fast. Texthero though is still in a beta version; soon, a faster and better version will be released and it will bring some major changes.

For instance, to give a more granular control over the pipeline, starting from the next version on, all `preprocessing` functions will require as argument an already tokenized text. This will be a major change.

Once released the stable version (Texthero 2.0), backward compatibility will be respected. Until this point, backward compatibility will be present but it will be weaker.

If you want to be part of this fast-growing movements, do not hesitate to contribute: CONTRIBUTING!

Installation
------------

Install texthero via `pip`:

pip install texthero

> ☝️Under the hoods, Texthero makes use of multiple NLP and machine learning toolkits such as Gensim, NLTK, SpaCy and scikit-learn. You don't need to install them all separately, pip will take care of that.

> For faster performance, make sure you have installed Spacy version >= 2.2. Also, make sure you have a recent version of python, the higher, the best.

Getting started
---------------

The best way to learn Texthero is through the Getting Started docs.

In case you are an advanced python user, then `help(texthero)` should do the work.

Examples
--------

### 1\. Text cleaning, TF-IDF representation and Visualization

import texthero as hero
import pandas as pd

df \= pd.read\_csv(
   "https://github.com/jbesomi/texthero/raw/master/dataset/bbcsport.csv"
)

df\['pca'\] \= (
   df\['text'\]
   .pipe(hero.clean)
   .pipe(hero.tfidf)
   .pipe(hero.pca)
)
hero.scatterplot(df, 'pca', color\='topic', title\="PCA BBC Sport news")

### 2\. Text preprocessing, TF-IDF, K-means and Visualization

import texthero as hero
import pandas as pd

df \= pd.read\_csv(
    "https://github.com/jbesomi/texthero/raw/master/dataset/bbcsport.csv"
)

df\['tfidf'\] \= (
    df\['text'\]
    .pipe(hero.clean)
    .pipe(hero.tfidf)
)

df\['kmeans\_labels'\] \= (
    df\['tfidf'\]
    .pipe(hero.kmeans, n\_clusters\=5)
    .astype(str)
)

df\['pca'\] \= df\['tfidf'\].pipe(hero.pca)

hero.scatterplot(df, 'pca', color\='kmeans\_labels', title\="K-means BBC Sport news")

### 3\. Simple pipeline for text cleaning

\>\>> import texthero as hero
\>\>> import pandas as pd
\>\>> text \= "This sèntencé    (123 /) needs to \[OK!\] be cleaned!   "
\>\>> s \= pd.Series(text)
\>\>> s
0    This sèntencé    (123 /) needs to \[OK!\] be cleane...
dtype: object

Remove all digits:

\>\>> s \= hero.remove\_digits(s)
\>\>> s
0    This sèntencé    (  /) needs to \[OK!\] be cleaned!
dtype: object

> Remove digits replaces only blocks of digits. The digits in the string "hello123" will not be removed. If we want to remove all digits, you need to set only\_blocks to false.

Remove all types of brackets and their content.

\>\>> s \= hero.remove\_brackets(s)
\>\>> s 
0    This sèntencé    needs to  be cleaned!
dtype: object

Remove diacritics.

\>\>> s \= hero.remove\_diacritics(s)
\>\>> s 
0    This sentence    needs to  be cleaned!
dtype: object

Remove punctuation.

\>\>> s \= hero.remove\_punctuation(s)
\>\>> s 
0    This sentence    needs to  be cleaned
dtype: object

Remove extra white-spaces.

\>\>> s \= hero.remove\_whitespace(s)
\>\>> s 
0    This sentence needs to be cleaned
dtype: object

Sometimes we also want to get rid of stop-words.

\>\>> s \= hero.remove\_stopwords(s)
\>\>> s
0    This sentence needs cleaned
dtype: object

API
---

Texthero is composed of four modules: preprocessing.py, nlp.py, representation.py and visualization.py.

### 1\. Preprocessing

**Scope:** prepare **text** data for further analysis.

Full documentation: preprocessing

### 2\. NLP

**Scope:** provide classic natural language processing tools such as `named_entity` and `noun_phrases`.

Full documentation: nlp

### 2\. Representation

**Scope:** map text data into vectors and do dimensionality reduction.

Supported **representation** algorithms:

1.  Term frequency (`count`)
2.  Term frequency-inverse document frequency (`tfidf`)

Supported **clustering** algorithms:

1.  K-means (`kmeans`)
2.  Density-Based Spatial Clustering of Applications with Noise (`dbscan`)
3.  Meanshift (`meanshift`)

Supported **dimensionality reduction** algorithms:

1.  Principal component analysis (`pca`)
2.  t-distributed stochastic neighbor embedding (`tsne`)
3.  Non-negative matrix factorization (`nmf`)

Full documentation: representation

### 3\. Visualization

**Scope:** summarize the main facts regarding the text data and visualize it. This module is opinionable. It's handy for anyone that needs a quick solution to visualize on screen the text data, for instance during a text exploratory data analysis (EDA).

Supported functions:

-   Text scatterplot (`scatterplot`)
-   Most common words (`top_words`)

Full documentation: visualization

FAQ
---

##### Why Texthero

Sometimes we just want things done, right? Texthero helps with that. It helps make things easier and give the developer more time to focus on his custom requirements. We believe that cleaning text should just take a minute. Same for finding the most important part of a text and the same for representing it.

In a very pragmatic way, texthero has just one goal: make the developer spare time. Working with text data can be a pain and in most cases, a default pipeline can be quite good to start. There is always time to come back and improve previous work.

Contributions
-------------

> "Texthero has been developed by a member of the NLP community for the whole NLP-community"

Texthero is for all of us NLP-developers and it can continue to exist with the precious contribution of the community.

Your level of expertise of python and NLP does not matter, anyone can help and anyone is more than welcome to contribute!

**Are you an NLP expert?**

-   open an issue and tell us what you like and dislike of Texthero and what we can do better!

**Are you good at creating websites?**

The website will be soon moved from Docusaurus to Sphinx: read the open issue there. Good news: the website will look like now :) Average news: we need to do some web-development to adapt this Sphinx template to our needs. Can you help us?

**Are you good at writing?**

Probably this is the most important piece missing now on Texthero: more tutorials and more "Getting Started" guide.

If you are good at writing you can help us! Why don't you start by Adding a FAQ page to the website or explain how to create a custom pipeline? Need help? We are there for you.

**Are you good in python?**

There are a lot of open issues for techie guys. Which one do you choose?

If you have just other questions or inquiry drop me a line at jonathanbesomi\_\_AT\_\_gmail.com

### Contributors (in chronological order)

-   Selim Al Awwa
-   Parth Gandhi
-   Dan Keefe
-   Christian Claus
-   bobfang1992
-   Ishan Arora
-   Vidya P
-   Cedric Conol
-   Rich Ramalho

License
-------

The MIT License (MIT)

Copyright (c) 2020 Texthero

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
