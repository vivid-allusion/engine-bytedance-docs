---
title: "EditEnv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-EditEnv-en"
---

Updates the environment variables of a function.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Add, delete, and update operations on environment variables will not take effect until the function is released again.</div>


<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=EditEnv&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `EditEnv`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |`23455331245` |
|Envs |Object[] |Yes |Configuration content |`[{"Key": "abc","Value": "123"}]` |
|Key |String |Yes |Key of the environment variable |`a` |
|Value |String |Yes |Value of the environment variable |`a` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```json
POST  https://cdn.byteplusapi.com?Action=EditEnv&Version=2021-03-01
{
    "FunctionId": "23455331245",
    "Envs": [
        {
            "Key": "abc",
            "Value": "123"
        }
    ]
}
```
