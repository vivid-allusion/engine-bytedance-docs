---
title: "CreateCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateCronJob-en"
---

Creates a Cron trigger.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=CreateCronJob&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `CreateCronJob`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example Value |
|---|---|---|---|---|
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |`3gyz993****` |
|JobName |String |Yes |Cron trigger name. The name must meet the following requirements:<br><br><br>* The name must be unique for each function.<br><br>* Length of the name cannot exceed 128 characters. |`cron1` |
|CronExpression |String |Yes |Cron expression. See [Supported Cron expressions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers#supported-cron-expressions) |`*/1 * * **` |
|Parameter |String |No |Custom parameter. When the function is executed, the edge function passes this parameter to the CronEvent object in the function code. |`cron` |
|Description |String |No |Cron trigger description. |`test` |
|CronType |Integer |Yes |Cron trigger execution mode:<br><br>&nbsp;<br><br>1: Global: Execute on all edge nodes.<br><br>&nbsp;<br><br>2: Single\-point: Execute randomly on any one edge node. |`1` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```json
POST  https://cdn.byteplusapi.com?Action=CreateCronJob&Version=2021-03-01
{
    "FunctionId":"3gyz993****",
    "JobName":"test1111",
    "CronExpression":"5 4 * * *",
    "Parameter":"fetch_1",
    "Description":"",
    "CronType":2
}
```
