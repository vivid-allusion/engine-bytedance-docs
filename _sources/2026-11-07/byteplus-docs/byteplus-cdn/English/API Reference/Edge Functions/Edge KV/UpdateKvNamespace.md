---
title: "UpdateKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateKvNamespace-en"
---

Updates the description of a namespace.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=UpdateKvNamespace&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `UpdateKvNamespace`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|Namespace |String |Yes |The name of the namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |`test-kv1` |
|NamespaceId |String |Yes |The ID of the namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Description |String |No |The new description for the namespace, with a maximum length of 80 characters. If this parameter is not specified, the original description will be retained. |`test` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="examples"></span>
## Examples

<span id="request-example"></span>
### Request example

```json
POST   https://cdn.byteplusapi.com?Action=UpdateKvNamespace&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Description": "test"
}
```
