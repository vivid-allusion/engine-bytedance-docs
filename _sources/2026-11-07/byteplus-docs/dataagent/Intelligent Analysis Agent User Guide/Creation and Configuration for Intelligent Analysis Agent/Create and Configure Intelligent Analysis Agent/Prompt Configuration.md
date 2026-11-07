---
title: "Prompt Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Prompt_Configuration"
---

Since the Agent is based on large model capabilities, and a key feature of large models is the ability to add Prompts, in simple terms, this means that you can configure some prerequisites for the large model, which enables the large model to provide more accurate answers. The Agent supports configuring Prompts, allowing users to obtain query results that better fit their specific scenarios. This article provides guidance on creating and configuring Prompts when creating and configuring an intelligent analysis Agent.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The intelligent analysis Agent system has built\-in Prompts, so there is no need to configure them repeatedly. You can add custom prompts as needed.</div>


<span id="d47b2def"></span>
# Add Prompt

On the Prompt configuration page, you can click the "Add Prompt" button on the right to add a Prompt.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/809bb373c2b743dba56361d3a24dbc20~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Configuration instructions |
|---|---|
|Application scenario |Select the application scenario for the currently added Prompt. The following options are currently supported: General, web page generation, and multi\-table association. |
|Prompt type |The following types are currently supported:<br><br><br>* Hint: Provides guiding clues or inspiration. Example: "Pay attention to seasonal fluctuation factors when analyzing sales data."<br><br>* Requirement: Specifies the output standard clearly. Example: "The queried financial data must be accurate to two decimal places." |
|Prompt |Prompt example:<br><br>❌: For questions about data under employment modes, such as how many people are in each employment type, select the "Employment Mode \- Active Workforce Usage" field as the dimension for employment mode; for questions about the proportion of non\-frontline staff in segmented employment modes, such as what is the proportion of non\-frontline staff in XX, select the "Employment Mode \- Non\-frontline Workforce Proportion Usage" field as the dimension for employment mode.<br><br>✅: If the question ends with "how many people are in each employment type", select the "Employment Mode \- Active Workforce Usage" field as the dimension when querying; if the question ends with "what is the proportion of non\-frontline staff", select the "Employment Mode \- Non\-frontline Workforce Proportion Usage" field as the dimension.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The examples here are provided only as a reference for description; actual configuration must be adjusted according to business logic.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more prompt\-related question suggestions and examples, refer to <a href="https://docs.byteplus.com/docs/dataagent/Best_Practices_Recommendations_and_Examples_for_Intelligent_Data_Query_Questions">Best Practices: Recommendations and Examples for Intelligent Data Query Questions</a>.</div><br> |


<span id="2f8371d1"></span>
# Import Prompt

Starting from version 3.5.0, you can directly import Prompt configurations from other Agents.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only users with administrator privileges can perform import operations.</div>


You can click the "Import from other Agent" button at the top right of the page.

<span id="46018759"></span>
# Edit and delete Prompts

You can edit or delete configured Prompts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/599a390e0fb9496cbc6aa6e94a81ea06~tplv-goo7wpa0wc-image.image) </span>
