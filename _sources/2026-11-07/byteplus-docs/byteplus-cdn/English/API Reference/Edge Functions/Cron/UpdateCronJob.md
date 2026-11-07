---
title: "UpdateCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateCronJob-en"
---

Updates a Cron trigger.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=UpdateCronJob&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `UpdateCronJob`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example Value |
|---|---|---|---|---|
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |`3gyz993****` |
|JobName |String |Yes |Cron trigger name. |`cron1` |
|CronExpression |String |Yes |Cron expression. |`*/1 * * **` |
|Parameter |String |No |Custom parameter. When the function is executed, the edge function passes this parameter to the CronEvent object in the function code. |`cron` |
|Description |String |No |Trigger description. |`test` |
|CronType |Integer |Yes |Execution mode of the Cron trigger.<br><br><br>* 1: Global.<br><br>* 2: Single\-point. |`1` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```json
POST  https://cdn.byteplusapi.com?Action=UpdateCronJob&Version=2021-03-01
{
    "FunctionId":"3gyz993****",
    "JobName":"test1",
    "CronExpression":"*/1 * * * *",
    "Parameter":"cron_al",
    "Description":"",
    "CronType":1
}
```
