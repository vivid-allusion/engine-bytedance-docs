---
title: "Get Session Task List"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Get_Session_Task_List"
---

<span id="976dbdf5"></span>
## A2A Get session task list listTasks

<span id="e7d198ed"></span>
### Request description

Used to query the task list under the specified session ( `contextId`/ `sessionId`), support paging.


* `ContextId`or `sessionId`**required** (choose one).

* `pageSize`defaults to `20`, with values ranging from `1 to 100`; the alias `limit`can also be used.

* It is recommended to use the `nextPageToken`returned by the last response as the `pageToken`for the next request; you can also directly pass the `offset`to turn the page.



|Project |Content |
|---|---|
|request method |`POST` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/` |
|`method` |`ListTasks` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|content type |`Content-Type: application/json` |


&nbsp;

<span id="483ef4db"></span>
### Request parameters

<span id="03df99cd"></span>
#### Top\-level parameters (JSON\-RPC)


|Parameter name |Type |Is it required? |Description |
|---|---|---|---|
|`jsonrpc` |string |Yes |Fixed as `"2.0"` |
|`id` |string |number |Yes |
|`method` |string |Yes |Fixed as `"ListTasks"` |
|`params` |object |Yes |Business parameter objects, see table below |


<span id="10c6a511"></span>
#### Params parameter


|Parameter name |Type |Is it required? |Description |
|---|---|---|---|
|`contextId` |string |No (required to choose one of the two) |Session/Context ID (required with `sessionId`). |
|`sessionId` |string |No (required to choose one of the two) |Session ID (required `with contextId`). |
|`pageSize` |integer |No |Number of entries per page, default `20`, range `1~ 100`. |
|`limit` |integer |No |`Alias for pageSize`. If passed in at the same time as `pageSize`, the priority is subject to the actual interface (it is recommended to pass only one). |
|`pageToken` |string |No |Flip mark. It is recommended to use the `result.nextPageToken`of the last response as the `pageToken`for the next request. |
|`nextPageToken` |string |No |**Returns only in response** . Returns when there is a next page, the `pageToken`for the next request. |
|`offset` |integer |No |Optional offset page turning method (not recommended for mixing with `pageToken`). |


&nbsp;

<span id="fd989a0e"></span>
### Request example

```Plain
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  --header 'Content-Type: application/json' \
  --data-raw '{"jsonrpc":"2.0","id":4,"method":"ListTasks","params":{"sessionId":"6620","pageSize":20,"pageToken":"0"}}' \
  --silent | jq
```


<span id="5b632eee"></span>
### Return parameters

<span id="5f8dd0e8"></span>
#### Top\-level field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`jsonrpc` |string |`2.0` |JSON\-RPC protocol version. |
|`id` |integer |`4` |Request ID, corresponding to the `id`in the request body. |
|`result` |object |*  |Business results after a successful request. |
|`result.tasks` |array |*  |List of tasks under the current session. |
|`result.nextPageToken` |string |`20`/ `eyJvZmZzZXQiOjIwfQ==`(example) |Next page cursor. Returns only if there is a next page; used as `params.pageToken`for the next request. |


<span id="3d62360f"></span>
#### Result.tasks[] field (task object)


|Field path |Type |Sample value |Descriptiontion |
|---|---|---|---|
|`result.tasks[]` |object |*  |Single A2A task object (summary). |
|`result.tasks[].id` |string |`7103` / `7098` |A2A Task ID. |
|`result.tasks[].contextId` |integer |`6620` |The session ID to which the task belongs. |
|`result.tasks[].status` |object |*  |Task state object. |
|`result.tasks[].status.state` |string |`TASK_STATE_COMPLETED` |Task status. The example indicates that the task has been completed. |
|`result.tasks[].metadata` |object |*  |Task extension meta\-information. |


<span id="4b395779"></span>
#### Result.tasks[].metadata field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`result.tasks[].metadata.version` |string |`v5` |AIDA A2A Extended Version. |
|`result.tasks[].metadata.sequence` |integer |`1` |The sequence number of the current task object. |
|`result.tasks[].metadata.phase` |string |`completed` |Mission phase. The example indicates that it has been completed. |
|`result.tasks[].metadata.planStatus` |string |`success` |Plan execution status. The example indicates success. |
|`result.tasks[].metadata.agentId` |integer |`279` |The Agent ID to execute the task. |
|`result.tasks[].metadata.deepResearchTaskId` |integer |`7103` |The corresponding DeepResearch task ID. |
|`result.tasks[].metadata.createTime` |integer |`1786507551000` |Task creation timestamp, in milliseconds. |
|`result.tasks[].metadata.timing` |object |*  |Task time\-consuming information. |


<span id="8f056e83"></span>
### Result.tasks[].metadata.timing field


|Field path |Type |Sample value |Description |
|---|---|---|---|
|`result.tasks[].metadata.timing.createTime` |integer |`1786507551000` |Task creation timestamp in milliseconds. |
|`result.tasks[].metadata.timing.startTime` |integer |`1786507551678` |The task starts execution timestamp (in milliseconds). |
|`result.tasks[].metadata.timing.endTime` |integer |`1786507608679` |End of task timestamp in milliseconds. |
|`result.tasks[].metadata.timing.durationMs` |integer |`57679` |Task execution time (milliseconds). |


<span id="289efc12"></span>
### Back to example

```Plain
{
  "jsonrpc": "2.0",
  "id": 4,
  "result": {
    "tasks": [
      {
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
        }
      }
    ]
  }
}
```
