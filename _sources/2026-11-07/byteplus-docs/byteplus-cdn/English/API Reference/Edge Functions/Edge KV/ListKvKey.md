---
title: "ListKvKey"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvKey-en"
---

Gets a list of key\-value pairs in a namespace.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListKvKey&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `ListKvKey`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|Namespace |String |Yes |The name of the namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |
|NamespaceId |String |Yes |The ID of the namespace. You can obtain it by calling the [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en) API. |
|Page |Integer |No |Page number. |
|Limit |Integer |No |Number of records per page. The default is 50. The maximum number of records is 50. |
|OrderBy |Integer |No |This parameter specifies the order of the query for key\-value pairs, accepting the following values:<br><br><br>* 1: Sort key\-value pairs in descending order.<br><br>* 2 (default): Sort key\-value pairs in ascending order. |
|OrderType |String |No |Available sorting types are:<br><br><br>* create_time (default): Sort key\-value pairs by creation time.<br><br>* update_time: Sort key\-value pairs by last update time. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example |
|---|---|---|---|
|NamespaceKeys |Object |Details of key\-value pairs in the namespace. | |
|Namespace |String |The name of the namespace to which the key\-value pair belongs. |`test-kv1` |
|NamespaceId |String |The ID of the namespace to which the key\-value pair belongs. |`14776510402228****` |
|Key |String |The key. |`testkey` |
|KeyStatus |Integer |The status of the key\-value pair.<br><br><br>* 100: Expired<br><br>* 200: Normal |`200` |
|DDL |Long |The expiration time of the key\-value pair. After the key\-value pair expires, the Value in the Key will not be accessible.<br><br><br>* Displayed in Unix timestamp format.<br><br>* 0: Permanent storage. |`0` |
|CreateTime |Long |The creation time of the key\-value pair. Displayed in Unix timestamp format. |`1662005890` |
|UpdateTime |Long |The update time of the key\-value pair. Displayed in Unix timestamp format. |`1664337001` |
|TotalCount |Long |The total number of key\-value pairs in the namespace. |`2` |


<span id="examples"></span>
## Examples

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListKvKey&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****&Page=1&Limit=10&OrderBy=2&OrderType=create_time
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230810210051741B321D8****",
        "Action": "ListKvKey",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "NamespaceKeys": [
            {
                "Namespace": "test-kv1",
                "NamespaceId": "14776510402****",
                "Key": "testkey",
                "KeyStatus": 200, 
                "DDL": 0,
                "CreateTime": 1678085786,
                "UpdateTime": 1678085786
            },
            {
                "Namespace": "test-kv1",
                "NamespaceId": "14776510402****",
                "Key": "key",
                "KeyStatus": 100,
                "DDL": 1678259532,
                "CreateTime": 1678092385,
                "UpdateTime": 1682327035
            },
        ],
        "TotalCount": 2
    }
}
```
