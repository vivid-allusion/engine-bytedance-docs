---
title: "StartCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-StartCronJob-en"
---

Enables a Cron trigger.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=StartCronJob&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `StartCronJob`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |`3gyz993****` |
|JobName |String |Yes |Cron trigger name. |`cron1` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```json
POST  https://cdn.byteplusapi.com?Action=StartCronJob&Version=2021-03-01
{
    "FunctionId":"3gyz993****",
    "JobName":"test1"
}
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022011110011401022524308102B1****",
        "Action": "StartCronJob",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```
