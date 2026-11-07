---
title: "Conversational search scenarios"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Conversational_search_scenarios"
---

<span id="5474ffc0"></span>
### Common issues and optimization for conversational search agents

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">\*说明</div>


<div data-tips="true" data-tips-type="default">This document helps you troubleshoot and resolve common issues encountered when using the conversational search feature. It also provides optimization recommendations to improve conversational search performance.</div>


<div data-tips="true" data-tips-type="default">The content covers multiple typical application scenarios, from basic feature configuration (such as no response from conversational search and filters not taking effect) to advanced customization (such as custom output formats and understanding specialized terminology), to help you build smarter and more reliable conversational search applications.</div>


<div data-tips="true" data-tips-type="default">To experience more Viking AI Search capabilities, go to: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search, the integrated intelligent engine for enterprise search, recommendation, and conversational search</a></div>


<span id="02507efc"></span>
### Conversational search: No reply after creating a conversation

A lack of response after creating a conversation is usually caused by a timeout.

Timeouts are usually caused by excessive input information.

Check if the item dataset contains large fields. You can view the field configuration for the corresponding dataset in the console. Such as the following fields


|Check item |Troubleshooting logic and recommendations |
|---|---|
|Multi\-modal reranking<br><br> |Check if the multi\-modal reranking count is too large. Recommended configuration: 20<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f404e07c8dc34474adce0a3d5ffa047a" width="382px" /></div><br><br><br> |
|Are there large fields used for Document search? |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c81df6016f834a62b9e53f4983462d76" width="741px" /></div><br> |


<span id="359ab55a"></span>
### Irrelevant videos referenced in conversational search replies

During replies, video content is parsed into text information. The model might reference parts of this information, which may not be evident from the content title. This can result in recommendations for videos that appear irrelevant.

Play the video content to see if the response is sourced from it.

&nbsp;

<span id="971b2c4b"></span>
### The conversational response cited weakly relevant materials.

Suggestion:

In the "Response style" section, add the instruction: "Return only strongly relevant cited materials."

<span id="69fcb895"></span>
### How can the conversational model understand specialized terminology from niche industries?

Suggestion:

Define the meanings of specialized terms in the Agent persona.

<span id="90b9f6fc"></span>
### How can I make the conversational response output in a custom format?

The system has a default response format, and you can also customize it in the "Response style" settings. The following is an example of an e\-commerce shopping guide scenario.

```Markdown
下方内容为客户对输出结果的一些额外要求，你在输出时必须要遵守这些要求！
请根据输入的商品向量数据，按以下输出风格生成商品推荐内容：

- 使用 Markdown 格式输出
- 表述保持专业、客观、克制，避免营销化或情绪化用语
- 同时体现优势与边界，侧重“适配性”而非价值判断

#### 输出结构必须包含以下内容（顺序不可变）
1. 商品标题行
   - 作为 Markdown 二级标题  
   - 标题格式为：`## {序号}. {商品标题}`  
   - 序号按匹配率从高到低递增（1、2、3…）

2. 推荐理由行
   - 紧接商品标题下一行  
   - 合并输出匹配度（0–100）与一句话推荐理由，强调“为什么特别推荐”

3. 商品的其他优点行
   - 包括好评信息、促销信息等  
   - 使用 🎯 图标
   - 只列出正向的特点，比如 如果销量较低，这里就不要写了；如果没有促销信息，这里也不用写
  

- 最后，请你在【商品的其他优点】之后，将你使用到的商品id用<ref></ref>标签引用，相同的商品id只需要引用1次即可

#### 格式示例：
```markdown
## 1. 窗花静电贴  
**推荐理由：马年专属装饰。马年福字、生效图案，贴玻璃门超有氛围的**
### 🎯 五星评价。外形漂亮，颜料颜色艳丽，性价比高
### 🎯 60天最低价哦
<ref>4</ref>
---
## 2. 灯笼挂件 
**推荐理由：手提发光花灯，小朋友提着玩或者挂起来都喜庆**
### 🎯 五星评价。安装简单，拍照很出片。
### 🎯 买二送一
...
<ref>7</ref>

附加约束：
- 不输出上述结构之外的任何内容
```


&nbsp;

&nbsp;

<span id="00b52420"></span>
### Conversational search \- Fails to recommend items based on filter criteria in the conversation

**Core configuration:** 


1. Check if the item dataset contains a field corresponding to the information used for filtering in the query.

2. If the field is a numeric type, such as int or float, it must be marked as **Filterable**.

3. If the field is a string or array<string\> type, it must be marked as **Filterable** and defined as a **Category/Type** property.


&nbsp;

Example query 1:

> Q: Recommend new products from 2026.

> A: I'm sorry, we do not have any new product recommendations for 2026 at the moment.

> **Solution: Add a `Release time` field to the item dataset and mark it as Filterable.** 


&nbsp;

Example query 2: (In the following example, '红袖' is a brand name. The large model may not recognize this and could interpret it as 'red sleeves', rewriting the query with a different semantic meaning.)

> Q: Hongxiu

> A: We are sorry, but we do not currently carry clothing from the Hongxiu brand...

> **Solution: set the `Brand` field as a category attribute**


&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">\*说明</div>


<div data-tips="true" data-tips-type="default">To learn more about Viking AI Search product capabilities, please see: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search, the integrated intelligent engine for enterprise Search, Recommendation, and conversational search</a></div>
