---
title: "GetKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetKeyValue-en"
---

Gets the value and expiration time of a key\-value pair.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=GetKeyValue&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `GetKeyValue`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|Namespace |String |Yes |The name of the KV namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |
|NamespaceId |String |Yes |The ID of the KV namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |
|Key |String |Yes |The key for which you want to query the value or expiration time. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example |
|---|---|---|---|
|DDL |Long |The expiration time of the key\-value pair. After the key\-value pair expires, the function will not be able to access the Value of the Key.<br><br><br>* Displayed in seconds\-level Unix timestamp format.<br><br>* 0: Never expires |`0` |
|Key |String |The key. |`testkey` |
|Value |String |The value of the key. The value is in Base64 encoded format. |`dGVzdHZhbHVlMTIz` |


<span id="examples"></span>
## Examples

<span id="request-example"></span>
### Request example

```HTTP
GET   https://cdn.byteplusapi.com?Action=GetKeyValue&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****&Key=testkey
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetKeyValue",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DDL": 0,
        "Key": "testkey",
        "Value": "dGVzdHZhbHVlMTIz"
    }
}
```
