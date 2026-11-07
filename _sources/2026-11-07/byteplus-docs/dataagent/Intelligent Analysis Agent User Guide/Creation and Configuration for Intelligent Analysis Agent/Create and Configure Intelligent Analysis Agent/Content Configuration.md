---
title: "Content Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Content_Configuration"
---

This article provides guidance on content configuration when creating and configuring an intelligent analysis Agent.

<span id="cad15180"></span>
# Background information

The configuration content is divided into four modules: data query recommendation questions, analysis recommendation questions, PC endpoint, and Lark endpoint.


* Data query recommendation questions: Supports setting data query\-related recommendation questions for users or Lark groups.

* Analysis recommendation questions: Supports setting data analysis\-related recommendation questions.

* PC endpoint: Displays a summary message on the Agent homepage when users access the PC endpoint.

* Lark endpoint: Displays a welcome card and proactive push messages when users access the Agent bot on the Lark endpoint.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Recommended questions: Added recommended questions will be displayed in the bot's default message card. Bot users can quickly obtain the required business data through recommended questions.</div>


<span id="66c4c171"></span>
# Configure data query recommendation questions


1. Go to the Agent configuration page, select "Content configuration" on the left, and then select the data query recommendation questions configuration page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3e83f76cd5a411094cd74afd81a33e4~tplv-goo7wpa0wc-image.image) </span>


2. After entering the editing page, you first need to select a configuration method. Currently, "Unified user configuration" and "User\-specific configuration" are supported.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1acd6bbc94184d4a8fc531503c1e2926~tplv-goo7wpa0wc-image.image) </span>


* "User\-specific configuration" allows you to configure recommendation questions individually for each Agent user.

* "Unified user configuration" means all users receive the same recommendation questions.

3. Click "Add recommendation question configuration" and configure the recommendation questions in the configuration pop\-up window. Drag\-and\-drop is supported to adjust the order. The order of questions here determines the order in which recommended questions are displayed on subsequent Agent usage pages.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af2c163d31ba4ad5b84cb6462cbb6a38~tplv-goo7wpa0wc-image.image) </span>

The relevant parameter configuration instructions are as follows:


|Parameters |Configuration instructions |
|---|---|
|Configuration name |Set the configuration name for recommended questions. |
|Recommended questions \- Add fuzzy questions |* Supports configuring multiple fuzzy questions. Fuzzy questions support configuring detailed sub\-questions and associating sub\-questions with datasets.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The intelligent analysis agent also provides an intent clarification feature. When the user's question is ambiguous, the agent can ask clarifying questions based on intent clarification rules to help further specify the question. For details, see <a href="https://docs.byteplus.com/docs/dataagent/Intent_Clarification_Configuration_in_limited_release">Intent Clarification Configuration (in limited release)</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For scenarios involving data queries, it is recommended that the question include key components such as the time of the data query and filtering criteria. For details, see <a href="https://docs.byteplus.com/docs/dataagent/Best_Practices_Recommendations_and_Examples_for_Intelligent_Data_Query_Questions">Best Practices: Recommendations and Examples for Intelligent Data Query Questions</a>.   </div><br>   <br><br>   * Each sub\-question must be bound to a dataset. The intelligent agent will recall data from the dataset bound to the sub\-question to provide answers.<br><br>   * When a fuzzy question is configured with multiple sub\-questions, clicking a question will simultaneously display the query results for all sub\-questions.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3250e824f2e94527941d5e24480015b6~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Supports enabling the generalization switch for fuzzy questions.<br><br>   After configuring the decomposition approach for a question and enabling question generalization, the decomposition approach will also apply to similar questions. For example: After configuring the decomposition approach for "Analyze the sales status of each region", enabling generalization will allow the decomposition approach to be reused for "Analyze the sales status of each province/city" as well. |
|Recommended questions \- Add non\-fuzzy questions |Supports configuring multiple non\-fuzzy questions and associating non\-fuzzy questions with datasets. |


<span id="29a667b3"></span>
# Configure analysis recommendation questions

On the Agent configuration page, select "Content configuration" on the left, and then select the analysis recommendation questions configuration page. Click "Add question" and set the recommendation question and select the associated knowledge in the pop\-up parameter configuration interface. After configuration, click "Save".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a56bf277ca124382a092dc6876cf2457~tplv-goo7wpa0wc-image.image) </span>

<span id="9293cf81"></span>
# Configure the PC endpoint

Go to the Agent configuration page, select "Content configuration" on the left, and find "PC endpoint". Here, click Edit in the upper right corner to configure the copy displayed on the PC endpoint homepage. After entering the content, you can preview the display effect.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9f79c2994084f67a0a1d8235ee904ca~tplv-goo7wpa0wc-image.image) </span>

<span id="233f977c"></span>
# Configure the Lark endpoint

Users must first complete [Lark-Side Intelligent Agent Configuration and Testing](https://docs.byteplus.com/docs/dataagent/Lark-Side_Intelligent_Agent_Configuration_and_Testing) before they can access the bot configuration page. Select "Content configuration" on the left to view the "Lark client" page. Here, you can configure the Lark client welcome card and proactive push content.

<span id="eada10b0"></span>
## Welcome card

The Lark client bot welcome card is displayed to users when they use the bot for the first time. You can add an introduction to the bot.

After configuring a card in the Lark card builder tool, users can copy the JSON code here for quick setup. For Lark card configuration, see [Lark Card Overview](https://open.larkoffice.com/document/feishu-cards/feishu-card-overview).

<span id="1c4fff2a"></span>
## Proactive push

The Analysis Agent supports proactively pushing in\-depth research reports via Lark cards and supports enabling the MCP switch during push. This section describes how to set up Lark proactive push cards.

<span id="494f0c4e"></span>
### Prerequisites

To enable the MCP switch during push, ensure that the MCP switch is enabled at the system or agent level.

<span id="9dbd92c7"></span>
### Procedure


1. Go to the bot configuration page, select "Content configuration" on the left, and in the "Lark client" configuration page, locate the "Lark client proactive push settings" module. Here, you can configure proactive push notifications.

2. Click "Add push summary" to configure push parameters and schedule the summary to be sent to specified users or Lark groups. After configuration is complete, click "Save" to apply the settings.

   
   |Parameters |Configuration instructions |
   |---|---|
   |Active push card title |Customize the push card title. |
   |Push frequency |Set the push frequency and time. The intelligent assistant will start executing the task at the specified time. You can set the push frequency according to your business needs.<br><br>You can also set immediate push or push after data is ready based on your data readiness status.<br><br><br>* Immediate push: If your data readiness time is determined, you can set the time in push frequency to the data readiness time and choose to push immediately at that time. The intelligent agent will check the data readiness status and push the data immediately after it is ready.<br><br>* Push after data is ready: If your data readiness time is uncertain, you can select this option. The intelligent agent will check the data readiness status before pushing, and will query and push the data after it is ready.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the summary report fails to generate, the agent will retry once every hour, up to 24 times. Excessive retries may cause a storm, so it is strongly discouraged to set hourly push notifications.</div><br> |
   |Description |Customize the remark for this push notification; it will only be displayed on the configuration page. |
   |Push users |Set the target users for this card push. These users are sourced from the available members you configured during the integration with Lark. For configuration details, see [Step 3: Add available members for the agent](https://docs.byteplus.com/docs/dataagent/Lark-Side_Intelligent_Agent_Configuration_and_Testing#6adaaffd).<br><br>When pushing by user, the analysis Agent will generate a separate report for each user, and the report content may differ.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can choose any one of the three push methods: push to users, shared push, or push to Lark groups.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When pushing by user, since the intelligent assistant generates a report for each user individually, if you set a large number of push users, the task execution time may be longer and the time to receive the report may be delayed.</div><br> |
   |Shared push |Used to push the same report to multiple people. When using shared push, the analysis Agent will push the same report to all users you have set.<br><br>**Operation steps**:<br><br><br>1. Click "Add", search for Lark users within the target user group, then click to add them.<br><br>2. Set the permission holder; the analysis Agent will grant the target users the report permissions held by the permission holder. |
   |Push Lark group |[Recommended] Push the card to a specified Lark group.<br><br>When using Lark group push, the analysis Agent will push the same report to the Lark group you have set.<br><br>**Operation steps**:<br><br><br>1. Add the intelligent bot to the Lark group. In the upper right corner of the Lark group, click "...", click Settings, click "Group Bot", click "Add Bot", search for your intelligent bot name, and click "Add".<br><br>2. In the configuration details of the analysis Agent content configuration, under "Push Lark group", click "Add", enter the Lark group name, and select the group from the dropdown list to add it.<br><br>3. Set the permission holder; the analysis Agent will grant the users in the target Lark group the report permissions held by the permission holder.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">There are security risks when using group or team "subscription" push. Please use with caution:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When sending a "subscription push", data authentication is not performed for members of the group.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the members in the group change, the recipients of the "subscription push" will change accordingly, and new members can view the "subscription push" in historical messages.</div><br> |
   |Active push summary |Configure the JSON script. The currently recommended script is the Deep Report Summary Script. The configuration example is as follows.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When filling in, the script must be merged into a single line. The summary module for proactive push <strong>reads content line by line</strong>, so the script content must be merged into a single line to facilitate system reading.</div><br><br><br>```JSON```<br>```{"pushConfig":{"enablePushImage":true,"imageType":"html","enablePushUrl":true,"enablePushSummary":true,"customSummaryPrompt":"Summary as follows: Observation period<YYYY-mm-DD>~<YYYY-mm-DD>VS baseline period<YYYY-mm-DD>~<YYYY-mm-DD>\ n • Observation period [<indicator name>], compared with baseline period<rise/fall><indicator change value>, change rate<indicator change rate>\ n"},"questionType":"deep_research","contentParams":{},"name":"This year is 2025. \Reference cycle date and observation cycle date: two days ago vs yesterday. Specific dimension: xxx","agentConfigs":{"enabledMCPServers":[{"mcpServerName":"Attribution Tool","tools":[{"name":"dimension_attribution","selected":true},{"name":"formula_attribution","selected":false},{"name":"Formula breakdown"},{"name":"trend_detection","selected":true}]}]}}```<br><br><br>For parameter descriptions in the JSON script, see below. |
   

   The syntax and parameter description for the proactive push summary JSON script are as follows. For your convenience, line breaks and indentation are used to display the JSON script. When actually filling in the push configuration, the script content must be merged into a single line.

   ```JSON
   {
     "pushConfig": {
       "enablePushImage": true, // Does the card need to include a screenshot of the report in HTML/markdown format
       "imageType": "html", // Report screenshot format, set to markdown or html
       "enablePushUrl": true, // Does the card need to include a 'complete report' link, which can directly redirect to the report display page
       "enablePushSummary": true, // Does the card need to include a paragraph summarizing the main content of the card
       "customSummaryPrompt": "" // Used to prompt the summary content on the large model generation card
     }, // Required
     "agentConfigs": {
       "enabledMCPServers": [
         {
           "mcpServerName": "<Expand MCP name>",
           "tools": [
             { "name": "<mcp tool name>", "selected": true } // Is a tool selected
           ]
         }
       ]
     },
     "questionType": "deep_research", // Required deep_research
     "name": "<Deep Research Questions>", // Required
     "contentParams": {} // Must include
   }
   ```
   

   
   |Parameters |Configuration details |
   |---|---|
   |`pushConfig` |* `enablePushImage`: Set to `true` to display a report screenshot in the push card.<br><br>* `imageType`: Set the screenshot type; currently supports `html` or `markdown`.<br><br>* `enablePushUrl`: Set to `true` to include a link to the "full report" in the push card.<br><br>* `enablePushSummary`: Set to `true` to display an automatically generated summary description in the card.<br><br>* `customSummaryPrompt`: You can customize the prompt for the report summary to guide the large model in generating the summary content for the card, for example:<br><br>   ```JSON```<br>```   "customSummaryPrompt": "Summary as follows: Observation period<YYYY-mm-DD>~<YYYY-mm-DD>VS baseline period<YYYY-mm-DD>~<YYYY-mm-DD>\ n • Observation period [<indicator name>], compared with baseline period<rise/fall><indicator change value>, change rate<indicator change rate>\ n"```<br>```   ```<br>    |
   |`agentConfigs` |* `enabledMCPServers`: Add a new object and enter either `mcpServerName` or `mcpServerId`; either one can be used.<br><br>   * `mcpServerName`: Enter the name of the extended MCP. You can view and copy the required MCP service name in "MCP Service Management".<br><br>   * `mcpServerId`: Enter the extended MCP ID.<br><br>* `tools`：<br><br>   * In the `tool` array, enter the name of the tool to be enabled in `name`. In the agent's interface, click "Extension" to view and copy the tool name of the MCP service you are using. You can copy either the value in the red box or the yellow box in the example below.<br><br>      Multiple tools can be configured. The following is an example:<br><br>      ```JSON```<br>```      "tools": [```<br>```                { "name": "dimension_attribution", "selected": true },```<br>```                { "name": "formula_attribution", "selected": false }, // Note that this tool has not been selected```<br>```                { "name": "Formula breakdown" }, // The default value for 'selected' is' true ', so' formula disassembly 'has also been selected```<br>```                { "name": "trend_detection", "selected": true }```<br>```              ]```<br>```      ```<br>      <br><br>   * `selected`: Set to `true` to select it; the default value is true. |
   |`questionType` |The question type is fixed as `deep_research`. |
   |`name` |Enter your deep research question. If an analysis template has been configured, you can enter commonly used or periodic questions here. For details, see [Optimization key: Analysis task knowledge](https://docs.byteplus.com/docs/dataagent/Deep_Research_Agent#27edd20b). |
   |`contentParams` |Must be kept as `{}`. |
   

3. After configuration is complete, you can send a preview. Click "Send preview" to view the effect of the configured push notification.
