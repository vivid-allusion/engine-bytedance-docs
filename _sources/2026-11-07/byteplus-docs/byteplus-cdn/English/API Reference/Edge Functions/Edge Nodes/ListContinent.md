---
title: "ListContinent"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListContinent-en"
---

Gets the list of continents where available edge nodes are located for a specified function.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListContinent&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `ListContinent`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example Value |
|---|---|---|---|
|Continents |String[] |List of continents. |`["Asia"]` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListContinent&Version=2021-03-01&FunctionId=3gyz993****
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "ListContinent",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Continents": [
            "Asia"
        ]
    }
}
```
