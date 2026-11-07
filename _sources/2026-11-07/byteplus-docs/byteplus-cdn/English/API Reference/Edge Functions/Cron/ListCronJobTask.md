---
title: "ListCronJobTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJobTask-en"
---

Gets the task execution list for a specified Cron trigger.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListCronJobTask&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `ListCronJobTask`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |
|JobName |String |Yes |Trigger name. |
|Page |Integer |No |Page number. |
|Limit |Integer |No |The number of records per page. The default is 50. The maximum is 50. |
|OrderBy |Integer |No |This parameter specifies the order of data query. It accepts the following values:<br><br><br>* 1: Sort data in descending order.<br><br>* 2 (default): Sort data in ascending order. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example Value |
|---|---|---|---|
|Tasks |Object[] |Task execution list of the Cron trigger. | |
|JobName |String |Name of the Cron trigger. |`cron1` |
|CronExpression |String |Cron expression. |`*/1 * * **` |
|Parameter |String |Custom parameter. When the function is executed, the edge function passes this parameter to the CronEvent object in the function code. |`cron` |
|CronTaskStatus |Long |Task status. |`1` |
|Description |String |Task description. |`test` |
|Uuid |String |UUID of the task. |`2xju****` |
|CreateTime |Long |Creation time. The format is Unix timestamp (seconds). |`1638326159` |
|UpdateTime |Long |Update time. The format is Unix timestamp (seconds). |`1638326159` |
|TotalCount |Long |Total number of task execution records. |`1` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCronJobTask&Version=2021-03-01&FunctionId=3gyz993****&JobName=cron1&Page=1&Limit=10&OrderBy=2
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "ListCronJobTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Tasks": [
            {
                "JobName": "cron1",
                "CronExpression": "*/30 * * * *",
                "Parameter": "cron_all",
                "JobState": 1,
                "CronTaskStatus": 6,
                "Description": "",
                "Uuid": "2xl2****",
                "CreateTime": 1639625400,
                "UpdateTime": 1639625401
            }
        ],
        "TotalCount": 1
    }
}
```
