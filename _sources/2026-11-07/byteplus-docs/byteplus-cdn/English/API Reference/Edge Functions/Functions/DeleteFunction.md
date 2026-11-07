---
title: "DeleteFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteFunction-en"
---

Deletes a function.

<span id="limits"></span>
## Limits

Request rate limit: A maximum of 20 requests can be sent per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=DeleteFunction&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `DeleteFunction`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID |`3gyz993****` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="examples"></span>
## Examples

<span id="request-example"></span>
### Request example

```HTTP
POST  https://cdn.byteplusapi.com?Action=DeleteFunction&Version=2021-03-01
{
  "FunctionId": "3gyz993****"
}
```
