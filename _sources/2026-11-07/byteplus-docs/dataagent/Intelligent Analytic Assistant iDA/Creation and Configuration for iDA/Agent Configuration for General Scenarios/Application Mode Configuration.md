---
title: "Application Mode Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Application_Mode_Configuration"
---

Support for defining the search scope as a global asset/knowledge base, enabling or disabling SQL tools, Python tools, and networked search.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26ee4d094d7a492396983ec72090802f~tplv-goo7wpa0wc-image.image) </span>


|Configuration item |Explain |
|---|---|
|Search Tool |Support to open the search tool, and the search scope can be selected as "global asset" or "knowledge base".<br><br>• **Global assets** : The system retrieves according to the global scope. If the administrator has configured data assets in the background, priority is given to retrieving the circled data assets.<br><br>• **Knowledge Base** : Retrieves the contents of the current agent\-bound knowledge base. |
|Query Aeolus Chart Tool |After opening, the corresponding data results can be directly obtained according to the Aeolus chart provided or retrieved by the user.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This item supports configuration only if the datawind is bound.</div><br> |
|SQL Tools |After opening, the agent can automatically generate and execute SQL statements based on user questions, completing data calculations and queries. |
|Python Tool |Once turned on, the agent can write and run Python code based on user questions, supporting advanced analysis such as data calculation and charting. |
|Internet Search |After opening, the agent can call a public search engine to retrieve real\-time information and supplement the answers.<br><br>At the same time, it supports opening the item under the question and answer dialog box. |


&nbsp;
