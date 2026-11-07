---
title: "Get a Task Snapshot"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Get_a_Task_Snapshot"
---

<span id="2c9ea846"></span>
## A2A Get task snapshot getTask

<span id="ada26d89"></span>
### Request description

Used to get the **current snapshot (snapshot)**  of the specified task. JSON\-RPC `result.task`, including task ID, session ID, current state, meta information, and products written to disk.


|Project |Content |
|---|---|
|request method |`POST` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/` |
|`method` |`GetTask` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|content type |`Content-Type: application/json` |


<span id="693be0bb"></span>
### Request parameters

> The original text does not provide a separate parameter table. The following are the **JSON\-RPC 2.0** request structure parameters organized according to the request description and examples.


<span id="88ffb1f4"></span>
#### Top\-level parameters (JSON\-RPC)


|Parameter name |Type |Is it required? |Description |
|---|---|---|---|
|`jsonrpc` |string |Yes |Fixed as `"2.0"` |
|`id` |string |number |Yes |
|`method` |string |Yes |Fixed as `"GetTask"` |
|`params` |object |Yes |Business parameter objects, see table below |


<span id="5bfff887"></span>
#### Params parameter

The taskId, id, and task.id are the task IDs (choose one of the three), which can be obtained from the [Start Streaming Q & A](https://docs.byteplus.com/docs/dataagent/Start_Streaming_Q_A) SSE return results.


|Parameter name |Type |Is it required? |Description |
|---|---|---|---|
|`id` |string |No (choose one of three) |Task ID (choose one of `taskId`and `task.id`) |
|`taskId` |string |No (choose one of three) |Task ID (choose one of `id`and `task.id`) |
|`task.id` |string |No (choose one of three) |Task ID (choose one of `id`and `taskId`) |
|`contextId` |string |No |Session/Context ID. Additional verification of task and session attribution is passed in |


<span id="5d49221f"></span>
### Request example

Standard Curl Example:

```Plain
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  --header 'Content-Type: application/json' \
  --data-raw '{"jsonrpc":"2.0","id":3,"method":"GetTask","params":{"id":"7103"}}' \
  --silent | jq
```


<span id="31d54f26"></span>
### Return parameters

<span id="4287fcb8"></span>
#### Top\-level field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`jsonrpc` |string |`2.0` |JSON\-RPC protocol version. |
|`id` |integer |`3` |Request ID, corresponding to the `id`in the request body. |
|`result` |object |*  |Business results after a successful request. |
|`result.task` |object |*  |The A2A task details found. |


<span id="14d20080"></span>
#### result.task field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`result.task.id` |string |`7103` |A2A Task ID. |
|`result.task.contextId` |integer |`6620` |The session ID to which the task belongs. |
|`result.task.status` |object |*  |Task state object. |
|`result.task.status.state` |string |`TASK_STATE_COMPLETED` |Task status. The example indicates that the task has been completed. |
|`result.task.metadata` |object |*  |Task extension meta\-information. |
|`result.task.artifacts` |array |*  |List of task products, including step products, tool results, or final products. |


<span id="4e098c69"></span>
#### result.task.metadata field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`result.task.metadata.version` |string |`v5` |AIDA A2A Extended Version. |
|`result.task.metadata.sequence` |integer |`1` |The sequence number of the current task object. |
|`result.task.metadata.phase` |string |`completed` |Mission phase. The example indicates that it has been completed. |
|`result.task.metadata.planStatus` |string |`success` |Plan execution status. The example indicates success. |
|`result.task.metadata.agentId` |integer |`279` |The Agent ID to execute the task. |
|`result.task.metadata.deepResearchTaskId` |integer |`7103` |The corresponding DeepResearch task ID. |
|`result.task.metadata.createTime` |integer |`1786507551000` |Task creation timestamp, in milliseconds. |
|`result.task.metadata.timing` |object |*  |Task time\-consuming information. |


<span id="376dfcba"></span>
#### result.task.metadata.timing field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`result.task.metadata.timing.createTime` |integer |`1786507551000` |Task creation timestamp in milliseconds. |
|`result.task.metadata.timing.startTime` |integer |`1786507551678` |The task starts execution timestamp (in milliseconds). |
|`result.task.metadata.timing.endTime` |integer |`1786507608679` |End of task timestamp in milliseconds. |
|`result.task.metadata.timing.durationMs` |integer |`57679` |Task execution time (milliseconds). |


<span id="1880c103"></span>
#### result.task.artifacts[] field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`result.task.artifacts[].artifactId` |string |`step-710301` |Product ID. Example indicates that the product from step `710301`. |
|`result.task.artifacts[].metadata` |object |*  |Product extension meta\-information. |
|`result.task.artifacts[].parts` |array |*  |List of product content segments. |
|`result.task.artifacts[].name` |string |`Find sales-related datasets, reports, metric definitions, and data portals` |Product name, usually corresponding to the step title. |
|`result.task.artifacts[].description` |string |`Task completed: [Default search tool] Sales, sales trend report, sales data set, sales indicator caliber` |Product description, usually used to illustrate the results of step execution. |


<span id="deab5e64"></span>
#### result.task.artifacts [].metadata field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`result.task.artifacts[].metadata.version` |string |`v5` |AIDA A2A Extended Version. |
|`result.task.artifacts[].metadata.sequence` |integer |`5` |Current product event number. |
|`result.task.artifacts[].metadata.phase` |string |`running` |The stage of the task at which the product was generated. |
|`result.task.artifacts[].metadata.planStatus` |string |`running` |The planned state when the product is generated. |
|`result.task.artifacts[].metadata.kind` |string |`step` |Product type. Examples represent step products. |
|`result.task.artifacts[].metadata.stepAction` |string |`step_changed` |Step action. The example indicates that the step has been updated. |
|`result.task.artifacts[].metadata.stepType` |string |`use_ai_search_tool` |Type of step. The example shows the use of an AI search tool. |
|`result.task.artifacts[].metadata.stepId` |integer |`710301` |Step ID. |
|`result.task.artifacts[].metadata.parentStepId` |integer |`0` |Parent step ID. `0`means no parent step. |
|`result.task.artifacts[].metadata.stepStatus` |integer |`1` |Step status. |
|`result.task.artifacts[].metadata.displayProcess` |boolean |`true` |Whether to show the execution process. |
|`result.task.artifacts[].metadata.llmMessageIndex` |integer |`1` |LLM message index. |
|`result.task.artifacts[].metadata.type` |string |`deep_research_running_step` |Event types compatible with older frontend. |
|`result.task.artifacts[].metadata.status` |integer |`1` |Compatible with the status values of the old frontend. |
|`result.task.artifacts[].metadata.assets` |array |*  |Step associate asset list. |
|`result.task.artifacts[].metadata.timing` |object |*  |Current step or tool call time\-consuming information. |
|`result.task.artifacts[].metadata.displayTitleWithDescription` |boolean |`false` |Whether to display a combination of title and description. |


<span id="e6b71571"></span>
#### result.task.artifacts [].metadata.timing field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`result.task.artifacts[].metadata.timing.toolName` |string |`unified_internal_search` |Tool name. |
|`result.task.artifacts[].metadata.timing.startTime` |integer |`1786507556246` |The tool starts executing timestamp in milliseconds. |
|`result.task.artifacts[].metadata.timing.endTime` |integer |`1786507556840` |The tool finishes execution timestamp in milliseconds. |
|`result.task.artifacts[].metadata.timing.durationMs` |integer |`594` |Tool execution time (milliseconds). |


<span id="0c938ced"></span>
#### result.task.artifacts[].metadata .assets[] field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`result.task.artifacts[].metadata.assets[].type` |string |`knowledge` |Asset type. Example represents a knowledge base/knowledge asset. |
|`result.task.artifacts[].metadata.assets[].createTime` |integer |`1786507556829` |Asset generation or retrieval timestamp in milliseconds. |
|`result.task.artifacts[].metadata.assets[].title` |string |`E-commerce platform sales data _ test (1).xlsx` |Asset title. |
|`result.task.artifacts[].metadata.assets[].version` |string |null |`null` |
|`result.task.artifacts[].metadata.assets[].contentType` |string |null |`null` |
|`result.task.artifacts[].metadata.assets[].content` |string |`E-commerce platform sales data _ test (1) xlsx_Sheet1... (truncated)` |Asset content summary (truncated in the example). |
|`result.task.artifacts[].metadata.assets[].result` |object |null |`null` |
|`result.task.artifacts[].metadata.assets[].url` |string |`https://[DOMAIN_REDACTED]/...` |Asset access address (domain name is desensitized in the example). |
|`result.task.artifacts[].metadata.assets[].iconUrl` |string |null |`null` |
|`result.task.artifacts[].metadata.assets[].keywords` |array |null |`null` |


<span id="d4ed17c4"></span>
#### result.task.artifacts[].parts[] field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`result.task.artifacts[].parts[].text` |string |`""` |Text fragment content. Example is an empty string. |
|`result.task.artifacts[].parts[].data` |object |*  |JSON data fragment. The example is used to host the retrieved knowledge asset information. |
|`result.task.artifacts[].parts[].mediaType` |string |`text/plain` / `application/json` |Content snippet media type. |


<span id="c4636142"></span>
#### result.task.artifacts [] .parts [] .data field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`result.task.artifacts[].parts[].data.type` |string |`knowledge` |Data type. Examples represent knowledge assets. |
|`result.task.artifacts[].parts[].data.createTime` |integer |`1786507556829` |Data generation or retrieval timestamp in milliseconds. |
|`result.task.artifacts[].parts[].data.title` |string |`E-commerce platform sales data _ test (1).xlsx` |Data title. |
|`result.task.artifacts[].parts[].data.version` |string |null |`null` |
|`result.task.artifacts[].parts[].data.contentType` |string |null |`null` |
|`result.task.artifacts[].parts[].data.content` |string |`E-commerce platform sales data _ test (1) xlsx_Sheet1... (truncated)` |Data content summary (truncated in the example). |
|`result.task.artifacts[].parts[].data.result` |object |null |`null` |
|`result.task.artifacts[].parts[].data.url` |string |`https://[DOMAIN_REDACTED]/...` |Data resource access address (domain name is desensitized in the example). |
|`result.task.artifacts[].parts[].data.iconUrl` |string |null |`null` |
|`result.task.artifacts[].parts[].data.keywords` |array |null |`null` |


<span id="df507290"></span>
### Structure description


|Project |Description |
|---|---|
|`result.task.status.state = TASK_STATE_COMPLETED` |Indicates that the task has been completed. |
|`result.task.metadata.phase = completed` |Indicates that the overall phase of the task has been completed. |
|`result.task.metadata.planStatus = success` |Indicates that the task plan was successfully executed. |
|`result.task.artifacts` |Collection of mission history products. The example returns a search step product. |
|`artifact.metadata.stepType = use_ai_search_tool` |Indicates that this step uses an AI search tool. |
|`artifact.metadata.assets` |List of assets retrieved in this step. |
|`artifact.parts` |A fragment of the same product. The example contains an empty text fragment and a JSON data fragment. |


<span id="70bd2a9e"></span>
### Back to example

```Plain
{
  "jsonrpc": "2.0",
  "id": 3,
  "result": {
    "task": {
      "id": "7103",
      "contextId": 6620,
      "status": {
        "state": "TASK_STATE_COMPLETED"
      },
      "metadata": {
        "version": "v5",
        "sequence": 1,
        "phase": "completed",
        "planStatus": "success",
        "agentId": 279,
        "deepResearchTaskId": 7103,
        "createTime": 1786507551000,
        "timing": {
          "createTime": 1786507551000,
          "startTime": 1786507551678,
          "endTime": 1786507608679,
          "durationMs": 57679
        }
      },
      "artifacts": [
        {
          "artifactId": "step-710301",
          "metadata": {
            "version": "v5",
            "sequence": 5,
            "phase": "running",
            "planStatus": "running",
            "kind": "step",
            "stepAction": "step_changed",
            "stepType": "use_ai_search_tool",
            "stepId": 710301,
            "parentStepId": 0,
            "stepStatus": 1,
            "displayProcess": true,
            "llmMessageIndex": 1,
            "type": "deep_research_running_step",
            "status": 1,
            "assets": [
              {
                "type": "knowledge",
                "createTime": 1786507556829,
                "title": "E-commerce platform sale data_test(1).xlsx",
                "version": null,
                "contentType": null,
                "content": "E-commerce platform sale data_test(1).xlsx_Sheet1... (truncated)",
                "result": null,
                "url": "https://[DOMAIN_REDACTED]/minio.cdp.rag/rag-1/1/E-commerce platform sale data_test_1.xlsx",
                "iconUrl": null,
                "keywords": null
              }
            ],
            "timing": {
              "toolName": "unified_internal_search",
              "startTime": 1786507556246,
              "endTime": 1786507556840,
              "durationMs": 594
            },
            "displayTitleWithDescription": false
          },
          "parts": [
            {
              "text": "",
              "mediaType": "text/plain"
            },
            {
              "data": {
                "type": "knowledge",
                "createTime": 1786507556829,
                "title": "E-commerce platform sale data_test(1).xlsx",
                "version": null,
                "contentType": null,
                "content": "E-commerce platform sale data_test(1).xlsx_Sheet1... (truncated)",
                "result": null,
                "url": "https://[DOMAIN_REDACTED]/minio.cdp.rag/rag-1/1/E-commerce platform sale data_test_1.xlsx",
                "iconUrl": null,
                "keywords": null
              },
              "mediaType": "application/json"
            }
          ],
          "name": "Search for sales related datasets, reports, metric definitions, and data entry",
          "description": "Task completed: [Default Search Tool] Sales, Sales Trend Report, Sales Dataset, Sales Metric Criteria"
        }
      ]
    }
  }
}
```
