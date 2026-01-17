---
project: vocabulary-corpus
stars: 417
description: 44000+ 词汇语料库
url: https://github.com/hubingkang/vocabulary-corpus
---

🔤 词汇语料库
========

✨ 功能特性
------

### 🎯 核心功能

-   **多维度词汇分析**: 提供音标、释义、词源、语法、文化背景等全方位分析
-   **智能速率控制**: 内置滑动窗口速率限制器，确保 API 调用稳定性
-   **批量处理**: 支持大规模词汇列表的自动化处理
-   **断点续传**: 自动跳过已处理的词汇，支持中断后继续处理
-   **结构化输出**: 生成标准化的 JSON 格式词汇数据

### 📊 数据维度

-   **语音学信息**: 英式/美式音标 (IPA 标准)
-   **语义分析**: 多层次释义、难度分级、使用频率
-   **词源研究**: 历史发展、词根分析、相关词汇
-   **语法信息**: 词性变化、句法模式、常见错误
-   **语义关系**: 同义词、反义词、搭配模式
-   **文化语境**: 地域差异、历史背景、现代用法
-   **记忆辅助**: 视觉场景、助记设备、词汇联想

📁 项目结构
-------

```
├── index.ts              # 主程序文件
├── word.txt              # 待处理词汇列表
├── data/                 # 生成的词汇数据目录
│   ├── tolerance.json    # 词汇分析结果
│   ├── democracy.json
│   └── ...
├── package.json          # 项目配置
├── tsconfig.json         # TypeScript 配置
└── README.md            # 项目说明
```

📋 数据结构
-------

每个词汇生成的 JSON 文件包含以下结构：

{
  "word": "词汇",
  "phonetics": {
    "british": "英式音标",
    "american": "美式音标"
  },
  "definitions": \[
    {
      "partOfSpeech": "词性",
      "definition": "英文释义",
      "chineseTranslation": "中文翻译",
      "level": "难度级别",
      "frequency": "使用频率",
      "register": "语域"
    }
  \],
  "phrases": \[...\],
  "examples": \[...\],
  "etymology": {...},
  "difficultyAnalysis": {...},
  "semanticRelations": {...},
  "culturalContext": {...},
  "memoryAids": {...},
  "grammaticalInfo": {...},
  "metadata": {...}
}

### 详细字段说明

字段

描述

示例

`phonetics`

音标信息

英式/美式 IPA 音标

`definitions`

词义定义

包含词性、释义、难度等

`etymology`

词源信息

历史发展、词根分析

`difficultyAnalysis`

难度分析

CEFR 等级、学习建议

`semanticRelations`

语义关系

同义词、反义词、搭配

`culturalContext`

文化语境

地域差异、历史背景

`memoryAids`

记忆辅助

视觉场景、助记方法

🎓 使用场景
-------

### 教育机构

-   制作词汇学习材料
-   构建个性化学习系统
-   生成词汇测试题库

### 语言学习者

-   深度理解词汇含义
-   掌握词汇文化背景
-   获得科学记忆方法

### 研究人员

-   语料库研究
-   词汇难度分析
-   跨文化语言研究

📈 数据质量
-------

### 数据来源

-   权威词典 (OED, COCA, BNC)
-   大规模语料库
-   认知科学研究
-   跨文化语言学研究
-   IPA 标准音标
-   多语域例句覆盖
-   历史准确的词源信息
-   基于学习理论的难度分析

📄 许可证
------

本项目采用 MIT 许可证。详见 LICENSE 文件。
