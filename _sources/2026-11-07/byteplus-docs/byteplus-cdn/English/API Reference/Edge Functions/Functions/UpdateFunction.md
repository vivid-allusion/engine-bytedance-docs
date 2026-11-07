---
title: "UpdateFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateFunction-en"
---

Updates the name or description of a function.

<span id="limits"></span>
## Limits

Request rate limit: A maximum of 20 requests can be sent per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=UpdateFunction&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of this API is `UpdateFunction`. |
|Version |String |Yes |API version. The version of this API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to obtain the function ID |`3gyz993****` |
|Name |String |Yes |New function name. The name must meet the following requirements:<br><br><br>* Can only contain letters, numbers, and hyphens (\-).<br><br>* Must not exceed 128 characters in length. |`test-Function2` |
|Remark |String |No |Remarks for this function. Input requirements are as follows:<br><br><br>* Any characters are allowed.<br><br>* Should not exceed 80 characters in length. |`This is a test Function` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```json
POST  https://cdn.byteplusapi.com/?Action=UpdateFunction&Version=2021-03-01
{
  "FunctionId": "bc36dc7c58e942f0b9f125d186df54d9",
  "Name": "test-doc",
  "Remark": ""
}
```
