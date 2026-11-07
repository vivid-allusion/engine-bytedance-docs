---
title: "Natural Language Processing"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Natural_Language_Processing"
---

<span id="_1-概述"></span>
# 1. Overview

Visual modeling supports processing data using various natural language processing methods, enabling more intuitive and convenient subsequent visual queries and analysis. This document introduces the functions of natural language processing operators.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c6fb2f0498d4b1da86ae9a9d5333695~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-功能介绍"></span>
# 2. Function overview

<span id="_2-1-生成句向量"></span>
## 2.1 Generate sentence vectors

Sentence vectors for text are generated based on word vectors. You can choose pre\-trained word vectors or generate sentence vectors using word vectors you trained yourself.

**Field settings**

Input column: Input column (the input is an array of type string, for example, the result after the tokenization operator can be used as input; the right port is optional, and the input can be word vectors trained by the user).

**Parameter settings**

Output column: Output column

<span id="_2-2-分词"></span>
## 2.2 Tokenization

The tokenization operator supports tokenizing Chinese documents. Unlike English, Chinese uses characters as units, and all characters in a sentence must be combined to convey a meaning. Segmenting a sequence of Chinese characters into meaningful words is called Chinese tokenization. For example: "我是一个学生", the tokenization result is: 我, 是, 一个, 学生. (The input is text of type string)

**Field settings**

Input column: Input column

**Parameter settings**

Output column name: Name of the output column

<span id="_2-3-移除停用词"></span>
## 2.3 Remove stop words

Remove specified stop words from a segment of text. To save storage space and improve search efficiency, certain characters or words are automatically filtered out before or after processing natural language data (or text). These characters or words are referred to as stop words. (The input must be an array of type string, usually following the tokenization operator)

**Field settings**

Input word column: Input word column

**Parameter settings**

Default stop word table language: Default stop word table language. The system provides stop word tables for three languages: Chinese, English, and French.
