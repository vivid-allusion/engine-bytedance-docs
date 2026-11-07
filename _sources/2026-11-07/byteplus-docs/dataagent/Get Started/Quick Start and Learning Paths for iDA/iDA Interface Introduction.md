---
title: "iDA Interface Introduction"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_Interface_Introduction"
---

When using iDA for the first time, a clear interface layout is the first step to getting the job done efficiently.

This document will explain the iDA's navigation structure, analysis workspace, and common function entry one by one, helping you quickly locate the tools you need, shortening the time from getting start to familiarity, and making data intelligence accessible.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">iDA supports two forms: SaaS version and private deployment version. The interface structure of the two forms is the same, and only the login entrance is different. The SaaS version can be entered from the <a href="https://console.byteplus.com/home">BytePlus console</a>, and the private deployment version can be entered from the enterprise login entrance address.</div>


<div data-tips="true" data-tips-type="tip">This document will use SaaS as an example to introduce the interface structure of iDA.</div>


<span id="b55c8ba4"></span>
# Before starting

For enterprise data consumption and business decision\-making scenarios, iDA uses natural language as a unified entrance to organize data, knowledge, tools, and skills into complete task links. It can perform both quick counting and attribution analysis, research reports, and subsequent content delivery.

Before starting, it is recommended to complete the following:


* ### Account number and permissions   <span id="account-number-and-permissions"></span>


The account must be logged in and have access to the target project, agent, and corresponding data assets. When you can't see the agent, please contact the project administrator for authorization first.


* ### Data or information   <span id="data-or-information"></span>


You can use the agent's configured datasets, add resources from the input field, or upload local files. Know the metric criteria and data time range in advance.


* ### Clarify task   <span id="clarify-task"></span>


Start by thinking through the analysis object, metrics, dimensions, time range, and desired outcome form. Usually, the more specific the description, the more stable the results are.

<span id="c2736599"></span>
# iDA interface overview

The user interface of iDA revolves around "select agent on the left/create a new chat/Scheduler, describe the task, view the execution process, and view the analysis results". After the user enters the page, they usually first determine the agent to be used this time on the left, and then add data or data in the middle workspace and enter tasks; during the execution of the task, they can view the analysis plan and stage progress, and after completion, they can continue to ask questions, view reports, or export results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/544faa8ce60748d69c22dd9cd305c642~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bee53f41606b4a7e888dfc383f2f9855~tplv-goo7wpa0wc-image.image) </span>


|Interface area |Main content |Common operations |Suggestions for use |Legend |
|---|---|---|---|---|
|Left navigation area |Official agents and custom agents that the current region and account have access to |Switch agents, new conversations, and timed tasks to enter corresponding business scenarios |When querying enterprise\-specific metrics, prioritize business agents that have been configured with corresponding data and knowledge |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2407a21ec184574972b0a90ac9a6dab~tplv-goo7wpa0wc-image.image) </span> |
|task input area |Text box, recommendation questions, resource and document entry, skills and online search |Enter tasks, upload materials, specify skills, and send questions |Specify the metrics, time horizon, analysis dimension, and expected output in the task description |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38eb49a9f3fb43b18aa03d6d6224be52~tplv-goo7wpa0wc-image.image) </span> |
|Dialogue and execution area |Agent response, analysis plan, execution steps, and intermediate results |Check the progress, check the process, supplement requirements, and continue to ask questions |Complex analysis first checks whether task disassembly meets expectations, and then waits for complete results |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e086199918e7447ba100a7631cb4f115~tplv-goo7wpa0wc-image.image) </span> |
|Results and reporting area |Metrics, tables, charts, analytical findings, and web or document reports |View details, edit reports, copy, export, and share |Check calculation methods, filters, sources and access rights before delivery |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1ad1ff817804be0bc3641875195673c~tplv-goo7wpa0wc-image.image) </span> |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Select an agent → Add data or information → Enter tasks → View analysis process → Check results → Further inquiry, export, or share. For tasks that require only querying a single metric, operations are typically concentrated in the dialogue area; when attribution analysis or full reporting is required, the execution process and results areas contain more content.</div>


<span id="0145e19e"></span>
## Left navigation area

The side navigation area is the core navigation and task management entrance of the agent page, located on the left of the interface.

It integrates key functions such as agent switching, conversation management, scheduled tasks, file loading, and template saving to help you quickly switch among different agents and efficiently manage historical conversations and analysis tasks.


|Function item |Explain |Example |
|---|---|---|
|**Search Agent** |Enter the agent name keyword in the top search box to quickly filter the list and locate the target agent. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e2ec01355c243dcb4cb97806a91293a~tplv-goo7wpa0wc-image.image) </span> |
|**toggle agent** |Click on the agent name to switch the current workspace and enter the agent's independent conversation environment. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23af1cfadee94654b74266f8e21a49aa~tplv-goo7wpa0wc-image.image) </span> |
|**Create an agent** |Click the "Create Agent" button at the bottom of the list to create a new agent (with corresponding permissions). |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8b1275408f341698fe695b2504682ce~tplv-goo7wpa0wc-image.image) </span> |
|**agent list** |Click the Agent List button next to the Create Agent button to jump to the Agent List interface. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db638a52880c4432a76d391679fd7e9e~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ab6761e3e0e411ba0ff7641ccccf9e5~tplv-goo7wpa0wc-image.image) </span> |
|**New Dialogue** |Click "New Conversation" to open a new conversation window under the current agent to start a new Q & A. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cdfa627a3f0457d8cfc4a92bf1df261~tplv-goo7wpa0wc-image.image) </span> |
|**timed task** |Click "Timed Tasks" to enter the timed push task management page of the current agent, and you can view or configure active push tasks.<br><br>The timed task documentation can be found in [Scheduled Task](https://docs.byteplus.com/docs/dataagent/Scheduled_Task). |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4fbf7025288415e8a7d91946bd6256e~tplv-goo7wpa0wc-image.image) </span> |


<span id="ee6e6117"></span>
## Task input area

The task input area is located in the **core area** of the agent page and is the main operation panel for you to initiate Q & A and perform analysis tasks to the agent. This area integrates dialogue input, skill evocation, shortcut template and function entrance, and supports text input, file upload, template reuse and other interaction patterns.


|Function item |Explain |Example |
|---|---|---|
|**Text input** |Enter natural language questions or task instructions in the text box, supporting multi\-line text. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d47474ca08474c61a0b73f34e951e0ab~tplv-goo7wpa0wc-image.image) </span> |
|**Skill arousal** |Enter the `@`key in the text box to quickly evoke the skill list and select the corresponding analytical ability (such as knowledge retrieval, data analytics, etc.).<br><br>After arousing the skill, enter the task instruction or question and click the send button. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efc55f31fc4b453daaa3fce1145859c9~tplv-goo7wpa0wc-image.image) </span> |
|**Add resources or upload files** |Through the Add entry in the lower right corner of the text box, select Connected Resources or Upload Local Files. Suitable for temporary analysis of Excel, documents, images, and other materials. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c0591099f1b430b823c9f2b2e4b79c6~tplv-goo7wpa0wc-image.image) </span> |
|**Select skills** |Specialize in tasks such as counting, data processing, exploration attribution, and report writing to reduce duplicate descriptions. Availability depends on the current agent configuration. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efc55f31fc4b453daaa3fce1145859c9~tplv-goo7wpa0wc-image.image) </span> |
|**Internet search** |Open when the latest industry information or public information is required. The intelligence will organize the answers together with the Internet search results and the data and knowledge that have been accessed. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08140a6ac9644cb7aac378be32e54eb6~tplv-goo7wpa0wc-image.image) </span> |
|**Quick Entry** |Below the text box are four preset shortcut portals that allow you to switch between different analysis modes by clicking. After clicking on any entry, the entry will open to display its corresponding specific ability sub\-items for you to choose on demand.<br><br>The shortcut portal supports configuration in the content configuration, which can be configured according to your actual needs.<br><br>The specific operation of the content configuration is detailed in the [Content Configuration](https://docs.byteplus.com/docs/dataagent/Content_Configuration_) document. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c463f11aab14a618eab94c09215bcd1~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2fe5ce43749499ba10acfb35a4a9477~tplv-goo7wpa0wc-image.image) </span> |
|**Template** |The template area is located below the shortcut entry, which supports quick template selection and creation.<br><br>For detailed operation of the template, please refer to the [Template Center](https://docs.byteplus.com/docs/dataagent/Template_Center) document. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a9b332114a14fbca06e3b26afeea9f7~tplv-goo7wpa0wc-image.image) </span> |


<span id="65d6ae28"></span>
## Review the analysis process and results

After the agent completes the Q & A or task processing, the page displays the complete **analysis process** and **final results**. You can view the progress of task execution in real time, and perform subsequent operations such as downloading, previewing, and saving templates on the generated content. The following is a detailed description of the functional elements of the interface (the example is to generate documents, other web page image tables may be slightly different):


|Function |Explain |Example |
|---|---|---|
|Task status tracking |During the execution of a task, the system updates the status in real time. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6153ee617b084803a5e91d9191293810~tplv-goo7wpa0wc-image.image) </span> |
|Process Node Display |During the execution of the task, the system will gradually display information such as loading skills, task progress, and task results. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33e6e71079184371afe24eafcb43eb2d~tplv-goo7wpa0wc-image.image) </span> |
|**Save as template** |Save the currently entered problem logic as a template for subsequent quick reuse. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd0b9647a3a1462582d9e728a57a29aa~tplv-goo7wpa0wc-image.image) </span> |
|**Reset conversation** |Empty the current conversation and start a new one. If you have connected local files, datasets, Aeolus charts, Lark documents, etc. above, you can still continue to use them. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d52245b4d66f4d2da229b2f5d2c19289~tplv-goo7wpa0wc-image.image) </span> |
|**Share the conversation** |Click the Share button to share the conversation with other users, and copy links are supported for sharing. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c56cc82ecc494d0b88c1378fd558f6b5~tplv-goo7wpa0wc-image.image) </span> |
|**Analysis Results \- Replication** |Copy analysis results to clipboard. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f57136844d3c48fd86bd9d3c216aa887~tplv-goo7wpa0wc-image.image) </span> |
|**Analysis Results \- Download** |Download the analysis results locally. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9225bf30961b433ca29c48cd9b860c92~tplv-goo7wpa0wc-image.image) </span> |
|**Analysis Results \- Code/Preview** |Supports different forms of viewing of analysis results, by switching tabs to select Code/Preview document viewing. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a76eea724590486aba4cc9ce4799dc7f~tplv-goo7wpa0wc-image.image) </span> |


<span id="5363814e"></span>
# Account and agent list entry

In the lower left corner of the iDA interface, you can find the account and agent list entry. After clicking to enter, you can view all the agents of your current account and switch as needed. Also, the language can be switched for use.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57c98975875f426d92d399f45e01a3da~tplv-goo7wpa0wc-image.image) </span>

<span id="8b7040ad"></span>
# Common problem

**Question 1: What if the target agent cannot be found on the left?** 

Answer: First confirm whether the region is correct, and then confirm whether the agent has been released and whether the account has obtained project and agent permissions. Contact the project administrator when still invisible.

**Question 2: Should I choose intelligent data query or in\-depth research?** 

Answer: Use Intelligent data query first when you only need to inquire about metrics, trends, or details; use in\-depth research when you need multi\-step analysis, attribution, external data research, or full reports.

**Question 3: When do I need to create a new chat?** 

Answer: When the new question is unrelated to the current task, or when the agent is not expected to continue referring to the previous context, reset the conversation or create a new chat to avoid historical information affecting the understanding.
