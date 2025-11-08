---
project: jailbreak_llms
stars: 3426
description: [CCS'24] A dataset consists of 15,140 ChatGPT prompts from Reddit, Discord, websites, and open-source datasets (including 1,405 jailbreak prompts).
url: https://github.com/verazuo/jailbreak_llms
---

In-The-Wild Jailbreak Prompts on LLMs
=====================================

This is the official repository for the ACM CCS 2024 paper "Do Anything Now'': Characterizing and Evaluating In-The-Wild Jailbreak Prompts on Large Language Models by Xinyue Shen, Zeyuan Chen, Michael Backes, Yun Shen, and Yang Zhang.

In this project, employing our new framework JailbreakHub, we conduct the first measurement study on jailbreak prompts in the wild, with **15,140 prompts** collected from December 2022 to December 2023 (including **1,405 jailbreak prompts**).

Check out our website here.

**Disclaimer. This repo contains examples of harmful language. Reader discretion is recommended. This repo is intended for research purposes only. Any misuse is strictly prohibited.**

Data
----

Prompts
-------

Overall, we collect 15,140 prompts from four platforms (Reddit, Discord, websites, and open-source datasets) during Dec 2022 to Dec 2023. Among these prompts, we identify 1,405 jailbreak prompts. To the best of our knowledge, this dataset serves as the largest collection of in-the-wild jailbreak prompts.

The data are provided here.

> Statistics of our data source. (Adv) UA refers to (adversarial) user accounts.

Platform

Source

\# Posts

\# UA

\# Adv UA

\# Prompts

\# Jailbreaks

Prompt Time Range

Reddit

r/ChatGPT

163549

147

147

176

176

2023.02-2023.11

Reddit

r/ChatGPTPromptGenius

3536

305

21

654

24

2022.12-2023.11

Reddit

r/ChatGPTJailbreak

1602

183

183

225

225

2023.02-2023.11

Discord

ChatGPT

609

259

106

544

214

2023.02-2023.12

Discord

ChatGPT Prompt Engineering

321

96

37

278

67

2022.12-2023.12

Discord

Spreadsheet Warriors

71

3

3

61

61

2022.12-2023.09

Discord

AI Prompt Sharing

25

19

13

24

17

2023.03-2023.04

Discord

LLM Promptwriting

184

64

41

167

78

2023.03-2023.12

Discord

BreakGPT

36

10

10

32

32

2023.04-2023.09

Website

AIPRM

\-

2777

23

3930

25

2023.01-2023.06

Website

FlowGPT

\-

3505

254

8754

405

2022.12-2023.12

Website

JailbreakChat

\-

\-

\-

79

79

2023.02-2023.05

Dataset

AwesomeChatGPTPrompts

\-

\-

\-

166

2

\-

Dataset

OCR-Prompts

\-

\-

\-

50

0

\-

**Total**

**169,933**

**7,308**

**803**

**15,140**

**1,405**

**2022.12-2023.12**

**Load Prompts**

You can use the Hugging Face `Datasets` library to easily load all collected prompts.

from datasets import load\_dataset

dataset \= load\_dataset('TrustAIRLab/in-the-wild-jailbreak-prompts', 'jailbreak\_2023\_05\_07', split\='train')
\# dataset = load\_dataset('TrustAIRLab/in-the-wild-jailbreak-prompts', 'jailbreak\_2023\_12\_25', split='train')
\# dataset = load\_dataset('TrustAIRLab/in-the-wild-jailbreak-prompts', 'regular\_2023\_05\_07', split='train')
\# dataset = load\_dataset('TrustAIRLab/in-the-wild-jailbreak-prompts', 'regular\_2023\_12\_25', split='train')

The original csv files are provided in our GitHub repo jailbreak\_llms.

Note: If you plan to use this dataset to train models, preprocessing the `prompt` field to remove duplicates is recommended. For more details, see this discussion.

Question Set
------------

To evaluate the effectiveness of jailbreak prompts, we construct a question set comprising 390 questions across 13 forbidden scenarios adopted from OpenAI Usage Policy.

We exclude `Child Sexual Abuse` scenario from our evaluation and focus on the rest 13 scenarios, including `Illegal Activity`, `Hate Speech`, `Malware Generation`, `Physical Harm`, `Economic Harm`, `Fraud`, `Pornography`, `Political Lobbying`, `Privacy Violence`, `Legal Opinion`, `Financial Advice`, `Health Consultation`, and `Government Decision`.

from datasets import load\_dataset

forbidden\_question\_set \= load\_dataset("TrustAIRLab/forbidden\_question\_set", split\='train')

The original file of the question set is also provided in our GitHub repo jailbreak\_llms.

Code
----

### Evaluator - ChatGLMEval

```
cd code/ChatGLMEval
<!-- add data paths in df_path_list of run_evaluator.py -->
python run_evaluator.py
```

### Semantics Visualization

Check `code/semantics_visualization/visualize.ipynb`

Ethics
------

We acknowledge that data collected online can contain personal information. Thus, we adopt standard best practices to guarantee that our study follows ethical principles, such as not trying to deanonymize any user and reporting results on aggregate. Since this study only involved publicly available data and had no interactions with participants, it is not regarded as human subjects research by our Institutional Review Boards (IRB). Nonetheless, since one of our goals is to measure the risk of LLMs in answering harmful questions, it is inevitable to disclose how a model can generate hateful content. This can bring up worries about potential misuse. However, we strongly believe that raising awareness of the problem is even more crucial, as it can inform LLM vendors and the research community to develop stronger safeguards and contribute to the more responsible release of these models.

We have responsibly disclosed our findings to related LLM vendors.

Citation
--------

If you find this useful in your research, please consider citing:

```
@inproceedings{SCBSZ24,
      author = {Xinyue Shen and Zeyuan Chen and Michael Backes and Yun Shen and Yang Zhang},
      title = {{``Do Anything Now'': Characterizing and Evaluating In-The-Wild Jailbreak Prompts on Large Language Models}},
      booktitle = {{ACM SIGSAC Conference on Computer and Communications Security (CCS)}},
      publisher = {ACM},
      year = {2024}
}
```

License
-------

`jailbreak_llms` is licensed under the terms of the MIT license. See LICENSE for more details.
