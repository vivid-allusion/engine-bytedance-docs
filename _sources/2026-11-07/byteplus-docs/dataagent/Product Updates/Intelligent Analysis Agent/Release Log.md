---
title: "Release Log"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Release_Log"
---

<span id="69255f35"></span>
# March 5, 2026

<span id="48a121a8"></span>
## Admin console


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|Agent configuration |Optimization |Optimized the question record function in the agent configuration audit module. Supports switching and viewing the list by mode, and allows users to select and view process and result details in different modes.<br><br>For more usage instructions, see the [Audit](https://docs.byteplus.com/docs/dataagent/Audit) operation documentation. |


<span id="cdb3469e"></span>
## General


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|OpenAPI |New |Added BytePlus TOP gateway invocation method, providing higher authentication security and refined rate limit control; currently supports the Smart query interface and only provides streaming results. |


<span id="6b7dceb8"></span>
# February 4, 2026

<span id="fcf1e5f6"></span>
## Deep research


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|Free Q&A |Optimization |When performing free Q&A, inserting a chart link directly in the dialog box will display both the chart link and the corresponding dataset link, allowing users to retain the required resources as needed. |
|OpenAPI |New |* Added support for the `exportConfig` parameter. Deep research reports obtained via OpenAPI now support downloading PDF, images, and raw data.<br><br>* Added support for multiple parameters:<br><br>   * `mcpConfig`, `OpenApiMcpConfig`, `RegisteredMcpServer`, `McpTool`: Used for MCP service invocation.<br><br>   * `sessionName`: Used to set the session name.<br><br>   * `enableAgentDataSet`: Sets whether to use the domain\-specific agent's dataset.<br><br>   * `enableDeepThinkingMode`: Sets deep research mode.<br><br><br>For more OpenAPI parameter descriptions, see [Execute Deep Research Task](https://docs.byteplus.com/docs/dataagent/Execute_Deep_Research_Task). |


<span id="62395439"></span>
## Insight report


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|Insight report |New |Supports sharing insight reports with specified users, and allows sharing reports by specifying users or copying links.<br><br>Operation path: "Agent usage" \- "Insight report"<br><br><br>* Specified users<br><br>* Copy link<br><br><br>For more configuration instructions on insight reports, see [Insight Report](https://docs.byteplus.com/docs/dataagent/Insight_Report). |


<span id="ed916a0c"></span>
## Admin console


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|Management console |New |Added support for copying the Demo agent. Users can log in to the intelligent analysis agent using their primary account or IAM sub\-account. By copying the Demo agent, users can reuse built\-in agents in the system, quickly experience the full product capabilities, and access the complete set of features, including agent configuration, dataset creation, knowledge base configuration, setting recommended questions, and generating in\-depth research reports.<br><br>Operation path: "Agent configuration" \- "Copy DEMO agent"<br><br>For more instructions on template rooms, see [Guide to Experiencing the Intelligent Analysis Agent Sample Room](https://docs.byteplus.com/docs/dataagent/Guide_to_Experiencing_the_Intelligent_Analysis_Agent_Sample_Room). |
|Dataset configuration |Optimization |The dataset configuration page has improved the guidance messages on the add dataset page and the display of dataset initialization status.<br><br>Operation path: "Agent configuration" \- "Data source configuration" \- "Dataset"<br><br><br>* New prompts on the interface explain the permissions and types of datasets that can be added.<br><br>* In the dataset list, the initialization status column prompts have been optimized to provide operation guidance for different statuses.<br><br>   After initialization is complete, you can click the "Completed" status name to go to the initialization configuration page, view the details of the initialization configuration, and configure vectorization.<br><br>* Removed the "Enable DataAgent analysis capability" button from the data preparation interface. You can now enable or disable this feature directly on the agent dataset initialization configuration page.<br><br>* For more instructions on dataset configuration, see [Data Preparation Overview](https://docs.byteplus.com/docs/dataagent/Data_Preparation_Overview). |
|System settings |Optimization |Added a switch for "Allow download/copy data", which is enabled by default and can be disabled.<br><br><br>* When enabled, users can download or copy the results of Intelligent Query and in\-depth research.<br><br>* When disabled, the download button is not displayed for any item in the system, and it is not possible to copy or download the results of Smart Q&A or in\-depth research.<br><br><br>Operation path: "System management" \- "System settings" \- "Copy and download" |


<span id="20b59a38"></span>
## General


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|OpenAPI |Optimization |The HiAgent interface is enabled by default. When users connect the Smart Analysis Agent to HiAgent, there is no need to contact the Smart Analysis Agent team to enable it. |


<span id="dcb73f5f"></span>
# December 31, 2025

<span id="ca58520b"></span>
## Insight report


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|Report variables |Optimization |The logic for deleting variables after binding has been optimized. After a variable is deleted, the corresponding variable in the template will also be deleted.<br><br>For more information about configuring report variables, see [Insight Report](https://docs.byteplus.com/docs/dataagent/Insight_Report). |


<span id="63f7df5c"></span>
## Admin console


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|Content configuration |New |The Lark card proactive push feature now supports enabling MCP services via JSON scripts and integrating analysis tools. Example of push effect<br><br><br>* Operation path: "Agent backend" \- "Content configuration" \- "Lark terminal"<br><br>* For operation guidance, see [Proactive push](https://docs.byteplus.com/docs/dataagent/Content_Configuration#1c4fff2a). |


<span id="97992cff"></span>
# December 22, 2025

<span id="accbb0e2"></span>
## Deep research


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|Analysis steps |New |Added support for manual intervention in analysis steps. When using the in\-depth research feature of the agent, it is now possible to manually intervene in specific analysis steps during the execution process planned by the model.<br><br><br>* You can intervene in steps during report generation. When adjusting analysis steps during report generation, by default, this step and all subsequent steps will be adjusted.<br><br>* It is also possible to adjust analysis steps after the report is generated and re\-analyze the report.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about step intervention features in Deep Research, see <a href="https://docs.byteplus.com/docs/dataagent/Deep_Research_Agent#e9651e28">Step intervention</a>.</div><br> |
|Analysis report |Optimization |Added support for editing web\-based reports, including adjusting text descriptions and dynamic charts in the report.<br><br>For more information about editing and modifying web\-based reports, see [Edit and modify the report](https://docs.byteplus.com/docs/dataagent/Deep_Research_Agent#02f08287). |


<span id="08f8b6e3"></span>
## General


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|General |Optimization |When using the Intelligent Analysis Agent, if model invocation is rate\-limited, the interface will display a prompt such as "The current limit has been exceeded. Please try again later." If you see this prompt, it means that the agent is currently processing a large number of tasks. You may try again later according to the optimization suggestions. |


<span id="ae613ad4"></span>
# December 11, 2025

<span id="7fa751e3"></span>
## Insight report


|**Product modules** |**Update types** |**Update descriptions** |
|---|---|---|
|Report template editing |Optimization |The Insight Report Templates have added the "Set as reference" and archiving capabilities.<br><br><br>* Set as reference: You can set modules from Insight Report Templates that have been tested and found to be of high quality as "memory samples" to serve as reference samples for subsequent reports. When generating content for other reports, the structure and analytical logic of the "memory sample" report will be referenced, which can improve the quality of generated reports.<br><br>   For more information about the set as reference feature, see [Set reference results](https://docs.byteplus.com/docs/dataagent/Insight_Report#b911ec7c).<br><br>* Archiving capability: This provides multi\-version management for Insight Report Templates. You can archive report templates, and after archiving, you can view each version of the Insight Report Template in "History Archive". |
||Optimization |The global variable functionality of Insight Reports has been upgraded.<br><br><br>* Support for date\-type global variables has been added.<br><br>* Variables can now be bound to DataWind visualization chart filters. After binding, when referencing DataWind visualization charts during the analysis report generation process, you can filter visualization chart data based on the variable values, and use the filtered data as the data source for the analysis report.<br><br><br>For more information about the variable functionality of Insight Reports, see [Configure and use report variables](https://docs.byteplus.com/docs/dataagent/Insight_Report#37239518). |


<span id="b90aac2e"></span>
## Smart query


|**Product modules** |**Update types** |**Update descriptions** |
|---|---|---|
|Wenshu \- Intent clarification |Optimization |Added the ability to manually stop the clarification process when intent clarification interaction is triggered during the Wenshu process. |
|OpenAPI<br><br>(New version) |Added |Smart Query provides you with the new version of the OpenAPI interface. The capabilities of the new OpenAPI interface are generally aligned with those of the Smart Query interface, allowing you to query data more flexibly through the interface.<br><br>For more information about the new version of OpenAPI, see [Intelligent Data Query API Description and Common Parameters (new version)](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_API_Description_and_Common_Parameters_new_version). |
|OpenAPI<br><br>(old version) |Optimization |The old version of the Smart Query OpenAPI interface now supports specifying a dataset for data queries in a query request using the dataset parameter (dataSetId). For details, see [Intelligent Data Query for Lark Client](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_for_Lark_Client) and [Intelligent Data Query for PC](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_for_PC). |


<span id="e83cf75c"></span>
## Deep research


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|Analysis process |Optimization |In the analysis process of Deep Research, you can now directly switch pages to view **the actual executed SQL**. When you need to trace and troubleshoot data results in a Deep Research report, this feature further improves the efficiency of identifying SQL issues. |
|Analysis report |Optimization |An exception prompt for model calls exceeding the token limit has been added to the web version of the analysis report. When using the Deep Research feature, if a model call exceeds the token limit during use, some content in the analysis report may be missing. If you see such a prompt, you can follow the optimization suggestions to adjust your query and regenerate the analysis report. |


<span id="9b025468"></span>
# November 26, 2025

<span id="e9fd2964"></span>
## Admin console


|**Feature module** |**Update description** |
|---|---|
|MCP service management |New MCP service access and management capabilities have been added. You can use this feature to access and manage external MCP services, expanding DataAgent's data acquisition scope (typically external data, such as online search, third\-party platform data, and more) and analysis capabilities (to enhance the data analysis capabilities of intelligent agents, such as attribution, prediction, and so on).<br><br>The Intelligent Analysis Agent provides both system\-level and agent\-level MCP access capabilities:<br><br><br>* Agent\-level: MCP services available only to the current intelligent agent.<br><br>* System\-level: MCP services available to all intelligent agents, and only system administrators can add them.<br><br><br>After integrating the MCP service, when using features such as deep research and insight reports, the large model will determine whether to invoke the MCP service based on your question and the MCP service configuration results, in order to further improve the quality of analysis results.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The current intelligent question count feature does not support the use of integrated MCP service capabilities.</div><br> |
|Basic information |Added a configuration switch to enable the time engineering feature.<br><br>When using the agent in the future, if the question description involves relative time expressions:<br><br><br>* When this switch is turned on (default), the large model will extract the time range from the question description, and the specific time range will be calculated by the code engineering module. This approach can improve the accuracy of time range\-related calculation results in most scenarios.<br><br>* When this switch is turned off, both extraction and calculation of the time range are performed by the large model.<br><br><br>For more information about basic information configuration, see [Basic Information Configuration](https://docs.byteplus.com/docs/dataagent/Basic_Information_Configuration). |
|Basic information |Added a configuration switch for "user\-visible mode". Here, administrators can configure the scope of detailed features displayed to end users by the agent.<br><br><br>* The configuration results only apply to end users of the agent; administrator accounts can see entry points for all purchased features of the agent.<br><br>* At least one feature option must be selected from intelligent Q&A, deep research, or insight reports; otherwise, the configuration cannot be saved.<br><br><br>For details, see [Basic Information Configuration](https://docs.byteplus.com/docs/dataagent/Basic_Information_Configuration). |


<span id="a600b604"></span>
## Smart query


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|General |Performance optimization |Optimized the overall performance of intelligent Q&A. After optimization, the total time for data queries is reduced, and page display during Q&A execution is smoother. |


<span id="e60e1c2e"></span>
## Deep research


|**Product module** |**Update type** |**Update description** |
|---|---|---|
|OpenAPI |Optimization |For deep research task execution, OpenAPI now supports a switch parameter for whether to return the reasoning process: `enableRunningStepOutput`. The default is false, which means the reasoning process is not returned. For more information about executing deep research tasks with OpenAPI, see [Execute Deep Research Task](https://docs.byteplus.com/docs/dataagent/Execute_Deep_Research_Task). |
|Deep research report |Optimization |Added support for exporting reports in HTML format to Lark cloud documents.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To use this feature, you must first complete the integration configuration between the Intelligent Analysis Agent and Lark (Chinese enterprise collaboration platform), and finish the account matching configuration for Lark.</div><br> |


<span id="a50b469b"></span>
# November 12, 2025

<span id="663a51e7"></span>
## Admin console


|**Feature modules** |**Update description** |
|---|---|
|Basic information |Added the "Enable chart analysis" switch and the "Enable multi\-path execution" switch in the basic information configuration of the agent.<br><br><br>* After turning on the "Enable chart analysis" switch, the agent will analyze the charts of the query results synchronously during data queries. When returning the agent's answer, the interpretation of the chart will be displayed synchronously below the query result chart.<br><br>* After turning on the "Enable multi\-path execution" switch, during the intelligent query phase, the agent will execute multiple times in parallel (default is 3 times) to ensure result stability. This also incurs performance costs for the agent, such as increased token consumption, approximately tripled parallel load, and longer data query times.<br><br><br>For more guidance on configuring basic information, please refer to [Basic Information Configuration](https://docs.byteplus.com/docs/dataagent/Basic_Information_Configuration). |
|Data source configuration |Added support for importing semantic models and knowledge base configurations of datasets from other agents.<br><br><br>* Only users with administrator permissions can perform import operations.<br><br>* If the imported dataset's semantic model contains fields identical to those in the current dataset's semantic model, the imported semantic model will overwrite the existing configuration for those fields.<br><br><br>For more guidance on importing semantic models and knowledge base configurations of datasets, please refer to [Import semantic models and knowledge bases from other agents](https://docs.byteplus.com/docs/dataagent/Dataset_Configuration#38d512e8). |
|Prompt configuration |Added support for importing prompts already added from other agents. |


<span id="b9baf30b"></span>
## Smart query


|**Product modules** |**Update type** |**Update description** |
|---|---|---|
|OpenAPI |Optimization |The Intelligent Query OpenAPI adds a request parameter for whether to enable chart analysis: `enableAnalysis`. For details, please refer to [Intelligent Data Query for Lark Client](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_for_Lark_Client) and [Intelligent Data Query for PC](https://docs.byteplus.com/docs/dataagent/Intelligent_Data_Query_for_PC). |


<span id="07d296b1"></span>
# November 4, 2025

<span id="08931cad"></span>
## Insight report (first launch, in phased rollout)


|**Product modules** |**Update description** |
|---|---|
|Insight report |The Insight Report feature of the intelligent analysis Agent is now available for the first time. The Insight Report is the latest core capability introduced by DataAgent. To perform data analysis for **routine analysis scenarios (such as daily, weekly, and monthly reports)**  in your business, and to automatically generate stable and reliable analysis reports using large models based on existing datasets or **dashboard charts**, the Insight Report feature is your ideal choice.<br><br>The current version allows users to freely drag and combine multiple functional modules to build the report framework, mainly including the following three modules:<br><br><br>* **Text block:**  Supports rich text editing and is used for writing fixed content such as analysis background, summary of conclusions, and data scope descriptions.<br><br>* **AI analysis:**  The core analysis unit of the report. Requires binding a data source (dataset/chart) and entering analysis instructions, with the large model outputting specific analysis conclusions and insights.<br><br>* **AI summary:**  Based on natural language instructions, performs secondary summarization, extraction, or comparison of the content generated in the text block and AI analysis modules to form the final conclusion.<br><br><br>For more information and usage details about the Insight Report, please refer to [Insight Report](https://docs.byteplus.com/docs/dataagent/Insight_Report). |


<span id="b61ee7fb"></span>
## Smart query


|**Functional modules** |**Update description** |
|---|---|
|Intent clarification |After configuring intent clarification in the management console, the interaction experience for intent clarification in smart query scenarios with unclear intent has been optimized.<br><br>The current intelligent agent will intelligently identify questions with unclear intent and provide a confirmation selection box for further clarification. You can make selections in the interface to further specify the question intent. |
|Specify dataset |When using smart query, newly added support allows specifying a dataset to further clarify the scope of data queries, which can greatly improve the accuracy of smart query results.<br><br>As shown in the figure above, you can select the dataset range for this query in the dataset dropdown list. You can also quickly search for datasets by dataset name or dataset ID. |


<span id="4601a790"></span>
## Admin console


|**Module** |**Update details** |
|---|---|
|Knowledge settings |Added support for manually configuring knowledge categories. Previously, only automatic parsing and labeling of uploaded knowledge by the agent was supported. With manual configuration of category tags, knowledge can now be categorized more precisely.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Knowledge categories mainly include: business knowledge, analysis templates, and analysis reports. In privatized scenarios, the analysis report knowledge type is disabled by default. To use it, contact BytePlus technical support to enable the feature switch. Knowledge previously labeled as "analysis report" type will be converted to "business knowledge" type.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more examples of knowledge configuration and usage, see <a href="https://docs.byteplus.com/docs/dataagent/Knowledge_Document_Configuration">Knowledge Document Configuration</a>.</div><br> |


<span id="d77b5e22"></span>
## Deep research


|**Module** |**Update details** |
|---|---|
|Detailed research report |Added support for making local adjustments to generated detailed research reports.<br><br>As shown in the figure above, you can hover the mouse over a chart in the detailed research report to adjust the chart. Simple modifications can be made to the chart using natural language descriptions. |
|OpenAPI |The OpenAPI request parameters for detailed research reports now support the html_id parameter, making it easier to hide unnecessary page header information when calling OpenAPI to obtain research reports. For more information about using OpenAPI, see [Execute Deep Research Task](https://docs.byteplus.com/docs/dataagent/Execute_Deep_Research_Task). |
|General updates |The interface experience for the detailed research feature has been optimized, with a focus on improving the display and demonstration of the detailed research analysis process and the report presentation style in document format, enhancing the report reading experience. |


<span id="e8eb2fd7"></span>
# October 23, 2025

<span id="0283589f"></span>
## Admin console & Smart query


|**Module** |**Update details** |
|---|---|
|Data source and chart configuration<br><br>Currently in grayscale testing; application required for access |When using the Intelligent Data Insight (DataWind) product together with the intelligent analysis agent, you can now add visual charts saved in DataWind as data sources for the agent.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62e10097670249d99499223a102c658e~tplv-goo7wpa0wc-image.image) </span><br><br>Currently, only charts you have permission to access can be added. When adding a chart, you can configure the chart description, sample questions, and other settings for the current chart. After completing the configuration, when using intelligent Q&A for data queries, if the query is related to the chart's data or the question matches the chart's sample questions, the intelligent analysis Agent will return the corresponding chart. By connecting relatively specific charts, query accuracy can be further improved, user experience enhanced, data sources expanded, and configuration efficiency increased.<br><br><br>* You can directly filter, sort, and perform other operations on charts in the results returned by intelligent Q&A.<br><br>* You can click the navigation button in the upper left corner of the chart to quickly jump to the chart editing page and view more chart details.<br><br>* You can hover the mouse over the dataset name below the chart to view the dataset details for the current chart.<br><br><br>For more information on configuring and using chart data sources, see [Content Configuration](https://docs.byteplus.com/docs/dataagent/Content_Configuration). |
|Audit configuration |Audit functionality enhancements allow you to view more usage record data. |


<span id="b3bba11c"></span>
# September 30, 2025

<span id="e92608ef"></span>
## Admin console


|**Feature modules** |**Update description** |
|---|---|
|Intent clarification (phased release) |The intelligent analysis Agent now supports intent clarification configuration capabilities.<br><br>By configuring intent clarification rules for the intelligent analysis Agent, when using the agent in the future, the intelligent analysis Agent will automatically determine whether the user's intent is clear based on the match between the user's input and the intent clarification rules. For ambiguous questions, it will ask follow\-up questions for clarification, thereby improving the agent's understanding and response accuracy.<br><br>This feature is currently in phased release and not fully available online. To use this feature, contact BytePlus technical support. For more details about intent clarification configuration, see [Intent Clarification Configuration (in limited release)](https://docs.byteplus.com/docs/dataagent/Intent_Clarification_Configuration_in_limited_release). |
|Prompt configuration |Prompt configuration now supports configuring the application scenarios for prompts.<br><br>The currently supported scenarios include: general, web page generation, and multi\-table association. For more operational guidance on prompt configuration, see [Prompt Configuration](https://docs.byteplus.com/docs/dataagent/Prompt_Configuration). |


<span id="8335b699"></span>
## Openness and integration


|**Feature modules** |**Update description** |
|---|---|
|OpenAPI |Now supports OpenAPI related to in\-depth research. For details, see [Deep Research API Description and Common Parameters](https://docs.byteplus.com/docs/dataagent/Deep_Research_API_Description_and_Common_Parameters). |


<span id="2b435208"></span>
# September 15, 2025

<span id="4452e137"></span>
## General


|**Feature modules** |**Update description** |
|---|---|
|Agent backend \- supports searching dataset IDs |In the new version, the dataset configuration module in the agent backend supports searching dataset IDs and viewing dataset configuration status.<br><br><br>* Operation path: "Agent backend" \- "Dataset configuration" \- "Add dataset" |
|Agent backend \- adds first\-use mode option |In the new version, the basic information module in the agent backend allows users to set the agent's first\-use mode to in\-depth research or intelligent query. After configuration, when a user uses the current agent for the first time, the default mode will be the mode configured by the administrator. When the user subsequently uses the agent, the mode last used by the user for this agent will be remembered.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This option is enabled only when the agent has Deep Research capabilities; the default option is Deep Research.</div><br><br><br><br>* Operation path: "Agent backend" \- "Basic information" \- "First\-use mode" |
|Agent backend \- supports configuring Lark welcome cards and proactive push |In the new version, the content configuration module in the agent backend supports configuring Lark welcome cards and proactive push.<br><br><br>* Operation path: "Agent backend" \- "Content configuration" \- "Lark"<br><br>   * Welcome card: The welcome card is the welcome interface that users see when they access the agent via Lark for the first time. It is typically used to briefly introduce the agent's main features and how to use the agent. Supports rapid import of card styles designed in the Lark card builder tool using JSON code, helping users understand intelligent agents in a more intuitive and user\-friendly way, and improving the initial onboarding experience.<br><br>   * Active push: The active push feature allows you to use the Lark platform to send specified content summaries or notifications to target users periodically or according to specific rules. You can configure the push title, content description, push frequency, and recipient range, and preview the effect before sending to ensure the accuracy and clarity of the push information, thereby improving the efficiency and experience of user reach. |
|Intelligent agent usage \- supports filtering conversation records by agent and mode |In the new version, you can filter conversation records by intelligent agent and mode to precisely locate target conversation records, significantly improving the efficiency of retrieving and managing historical conversations and facilitating analysis and review of intelligent agent usage.<br><br><br>* Operation path: "Intelligent agent usage" \- "Conversation records" \- "View all" |
|Intelligent agent list \- new general intelligent agent card |In the new version, a DataAgent general intelligent agent card has been added to the intelligent agent list page, allowing users to perform agent configuration, deactivation, publishing, deletion, and other operations on general intelligent agents, while also optimizing the general agent icon.<br><br><br>* Operation path: "Intelligent agent list" \- "Data Agent general" |


<span id="a3499450"></span>
## Data Query Agent\-related

None

<span id="391bff93"></span>
## Deep research Agent\-related


|**Feature modules** |**Update description** |
|---|---|
|Research reports support users in sharing links, copying content, exporting content, and directly sharing with other DataAgent users |In the new version, for document\-type research reports generated by the Deep Research Agent, users can copy report links, copy report content, export report content (PDF, images, raw data), and share reports with other users. Web\-type reports do not support copying report content.<br><br><br>* Operation path: "Intelligent agent usage" \- "Deep research"<br><br>   * Document type<br><br>   * Web type |


<span id="5a1d1bee"></span>
# June 9, 2025 First release

<span id="673c4f33"></span>
## General


|**Feature modules** |**Update description** |
|---|---|
|Launch general DataAgent |In the new version, the DataAgent module has been added. This module requires no user configuration and allows users to upload files to directly experience deep research functionality. It also supports the "online search" feature.<br><br><br>* Operation path: "Agent usage" \- "Data Agent"<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a0a76c1166d47029919eae684814885~tplv-goo7wpa0wc-image.image) </span> |
|Optimizing the management console entry |In the new version, a management console entry has been added to the agent usage page, making it easier for users to manage all agents. Clicking the entry takes users to the "Agent list" page.<br><br><br>* Operation path: "Agent usage" \- "Management console"<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0eab9623a08f45c0960e129521441126~tplv-goo7wpa0wc-image.image) </span> |
|Optimizing the agent settings entry |In the new version, an agent settings entry has been added to the agent usage page, making it easier for users to configure agents. Clicking the entry takes users to the "Agent configuration" page.<br><br><br>* Operation path: "Agent usage" \- "Agent settings" |
|Support for optimized dataset configuration |In the new version, the dataset configuration module allows users to download a question template, fill it out, and upload it. The system will automatically provide dataset configuration recommendations based on the questions, helping users quickly configure datasets relevant to their questions.<br><br><br>* Operation path: "Agent configuration" \- "Dataset configuration" \- "Optimize dataset configuration" |


<span id="8b6ada14"></span>
## Data Query Agent\-related


|**Feature modules** |**Update description** |
|---|---|
|Support for attribution analysis |In the new version, the data query Agent module supports "attribution analysis" for intelligent query results. The agent can perform time series analysis on influencing factors of abnormal metrics, displaying the top three influencing factors with the highest positive and negative contributions, their corresponding contribution values, contribution rates, comparison differences, and comparison percentages, enabling intelligent attribution.<br><br><br>* Operation path: "Agent usage" \- "Intelligent query" \- "Reply" \- "Attribution analysis" |
|Support for question modification suggestions |In the new version, the data query Agent module automatically provides modification suggestions for users' questions, helping users refine their queries to obtain more accurate data query results.<br><br><br>* Operation path: "Agent usage" \- "Intelligent query" \- "Question" \- "Modification suggestions" |
|Support for favoriting questions |In the new version, the Data Query Agent module supports saving intelligent query results as favorites, helping users quickly reuse them. Saved results will be displayed in the "Favorites chart" below the dialog box, and users can ask AI follow\-up questions or remove items from favorites.<br><br><br>* Operation path: "Agent usage" \- "Reply" \- "Favorite" |
|Support for summary cards |In the new version, the Data Query Agent module supports configuring summary cards on the PC, enabling users to quickly view important data. The configured summary cards will be displayed in the "Favorites chart" \- "Today's summary" below the dialog box.<br><br><br>* Operation path: "Agent list" \- "Agent configuration" \- "Content configuration" \- "PC" |


<span id="ae0895ad"></span>
## Deep research Agent\-related


|**Feature modules** |**Update description** |
|---|---|
|Launch of Deep Research Agent |In the new version, the Deep Research Agent module has been added, providing core intelligent analysis capabilities. Based on the Data Query Agent for interaction, it integrates the deep reasoning capabilities of large models to help users generate in\-depth research reports and achieve intelligent transformation from raw data to business insights. Users can switch between the "Intelligent query" and "Deep research" features in the agent conversation interface.<br><br><br>* Operation path: "Agent usage" \- "Deep research" |
|Support for online search |In the new version, the Deep Research Agent module introduces an online search feature. By accessing the latest data sources from the internet in real time and combining the analytical and reasoning capabilities of large models, it enables full\-process automation, including dynamic information acquisition, intelligent strategy planning, multi\-source data integration, and structured report generation.<br><br><br>* Operation path: "Agent usage" \- "Deep research" \- "Online search" |
|Support for enterprise knowledge engine |In the new version, the Data Query Agent module supports saving intelligent query results as favorites, helping users quickly reuse them. Saved results will be displayed in the "Favorites chart" below the dialog box, and users can ask AI follow\-up questions or remove items from favorites.<br><br><br>* Operation path: "Agent usage" \- "Reply" \- "Favorite" |
|Support for configuring recommended analysis questions |In the new version, after conducting in\-depth research on the Agent module, users can configure recommended analysis questions in the agent content settings. Once configured, recommended questions will be provided in the Deep Research dialog box, and users can click a recommended question to ask it directly.<br><br><br>* Operation path: "Agent list" \- "Agent configuration" \- "Content configuration" |
