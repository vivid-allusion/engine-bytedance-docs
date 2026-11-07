---
title: "Session Completion"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Session_Completion"
---

You can use the chat completion API to obtain real\-time results during the intelligent query process. The chat completion API is a streaming interface; the event stream outputs `[DONE]` or the termination of the API response stream indicates the end.

<span id="dab5d90d"></span>
# Precautions

This API currently does not support multi\-turn conversations.

<span id="6a137406"></span>
# **Request description**


* Request method: POST

* Request URL: `/dataAgent/llm/openApi/v2/signed/agent/chatCompletion`

* Content\-Type：`text/event-stream`


<span id="898409ea"></span>
# **Request parameters**

The body parameters are as follows.


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|sessionId |int |Yes |12886164 |Session ID. Enter the `data.sessionInfo.id` returned by createSession above. |
|type |string |Yes |query |Enter "query" as a fixed value. |
|source |string |Yes |openapi |Request source. Enter the fixed value "openapi". |
|data |object |Yes |See the request example below |Details of the chat completion session. |
|data.userInput |string |Yes |See the request example below |The question for intelligent query. |
|data.enableClarify |boolean |No |true |Indicates whether to enable clarification. When this value is true and the clarification switch is enabled in the agent management console, clarification will be enabled. |
|data.enable_report_search |boolean |No |true |Indicates whether to enable chart search. When this value is true and a chart\-type data source is configured in the agent management console, chart search will be enabled. |
|data.clarifyResults |object |No |See the request example below |Intent clarification result. When the previous conversation result is returned in the format of message number **11**, fill in this field to indicate the user's selection during the clarification interaction. |
|data.clarifyResults.toolCallId |string |Yes |See the request example below |Fill in the toolCallId from the event in the previous conversation result. |
|data.clarifyResults.skipClarify |boolean |No |false |Indicates whether to skip clarification and let the model proceed autonomously. The default is false. |
|data.clarifyResults.userChoices |array |Yes |Refer to the request example below |Selection of clarification content for ambiguous questions. |
|data.clarifyResults.userChoices[].type |string |Required |Refer to the request example below |Populate the result.suggestions[].type field from event. |
|data.clarifyResults.userChoices[].options |array |Required |Refer to the request example below |Populate the information from result.suggestions[].options in the event selected by the user. |
|data.clarifyResults.userChoices[].description |string |Required |Refer to the request example below |Populate the result.suggestions[].description field from event. |


<span id="2b7443e3"></span>
# Request example

```JSON
{
    "sessionId": 12886164,
    "type": "query",
    "data": {
        "userInput": "在超市数据集中，有哪些带“北”字的城市",//Meaning: What are the cities with the word 'north' in the supermarket dataset
        "enableClarify": true,
        "enable_report_search": true,
        "clarifyResults": { // The initial question can be empty.
            "toolCallId": "",
            "skipClarify": false,
            "userChoices": [
                {
                    "type": "",
                    "options": [
                        {
                            "tableName": "",
                            "tableId": int,
                            "fieldName": "",
                            "value": "",
                            "appId": int,
                        }
                    ],
                    "description": ""
                }
            ]
        }
    }
}
```


<span id="2bdcee05"></span>
# **Response parameters**

The response (text/event\-stream) of this API follows the SSE protocol. For details about the SSE protocol, see [SSE protocol description](https://juejin.cn/post/7362922163723042868). The returned result is a message prefixed with `data:`. The parameters include key streaming output messages. The details of data are as follows.

<span id="c6def1fb"></span>
## data

The returned data field is described in detail as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The core parameters included in the data response message are as follows:</div>



* <div data-tips="true" data-tips-type="tip">type: The type parameter is used to determine the type of the current response message.</div>


   * <div data-tips="true" data-tips-type="tip">For example, init (session initialization), result (model return result), and so on.</div>


   * <div data-tips="true" data-tips-type="tip">The currently supported type enumeration values can be found in <a href="https://docs.byteplus.com/docs/dataagent/Session_Completion#3a3ecdb1">Enumeration values for type</a> below.</div>


* <div data-tips="true" data-tips-type="tip">status: Messages of the same type may include multiple stages in the question process. The status parameter is used to indicate the stage of messages of the same type.</div>


   * <div data-tips="true" data-tips-type="tip">For example, when <code>type=result</code>, it means the returned message is a model result; <code>status=success</code> indicates that the model result was successfully queried.</div>


   * <div data-tips="true" data-tips-type="tip">The currently supported status enumeration values can be found in <a href="https://docs.byteplus.com/docs/dataagent/Session_Completion#e8bc2c7c">Enumeration values for status</a> below.</div>



The current data message types and examples are described as follows.


|Number |Sample message format |Key parameter description |
|---|---|---|
|1 |{"type":"init","query_type":"normal","sub_query_info":[{"question": ${user_input} }],"is_thought_mode":true} |* type: init<br><br>* Message meaning: session initialization message |
|2 |{"sub_id":0,"type":"result","status":"failed","msg":"Error Info","result": |* type: result<br><br>* status：field<br><br>* Message meaning: error message |
|3 | |* type: thought<br><br>* Message meaning: model thinking information message |
|4 | |* type: code<br><br>* Message meaning: model output message, can be ignored. |
|5 | |* type: tool<br><br>* Message meaning: tool invocation process information |
|6 | |* type: debug<br><br>* Message meaning: debug information for multi\-turn or parallel invocation, can be ignored |
|7 |{"round_id": 0, "sub_id": 0, "is_major": true, "type": "exec_context", "content": "\-\- SQL generated by the model \n SELECT DISTINCT City \n FROM `4250665` \n WHERE `City` LIKE '%北%' ;"} |* type: exec_context<br><br>* Message meaning: context information output during tool execution |
|8 | |* type: exec_result<br><br>* Message meaning: tool execution result |
|9 |{"round_id": 1, "sub_id": 0, "type": "tool", "status": "tool_end", "msg": "{Parameters and results of calling tools}"} |* type: tool<br><br>* status：tool_end<br><br>* Message meaning: detailed information about tool invocation |
|9 | |* type: interpret<br><br>* Message meaning: message for explanation after successful completion |
|10 |{"round_id": 0, "sub_id": 0, "type": "result", "status": "success", "msg": "success", "result": {"**historyId**": 4225437, "dataSetId": 4250665}, "title": "What are the cities with the word 'north' in the supermarket dataset", "round_title": "What are the cities with the word 'north' in the supermarket dataset"} |* type: result<br><br>* status：success<br><br>* Message meaning: message for generating historyId |
|11 |{"round_id": null, "sub_id": 0, "type": "result", "status": "success", "msg": "success", "result": {"thought": "The user needs to analyze data trends, but has not specified the time range or the metric definition for analysis. According to the table information, multiple tables contain date fields and different metric fields. The user needs to specify the time range and metric definition.", "fuzzyRequirements": "The time range and metric definition for analysis need to be specified.", "suggestions": [{"options": [{"tableId": 4530118, "value": "2015\-09\-30 to 2022\-01\-05", "tableName": "zhouyf_simple_test_01", "fieldName": "Date of employment", "appId": 1008919}, {"tableId": 4494668, "value": "2015\-01\-01 to 2018\-12\-30", "tableName": "mxl0903 regression", "fieldName": "Order date", "appId": 555163}, {"tableId": 4494668, "value": "2015\-01\-03 to 2019\-01\-06", "tableName": "mxl0903 regression", "fieldName": "Shipping date", "appId": 555163}], "description": "You have not specified the time range. Here are several possible time range options for you. Please select the appropriate time range.", "type": "Time range"}, {"options": [{"tableId": 4530127, "tableName": "zhouyf_simple_test_03", "fieldName": "Deposit balance (CNY)", "appId": 1008919}, {"tableId": 4494668, "tableName": "mxl0903 regression", "fieldName": "Sales amount", "appId": 555163}, {"tableId": 4530123, "tableName": "zhouyf_simple_test_02", "fieldName": "Annual income (ten thousand CNY)", "appId": 1008919}], "description": "You have not specified the metric definition to analyze. Here are several possible metric options for you. Please select the appropriate metric.", "type": "Metric definition"}], "toolCallId": "call_41cplq8c5exulc5jnzc8py1d"}, "title": "", "round_title": ""} |* type: result<br><br>* status：success<br><br>* Message meaning: Clarification message, requires user interaction to confirm information |
|12 |{"sub_id": 0, "round_id": 0, "is_major": true, "type": "report", "status": "success", "result": {"reportId": 11587438, "appId": 555371, "reportName": "Top customers by sales amount", "dataSetName": "Supermarket data \- Zhixing (copy)", "dataSetId": 2978669, "dashboardId": 0, "dashboardName": null, "role": true, "whereList": [{"id": "10000006952807", "name": "Customer names longer than 2 characters", "op": "==", "option": {"customList": [], "desensitizationList": [], "displayType": "multiDropDownList", "filterPattern": "Condition", "isReportFilter": false}, "preRelation": "and", "uniqueId": 250710205658092, "val": [1], "valOption": {"currentTab": "manual"}}]}} |* type: report<br><br>* status：success<br><br>* Message meaning: Chart retrieval message |
|13 |[DONE] |* Message meaning: Message indicating end of conversation |


<span id="3a3ecdb1"></span>
### Enumeration values for type


|Enum value |Description |
|---|---|
|init |Chat initialization signal |
|report |The model returns a chart |
|thought |The model's thought process, or the thought process during tool invocation (execution reasoning). |
|exec_context |Information about the execution process during tool invocation (execution content). |
|exec_result |Summary of the result from tool invocation (execution result). |
|result |The model returns results, including both clarification messages and final results<br><br><br>* Fields returned for clarification:<br><br>   * thought: The thought process for clarification.<br><br>   * fuzzyRequirements: Information requiring user interaction and confirmation.<br><br>   * suggestions: Clarification selection results. The structure is similar to that of `data.clarifyResults.userChoices` in the request parameters.<br><br>* Fields returned for final results:<br><br>   * historyId: The result ID for the current session. For example, when a vague question is broken down into multiple sub\-questions, each sub\-question result will have a session result ID.<br><br>   * dataSetId: The data set ID for querying the result of the current question. |
|code |Some model outputs, which can be ignored. |
|tool |Information related to MCP tool invocation, used for exposing key messages, no need to pay attention. |
|interpret |Data interpretation is enabled only when the "Enable chart analysis" switch is turned on in the "Basic information" section of the agent management console. |
|debug |Partial debug keyframe information, including: generation and results of voting, streaming heartbeat, and more. |


<span id="e8bc2c7c"></span>
### Enumeration values for status


* When `type = result`, the status field has the following enumeration values.

   
   |Enum value |Meaning |
   |---|---|
   |failed |Query failed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">In the returned message, if <code>status=failed</code>, it does not necessarily indicate a query failure. When the agent enables "Multi\-path execution", failures in individual rounds (<code>round_id=1/2/3</code>) can be ignored, and other rounds will automatically correct errors.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If "Multi\-path execution" is not enabled or the primary path of "Multi\-path execution" (<code>round_id=0</code>) has <code>status=failed</code>, it indicates a query failure.</div><br> |
   |success |Query succeeded. |
   |simple_text_shut_down |Simple Q&A ended. |
   

* When `type = tool`, the status field has the following enumeration values.

   
   |Enum value |Meaning |
   |---|---|
   |tool_end |Tool invocation ended. |
   


<span id="21194718"></span>
### Other data field descriptions


* round_id: When the agent enables [multi\-path execution], multiple paths are opened for querying. round_id is used to identify the query path.

* is_major: Indicates whether it is the primary path.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You only need to pay attention to messages where <code>round_id=0</code> and <code>is_major = true</code>.</div>
