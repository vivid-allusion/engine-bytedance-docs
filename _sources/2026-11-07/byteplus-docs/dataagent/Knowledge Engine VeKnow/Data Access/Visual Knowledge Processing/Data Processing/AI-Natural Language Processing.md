---
title: "AI-Natural Language Processing"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/AI-Natural_Language_Processing"
---

<span id="a7296ac2"></span>
# Feature Overview

Natural language processing means that visual knowledge processing supports processing data in a variety of natural language processing methods, so as to more intuitively and conveniently perform subsequent visualized query and analysis. This article will introduce you to the capabilities of natural language processing operators.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/228631b350e6466db2fa13e785dea515~tplv-goo7wpa0wc-image.image) </span>

<span id="42596036"></span>
# Operator Introduction


1. **Generate sentence vector**


The sentence vector of the text is generated according to the word vector. You can choose the pre\-trained word vector, or you can generate the sentence vector according to your own trained word vector.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Field setting</strong> input column: input column (input is an array of string type, such as the result after the word segmentation operator as input, the right port is optional, and the input is the word vector trained by the user himself).</div>


* <div data-tips="true" data-tips-type="tip"><strong>Parameter settings</strong> Output column: Output column</div>


2. **Participle**


Word segmentation operator, supports segmentation of Chinese documents. Unlike English, Chinese is word\-based, and all the words in a sentence can be connected to describe a meaning. Chinese word segmentation is to divide the sequence of Chinese characters into meaningful words.

For example: I am a student, the result of the participle is: I, is, one, student. (Enter as string type text)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Field settings</strong> Input column: Input column</div>


* <div data-tips="true" data-tips-type="tip"><strong>parameter setting</strong></div>


   <div data-tips="true" data-tips-type="tip">Word segmentation methods: word segmentation methods include standard word segmentation, traditional Chinese word segmentation, NLP word segmentation, index word segmentation, N\-shortest path word segmentation, web link word segmentation and speed dictionary word segmentation   </div>
   

   <div data-tips="true" data-tips-type="tip">Output column name: the name of the output column   </div>
   

3. **Remove stop words**


Removes the specified stop word from a piece of text. To save storage space and improve search efficiency, certain words or phrases are automatically filtered out before or after processing natural language data (or text), which are called Stop Words. (You need to enter an array of type string, usually after the participle operator)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Field settings</strong> input word column: input word column</div>


* <div data-tips="true" data-tips-type="tip"><strong>Parameter settings</strong> Default disable vocabulary language: Default disable vocabulary language, the system provides three languages to disable vocabulary: Chinese, English and French.</div>
