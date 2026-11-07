---
title: "Text Processing"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Text_Processing_"
---

<span id="985d775a"></span>
# Feature Overview

Text processing refers to the process of analyzing, cleaning, converting and formatting text data using automated programs. The main goal is to transform raw, unstructured, or semi\-structured text data into clean, organized, and directly usable by downstream model training or data analytics tasks. This article will show you how to use text processing operators.

<span id="1611d320"></span>
# Operator introduction

<span id="9929ea08"></span>
## **Specific character substitution**

For special characters, they can be replaced with new characters by exact matching or regular matching.

**Application scenario**

When text data is obtained from web pages, crawlers, user input, etc., the data is often "dirty data" and must be cleaned before use, for example:


* Replace irrelevant characters such as URLs, email addresses, and mobile phone numbers with unified identifiers (e.g. [URL]) to avoid interfering with semantic analysis.

* Replace special control characters (such as\ n,\ t,\ r, spaces) with a uniform format (such as a single space).

* Replace duplicate characters (such as "ah ah" → "ah") and garbled characters (such as "") to ensure text readability.


**Operating instructions**

Click the plus sign + to add the **text processing \> special character replacement** operator to the visual knowledge processing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fda1f6c615844d03ab01fcb7219f725f~tplv-goo7wpa0wc-image.image) </span>


|parameter |explain |
|---|---|
|action field |Select an upstream output field, a field cannot be selected repeatedly. |
|primitive character |Support for entering multiple ordinary characters, and use the Enter key to separate multiple characters. You can also switch to regular expressions. |
|substitution character |user defined |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The number of rules should not exceed 10.</div>


<span id="6cfca8d6"></span>
## **HTML tag removal**

Remove `< div >`, `< p >`, `< span >`, `< a >`and other HTML tags used for web page rendering, which are "meaningless noise, which may cause distortion of analysis/training results, ensure the" purity "of the text data, and let the model focus only on the semantics of the text itself.

**Application scenario**

When crawling web content, the text will be mixed with `< p >`, `< div >`, `< br >`, `< a >`and other HTML tags, these tags are meaningless to the text content itself, such as crawling the news body, you need to keep only plain text content.

**Operating instructions**

Click the plus sign + to add the **text processing \> HTML tag removal** operator to the visual knowledge processing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56dee55891a74d63a33afe70eff8edb2~tplv-goo7wpa0wc-image.image) </span>


* Action field: Select the field to remove the HTML tag.

* Remove tag type: Select the HTML tag type to be removed during processing. Optional tag types include: `div`, `p`, `span`, `table`, `td`, `th`, `h1`, `h2`, `h4`, `form`, `button`, `img`, `input`, etc.


<span id="070df7d7"></span>
## **Hash calculation**

Calculates the unique identity of the text and generates a corresponding MD5 hash value for each text.

**Application scenario**

Applied to detect duplicate text, deduplicate data, reduce the calculation of duplicate data.

**Operating instructions**

Click the plus sign + to add the **text processing \> hash calculation** operator to the visual knowledge processing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d39115b03044d7ebd47d62c7b1fa7f9~tplv-goo7wpa0wc-image.image) </span>


* Action field: Select the field to detect.

* Hash calculation method: radio, MD5 is selected by default, and sha256 can be selected.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b879a5969194aaa948e7a6918064a21~tplv-goo7wpa0wc-image.image) </span>

<span id="0ad91544"></span>
## **Special character removal**

Remove punctuation, repetitive punctuation, emoji, etc. from text

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/564ea6d668414f2d90fe40739870dfda~tplv-goo7wpa0wc-image.image) </span>

**Operating instructions**

Click the plus sign + to add the **text processing \> character removal** operator to the visual knowledge processing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe51a98db5384b9dbdca88fa68cdb8be~tplv-goo7wpa0wc-image.image) </span>


* Action field: Select the field to detect.

* Remove Characters: Select Emoji, Punctuation, Repeated Punctuation, etc. Repeated Punctuation is for example changing "!!!" to "!".


<span id="93605b4b"></span>
## Text language recognition

Identify the language of the input.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/164ba09d572244689c893f9b8d398b6c~tplv-goo7wpa0wc-image.image) </span>

**Operating instructions**

Click the plus sign + to add the **text processing \> text language recognition** operator in the visual knowledge processing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a173cb8a1cb148dfb7cff7be15badd2d~tplv-goo7wpa0wc-image.image) </span>


* Processing configuration: Set the input field, and the current operator will detect the input content and recognize the language.

* Output configuration:

   * Output field: The recognition result is output through this field.

   * Output confidence level: You can choose to turn it on. After turning it on, the output field will contain the confidence level score, which is 0 to 1. The higher the value, the higher the confidence level.


<span id="9a7ad099"></span>
## Multilingual Text Translation \- Volcano

Translate specified text content based on Volcano Engine machine translation's [text translation API ](https://www.volcengine.com/docs/4640/65067?lang=zh)capabilities.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb3245e8978d416096224126386386c4~tplv-goo7wpa0wc-image.image) </span>

**Operating instructions**

Click the plus sign + to add **text processing \> multilingual text translation \- volcano** operator in visual knowledge processing.

The configuration instructions are as follows:


|**Configuration item** |**Parameter description** |
|---|---|
|Model information |* Access Key ID: Request a security certificate for the Volcano Engine API, please refer to [Access Key Management ](https://www.volcengine.com/docs/6291/65568).<br><br>* Secret Access Key: Request a security certificate for the Volcano Engine API, please refer to [Access Key Management ](https://www.volcengine.com/docs/6291/65568). |
|Handle configuration |* Action Fields: Select the field from the input field for which the text needs to be translated.<br><br>* Source language: Select the source language type, and automatically detect the language by default when not set.<br><br>* Target language: Select the target language after translation. |
|Advanced Settings |* Concurrency size: Set the concurrency limit for translation requests.<br><br>* Timeout: Set the timeout for translation requests, after which a retry mechanism will be triggered.<br><br>* Retries: Set a limit on the number of times a translation request can be retried.<br><br>* Retry interval: Set the interval between each retry in ms.<br><br>* Exception handling: Configure the handling strategy when a task is abnormal.<br><br>   * Terminate the task: If the call fails, the task fails and intermediate results are cleared.<br><br>   * Ignore exceptions: Ignore the data of the failed call, fill it with null, and keep the result of the successful call, and the final task is successful. |
|Output Configuration |Output field: The translation result is output through this field. |
