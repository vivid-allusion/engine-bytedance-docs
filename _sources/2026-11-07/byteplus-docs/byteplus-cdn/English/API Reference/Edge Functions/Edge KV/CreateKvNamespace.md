---
title: "CreateKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKvNamespace-en"
---

Creates a namespace.

<span id="instructions"></span>
## Instructions

Request limit: Maximum 20 requests per second.

<span id="request-details"></span>
## Request details


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=CreateKvNamespace&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of this API is `CreateKvNamespace`. |
|Version |String |Yes |API version. The version of this API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|Namespace |String |Yes |Set an identifiable name for the namespace. Input requirements:<br><br><br>* Length must be between 2 and 64 characters.<br><br>* Can only contain letters, numbers, hyphens (\-), and underscores (_).<br><br>* Case\-insensitive, meaning 'Namespace' and 'NAMESPACE' are considered the same. Note that Edge Functions will not convert the case. |`test-kv1` |
|Description |String |No |Set a description for the namespace. The length must not exceed 80 characters. |`test` |
|ProjectName |String |No |The project name to which the namespace belongs. Defaults to `default`. |`default` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```json
POST   https://cdn.byteplusapi.com?Action=CreateKvNamespace&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "Description": "test",
    "ProjectName": "default"
}
```
