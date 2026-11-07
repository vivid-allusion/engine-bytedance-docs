---
title: "CreateKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKeyValue-en"
---

Adds a key\-value pair to the namespace.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.


* After successfully adding a key\-value pair, the key cannot be modified.

* Keys in the same namespace must be unique. Keys are case\-insensitive, meaning `Key` and `KEY` are considered the same.


<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=CreateKeyValue&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `CreateKeyValue`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Description |Example value |
|---|---|---|---|---|
|Namespace |String |Yes |Name of the namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |`test-kv1` |
|NamespaceId |String |Yes |ID of the namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Key |String |Yes |Key. Input requirements are as follows:<br><br><br>* Can only contain English letters, numbers, hyphens (\-), and underscores (_).<br><br>* Must not exceed 512 bytes. |`testkey` |
|Value |String |Yes |Value. Input requirements are as follows:<br><br><br>* Must be in Base64 encoded format.<br><br>* Must not exceed 128KB. |`dGVzdHZhbHVlMTIz` |
|TTL |Long |No |Set the validity duration for the key\-value pair. Unit: seconds. After the key\-value pair expires, the function will not be able to read the value of the key.<br><br><br>* If this parameter is not specified or the parameter value is 0, it never expires.<br><br>* The validity duration must not be less than 60s. |`0` |


<span id="response-parameters"></span>
## Response parameters

None

<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```json
POST   https://cdn.byteplusapi.com?Action=CreateKeyValue&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key": "testkey",
    "Value": "dGVzdHZhbHVlMTIz",
    "TTL": 0
}
```


&nbsp;
