---
title: "GetKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetKvNamespace-en"
---

Gets detailed information about a namespace.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=GetKvNamespace&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `GetKvNamespace`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|Namespace |String |Yes |The name of the namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |
|NamespaceId |String |Yes |The ID of the namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example |
|---|---|---|---|
|Namespace |Object |namespace details. | |
|Namespace |String |The name of the namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |`test-kv1` |
|NamespaceId |String |The ID of the namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Description |String |The description of the namespace. |`test` |
|Creator |String |The creator of the namespace. |`testuser` |
|CreateTime |Long |The creation time. Displayed in UNIX timestamp format. |`1661864175` |
|UpdateTime |Long |The update time. Displayed in UNIX timestamp format. |`1678288603` |
|ProjectName |String |The name of the project to which the namespace belongs. |`default` |


<span id="examples"></span>
## Examples

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetKvNamespace&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202308080952004CD21902****",
        "Action": "GetKvNamespace",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Namespace": {
            "Namespace": "test-kv1",
            "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
            "Description": "test",
            "Creator": "testuser",
            "ProjectName": "default",
            "CreateTime": 1661864175,
            "UpdateTime": 1678288603
        }
    }
}
```
