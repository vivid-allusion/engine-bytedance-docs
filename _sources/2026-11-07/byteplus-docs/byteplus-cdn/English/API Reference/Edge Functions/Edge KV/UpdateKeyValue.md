---
title: "UpdateKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateKeyValue-en"
---

Updates the value and TTL of a key\-value pair.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=UpdateKeyValue&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `UpdateKeyValue`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example |
|---|---|---|---|---|
|Namespace |String |Yes |The name of the KV namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |`test-kv1` |
|NamespaceId |String |Yes |The ID of the KV namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Key |String |Yes |The key for which you want to modify the value or TTL. You can obtain it by calling the [ListKvKey](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvKey-en) API. |`testkey` |
|Value |String |Yes |The new value. If this parameter is not specified, the original value will be retained. Input requirements are as follows:<br><br><br>* Only Base64 encoded format is allowed.<br><br>* Must not exceed 128KB. |`dGVzdDEyMw==` |
|TTL |Long |Yes |The new TTL. Unit: seconds. The key\-value pair cannot be accessed after it expires. If this parameter is not specified, the original value will be retained.<br><br><br>* 0: Never expires.<br><br>* The TTL must not be less than 60 seconds. |`0` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="examples"></span>
## Examples

<span id="request-example"></span>
### Request example

```json
POST  https://cdn.byteplusapi.com?Action=UpdateKeyValue&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key": "testkey",
    "Value": "dGVzdDEyMw==",
    "TTL": 0
}
```
