---
title: "CreateKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-CreateKeyValue"
---

This interface is used to add a key\-value pair in the namespace.

<span id="limits"></span>
## Limits

Request Throttling: You can send a maximum of 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com?Action=CreateKeyValue&Version=2021\-03\-01**


<span id="api-description"></span>
## API description


* After successfully adding the key\-value pair, the Key cannot be modified.

* The keys in the same namespace cannot be duplicated.


<span id="request-parameters"></span>
## Request parameters

<span id="query-parameters"></span>
### Query Parameters


|**Parameter** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is CreateKeyValue. |
|Version |String |Yes |API version. The version of the current API is 2021\-03\-01. |


<span id="request-body"></span>
### Request Body


|**Parameter** |**Data Type** |**Required** |**Description** |**Value Sample** |
|---|---|---|---|---|
|Namespace |String |Yes |The name of the namespace to which the key\-value pair belongs. You can get it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListKvNamespace) API. |test\-kv1 |
|NamespaceId |String |Yes |The ID of the namespace to which the key\-value pair belongs. You can get it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListKvNamespace) API. |46d79a9944ae2fd81f2643e2fe5ef42d\*\*\*\* |
|Key |String |Yes |The key you want to create. Input requirements are as follows:<br><br><br>* Can only contain English letters, numbers, hyphens (\-), and underscores (_).<br><br>* Case\-insensitive. Edge Functions will not automatically convert case.<br><br>* No more than 512 bytes. |testkey |
|Value |String |Yes |The value of the key you need to create. Input requirements are as follows:<br><br><br>* Must be in Base64 encoding format.<br><br>* No more than 128KB. |dGVzdHZhbHVlMTIz |
|TTL |Int64 |No |Set the storage duration of the key\-value pair. Unit: seconds. After the key\-value pair expires, the value of the key will no longer be accessible by any function.<br><br><br>* If this parameter is not specified or the parameter value is 0, it will be stored permanently by default.<br><br>* The Storage duration must not be less than 60s. |0 |


<span id="response-parameters"></span>
## Response Parameters

None

<span id="examples"></span>
## Examples

<span id="sample-request"></span>
### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=CreateKeyValue&Version=2021-03-01

{
    "Namespace":"test-kv1",
    "NamespaceId":"46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key":"testkey",
    "TTL":0,
    "Value":"dGVzdHZhbHVlMTIz"
}
```


<span id="sample-response"></span>
### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202408090228427005A95850F6DA31D859",
        "Action": "CreateKeyValue",
        "Version": "2021-03-01",
        "Service": "cdn",
        "Region": "ap-singapore-1"
    }
}
```
