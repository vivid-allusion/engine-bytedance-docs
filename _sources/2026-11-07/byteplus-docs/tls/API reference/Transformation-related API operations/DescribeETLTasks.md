---
title: "DescribeETLTasks"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeETLTasks"
---

Call the DescribeETLTasks API to obtain the list of transformation tasks.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **GET**

* Request URL: **https://tls\-{Region}.bytepluses.com/DescribeETLTasks**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectId |String |False |`f3e901c3-b17f-42fd-aa8c-dc91a6c7****` |Specify the project ID, which is used to query the data transformation tasks under the specified project. |
|ProjectName |String |False |`myproject` |Specify the project name, which is used to query the data transformation tasks under the specified project. Fuzzy search is supported. |
|IamProjectName |String |False |`default` |Specify the IAM project name, which is used to query the data transformation tasks under the IAM project. |
|SourceTopicId |String |False |`f3e901c3-b17f-42fd-aa8c-dc91a6c7****` |Specify the topic ID, which is used to query the data transformation tasks related to this topic. |
|SourceTopicName |String |False |`topic` |Specify the log topic name for querying data processing tasks related to that log topic. Fuzzy matching is supported. |
|TaskId |String |False |`f3e901c3-b17f-42fd-aa8c-dc91a6c7****` |Specify the transformation task ID. |
|TaskName |String |False |`test-task` |Specify the transformation Task name. |
|Status |String |False |`WAITING` |Specify the transformation task status used to query transformation tasks in that state. |
|PageNumber |Integer |False |`10` |The page number when performing paged query. The default value is 1, that is, the data of the first page will be returned. |
|PageSize |Integer |False |`20` |The paging size. The default is 20, and the maximum is 100. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|Tasks |Array of [DescribeETLTaskResp](https://docs.byteplus.com/en/docs/38/36173#describeetltaskresp) |`/` |The detailed information of the transformation task. |
|Total |Integer |`5` |The number of transformation tasks. |


<span id="describeetltaskresp"></span>
### DescribeETLTaskResp


|Name |Type |Example |Description |
|---|---|---|---|
|Name |String |`etl-task-name` |The transformation Task Name. |
|Enable |Boolean |`true` |The transformation task running status. |
|Script |String |`f_set("key","value")` |The transformation Rules. |
|TaskId |String |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The processing task ID. |
|ToTime |Integer |`1643684482` |The end time of the data range for log processing. Empty means there is no limit. |
|DSLType |String |`NORMAL` |The DSL type is fixed to NORMAL. |
|FromTime |Integer |`1643684482` |The start time of the data to be processed. Empty represents processing all historical data. |
|TaskType |String |`Resident` |The task type is fixed to resident. |
|ETLStatus |String |`WAITING` |The task scheduling status.<br><br><br>* WAITING: Preparing.<br><br>* RUNNING: Running.<br><br>* STOPPING: Stopping.<br><br>* STOPPED: Stopped.<br><br>* RESTARTING: Restarting. |
|ProjectId |String |`f***********` |The ID of the project where the data to be processed is located. |
|CreateTime |String |`2022-12-01 14:01:02` |The creation time of the transformation task. |
|ModifyTime |String |`2022-12-01 14:01:02` |The modification time of the transformation task. |
|Description |String |`This is a test project` |A brief description of the data transformation task. |
|ProjectName |String |`myproject` |The name of the project where the data to be processed is located. |
|SourceTopicId |String |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the topic where the data to be processed is located. |
|LastEnableTime |String |`2022-12-01 14:01:02` |The recent startup time. |
|SourceTopicName |String |`test-topic` |The name of the topic where the data to be processed is located. |
|TargetResources |Array of [TargetResourcesResp](https://docs.byteplus.com/en/docs/38/36173#targetresourcesresp) |`targettopic` |The Related information of the output target. |


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
GET https://tls-{Region}.bytepluses.com/DescribeETLTasks?&ProjectId=f3e901c3-b17f-42fd-aa8c-dc91a6c7****&ProjectName=&IamProjectName=&SourceTopicId=f3e901c3-b17f-42fd-aa8c-dc91a6c7****&SourceTopicName=topic名称&TaskId=f3e901c3-b17f-42fd-aa8c-dc91a6c7****&TaskName=test-task&PageNumber=10&PageSize=20 HTTP/1.1
Content-Type: application/json
```


<span id="sample-response"></span>
## Sample Response

```json
{
    "Total": 2,
    "Tasks": [
        {
            "TaskId": "e9b00e4a-ae***c4-83e5-a38d7f73ebfc",
            "Name": "zy-access-",
            "SourceTopicId": "5687efb0-4ada*****5-4447770a3fe6",
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
        },
        {
            "TaskId": "597887ea-b6b****8289b92fec2",
            "Name": "search-server-test",
            "SourceTopicId": "ffbcf0dd****9bc2-e5702e159e23",
            "SourceTopicName": "search-server-log",
            "DSLType": "NORMAL",
            "Script": "e_keep(f_search(\"__content__:\\\"task done\\\"\"))\next_kv(\"__content__\", pair_sep=\"] [\", kv_sep=\":\", prefix=\"\", suffix=\"\", mode=\"fill\")\nf_set(\"ReqId\", regex_replace(v(\"__content__\"), \".*ReqId:([0-9a-z_.:]*).*\", replace=\"$1\"))\nf_drop(\"__content__\", \"__context_flow__\", \"\")\nf_set(\"insertResultCost\", str_replace(v(\"insertResultCost\"), \"us]\", \"\", 1))\nf_set(\"searchTotalCost\", str_replace(v(\"searchTotalCost\"), \"us]\", \"\", 1))\nf_set(\"resultSize\", str_replace(v(\"resultSize\"), \"]\", \"\", 1))\nf_set(\"ReadRawQuotaTotalCostUs\", str_replace(v(\"ReadRawQuotaTotalCostUs\"), \"]\", \"\", 1))\ne_keep(f_has(\"HitFiles\"))",
            "TaskType": "Resident",
            "TargetResources": [
                {
                    "TopicId": "affa167b-d2****ec-e202a98cfa7a",
                    "TopicName": "search-server-static",
                    "ProjectId": "d11be542-3ba2*****72c318262132",
                    "ProjectName": "log-sy",
                    "Alias": "target"
                }
            ],
            "Enable": true,
            "Description": "",
            "ETLStatus": "RUNNING",
            "FromTime": 1709010000,
            "CreateTime": "2024-02-27 17:08:10",
            "ModifyTime": "2024-02-27 17:08:30",
            "LastEnableTime": "2024-02-27 17:08:10",
            "ProjectId": "d11be542-3ba2*****318262132",
            "ProjectName": "log-sy"
        }
    ]
}
```


<span id="error-code"></span>
## Error code

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
