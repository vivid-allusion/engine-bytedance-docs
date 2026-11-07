---
title: "Retrieve Task Status"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Retrieve_Task_Status"
---

<span id="f635a0f1"></span>
# **Request description**

Request method: GET

Request URL: https://{domain}/dataAgent/llm/openApi/v2/deepresearch/taskStatus

<span id="12188641"></span>
# **Request parameters**


|Location |Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|QueryParams |id |string |Yes |314b788f83394219afa563e47a2938a9 |Task ID. After you call the "Execute deep research task" API, the returned result contains the task ID of the corresponding execution task. |


<span id="98b37521"></span>
# Request example

```JSON
https://{domain}/dataAgent/llm/openApi/v2/deepresearch/taskStatus?id=314b788f83394219afa563e47a2938a9
```


<span id="4839450d"></span>
# Response parameters


|Location |Parameter |Type |Example value |Description |
|---|---|---|---|---|
|ROOT |taskId |string |314b788f83394219afa563e47a2938a9 |Task ID |
||status |TaskStatus |```JSON```<br>```{```<br>```            "state": "completed",```<br>```            "timestamp": "2025-09-26T14:52:00.878760"```<br>```        }```<br> |The task status for the corresponding deep research task, including the state and timestamp parameters.<br><br><br>* state: The current status of the task, including:<br><br>   * submitted<br><br>   * working<br><br>   * completed<br><br>   * failed<br><br>   * unknown<br><br>* timestamp: The timestamp for the current task status, formatted as an ISO 8601 time string. |


<span id="81c377e6"></span>
# Response example

```JSON
{
    "JSONIFY_PRETTYPRINT_REGULAR": false,
    "code": "llm/ok",
    "data": {
        "status": {
            "state": "completed",
            "timestamp": "2025-09-26T14:52:00.878760"
        },
        "taskId": "314b788f83394219afa563e47a2938a9"
    },
    "msg": {}
}
```
