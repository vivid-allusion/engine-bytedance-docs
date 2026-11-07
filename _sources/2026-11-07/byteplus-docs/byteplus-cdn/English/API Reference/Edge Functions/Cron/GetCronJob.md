---
title: "GetCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetCronJob-en"
---

Gets detailed information about a Cron trigger.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=GetCronJob&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `GetCronJob`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |
|JobName |String |Yes |Trigger name. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example value |
|---|---|---|---|
|Job |Object[] |Cron trigger list. |`Task details` |
|JobName |String |Trigger name. |`cron2` |
|CronExpression |String |Cron expression. |`*/1 * * **` |
|Parameter |String |Custom parameter. When the function is executed, the edge function passes this parameter to the CronEvent object in the function code. |`cron` |
|Description |String |Description of the Cron trigger. |`test` |
|JobState |Long |Status of the Cron trigger.<br><br><br>* 1: Pending execution<br><br>* 3: Disabled<br><br>* 4: Execution canceled |`1` |
|CronType |Integer |Execution mode of the Cron trigger.<br><br><br>* 1: Global<br><br>* 2: Single\-point |`1` |
|CreateTime |Long |Creation time. The format is Unix timestamp (seconds). |`1638326159` |
|UpdateTime |Long |Update time. The format is Unix timestamp (seconds). |`1638326159` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET https://cdn.byteplusapi.com?Action=GetCronJob&Version=2021-03-01&FunctionId=3gyz993****&JobName=cron2
```


<span id="response-example"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20211207213413010225146063****",
    "Action": "GetCronJob",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
    "Job": {
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
  }
}
```
