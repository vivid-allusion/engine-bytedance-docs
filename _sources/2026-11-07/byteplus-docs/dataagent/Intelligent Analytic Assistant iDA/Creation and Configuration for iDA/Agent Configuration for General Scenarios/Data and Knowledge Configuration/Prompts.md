---
title: "Prompts"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Prompts"
---

Since the agent is based on the function of the large model, one of the characteristics of the large model is that it can add prompts. In simple terms, it can configure some preconditions for the large model, so that the large model can give more accurate answers. The agent supports the ability to configure prompts, allowing users to obtain query results that are more in line with their own scenarios. This article provides you with configuration guidance related to prompt word configuration when creating a new version of Configuration Data Agent.

<span id="9f55fce5"></span>
# Precautions


* The Data Agent (New Version) system has built\-in prompts, no need to reconfigure, you can add custom prompts according to your needs.


<span id="cad1591e"></span>
# Add Prompts

On the prompt word configuration page, you can click the "Add prompt word" button on the right to add the prompt word.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66f059d4882c4a40a648ff4ca1af82c0~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Application scenario |Select the application scenario of the currently added prompt word, currently supports selection: general, web page generation, multi\-table association. |
|Prompt type |The following types are currently supported:<br><br><br>* Hint: Provide guiding clues or inspiration. Example: "Be aware of seasonal fluctuations when analyzing sales data."<br><br>* Requirements: Clearly specify the standards for output. Example: "The queried financial data must be accurate to two decimal places." |
|Prompt |Prompt examples:<br><br>❌: If the user asks about the relevant data under the employment mode, such as how many people there are in different employment types, select the "Employment Mode \- On\-the\-job Manpower Usage" field for the dimension of the employment mode; if the data related to the non\-first\-line proportion under the employment mode is asked, such as what is the proportion of XX non\-first\-line, select the "Employment Mode \- Non\-first\-line Manpower Usage" field for the dimension of the employment mode<br><br>✅: If the question ends with "How many people are there in different employment types", select the "Employment mode \- on\-the\-job manpower usage" field in the dimension when inquiring; if the question ends with "What is the proportion of non\-first\-line manpower", select the "Employment mode \- non\-first\-line manpower usage" field in the dimension<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The example here is for reference only, and the actual configuration process needs to be adjusted according to business logic.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">More questions and suggestions related to prompts and examples can be referred to <a href="https://docs.byteplus.com/docs/dataagent/Best_Practices_Recommendations_and_Examples_for_Intelligent_Data_Query_Questions">Best Practices: Recommendations and Examples for Intelligent Data Query Questions</a>.</div><br> |


<span id="d38b59d8"></span>
# Import Prompts

Since the 3.5.0 version, it supports the direct import of prompt word configurations for other agents.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only users with administrative privileges can perform import operations.</div>


You can click the "Import from Other Agents" button at the top right of the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23c0c2f6c9984564b18b6fdf3c60554a~tplv-goo7wpa0wc-image.image) </span>

<span id="6d6fafbd"></span>
# Edit and Delete Prompts

Supports everyone to edit or delete the configured prompts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca72919ddbf94f92ae5f63014ca51901~tplv-goo7wpa0wc-image.image) </span>
