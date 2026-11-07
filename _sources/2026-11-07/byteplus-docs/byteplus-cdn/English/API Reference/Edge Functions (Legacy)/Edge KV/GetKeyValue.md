---
title: "GetKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-GetKeyValue"
---

This interface is used to view the value and expiration time of a key.

<span id="limits"></span>
## Limits

Request Throttling: A maximum of 20 requests can be sent per second.

<span id="usage"></span>
## Usage


* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com?Action=GetKeyValue&Version=2021\-03\-01**


<span id="request-parameters"></span>
## Request parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |Value Sample |
|---|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is GetKeyValue. |GetKeyValue |
|Version |String |Yes |API version. The version of the current API is 2021\-03\-01. |2021\-03\-01 |
|Namespace |String |Yes |The name of the namespace to which the key\-value pair belongs. You can get it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListKvNamespace) API. |test\-kv1 |
|NamespaceId |String |Yes |The ID of the namespace to which the key\-value pair belongs. You can get it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListKvNamespace) API. |46d79a9944ae2fd81f2643e2fe5ef42d\*\*\*\* |
|Key |String |Yes |The key for which you want to query the value or expiration time. |testkey |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Description |Value Sample |
|---|---|---|---|
|DDL |Int64 |The expiration time of the key\-value pair. After the key\-value pair expires, the value of the key will no longer be accessible by any function.<br><br><br>* Displayed as a UNIX timestamp in seconds.<br><br>* 0: Permanent storage |0 |
|Key |String |The queried key. |testkey |
|Value |String |The value of the queried key. The value is in Base64 encoding format. |dGVzdHZhbHVlMTIz |


<span id="examples"></span>
## Examples

<span id="request-example"></span>
### Request example

```HTTP
GET https://cdn.byteplusapi.com/?Action=GetKeyValue&Version=2021-03-01
&Namespace=test-kv1
&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****
&Key=testkey
```


<span id="response-example"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201131150180102252431470****",
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
