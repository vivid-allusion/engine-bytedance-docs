---
title: "CreateFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateFunction-en"
---

Creates a function.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=CreateFunction&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `CreateFunction`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|Name |String |Yes |Function name. The naming rules are as follows:<br><br><br>* Can use uppercase letters, lowercase letters, numbers, and hyphens (\-).<br><br>* The name should not be longer than 128 characters. |`test-Function` |
|ProjectName |String |No |The name of the project to which the function belongs. The default value is `default`. |`default` |
|Remark |String |No |Remarks for this function. Input requirements are as follows:<br><br><br>* Any characters are allowed.<br><br>* The length should not exceed 128 characters. |`This is a test Function` |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example value |
|---|---|---|---|
|FunctionId |String |The ID of the function. |`3gyz993****` |


<span id="examples"></span>
## Examples

<span id="request-example"></span>
### Request example

```HTTP
POST  https://cdn.byteplusapi.com?Action=CreateFunction&Version=2021-03-01
{
  "Name": "test-Function"
}
```


<span id="response-example"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202404220916070BE49FB085D18E85BA26",
    "Action": "CreateFunction",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
    "FunctionId": "bc36dc7c58e942f0b9f125d186df****"
  }
}
```
