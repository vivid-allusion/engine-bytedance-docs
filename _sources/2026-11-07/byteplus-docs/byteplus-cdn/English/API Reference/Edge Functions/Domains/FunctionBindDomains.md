---
title: "FunctionBindDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FunctionBindDomainList-en"
---

Associates a function with domain names.

<span id="instructions"></span>
## Instructions

Request limit: Maximum 20 requests per second.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Edge Functions can only be bound to domains that have been added to BytePlus CDN under your current BytePlus account.</div>


<span id="request-details"></span>
## Request details


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=FunctionBindDomains&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of this API is `FunctionBindDomains`. |
|Version |String |Yes |API version. The version of this API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|Domains |String[] |Yes |Enter the domains you want to associate with the function. You can call [ListFunctionDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCDNDomain-cn) to get the list of available CDN domains. |`["test1.example.com","test2.example.com"]` |
|FunctionId |String |Yes |Enter the function ID you want to associate with the domains. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-cn) to get the FunctionId. |`3gyz993****` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```json
POST  https://cdn.byteplusapi.com?Action=FunctionBindDomains&Version=2021-03-01
{
  "FunctionId": "b21f19d28c7f4fbbb8b8bc799f28****",
  "Domains":[
    "a.example.com",
    "b.example.com"
    ]
}
```
