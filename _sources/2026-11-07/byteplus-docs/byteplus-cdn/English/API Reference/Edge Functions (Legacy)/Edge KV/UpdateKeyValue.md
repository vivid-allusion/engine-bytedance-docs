---
title: "UpdateKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateKeyValue"
---

This interface is used to modify the value and TTL (Time To Live) of a key\-value pair.

<span id="limits"></span>
## Limits

Request Throttling: A maximum of 20 requests can be sent per second.

<span id="usage"></span>
## Usage


* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com?Action=UpdateKeyValue&Version=2021\-03\-01**


<span id="request-parameters"></span>
## Request parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is UpdateKeyValue. |
|Version |String |Yes |API version. The version of the current API is 2021\-03\-01. |


<span id="body"></span>
### Body


|Parameter |Data Type |Required |Description |Value Sample |
|---|---|---|---|---|
|Namespace |String |Yes |The name of the namespace to which the key\-value pair belongs. You can get it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListKvNamespace) API. |test\-kv1 |
|NamespaceId |String |Yes |The ID of the namespace to which the key\-value pair belongs. You can get it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListKvNamespace) API. |46d79a9944ae2fd81f2643e2fe5ef42d\*\*\*\* |
|Key |String |Yes |The key for which you want to modify the value or storage duration.You can get it by calling the [ListKvKey](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListKvKey) API. |testkey |
|Value |String |No |The value you want to modify. If this parameter is not specified, the original value is retained. Input requirements are as follows:<br><br><br>* Must be in Base64 encoding format.<br><br>* No more than 128KB. |dGVzdDEyMw== |
|TTL |Int64 |No |The storage duration you want to modify. Unit: seconds. After the key\-value pair expires, the value of the key will no longer be accessible by any function. If this parameter is not specified, the original value is retained.<br><br><br>* 0: Permanent storage.<br><br>* Storage duration cannot be less than 60 seconds. |0 |


<span id="response-parameters"></span>
## Response parameters

None

<span id="examples"></span>
## Examples

<span id="request-example"></span>
### Request example

```HTTP
POST  https://cdn.byteplusapi.com/?Action=UpdateKeyValue&Version=2021-03-01

{
    "Namespace":"test-kv1",
    "NamespaceId":"46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key":"testkey",
    "TTL":0,
    "Value":"dGVzdDEyMw=="
}
```


<span id="response-example"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240809085350B8C742AB9D05B8433CD8",
        "Action": "UpdateKeyValue",
        "Version": "2021-03-01",
        "Service": "cdn",
        "Region": "ap-singapore-1"
    }
}
```
