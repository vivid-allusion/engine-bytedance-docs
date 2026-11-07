---
title: "Deep Research Agent"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Deep_Research_Agent"
---

**The Intelligent Analysis Agent (hereinafter referred to as the Analysis Agent or Intelligent Agent) is an expert advisor based on AI deep reasoning and big data analysis**. The Analysis Agent includes the Data Query Agent and the Deep Research Agent. In business analysis and decision support scenarios, the **Deep Research Agent** provides core intelligent analysis capabilities, using data queries as the basis for interaction, integrating the deep reasoning capabilities of large models, and enabling intelligent transformation from raw data to business insights.

<span id="053f46f3"></span>
# Feature overview

The Deep Research Agent feature of the **Intelligent Analysis Agent** can automatically parse natural language requirements, build a complete analysis framework, generate SQL and Python code to perform data insights, and output deep research reports to help enterprises make efficient decisions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98e14ed0c52d49a3b0b462ae90f17675~tplv-goo7wpa0wc-image.image) </span>

**The specific features are as follows**:


* **Reasoning and planning analysis outline**: Based on user questions, the large model performs reasoning to generate the thought process, automatically constructs the analysis path of "problem definition → hypothesis validation → conclusion derivation," generates an analysis outline, and transforms business requirements into executable analysis plans.

* **Decompose and execute analysis tasks**: Automatically invokes the dataset SQL query tool to perform data queries, supports Python code generation and execution, and conducts data insight analysis.

* **Deep research report generation**: Deeply integrates internal business data, enterprise knowledge engines, and online search capabilities to generate core conclusions, multidimensional analysis charts, and decision recommendations, producing deep research reports that are more aligned with enterprise scenarios.


<span id="a03f78f1"></span>
# Prerequisites


* Project creation and user authorization have been completed. For details, see [Project Information](https://docs.byteplus.com/docs/dataagent/Project_Information), [User Management](https://docs.byteplus.com/docs/dataagent/User_Management)

* Data preparation has been completed. For details, see [Data Preparation Overview](https://docs.byteplus.com/docs/dataagent/Data_Preparation_Overview)

* Intelligent Agent configuration has been completed. For details, see[Overview of Creation and Configuration Procedures](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures)


<span id="8e67646b"></span>
# Configure analysis tasks

<span id="adbe7140"></span>
## Entry point


1. After logging in to the [BytePlus DataAgent - Analysis Agent page](https://console.volcengine.com/api/abi/bi/datawind/data-agent/analytics-agent?region=cn-beijing#/agentManage/index?appId=20050879&region=cn-beijing) with your account and password, select the published Intelligent Agent on the left side of the page to enter the conversation page and experience the data query feature.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/317002d4269a45c591b6a1ec280ae8ef~tplv-goo7wpa0wc-image.image) </span>

2. After entering the intelligent agent conversation interface, click the function switch button below the dialog box to switch to the "Deep Research" functionality.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ab44ed190a1413bb5f61693c01c2e9a~tplv-goo7wpa0wc-image.image) </span>

3. Test questions. You can enter task prompts for deep research analysis in the question dialog box, or select a pre\-configured recommended question to submit (recommended questions for analysis scenarios are configured during intelligent agent setup).

   
   |Directly input analysis task prompts using natural language |Quickly select pre\-configured recommended questions |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/349235ec31c24f6aa7c8de2d6df8fc92~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Primary use: users can describe their in\-depth research needs directly in text to the agent. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da7c202bf8f64452ad5d4a5c09ba5806~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Recommended questions are provided below the dialog box. You can click any recommended question to ask directly.<br><br>* Recommended questions can be customized in the agent's management console. |
   

4. Deep research.

   When conducting deep research analysis, it is recommended to organize the analysis scenarios first, refer to the sections above to test questions for each scenario, consolidate the requirements for analysis task thinking, report generation, and business knowledge involved in the analysis process, then upload them as knowledge for the intelligent agent for actual analysis use. For details, see the **Plan and configure analysis task knowledge** section below.


<span id="27edd20b"></span>
## Optimization key: Analysis task knowledge

<span id="a5eb0e97"></span>
### Testing and consolidation


* Before writing analysis task prompts, it is recommended to organize the main analysis elements to improve writing efficiency. It is recommended to organize analysis elements using the following approach: clarify analysis objectives \> identify analysis objects \> clarify analysis methods \> clarify output requirements.

* For complex analysis scenarios, it is recommended to separately plan, test, and consolidate business knowledge, analysis templates, and analysis report requirements.

   
   |Categories |Purpose |Key content points |
   |---|---|---|
   |Business knowledge |Essential background knowledge and definitions for daily business operations, helping the model interpret data more accurately.<br><br>For example: indicator definition explanations, activity event configurations, business process specifications. ||
   |Analysis templates |Standard analytical approaches or steps for similar business issues, used to guide the model in breaking down problems.<br><br>For example: order volume fluctuations → analyze causes step by step by channel, user type, and time distribution. |* Pay attention to formatting standards:<br><br>   * It is recommended to use Markdown format for writing, which facilitates model understanding.<br><br>   * Organize the corresponding knowledge structure using nested chapter hierarchies based on Markdown format.<br><br>* Clarify content requirements:<br><br>   * Specify the indicator calculation definitions and complete data retrieval logic for each segmented analysis scenario<br><br>   * The template must be sufficiently general to support analysis of multiple related business scenarios. |
   |Analysis reports |Completed business analysis results, including historical data, conclusions, and insights, for reuse and reference.<br><br>For example: analysis report on marketing campaign effectiveness for the previous quarter. ||
   


<span id="9698a330"></span>
### Upload knowledge

After completing the consolidation of relevant knowledge, you can upload the knowledge to the intelligent agent. For details, see [Knowledge Document Configuration](https://docs.byteplus.com/docs/dataagent/Knowledge_Document_Configuration).

<span id="786c31b3"></span>
### Limitations and cautions

To achieve better deep research results and experience, please ensure your configuration and usage meet the following requirements.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using in\-depth analysis, data query capabilities are typically involved. Therefore, attention must also be paid to the restriction requirements in the "Intelligent Query Limitations" section. For details, see <a href="https://docs.byteplus.com/docs/dataagent/Intelligent_Analysis_Agent_Overview#93082850">Intelligent query limitations</a>.</div>



|Sub\-item |Detailed description of restriction requirements |
|---|---|
|Character count of analysis template |The character count of an analysis template must not exceed 2,000. |


<span id="83fa315e"></span>
## Optimization key: Data source quality assurance

Most deep research scenarios also involve data query capabilities, so you must also ensure the quality of the intelligent agent's datasets, including ETL governance before adding datasets, semantic model and dataset knowledge configuration after adding datasets, and other related configurations.

<span id="7f7e6450"></span>
## Analysis capability expansion: MCP service

The Intelligent Analysis Agent supports MCP service management functionality. You can use this feature to integrate and manage external MCP services, expanding the data acquisition scope of DataAgent (typically external data, such as online searches, third\-party platform data, and more) and enhancing analysis capabilities (to improve the agent's data analysis abilities, such as attribution, prediction, and so on).


* To strengthen analysis capabilities during deep research tasks, you can also add the corresponding MCP service and invoke the relevant tools.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d1833c882ec40699ac4b18d739396e6~tplv-goo7wpa0wc-image.image) </span>

* You can then flexibly use the corresponding tools during subsequent deep research tasks.


<span id="2a6ae2dc"></span>
# Model analysis process

<span id="b9c50bb1"></span>
## **Reasoning and planning analysis outline**

When performing deep research tasks, the large model automatically queries relevant data and knowledge, plans the analysis task schedule, and executes queries and analyses step by step according to the planned process. During task execution, you can view the current reasoning, the progress of the analysis plan, and detailed information in the interface.


* Users can directly describe their data query requirements to the agent in text form.

   * For example: "Help me analyze the characteristics of the provinces with the highest GDP."

* The agent does not require you to select a dataset for queries; it automatically queries data from the datasets configured for the agent.


<span id="7cae463a"></span>
## **Decompose and execute analysis tasks**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4aeb5995cf8468387d621ecaa28d9d3~tplv-goo7wpa0wc-image.image) </span>


* The agent automatically invokes the dataset SQL query tool to perform data queries.

* Supports intelligent generation of Python code for data insight and analysis.


<span id="17a2bee2"></span>
## Retrospective execution process

After completing a deep analysis task, you can retrospectively review the analysis process for each sub\-step in the execution steps.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afbdc2039ba84601987906aaecd00a8a~tplv-goo7wpa0wc-image.image) </span>

<span id="e9651e28"></span>
## Step intervention

The Intelligent Analysis Agent supports step intervention functionality. When using the agent's deep research features, you can intervene in specific sub\-analysis steps while the model plans and sequentially executes the steps.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When intervening in a particular step, simultaneous intervention in other steps is not supported.</div>



* You can intervene in steps during the report generation process. In this scenario, by default, this step and all subsequent steps will be reanalyzed.

* It is also possible to adjust the analysis steps during the analysis process after the report is generated and reanalyze the


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9efddc36ae534d639ba5b403e29d3032~tplv-goo7wpa0wc-image.image) </span>

In this scenario:


* You need to manually configure whether to synchronize adjustments to subsequent steps.

* If there is no need to synchronize adjustments to subsequent steps and only the current step is adjusted, after completing the intervention adjustment for the step, you need to manually click the "Regenerate" button to merge the adjusted analysis step content back into the analysis report.


<span id="5c38789c"></span>
# **Generate a deep research report**

<span id="5254b701"></span>
## View report results


* The current agent will generate reports for you in both document format and web format. The current web version of the report offers a more visually appealing and richer style. It is recommended to prioritize using the web version of the report.

   
   |Document format report |Web format report |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca51d84b5a394ce28c821e3a202b8722~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1ba4664922f426d8a93876f8c97a2e0~tplv-goo7wpa0wc-image.image) </span> |
   

* The structure of the report content will be organized with reference to the analysis report\-related knowledge you provide, and key analytical conclusions in the content will be annotated with citation information for the data sources.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fa717c70dfe457e904d1059f3b8dc78~tplv-goo7wpa0wc-image.image) </span>

<span id="02f08287"></span>
## Edit and modify the report

The intelligent analysis agent supports editing and modifying the web version of the report, including adjusting textual descriptions and dynamic charts within the report.


* Edit entry

   Click the "Edit" button at the top of the web version of the report to start editing the report.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25331fe8008a46cdbd190f20472881c7~tplv-goo7wpa0wc-image.image) </span>


* Edit and modify the report

   
   |Edit text content in the report |Adjust dynamic charts in the report |
   |---|---|
   |After entering edit mode, editing and modifying the text content in the report is currently supported.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30f267f7c2184ffdac735734a149bd41~tplv-goo7wpa0wc-image.image) </span><br><br>The text descriptions in the report can be adjusted as needed. |After entering edit mode, flexible adjustment of dynamic charts in the report is currently supported.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1966b98623d4d8da5406274531bf252~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Hover the mouse over a dynamic chart to make simple adjustments and modifications to the chart using natural language descriptions.<br><br>* Adjusted charts support one\-click restoration to the initial version.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only dynamic charts support such adjustments. For static charts, only deletion is supported; direct editing and modification are not supported.</div><br> |
   

* Historical versions and recovery

   
   |View report versions after editing the report |Restore the report to a historical version |
   |---|---|
   |After editing and saving the report, an "Edited" prompt appears next to the report on the left. At the same time, historical versions of the report can be viewed in the "Edit" dropdown at the top of the report.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1fae393865a407bb9ae3acf1f849dca~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, up to three versions of the report can be retained: the initial report, the latest version, and the last saved version.</div><br> |Click a report version to view the content of the corresponding version. To restore the content of this version, click the "Restore this historical version" button at the top.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30f267f7c2184ffdac735734a149bd41~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="3741805c"></span>
## Copy, export, and share the report

After the report is generated, you can click the copy, export, and share buttons in the upper right corner of the report to copy, export, or share the report.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32e8cb1a32d54814a8a66ab34bc5b609~tplv-goo7wpa0wc-image.image) </span>


* Before exporting the web version of the report to a Lark document, you need to complete the integration configuration between the intelligent analysis agent and the Lark application, as well as the matching configuration for the Lark account.


<span id="3a927f37"></span>
# Openness statement

Currently, the deep research feature and analysis result reports can be accessed via OpenAPI, Web JS SDK, and other methods. For openness capabilities, please refer to [Intelligent Analysis Agent Openness Overview](https://docs.byteplus.com/docs/dataagent/Intelligent_Analysis_Agent_Openness_Overview).

<span id="a84d9d74"></span>
# Special statement

(1) All content output by this service is generated by artificial intelligence models.

(2) Applicable users for this functionality: It is limited to customers for internal use, their own business operations, and for their own use. Customers are not permitted to provide generative artificial intelligence services to the public through the AI agent.

(3) This product supports both SaaS and on\-premises deployment versions. To purchase or request a trial, please contact the sales staff for consultation.
