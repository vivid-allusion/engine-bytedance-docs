---
title: "CreateETLTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/CreateETLTask"
---

Call the CreateETLTask interface to create a transformation task.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/CreateETLTask**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|DSLType |String |True |`NORMAL` |The DSL type is fixed to NORMAL. |
|Description |String |False |`This is a test project` |A brief description of the data transformation task.<br><br><br>* The characters `<>`, `'`, `\`, `\\` are not supported.<br><br>* The length is from 0 to 64 characters. |
|Enable |Boolean |True |`true` |Whether to enable the data transformation task. Optional values:<br><br><br>* true: Enable.<br><br>* false: Disable. |
|FromTime |Integer |False |`1643684482` |The start time of the data to be processed. |
|Name |String |True |`etl-task-name` |The name of the transformation task, please refer to the [Resource Naming Convention](https://docs.byteplus.com/en/docs/tls/Limits#resource-naming-limit). |
|Script |String |True |`f_set("key","value")` |The transformation rules. |
|SourceTopicId |String |True |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the topic where the data to be processed is located. |
|TargetResources |Array of [TargetResources](https://docs.byteplus.com/en/docs/38/36169#targetresources) |True |`/` |The Related information of the output target. |
|TaskType |String |True |`resident` |The task type is fixed to resident. |
|ToTime |Integer |False |`1675393337` |The end time of the data to be processed. |


<span id="targetresources"></span>
### TargetResources


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Alias |String |True |`test` |Customize the name of the output target, which will be used to refer to the output target in the data transformation rules. |
|TopicId |String |True |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The log topic used to store the processed logs. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|TaskId |String |`063e66a3-7764-4bdc-****-709a2f4219b4` |The ID of the transformation task. |


<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/CreateETLTask HTTP/1.1
Content-Type: application/json
POST https://tls-{Region}.bytepluses.com/CreateScheduleSqlTask HTTP/1.1
Content-Type: application/json
{
    "TaskName":"test2",
    "Description":"测试",
    "TopicID":"c5c6b3a7-c730-4527-8d5f-e527b381****",
    "DestRegion":"cn-shanghai",
    "DestTopicID":"66b42cb6-3436-44ae-97bf-efab3043****",
    "Status": 1,
    "ProcessStartTime":1689042649,
    "RequestCycle":{
        "Type":"Period",
        "Time":1
    },
    "ProcessTimeWindow":"@m-m,@m",
    "Query":"",
    "ProcessSqlDelay": 0
}
```


<span id="sample-response"></span>
## Sample Response

```json
{"TaskId": "063e66a3-7764-4bdc-****-709a2f4219b4"}
```


<span id="error-code"></span>
## Error code

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
