---
title: "ListCronJobTaskLog"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJobTaskLog-en"
---

Gets the task execution log list for a specified Cron trigger.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListCronJobTaskLog&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `ListCronJobTaskLog`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |
|JobName |String |Yes |Cron trigger name. |
|Uuid |String |Yes |Task UUID. You can call [ListCronJobTask](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJobTask-en) to get the task UUID. |
|Page |Integer |No |Page number. |
|Limit |Integer |No |Number of records per page. Default is 50. Maximum is 50. |
|OrderBy |Integer |No |This parameter specifies the order of the query data and accepts the following values:<br><br><br>* 1: Sort data in descending order.<br><br>* 2 (default): Sort data in ascending order. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example value |
|---|---|---|---|
|Logs |Object[] |Log list. | |
|JobName |String |Task name. |`cron1` |
|CronExpression |String |Cron expression. |`*/1 * * **` |
|Parameter |String |Custom parameter. |`cron` |
|Continent |String |Continent. |`America` |
|Country |String |Country or region. |`America` |
|JobState |Long |Task status.<br><br><br>* 1: Executed<br><br>* 3: Disabled<br><br>* 4: Not executed |`1` |
|Description |String |Task description. |`test` |
|Uuid |String |Task UUID |`2xuls***` |
|SchedulerState |Long |Task status.<br><br><br>* 5: Execution failed.<br><br>* 6: Execution completed. |`5` |
|ResponseMsg |String |Response message |`this is a msg` |
|CreateTime |Long |Creation time. |`1638326159` |
|UpdateTime |Long |Update time. |`1638326159` |
|TotalCount |Long |Total number of logs. |`1` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCronJobTaskLog&Version=2021-03-01&FunctionId=3gyz993****&JobName=cron1&Uuid=2xl2l4u****&Page=1&Limit=10&OrderBy=2
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "ListCronJobTaskLog",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Logs": [
            {
                "JobName": "cron1",
                "CronExpression": "*/30 * * * *",
                "Event": "cron",
                "Parameter": "cron_all",
                "ClusterName": "test-local",
                "ClusterAlias": "telecom",
                "JobState": 1,
                "Uuid": "2xl2****",
                "SchedulerState": 6,
                "ResponseMsg": "",
                "CreateTime": 1639625401,
                "UpdateTime": 1639625401
            }
        ],
        "TotalCount": 1
    }
}
```
