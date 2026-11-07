---
title: "UpdateCountryCluster"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateCountryCluster-en"
---

Updates the edge nodes included in the canary environment or the full release environment.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=UpdateCountryCluster&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `UpdateCountryCluster`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |`3gyz993****` |
|ClusterType |Integer |Yes |Type.<br><br><br>* 100: Canary environment<br><br>* 200: Production environment |`100` |
|Countries |String[] |Yes |Countries or regions where edge nodes are located. |`["Singapore"]` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```json
POST  https://cdn.byteplusapi.com?Action=UpdateCountryCluster&Version=2021-03-01
{
    "ClusterType": 200,
    "Countries": [
        "Singapore"
    ],
    "FunctionId": "3gyz993****",
}
```
