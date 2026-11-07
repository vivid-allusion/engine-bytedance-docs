---
title: "ListVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListVersions-en"
---

Gets the list of released code versions for a specified function.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListVersions&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `ListVersions`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |
|Page |Integer |No |Page number. |
|Limit |Integer |No |Number of records per page. Default is 50. Maximum is 50. |
|OrderBy |Integer |No |This parameter specifies the order of data query. It accepts the following values:<br><br><br>* 1: Sort data in descending order.<br><br>* 2 (default): Sort data in ascending order. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example Value |
|---|---|---|---|
|Revisions |Object[] |List of code versions | |
|Id |Long |ID |`1` |
|VersionTag |String |Version number of this version. |`1.0.1` |
|Description |String |Description of this version. |`this is a sparrow` |
|Creator |String |Creator of this version. |`example` |
|TotalCount |Long |Total number of code versions |`1` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListVersions&Version=2021-03-01&FunctionId=3gyz993****&Page=1&Limit=10&OrderBy=2
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022011310282201022524312506*******",
        "Action": "ListVersions",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Revisions": [
            {
                "Id": 133,
                "VersionTag": "1.0.1",
                "Description": "test publish",
                "Creator": "*****"
            }
        ],
        "TotalCount": 1
    }
}
```
