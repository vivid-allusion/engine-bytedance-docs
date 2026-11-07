---
title: "CanaryPublish"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CanaryPublish-en"
---

Performs a canary release for a function.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second. Additionally, for each function, a maximum of 1 request per second is allowed.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=CanaryPublish&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `CanaryPublish`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example Value |
|---|---|---|---|---|
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |`3gyz993****` |
|Description |String |No |Description for this release. |`test publish` |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example value |
|---|---|---|---|
|TicketId |Long |ID of the publish record. |`261285442399182****` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```json
POST https://cdn.byteplusapi.com/?Action=CanaryPublish&Version=2021-03-01
{
    "FunctionId": "3gyz993****",
    "Description": "test publish"
}
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202112072116030102251331430*****",
        "Action": "CanaryPublish",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TicketId": "261285442399182****"
    }
}
```
