---
title: "SnapshotPublish"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-SnapshotPublish-en"
---

Rolls back the function code to a specified version.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second. Additionally, for each function, a maximum of 1 request per second is allowed.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=SnapshotPublish&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `SnapshotPublish`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |`3gyz993****` |
|VersionTag |String |Yes |Version number. You can call the [ListVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListVersions-en) API to get the version number. |`1.0.1` |
|PublishType |Integer |Yes |Publish type:<br><br><br>* 200: Full release<br><br>* 100: Canary release |`200` |
|Description |String |No |Description for this release. |`test publish` |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example value |
|---|---|---|---|
|TicketId |String |ID of the publish record. |`278335600748419****` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```JSON
POST https://cdn.byteplusapi.com/?Action=SnapshotPublish&Version=2021-03-01
{
    "FunctionId": "3gyz993****",
    "PublishType": 200,
    "VersionTag": "1.0.1"
}
```


<span id="response-example"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202112072116030102251331430*****",
        "Action": "SnapshotPublish",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TicketId": "278335600748419****"
    }
}
```
