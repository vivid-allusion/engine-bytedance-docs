---
title: "Natural Language Processing"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Natural_Language_Processing"
---

<span id="_1-概述"></span>
# 1. Overview

Natural language processing refers to the support for processing data using various natural language processing methods in visual modeling, enabling more intuitive and convenient subsequent visual queries and analytical presentations. This document will introduce the functions of natural language processing operators.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ca471c534fb4a289f3a99f4413804ea~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-功能介绍"></span>
# 2. Introduction to functions

<span id="_2-1-生成句向量"></span>
## 2.1 Generate sentence vectors

Generate sentence vectors for text based on word vectors. You can choose pre\-trained word vectors or generate sentence vectors using custom\-trained word vectors.

**Field settings**

Input column: Input column (input is an array of type string, for example, the result from the tokenization operator can be used as input; the right port is optional, and the input can also be word vectors trained by the user).

**Parameter settings**

Output column: Output column

<span id="_2-2-分词"></span>
## 2.2 Tokenization

The tokenization operator supports tokenizing Chinese documents. Unlike English, Chinese uses characters as units, and the meaning of a sentence is conveyed by combining all the characters in a sentence. Segmenting a sequence of Chinese characters into meaningful words is called Chinese word segmentation. For example: 我是一个学生. The result of tokenization is: 我, 是, 一个, 学生. (Input is text of type string)

**Field settings**

Input column: Input column

**Parameter settings**

Output column name: Name of the output column

<span id="_2-3-移除停用词"></span>
## 2.3 Remove stop words

Remove specified stop words from a piece of text. To save storage space and improve search efficiency, certain characters or words are automatically filtered out before or after processing natural language data (or text). These characters or words are called stop words. (Input needs to be an array of type string, usually following the tokenization operator)

**Field settings**

Input word column: Input word column

**Parameter settings**

Default stop word list language: The system provides stop word lists in three languages: Chinese, English, and French.
