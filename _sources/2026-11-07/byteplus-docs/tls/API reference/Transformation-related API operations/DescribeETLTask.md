---
title: "DescribeETLTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeETLTask"
---

Call DescribeETLTask to obtain the detailed information of the specified data transformation task.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **GET**

* Request URL: **https://tls\-{Region}.bytepluses.com/DescribeETLTask**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TaskId |String |True |`f3e901c3-b17f-42fd-aa8c-dc91a6c7****` |The ID of the transformation task to be queried. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|CreateTime |String |`2022-12-01 14:01:02` |The creation time of the transformation task. |
|DSLType |String |`NORMAL` |The DSL type is fixed to NORMAL. |
|Description |String |`This is a test project` |A brief description of the data transformation task. |
|ETLStatus |String |`WAITING` |The task scheduling status.<br><br><br>* WAITING: Preparing.<br><br>* RUNNING: Running.<br><br>* STOPPING: Stopping.<br><br>* STOPPED: Stopped.<br><br>* RESTARTING: Restarting. |
|Enable |Boolean |`true` |Whether to enable the data transformation task. Optional values:<br><br><br>* true: Enable.<br><br>* false: Disable. |
|FromTime |Integer |`1643684482` |The start time of the data to be processed. Empty represents processing all historical data. |
|LastEnableTime |String |`2022-12-01 14:01:02` |The recent startup time. |
|ModifyTime |String |`2022-12-01 14:01:02` |The modification time of the transformation task. |
|Name |String |`etl-task-name` |The name of the transformation task. |
|ProjectId |String |`f***********` |The ID of the project where the data to be processed is located. |
|ProjectName |String |`myproject` |The name of the project where the data to be processed is located. |
|Script |String |`f_set("key","value")` |The transformation rules. |
|SourceTopicId |String |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the topic where the data to be processed is located. |
|SourceTopicName |String |`test-topic` |The name of the topic where the data to be processed is located. |
|TargetResources |Array of [TargetResourcesResp](https://docs.byteplus.com/en/docs/38/36172#targetresourcesresp) |`/` |The Related information of the output target. |
|TaskId |String |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the transformation task. |
|TaskType |String |`resident` |The task type is fixed to resident. |
|ToTime |Integer |`1643684482` |The end time of the data range for log processing. Empty means there is no limit. |


<span id="targetresourcesresp"></span>
### TargetResourcesResp


|Name |Type |Example |Description |
|---|---|---|---|
|Alias |String |`test` |Customize the name of the output target, which will be used to refer to the output target in the data transformation rules. |
|TopicId |String |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the topic for storing processed logs. |
|ProjectId |String |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the project for storing processed logs. |
|TopicName |String |`mytopic` |The name of the log topic for storing processed logs. |
|ProjectName |String |`myproject` |The name of the project for storing processed logs. |


<span id="sample-request"></span>
## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/DescribeETLTask?&TaskId=f3e901c3-b17f-42fd-aa8c-dc91a6c7**** HTTP/1.1
Content-Type: application/json
```


<span id="sample-response"></span>
## Sample Response

```json
{
            "TaskId": "e9b00e4a-ae***c4-83e5-a38d7f73ebfc",
            "Name": "zy-access-",
            "SourceTopicId": "5687efb0-4a*****5-4447770a3fe6",
            "SourceTopicName": "access-log",
            "DSLType": "NORMAL",
            "Script": "e_keep(f_has(\"__time__\"))",
            "TaskType": "Resident",
            "TargetResources": [
                {
                    "TopicId": "e2cc153d-3ba8-4****80e1ef1bead9",
                    "TopicName": "topic1",
                    "ProjectId": "4012777e-c******dc4b3a4ab",
                    "ProjectName": "zy-test",
                    "Alias": "target"
                }
            ],
            "Enable": true,
            "Description": "test",
            "ETLStatus": "RUNNING",
            "FromTime": 1709025132,
            "CreateTime": "2024-02-27 17:12:30",
            "ModifyTime": "2024-02-27 17:12:49",
            "LastEnableTime": "2024-02-27 17:12:30",
            "ProjectId": "d11be542-****170-72c318262132",
            "ProjectName": "log-sy"
        }
```


<span id="error-code"></span>
## Error code

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
