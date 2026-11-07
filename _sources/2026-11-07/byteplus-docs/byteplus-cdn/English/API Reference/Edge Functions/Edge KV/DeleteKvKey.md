---
title: "DeleteKvKey"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteKvKey-en"
---

Deletes a key\-value pair.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=DeleteKvKey&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `DeleteKvKey`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|Namespace |String |Yes |The name of the KV namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |`test-kv1` |
|NamespaceId |String |Yes |The ID of the KV namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Key |String |Yes |The key of the key\-value pair to be deleted. |`testkey` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```json
POST  https://cdn.byteplusapi.com?Action=DeleteKvKey&Version=2021-03-01
{
    "Namespace":"test-kv1",
    "NamespaceId":"46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key":"testkey"
}
```
