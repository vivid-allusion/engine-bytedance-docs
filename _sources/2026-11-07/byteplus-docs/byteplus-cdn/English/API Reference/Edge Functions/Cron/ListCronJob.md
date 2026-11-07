---
title: "ListCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJob-en"
---

Get the list of Cron triggers.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListCronJob&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `ListCronJob`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |
|Page |Integer |No |Page number. |
|Limit |Integer |No |Number of records per page. Default is 50. The maximum is 50. |
|OrderBy |Integer |No |This parameter specifies the order of data query. It accepts the following values:<br><br><br>* 1: Sort data in descending order.<br><br>* 2 (default): Sort data in ascending order. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example Value |
|---|---|---|---|
|Jobs |Object[] |List of triggers. | |
|JobName |String |Cron trigger name. |`cron1` |
|CronExpression |String |Cron expression. |`*/1 * * **` |
|Parameter |String |Custom parameter. When the function is executed, the edge function passes this parameter to the CronEvent object in the function code. |`cron` |
|Description |String |Trigger description. |`test` |
|JobState |Long |Trigger status.<br><br><br>* 1: Execution pending<br><br>* 3: Disabled<br><br>* 4: Execution canceled |`1` |
|CronType |Integer |Cron trigger execution mode. Possible values are:<br><br>&nbsp;<br><br>1: Global: Execute on all edge nodes.<br><br>&nbsp;<br><br>2: Single\-point: Execute on a random edge node. |`1` |
|CreateTime |Long |Creation time. The format is Unix timestamp (seconds). |`1638326159` |
|UpdateTime |Long |Update time. The format is Unix timestamp (seconds). |`1638326159` |
|TotalCount |Long |Total number of triggers. |`1` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCronJob&Version=2021-03-01&FunctionId=3gyz993****&Page=1&Limit=10&OrderBy=2
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "ListCronJob",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Jobs": [
            {
                "JobName": "cron2",
                "CronExpression": "*/59 * * * *",
                "Parameter": "cron_all",
                "Description": "",
                "JobState": 1,
                "CronType": 2,
                "Operator": "****",
                "CreateTime": 1638871686,
                "UpdateTime": 1638871686
            }
        ],
        "TotalCount": 1
    }
}
```
