---
title: "Execute Deep Research Task"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Execute_Deep_Research_Task"
---

<span id="4d245389"></span>
# **Request description**

Request method: POST

Request URL: https://{domain}/dataAgent/llm/openApi/v2/deepresearch/executeTask

<span id="57da8b29"></span>
# **Request parameters**


|Position |Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|ROOT |stream |bool |Yes |False |Streaming output |
||content |string |Yes |Analyze the sales trend |Specific task to execute |
||pushNotificationconfig |PushNotificationConfig |No |Optional, see request example |Asynchronous push notification configuration |
||metadata |TaskMeataData |Yes |See request example |Task metadata |
|TaskMeataData |agentId |int |Yes |1 |Agent ID. You can view the corresponding agent ID on the agent list page. For information on how to obtain the agent ID, see [agentId](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#6c63d736). |
||templateId |int |No |1 |Mandatory recall template ID. If a mandatory recall template is provided in the request parameters, the subsequent deep research task will always use the analysis logic of this recall template for in\-depth analysis. For information on how to obtain the mandatory recall template ID, see [Forced recall template ID](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#06ef8660). |
||fileList |List[string] |No |["storage\-A"] |Files that require additional analysis (available only for general agents). To reference specific files during the execution of a deep research task, first upload the reference files using the file upload API. After uploading, you will receive a returned storageKey value, which is used as the value for fileList here.<br><br>For details about the file upload API, see [File Upload](https://docs.byteplus.com/docs/dataagent/File_Upload). |
||dataSetList |List[TaskDataSetInfo] |No |```JSON```<br>```[```<br>```    {"id": 1, "appId": 1},```<br>```    {"id": 2, "appId": 1}```<br>```]```<br> |Datasets that require additional analysis. For vertical agents with pre\-configured datasets, this parameter is optional. Details:<br><br><br>* appId: The project ID where the dataset resides. For information on how to obtain it, see [appId](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#c5a6072e).<br><br>* Id: The dataset ID. For information on how to obtain it, see [dataSetId](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#67395b57). |
||reportList |List[TaskReportInfo] |No |```JSON```<br>```[```<br>```    {```<br>```        "reportId": 1,```<br>```        "appId": 1,```<br>```        "dashboardId": 1,```<br>```        "sheetId": 1```<br>```    },```<br>```    {```<br>```        "reportId": 2,```<br>```        "appId": 1,```<br>```    }```<br>```]```<br> |Visualization charts that require additional analysis. Details:<br><br><br>* reportId: Visualization chart ID. For information on how to obtain it, see [rid（reportid）](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#af7185c7).<br><br>* appId: The project ID where the visualization chart resides. For information on how to obtain it, see [appId](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#c5a6072e).<br><br>* dashboardId: The dashboard ID where the chart resides (optional). For information on how to obtain it, see [dashboardid](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#48db6b9d).<br><br>* sheetId: The sheetId corresponding to the dashboard where the chart resides (optional). For information on how to obtain it, see [sheetid](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#9d7e39e7). |
||exportConfig |ExportConfig |No |```JSON```<br>```{```<br>```    "htmlExportTypes": [```<br>```        "PDF",```<br>```        "IMG",```<br>```        "RAW_DATA"```<br>```    ]```<br>```}```<br> |This parameter is supported starting from version 3.16. It is used to support exporting PDF, images, and raw data after the report is generated.<br><br>htmlExportTypes: Export based on the HTML report<br><br><br>* PDF: PDF document<br><br>* IMG: PNG image<br><br>* RAW_DATA: Raw data (Excel)<br><br><br>After enabling, the following artifact types are added. For specific definitions, see [Report export artifact: PDF\IMG\RAW_DATA](https://docs.byteplus.com/docs/undefined/69eafccbcad2c105c48a5536#98e30351).<br><br><br>* deep_research_html_report_export_pdf<br><br>* deep_research_html_report_export_image<br><br>* deep_research_html_report_export_raw_data |
||mcpConfig |OpenApiMcpConfig |No |```JSON```<br>```{```<br>```    "serverFilterMode": "ONLY_SELECTED",```<br>```    "registeredMcpServer": [```<br>```        {```<br>```            "mcpServerId": 219,```<br>```            "toolFilterMode": "ONLY_SELECTED",```<br>```            "tools": [```<br>```                {```<br>```                    "toolName": "get_weather"```<br>```                }```<br>```            ]```<br>```        }```<br>```    ]```<br>```}```<br> |This parameter is supported starting from version 3.16. MCP tool definition.<br><br>The meaning of the sample value is as follows:<br><br>Only the MCP service configured in the backend for the agent with ID 219 is enabled,<br><br>and only the get_weather tool is enabled. |
||sessionName |string |No |Query sales amount records |This parameter is supported starting from version 3.16. It is used to manually specify the session name. If not specified, the first 128 characters of your input question will be used by default. |
||enableAgentDataSet |bool |No |True |Supported since version 3.16. This parameter is used to specify whether to ignore the dataset of vertical agents.<br><br>The default value is True, which means the dataset configured for vertical agents is used.<br><br>When set to False, the dataset configured for vertical agents is ignored. This does not affect the dataset list passed directly in the request. |
||enableDeepThinkingMode |bool |No |True |Supported since version 3.16. This parameter is used to configure deep research mode.<br><br>When set to True, deep thinking mode is enabled. When set to False, fast mode is enabled.<br><br>If this parameter value is not provided, the system automatically determines the mode. |
||enableRunningStepOutput |bool |No |False |The default is False. When set to True, process output is enabled. See the streaming return example and [Reference: Output result module description](https://docs.byteplus.com/docs/dataagent/Execute_Deep_Research_Task#1550137b) section. |
||enableWebSearch |bool |No |False |Configure whether to enable web search. |
|OpenApiMcpConfig |serverFilterMode |StrEnum |No |DISABLE |Supported since version 3.16. This parameter is used to set the MCP service filter mode. The default value is DISABLE.<br><br><br>* DISABLE: No MCP services are enabled.<br><br>* FOLLOW_AGENT_SETTINGS: Follows the agent configuration.<br><br>* ONLY_SELECTED: Only MCP services provided in registeredMcpServer are enabled. |
||registeredMcpServer |List[RegisteredMcpServer] |No |None |Supported since version 3.16. This parameter indicates MCP service information configured in the agent backend. |
|RegisteredMcpServer |mcpServerId |int |Yes |219 |Supported since version 3.16. This parameter is used to set the MCP service ID in the agent backend configuration. |
||toolFilterMode |StrEnum |No |FOLLOW_AGENT_SETTINGS |Supported since version 3.16. This parameter is used to set the tool filter mode. The default is FOLLOW_AGENT_SETTINGS.<br><br><br>* FOLLOW_AGENT_SETTINGS: Follows the agent configuration.<br><br>* ONLY_SELECTED: Only the tools selected in the tools list.<br><br>* INCLUDE_ALL: All tools provided by MCP services. |
||tools |List[McpTool] |No |```JSON```<br>```{```<br>```    ...```<br>```    "tools": [```<br>```        {```<br>```            "toolName": "get_weather"```<br>```        },```<br>```        {```<br>```            "toolName": "get_temperature"```<br>```        }```<br>```    ]```<br>```    ...```<br>```}```<br> |Supported since version 3.16. This parameter is used to set the tool information list. Currently, it is only used to filter tools by passing toolName.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Although McpTool currently has only one parameter, it is a List[Dict] rather than a List[str].</div><br> |
|McpTool |toolName |string |Yes |get_weather |Supported since version 3.16. This parameter is used to set the specific tool name for filtering tools according to toolFilterMode. |
|PushNotificationConfig |id |string |No |"push\-1" |Custom push ID used to identify the push method. Optional. |
||url |string |Yes |"https://example.com/webhook" |URL for receiving push notifications. |
||token |string |No |"123456" |Token for recipient verification. Optional. |
||authentication |PushNotificationAuthentication |No |Bearer Token<br><br>```JSON```<br>```{```<br>```    "schemes": ["Bearer"],```<br>```    "credentials": "sk-12345"```<br>```}```<br><br><br>Custom ApiKey<br><br>```JSON```<br>```{```<br>```    "schemes": ["ApiKey"],```<br>```    "credentials": "key:value"```<br>```}```<br> |Authentication information. When provided, the corresponding structure is added to the header.<br><br><br>* For Bearer Token, it is always provided in the Authorization request header.<br><br>* For custom ApiKey, it is split by the first colon. The part before the colon is the key in the header, and the part after the colon is the value for that key. |


<span id="f7d6074f"></span>
# **Request example**

```JSON
{
    "stream": true,
    "metadata": {
        "agentId": 17368,
        "reportList":[
            {
                "appId":1004033,
                "reportId": 7112515
            }
        ],
        "dataSetList": [
            {
                "id": 1836089,
                "appId": 1004033
            }
        ],
        "fileList": [
            "agent-upload-20250916121852-a79607aef5e44339ad9afa1aa41c81b5"
        ]
    },
    "content": "Immediately enter the report writing phase, and use the render_tochart method to render the incoming file df as a chart during the report writing phase. This step is all that is needed, and the report length should not exceed 100 words"
}
```


<span id="d2ddead6"></span>
# **Response parameters**

<span id="352ed76b"></span>
## Non\-streaming response


|Location |Parameter |Type |Example value |Description |
|---|---|---|---|---|
|ROOT |taskId |string |d9ec4b426c5a4f7d8e30ced79d5ecb0e |Task ID |


```JSON
{
    "JSONIFY_PRETTYPRINT_REGULAR": false,
    "code": "llm/ok",
    "data": {
        "taskId": "d9ec4b426c5a4f7d8e30ced79d5ecb0e"
    },
    "msg": {}
}
```


<span id="dd2a3a30"></span>
## Streaming response


|Location |Parameter |Type |Example value |Description |
|---|---|---|---|---|
|ROOT |task |DeepResearchTask |See the return value example below |Task information |
||artifactUpdate |DeepResearchTaskArtifactUpdateEvent |See the return value example below |Artifact update result, including multiple fields such as artifactId, name, and metadata. For details, see the artifact definition section below. |
||statusUpdate |DeepResearchTaskStatusUpdateEvent |See the return value example below |Task status update |


```JSON
data: {"task": {"kind": "task", "id": "314b788f83394219afa563e47a2938a9", "contextId": "fd86552d317b4733aa8e7438f81c84b5", "status": {"state": "submitted", "timestamp": "2025-09-26T14:50:42.280030"}, "metadata": {"agentId": 17368, "dataSetList": [{"id": 1836089, "appId": 1004033}], "reportList": [{"reportId": 7112515, "appId": 1004033}], "fileList": ["agent-upload-20250916121852-a79607aef5e44339ad9afa1aa41c81b5"]}}}

data: {"statusUpdate": {"kind": "status-update", "taskId": "314b788f83394219afa563e47a2938a9", "contextId": "fd86552d317b4733aa8e7438f81c84b5", "status": {"state": "working", "timestamp": "2025-09-26T14:50:45.351049"}, "final": false, "metadata": {"agentId": 17368, "sessionId": 12013496, "deepResearchTaskId": 181928, "dataSetList": [{"id": 1836089, "appId": 1004033}], "reportList": [{"reportId": 7112515, "appId": 1004033}], "fileList": ["agent-upload-20250916121852-a79607aef5e44339ad9afa1aa41c81b5"]}}}

data: {"statusUpdate": {"kind": "status-update", "taskId": "314b788f83394219afa563e47a2938a9", "contextId": "fd86552d317b4733aa8e7438f81c84b5", "status": {"state": "working", "timestamp": "2025-09-26T14:51:15.928361"}, "final": false, "metadata": {"agentId": 17368, "sessionId": 12013496, "deepResearchTaskId": 181928, "dataSetList": [{"id": 1836089, "appId": 1004033}], "reportList": [{"reportId": 7112515, "appId": 1004033}], "fileList": ["agent-upload-20250916121852-a79607aef5e44339ad9afa1aa41c81b5"]}}}

data: {"artifactUpdate": {"kind": "artifact-update", "taskId": "314b788f83394219afa563e47a2938a9", "contextId": "fd86552d317b4733aa8e7438f81c84b5", "artifact": {"artifactId": "821c905ef77c4e0ead2c22f4a20e4365", "name": "0x Verification Data Visualization Report", "description": "Markdown Report", "parts": [{"kind": "text", "text": "#0x Validation Data Visualization Report \ n \ n # 1 Data Overview and Chart Display \ n \ nBased on the data analysis of the 0x validation table, this dataset contains 3 dates (April 20, 2023 to April 22, 2023), 2 projects (A and B), and a total of 6 records. \N \ n \ n \ n | Date | Project | Number | Floating Point|\ n|------------|------|-------|---------|\n| 2023-04-20 | B    | 49930 | 39940.4 |\n| 2023-04-20 | A    |  9980 | 19980.5 |\n| 2023-04-21 | A    |  9990 | 19990.7 |\n| 2023-04-21 | B    | 49980 | 39980.6 |\n| 2023-04-22 | A    | 10000 | 20000.9 |\n| 2023-04-22 | B    | 50000 | 40000.8 |\n\n\n\n Data visualization shows that the total number of project B is 149910, significantly higher than project A's 29970, with a ratio of approximately 5:1. Floating point data also shows a similar distribution trend, with the total floating point of project B being approximately twice that of project A. \Reference Information: The data sources and chart references for this report are as follows:"}], "metadata": {"type": "deep_research_markdown_report"}}}}

data: {"statusUpdate": {"kind": "status-update", "taskId": "314b788f83394219afa563e47a2938a9", "contextId": "fd86552d317b4733aa8e7438f81c84b5", "status": {"state": "completed", "timestamp": "2025-09-26T14:52:00.878760"}, "final": true, "metadata": {"agentId": 17368, "sessionId": 12013496, "deepResearchTaskId": 181928, "dataSetList": [{"id": 1836089, "appId": 1004033}], "reportList": [{"reportId": 7112515, "appId": 1004033}], "fileList": ["agent-upload-20250916121852-a79607aef5e44339ad9afa1aa41c81b5"]}}}
```


<span id="1550137b"></span>
# Reference: Output result module description

<span id="74a23de3"></span>
## Artifact definition

The following provides an example and detailed field description of the artifact field contained in the artifactUpdate result in streaming responses.

```JSON
{
    "artifactId": "080e334f-29c1-5587-bd0c-e230bd78da0d",
    "name": "Draw sales distribution maps for various regions",
    "description": "Task completed: [Execute Python code] Draw sales distribution maps for various regions",
    "parts": [
        {
            "kind": "text",
            "text": "......"
        },
        {
            "kind": "data",
            "data": {
                "type": "python_sandbox",
                "content": "```python......```\n\n",
                "result": "The code execution was successful, and the output content is as follows：......"
            }
        }
    ],
    "metadata": {
        "type": "deep_research_running_step",
        "stepType": "python_sandbox",
        "stepId": -15913542,
        "parentStepId": 15913542
    }
}
```



|Field name |Field type |Example value |Field description |
|---|---|---|---|
|artifactId |string |52df4714\-4fc2\-5025\-aea9\-bd8837ca\*\*\*\* |Artifact ID. The same artifact ID represents the same artifact. |
|name |string |Obtain dataset\-related information |Artifact name, which may change during execution |
|description |string |Task completed: Obtain dataset\-related information |Artifact description, which may change during execution |
|parts |List[Part] |```JSON```<br>```[```<br>```    {```<br>```        "kind": "text",```<br>```        "text": "\n\n## ......"```<br>```    },```<br>```    {```<br>```        "kind": "data",```<br>```        "data": {```<br>```            ...```<br>```        }```<br>```    },```<br>```    {```<br>```        "kind": "file",```<br>```        "file": {```<br>```            "name": "filename.xlsx",```<br>```            "mimeType": "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",```<br>```            "uri": "https://example.com/path/to/filename.xlsx"```<br>```        }```<br>```    }```<br>```]```<br> |Artifact content blocks:<br><br><br>* The text block contains textual information<br><br>* The data block contains structured information<br><br>* The file block contains file information |
|metadata |Metadata |See the example above |Different artifact types have different metadata fields. Among them, the type field can be used to determine the artifact type of the deep research report. The descriptions of different artifact types are as follows:<br><br><br>* deep_research_markdown_report: Document version report (Markdown format). The report content has converted line charts and other special charts into Markdown tables.<br><br>   * When the artifact contains tables, they are returned as Markdown\-formatted tables.<br><br>   * When the artifact contains images, the image URL is returned. To read the image, an account with appropriate permissions is required (it is recommended to use the account that calls the current API).<br><br>* deep_research_html_report_key: Web version report. You can obtain the key for the web version report to construct the web report access URL. Accessing this web URL will display the web version report. The format is as follows:<br><br>   * `https://{domain}/{PATH_TO_DATAAGENT}/agent/report/html?region=AAA&reportKey=XXX`<br><br>   * `https://{domain}/{PATH_TO_DATAAGENT}-open#/agent/report/html?region=AAA&reportKey=XXX&jwtToken=YYY`<br><br>      For details on how to construct the web version report URL, see the [Concatenate deep research report URL](https://docs.byteplus.com/docs/dataagent/Execute_Deep_Research_Task#8c5d2628)section in Application Practice below.<br><br>* deep_research_running_step: Intermediate process information, provided only when enableRunningStepOutput: true is set in metadata when requesting the task. For specific definitions, see the [Intermediate step artifact: deep_research_running_step](https://docs.byteplus.com/docs/dataagent/Execute_Deep_Research_Task#800b1f79)section below.<br><br>* deep_research_html_report_export_pdf: Export PDF file based on the HTML report. For specific definitions, see [HTML PDF: deep_research_html_report_export_pdf](https://docs.byteplus.com/docs/undefined/69eafccbcad2c105c48a5536#17dceeba) below.<br><br>* deep_research_html_report_export_image: Export IMG file based on the HTML report. For specific definitions, see [HTML IMG: deep_research_html_report_export_image](https://docs.byteplus.com/docs/undefined/69eafccbcad2c105c48a5536#a54ab837) below.<br><br>* deep_research_html_report_export_raw_data: Export raw data based on the HTML report. For specific definitions, see [HTML RAW DATA: deep_research_html_report_export_raw_data](https://docs.byteplus.com/docs/undefined/69eafccbcad2c105c48a5536#023c4d55) below. |


<span id="800b1f79"></span>
## Intermediate step artifact: deep_research_running_step


|Location |Field name |Field type |Example value |Field description |
|---|---|---|---|---|
|Metadata |type |string |deep_research_running_step |Artifact type |
||stepType |string |executor_think |Intermediate step types, used to identify the type of intermediate step:<br><br><br>* executor_think: Reasoning step<br><br>* sql_sandbox: Data query SQL processing step<br><br>* python_sandbox: Analysis processing step<br><br>* table_insight: Dataset retrieval step<br><br><br>For detailed descriptions of the locations of the returned content and examples for each intermediate step type, see below. |
||stepId |Optional[int] |1919810 |The step ID of the current step, used to establish associations between intermediate steps |
||parentStepId |Optional[int] |114514 |The step ID of the upstream step, used to establish associations between intermediate steps.<br><br>Currently, intermediate steps are fixed as a two\-level structure. Steps with parentStepId equal to 0 represent information about a "step group". The actual step content should be obtained from steps where parentStepId is not 0. |


<span id="bf448e4a"></span>
### Executor_think


* Does not contain data block

* Streamed updates are present, updated in the text block


```JSON
data: {"artifactUpdate": {"kind": "artifact-update", "taskId": "49e0fed9b5714bf9807164d012ce4b2a", "contextId": "0c4f27bcb95f40fd8a0e72c93647dca0", "artifact": {"artifactId": "9c73aa1e-4b6a-574a-92ae-5b3e7523e98a", "name": "Thinking and reasoning", "description": "Thinking and reasoning", "parts": [{"kind": "text", "text": ""}], "metadata": {"type": "deep_research_running_step", "stepType": "executor_think", "stepId": 15913627, "parentStepId": 15913542}}, "lastChunk": false}}

data: {"artifactUpdate": {"kind": "artifact-update", "taskId": "49e0fed9b5714bf9807164d012ce4b2a", "contextId": "0c4f27bcb95f40fd8a0e72c93647dca0", "artifact": {"artifactId": "9c73aa1e-4b6a-574a-92ae-5b3e7523e98a", "parts": [{"kind": "text", "text": "##"}]}, "append": true, "lastChunk": false}}

......

data: {"artifactUpdate": {"kind": "artifact-update", "taskId": "49e0fed9b5714bf9807164d012ce4b2a", "contextId": "0c4f27bcb95f40fd8a0e72c93647dca0", "artifact": {"artifactId": "9c73aa1e-4b6a-574a-92ae-5b3e7523e98a", "parts": [{"kind": "text", "text": "。"}]}, "append": true, "lastChunk": false}}

data: {"artifactUpdate": {"kind": "artifact-update", "taskId": "49e0fed9b5714bf9807164d012ce4b2a", "contextId": "0c4f27bcb95f40fd8a0e72c93647dca0", "artifact": {"artifactId": "9c73aa1e-4b6a-574a-92ae-5b3e7523e98a", "name": "Thinking and reasoning", "description": "Thinking and reasoning complete.", "parts": [{"kind": "text", "text": "## Train of thought analysis \ n \ nWe have completed the query and analysis of sales revenue in various regions, obtained data from 61 cities, and drawn sales revenue distribution maps for each province. Data shows: \ n - Guangdong Province and Jiangsu Province lead in sales \ n - The top 10 provinces account for 74.37% of total sales \ n - The distribution has been visualized. \ n \ n The task has been completed and we can enter the report writing stage."}], "metadata": {"type": "deep_research_running_step", "stepType": "executor_think", "stepId": 15913627, "parentStepId": 15913542}}, "lastChunk": true}}
```


<span id="db093c7d"></span>
### Table_insight


* Does not contain data block


```JSON

data: {"artifactUpdate": {"kind": "artifact-update", "taskId": "49e0fed9b5714bf9807164d012ce4b2a", "contextId": "0c4f27bcb95f40fd8a0e72c93647dca0", "artifact": {"artifactId": "86875483-3508-56b3-8f16-7cb041226e2a", "name": "Obtain information related to the dataset", "description": "Task completed: Obtain information related to the dataset", "parts": [{"kind": "text", "text": "\n\n## The relevant information of table '1836089' is as follows:\nTableID: `1836089`\nTable Name: 'Sales GMV Direct Connection'\n\n\nEngine Column Name and Data Type:\n|Column Name|Data Type|\n| ---- | ---- |\n|sale_price|Nullable(Float32)|\n|order_count|int|\n\n\nA field list created based on engine columns, which can be used directly, with field names surrounded by '':\n\n|Field Name|Data Type|Related Info|Sample values (non full quantity)|\n| ---- | ---- | ---- | ---- |\n|`Sales Year`|int|||\n|`customer_id`|int|||\n|`order_date`|date|Data available date range: maximum value: 2016-06-30,minimum: 2013-07-01||\n|`sale_price`|float|||\n|`order_count`|int|||\n|`price`|float|||\n|`null dimension`|string|||\n|`product_id`|string|||\n|`Common dimensions that do not appear in the chart`|string|||\n|`sale_city`|string|||\n|`public dimension`|string|||\n|`product type`|string|||\n|`province`|string|||\n|`GMV`|float|||\n\n\nDefinition reference for aggregation indicators:\n\n```\n`Total Sales`: sum(((order_count) * (sale_price)))\n```\n\n\n## The relevant information of table 2133291 is as follows:\nTableID: `2133291`\nTable Name: `0xvalidation table`\n\nField Lists,Field names are surrounded by ''：\n\n|Field Name|Data Type|Related Info|Sample values (non full quantity)|\n| ---- | ---- | ---- | ---- |\n|`Date`|date|Data available date range: maximum value: 2023-04-22,minimum: 2023-04-20||\n|`number`|int|||\n|`Float`|float|||\n\n\n\n"}], "metadata": {"type": "deep_research_running_step", "stepType": "table_insight", "stepId": -15913420, "parentStepId": 15913420}}, "lastChunk": true}}
```


<span id="36fea074"></span>
### Sql_sandbox


* Data block definition



|Field name |Field type |Sample value |Field description |
|---|---|---|---|
|type |string |execute_sql |Fixed as execute_sql, used to identify the type of this data block |
|content |string |See the example below. |Note: Distinguish from the actual text block<br><br>May appear before the actual text block is updated<br><br>Can be used for partial content rendering |
|result |string |Query result [XX]... |Text of the query result |
|executeSql |string |Select XX from XX |The SQL actually executed |
|rewriteSql |string |Select `170001_XX` from XX |The rewritten SQL, used for display to the user |


```JSON
data: {"artifactUpdate": {"kind": "artifact-update", "taskId": "49e0fed9b5714bf9807164d012ce4b2a", "contextId": "0c4f27bcb95f40fd8a0e72c93647dca0", "artifact": {"artifactId": "81301578-a38a-5df9-aeb6-403249f7b650", "name": "Query Sales Amount Data in different region", "description": "Task Complete：[Execute SQL]Query Sales data by region dimension, including province and city information, and calculate the total Sales amount", "parts": [{"kind": "text", "text": "```sql\nSELECT `province`,\n       `sale_city`,\n       SUM(`order_count` * `sale_price`) as `Sales Amount`\nFROM   `SalesGMV-Direct Connection`\nWHERE  `province` IS NOT NULL\n   AND `sale_city` IS NOT NULL\nGROUP BY `province`, `sale_city`\nORDER BY `Sales Amount` DESC\n```\n\nQuery Result[sales_by_region]61 row in total, as follows:\n||province|sale_city|Sales Amount|\n|--|--|--|--|\n|0|Shanghai|Shanghai|2832629.8676199913|...Query Success。Query Resultalready stored in memory variable sales_by_region, which type is pandas.DataFrame\The column names and data types of nsales_by_region are as follows:\n|column name|data type|\n|--|--|\n|province|string|\n|sale_city|string|\n|Sales Amount|float|\n\nQuery Resultsales_by_region column number：61\n\The complete result data of nsales_by_region is as follows：\n||province|sale_city|Sales Amount|\n|--|--|--|--|\n|0|Shanghai|Shanghai|2832629.8676199913|..."}, {"kind": "data", "data": {"type": "execute_sql", "content": "```sql\nSELECT `province`,\n       `sale_city`,\n       SUM(`order_count` * `sale_price`) as `Sales Amount`\nFROM   `SalesGMV-Direct Connection`\nWHERE  `province` IS NOT NULL\n   AND `sale_city` IS NOT NULL\nGROUP BY `province`, `sale_city`\nORDER BY `Sales Amount` DESC\n```\n\n", "result": "Query Result[sales_by_region]61 rows in total, as follows：\n||province|sale_city|Sales Amount|\n|--|--|--|--|\n|0|Shanghai|Shanghai|2832629.8676199913|", "executeSql": "SELECT (sale_province) AS `alias_prefix_province`,\n       (sale_city) AS `alias_prefix_sale_city`,\n       SUM((order_count) * (sale_price)) AS `alias_prefix_Sales Amount`\nFROM   (SELECT `product_type` as `product_type`,\n               `product_id` as `product_id`,\n               `order_count` as `order_count`,\n               `price` as `price`,\n               `sale_province` as `sale_province`,\n               `sale_price` as `sale_price`,\n               `sale_city` as `sale_city`,\n               `order_date` as `order_date`,\n               `customer_id` as `customer_id`\n        FROM   `aeolus_excel_upload_aeolus_rei`.`table_cede732c_c35a_424c_85e7_174fee1739ae`\n        WHERE  1 = 1) AS `SalesGMV-Direct Connection`\nWHERE  NOT ((sale_province) IS NULL)\n   AND NOT ((sale_city) IS NULL)\nGROUP BY `alias_prefix_province`, `alias_prefix_sale_city`\nORDER BY `alias_prefix_Sales Amount` DESC LIMIT 10000 FORMAT JSONCompact", "rewriteSql": "SELECT (`1700031515177_province`) AS `alias_prefix_province`,\n       (`1700031515178_sale_city`) AS `alias_prefix_sale_city`,\n       SUM((`1700031515180_order_count`) * (`1700031515182_sale_price`)) AS `alias_prefix_Sales Amount`\nFROM   `chenrui.ovo test.SalesGMV-Direct Connection` AS `SalesGMV-Direct Connection`\nWHERE  NOT ((`1700031515177_province`) IS NULL)\n   AND NOT ((`1700031515178_sale_city`) IS NULL)\nGROUP BY `alias_prefix_province`, `alias_prefix_sale_city`\nORDER BY `alias_prefix_Sales Amount` DESC LIMIT 10000"}}], "metadata": {"type": "deep_research_running_step", "stepType": "sql_sandbox", "stepId": -15913462, "parentStepId": 15913462}}, "lastChunk": true}}
```


<span id="8533da5e"></span>
### Python_sandbox


* The data block definition is as follows



|Field name |Field type |Sample value |Field description |
|---|---|---|---|
|type |string |python_sandbox |Fixed as python_sandbox, used to identify the type of this data block |
|content |string |See the example below |Note: Distinguish from the actual text block. May appear before the actual text block is updated<br><br>Can be used for partial content rendering |
|result |string |See the example below |Output result prompt |


```Python
data: {"artifactUpdate": {"kind": "artifact-update", "taskId": "49e0fed9b5714bf9807164d012ce4b2a", "contextId": "0c4f27bcb95f40fd8a0e72c93647dca0", "artifact": {"artifactId": "080e334f-29c1-5587-bd0c-e230bd78da0d", "name": "Draw sales distribution maps for various regions", "description": "Task execution: [Executing Python code]Draw sales distribution maps for various regions", "parts": [{"kind": "text", "text": ""}, {"kind": "data", "data": {"type": "python_sandbox", "content": "```python\nimport matplotlib.pyplot as plt\nimport pandas as pd\n\n# Set Chinese font\nplt.rcParams['font.sans-serif'] = ['SimHei']\nplt.rcParams['axes.unicode_minus'] = False\n\n# province Sales Amount\nprovince_sales = sales_by_region.groupby('province')['Sales Amount'].sum().sort_values(ascending=False)\n\n# Draw a bar chart\nplt.figure(figsize=(12, 8))\nprovince_sales.plot(kind='bar', color='skyblue')\nplt.title('Province Sales AmountDistribution')\nplt.xlabel('province')\nplt.ylabel('Sales Amount')\nplt.xticks(rotation=45)\nplt.tight_layout()\nplt.show()\n\n# Output the top 10 provinces\nprint(\"Sales Amountthe top 10 provinces:\")\nprint(province_sales.head(10))\n\n# calculate the top 10 provinces proportion of Sales Amount\ntop10_ratio = province_sales.head(10).sum() / province_sales.sum()\nprint(f\"\\nthe top 10 provinces proportion of Sales Amount: {top10_ratio:.2%}\")\n```\n\n"}}], "metadata": {"type": "deep_research_running_step", "stepType": "python_sandbox", "stepId": -15913542, "parentStepId": 15913542}}, "lastChunk": false}}

data: {"artifactUpdate": {"kind": "artifact-update", "taskId": "49e0fed9b5714bf9807164d012ce4b2a", "contextId": "0c4f27bcb95f40fd8a0e72c93647dca0", "artifact": {"artifactId": "080e334f-29c1-5587-bd0c-e230bd78da0d", "name": "Draw sales distribution maps for various regions", "description": "Task Complete：Execute Python codeDraw sales distribution maps for various regions", "parts": [{"kind": "text", "text": "```python\nimport matplotlib.pyplot as plt\nimport pandas as pd\n\n# Set Chinese font\nplt.rcParams['font.sans-serif'] = ['SimHei']\nplt.rcParams['axes.unicode_minus'] = False\n\n# province proportion of Sales Amount\nprovince_sales = sales_by_region.groupby('province')['Sales Amount'].sum().sort_values(ascending=False)\n\n# Draw a bar chart\nplt.figure(figsize=(12, 8))\nprovince_sales.plot(kind='bar', color='skyblue')\nplt.title('Province Sales Amount Distribution')\nplt.xlabel('province')\nplt.ylabel('Sales Amount')\nplt.xticks(rotation=45)\nplt.tight_layout()\nplt.show()\n\n# outputthe top 10 provinces\nprint(\"Sales Amountthe top 10 provinces:\")\nprint(province_sales.head(10))\n\n# calculatethe top 10 provinces proportion of Sales Amount\ntop10_ratio = province_sales.head(10).sum() / province_sales.sum()\nprint(f\"\\nthe top 10 provinces proportion of Sales Amount: {top10_ratio:.2%}\")\n```\n\nThe code execution was successful, and the output content is as follows:\n\nSales Amountthe top 10 provinces:\n                  Sales Amount\nprovince                    \nGuangdong  4822876.405101776\nJiangsu  4590771.994219542\nShanghai 2832629.8676199913\nBeijing 2738369.6146588326\nZhejiang 2471835.6385302544\nHebei  1499687.414835453\nFujian  936069.9314939976\nTianjin  687273.1442761421\nShannxi  615094.7341973782\nChongqing  602230.6761865616\n\nthe top 10 provinces proportion of Sales Amount: 74.37%\n\nRendered image：\n  - title：Province Sales Amount Distribution\n  - img_key： b2134d0c161e4822a7d697271802a1d4\n  - img_url：https://data.bytedance.net/dataAgent/llm/api/v2/deepresearch/images?img_key=13464321-286833-b2134d0c161e4822a7d697271802a1d4\n\n"}, {"kind": "data", "data": {"type": "python_sandbox", "content": "```python\nimport matplotlib.pyplot as plt\nimport pandas as pd\n\n# Set Chinese font\nplt.rcParams['font.sans-serif'] = ['SimHei']\nplt.rcParams['axes.unicode_minus'] = False\n\n# province Sales Amount\nprovince_sales = sales_by_region.groupby('province')['Sales Amount'].sum().sort_values(ascending=False)\n\n# Draw a bar chart\nplt.figure(figsize=(12, 8))\nprovince_sales.plot(kind='bar', color='skyblue')\nplt.title('Province Sales Amount Distribution')\nplt.xlabel('province')\nplt.ylabel('Sales Amount')\nplt.xticks(rotation=45)\nplt.tight_layout()\nplt.show()\n\n# outputthe top 10 provinces\nprint(\"Sales Amountthe top 10 provinces:\")\nprint(province_sales.head(10))\n\n# calculatethe top 10 provinces proportion of Sales Amount\ntop10_ratio = province_sales.head(10).sum() / province_sales.sum()\nprint(f\"\\nthe top 10 provinces proportion of Sales Amount: {top10_ratio:.2%}\")\n```\n\n", "result": "The code execution was successful, and the output content is as follows:\n\nSales Amountthe top 10 provinces:\n\n\n\n| province   | Sales Amount               |\n|:-----|:-------------------|\n| Guangdong  | 4822876.405101776  |\n| Jiangsu  | 4590771.994219542  |\n| Shanghai  | 2832629.8676199913 |\n| Beijing  | 2738369.6146588326 |\n| Zhejiang  | 2471835.6385302544 |\n| Hebei  | 1499687.414835453  |\n| Fujian  | 936069.9314939976  |\n| Tianjin  | 687273.1442761421  |\n| Shannxi  | 615094.7341973782  |\n| Chongqing  | 602230.6761865616  |\n\n\n\n\nthe top 10 provinces proportion of Sales Amount: 74.37%\n\n\n\n\n\n![Rendered image\"Province Sales Amount Distribution\"，access through https://data.bytedance.net/dataAgent/llm/api/v2/deepresearch/images?img_key=13464321-286833-b2134d0c161e4822a7d697271802a1d4](https://data.bytedance.net/dataAgent/llm/api/v2/deepresearch/images?img_key=13464321-286833-b2134d0c161e4822a7d697271802a1d4 \"Province Sales Amount Distribution\")\n\n\n\n\n\n"}}], "metadata": {"type": "deep_research_running_step", "stepType": "python_sandbox", "stepId": -15913542, "parentStepId": 15913542}}, "lastChunk": true}}
```


<span id="8351ab19"></span>
## Report export artifact: PDF\IMG\RAW_DATA

The following provides an example and detailed field description of the artifact field contained in the artifactUpdate result in streaming output.

Visible when exportConfig is enabled during report generation.

```JSON
{
    "artifactUpdate": {
        "kind": "artifact-update",
        "taskId": "914a00b1fa1c4ef1a0be71206a9c****",
        "contextId": "a11ffa94f0854cafb06d339fdfc4****",
        "artifact": {
            "artifactId": "bca21b42-5d90-5065-ae9d-2c574384****",
            "name": "html report pdf",
            "description": "html report pdf",
            "parts": [
                {
                    "kind": "file",
                    "file": {
                        "name": "***analysis report_html_2026010612****.pdf",
                        "mimeType": "application/pdf",
                        "uri": "https://example.com/path/to/filename.pdf"
                    }
                }
            ],
            "metadata": {
                "type": "deep_research_html_report_export_pdf"
            }
        },
        "lastChunk": true
    }
}
```



|Field name |Field type |Sample value |Field description |
|---|---|---|---|
|taskId |string |914a00b1fa1c4ef1a0be71206a9c\*\*\*\* |Task ID |
|contextId |string |a11ffa94f0854cafb06d339fdfc4\*\*\*\* |Context ID |
|artifactId |string |52df4714\-4fc2\-5025\-aea9\-bd8837ca\*\*\*\* |Artifact ID; the same artifact ID represents the same artifact. |
|name |string |html report pdf |Artifact name, which may change during execution |
|description |string |html report pdf |Artifact description, which may change during execution |
|parts |List[Part] |```JSON```<br>```[```<br>```    {```<br>```        "kind": "file",```<br>```        "file": {```<br>```            "name": "Regional Sales Amount Analysis Report_html_20260106124045.pdf",```<br>```            "mimeType": "application/pdf",```<br>```            "uri": "https://example.com/path/to/filename.pdf"```<br>```        }```<br>```    }```<br>```]```<br> |Artifact content block: file block contains file information. The specific parameter definitions are as follows:<br><br><br>* kind: file indicates a file block.<br><br>* name: The name of the exported file.<br><br>* mimeType: Used to identify the file format. Descriptions for different file formats are as follows:<br><br>   * application/pdf: Export PDF file based on HTML<br><br>   * image/png: Export IMG file based on HTML<br><br>   * application/vnd.openxmlformats\-officedocument.spreadsheetml.sheet: Export raw data based on HTML<br><br>* uri: The path of the exported HTML report. You can use this path to download the report. |
|metadata |Metadata |None |type field: Artifact type of the deep research report. Descriptions for different types are as follows:<br><br><br>* deep_research_html_report_export_pdf: Export PDF file based on HTML report.<br><br>* deep_research_html_report_export_image: Export IMG files based on HTML reports.<br><br>* deep_research_html_report_export_raw_data: Export raw data based on HTML reports. |


<span id="c36246e0"></span>
### HTML PDF: deep_research_html_report_export_pdf

Export PDF file based on the HTML report.

```JSON
{
    "artifactId": "bca21b42-5d90-5065-ae9d-2c5743847fba",
    "name": "html report pdf",
    "description": "html report pdf",
    "parts": [
        {
            "kind": "file",
            "file": {
                "name": "Regional Sales Amount Analysis Report_html_20260106124045.pdf",
                "mimeType": "application/pdf",
                "uri": "https://example.com/path/to/filename.pdf"
            }
        }
    ],
    "metadata": {
        "type": "deep_research_html_report_export_pdf"
    }
}
```


<span id="21ec7d84"></span>
### HTML IMG: deep_research_html_report_export_image

Export IMG file based on the HTML report.

```JSON
{
    "artifactId": "d1b1d6d3-8b04-52d7-bd34-458015eda533",
    "name": "html report image",
    "description": "html report screenshot",
    "parts": [
        {
            "kind": "file",
            "file": {
                "name": "Regional Sales Amount Analysis Report_html_20260106124045.png",
                "mimeType": "image/png",
                "uri": "https://example.com/path/to/filename.png"
            }
        }
    ],
    "metadata": {
        "type": "deep_research_html_report_export_image"
    }
}
```


<span id="ecf25cfb"></span>
### HTML RAW DATA: deep_research_html_report_export_raw_data

Export raw data.

```JSON
{
    "artifactId": "3ad2bfa8-cbbd-5037-9ca5-47edd677e5ad",
    "name": "deepresearch html raw data",
    "description": "Deep analysis of HTML report raw data",
    "parts": [
        {
            "kind": "file",
            "file": {
                "name": "Regional Sales Amount Analysis Report_html_20260106124045.xlsx",
                "mimeType": "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "uri": "https://example.com/path/to/filename.xlsx"
            }
        }
    ],
    "metadata": {
        "type": "deep_research_html_report_export_raw_data"
    }
}
```


<span id="366914ba"></span>
# Practical application

<span id="8c5d2628"></span>
## Concatenate deep research report URL

The following describes how to concatenate the final research report URL based on the returned result after executing the deep research task openAPI. Once the report URL is concatenated, you can use this URL to display the web version of the report content.

First, we need to understand that there are currently two formats for concatenating the deep research report URL.


|Comparison criteria |Method 1: SSO login scenario |Method 2: Separate authentication scenario |
|---|---|---|
|URL concatenation example |`https://{domain}/{PATH_TO_DATAAGENT}/agent/report/html?region=AAA&reportKey=XXX` |`https://{domain}/{PATH_TO_DATAAGENT}-open#/agent/report/html?region=AAA&reportKey=XXX&jwtToken=YYY` |
|Applicable scenarios |After SSO login authentication, subsequent access to the deep research report page does not require further authentication.<br><br>This approach is typically used in private deployment scenarios, where SSO login authentication can be performed within a private internal network environment. |Applicable when accessing the deep research report page and using jwtToken for authentication.<br><br>This method is typically required for login authentication in SaaS scenarios. |
|Variable: `{domain}` |* SaaS domain: Fixed value, `https://console.volcengine.com/bi/datawind` | |
|Variable: `{PATH_TO_DATAAGENT}` |Not applicable |For path parameters, it is recommended to first open a session page of the Intelligent Analysis Agent, copy the page URL, and the path parameters are in this URL. For details, refer to the URL concatenation operation example below. |
|Variable: `region` |The region information where the currently used agent is located. ||
|Variable: `reportKey` |The generated deep research report ID. The acquisition method is as follows.<br><br><br>1. After calling the "Execute Deep Research Task" API, check the `artifact` in the returned streaming result, and review the `metadata` field's `type` field in the returned result.<br><br>2. When the value of the metadata's type field is `deep_research_html_report_key`, in the parts field of `artifact`, find the value(s) of type `text` and `text`. This value is the deep research report ID `reportKey`.<br><br><br>As shown in the example below.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c53cc983f5748e09d8a3dc16d0ea321~tplv-goo7wpa0wc-image.image) </span><br><br>Caution: The deep research report ID `reportKey` is the complete value result of text. You can directly copy the complete value result. | |
|Variable: `jwtToken` |Not applicable |Call the jwttokens of OpenAPI. For acquisition method, please refer to: [Invocation Methods](https://docs.byteplus.com/docs/dataagent/Invocation_Methods). |


When concatenating the deep research report URL, it is recommended to first open a session page of the intelligent analysis Agent, copy the page URL, and then modify and concatenate the URL as needed. This allows you to quickly complete the URL concatenation. The following demonstrates the operation steps.


1. Log in and enter a session page of the intelligent analysis Agent. For example, open the question submission page of Smart Query, then copy the page URL from the browser.

   For example, the copied page URL is: `https://console.volcengine.com/bi/datawind/data-agent/analytics-agent/pages/agent/session?agentId=2730&appId=1000326&forceSwitchToShowAgent=true&region=cn-shanghai&sessionId=258880`.

2. Modify the copied URL to obtain the concatenated deep research report URL.

   
   |Comparison description |Method 1: SSO login scenario |Method 2: Separate authentication scenario |
   |---|---|---|
   |Final report URL |* https://console.volcengine.com/bi/datawind/data\-agent/analytics\-agent/pages/agent/`report/html?region=cn-shanghai&reportKey=XXX` |* https://console.volcengine.com/bi/datawind/data\-agent/analytics\-agent`-open`/pages/agent/`report/html?region=cn-shanghai&reportKey=XXX&jwtToken=YYY` |
   |Modification instructions |* Starting from `session?` in the session page URL, delete everything after it, then append the `report/html?region=cn-shanghai&reportKey=XXX` part. For the explanation and acquisition method of each variable parameter during concatenation, see above. Among them:<br><br>* The value of reportKey=XXX is the deep research report ID returned by the OpenAPI for executing the deep research report.<br><br>   * `region` is the region information where the currently used agent is located.<br><br>   * `region` refers to the region where the agent currently in use is located.<br><br>* The remaining part of the URL, where the `https://……bi/datawind` segment in the session page URL you obtained corresponds to the value of the domain `{domain}`. No modification is required; use the result copied from the page.<br><br>* The remaining part of the URL, where the segment between `{domain}` and `agent` in the session page URL you obtained is the path parameter (the `data-agent/……/pages` segment). No modification is required; use the result copied from the page. |* Starting from the `session?` segment in the session page URL you obtained, delete all subsequent content, and append the report segment `report/html?region=cn-shanghai&reportKey=XXX&jwtToken=YYY`.<br><br>* For an explanation of each variable parameter and how to obtain them during concatenation, refer to the previous section. Specifically:<br><br>   * The value of `reportKey=XXX` is the deep research report ID returned in the result of executing the Deep Research Report OpenAPI.<br><br>   * `jwtToken=YYY` is the jwtToken used to call the OpenAPI.<br><br>   * `region` refers to the region information where the currently used agent is located.<br><br>* The remaining part of the URL, where the `https://……bi/datawind` segment in the session page URL you obtained corresponds to the value of the domain `{domain}`. No modification is required; use the result copied from the page.<br><br>* The remaining part of the URL, where the segment between `{domain}` and `agent` in the session page URL you obtained is the path parameter (the `data-agent/……//pages/` segment). After copying the path parameter, you need to add `-open` immediately after `analytics-agent` as the final path parameter for this access method. |
