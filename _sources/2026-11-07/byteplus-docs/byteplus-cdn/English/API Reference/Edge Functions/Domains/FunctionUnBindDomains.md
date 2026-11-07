---
title: "FunctionUnBindDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FunctionUnBindDomains-en"
---

Disassociates domain names from a function.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=FunctionUnBindDomains&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `FunctionUnBindDomains`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|Domains |String[] |Yes |Enter the domain names to be disassociated. You can call the [ListFunctionDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCDNDomain-en) API to get a list of available CDN domain names. |`["test1.example.com","test2.example.com"]` |
|FunctionId |String |Yes |Enter the function ID to be disassociated. You can call the [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-en) API to get the FunctionId. |`3gyz993****` |


<span id="response-parameters"></span>
### Response Parameters

None

<span id="example"></span>
## Example

<span id="request-example"></span>
### Request Example

```json
POST  https://cdn.byteplusapi.com?Action=FunctionUnBindDomains&Version=2021-03-01
{
  "FunctionId": "b21f19d28c7f4fbbb8b8bc799f28****",
  "Domains":[
    "a.example.com",
    "b.example.com"
    ]
}
```
