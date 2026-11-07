---
title: "ListKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en"
---

Gets a list of namespaces.

<span id="limits"></span>
## Limits

Request limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListKvNamespace&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `ListKvNamespace`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|Page |Integer |No |Page number. The default is 1. |
|Limit |Integer |No |Number of records per page. The default is 50 records.<br><br>The maximum number of records is 50. |
|OrderBy |Integer |No |This parameter specifies the order of the query data, accepting the following values:<br><br><br>* 1: Sort namespaces in descending order.<br><br>* 2 (default): Sort namespaces in ascending order. |
|OrderType |String |No |Available sorting types are:<br><br><br>* create_time (default): Sort namespaces by creation time.<br><br>* update_time: Sort namespaces by last update time. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example |
|---|---|---|---|
|Namespaces |Object |List of namespaces. | |
|Namespace |String |The name of the namespace. |`test-kv1` |
|NamespaceId |String |The ID of the namespace. |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Description |String |The description of the namespace. |`test` |
|Creator |String |The creator of the namespace. |`testuser` |
|CreateTime |Long |The creation time. Displayed in Unix timestamp format. |`1661864175` |
|UpdateTime |Long |The update time. Displayed in Unix timestamp format. |`1678288603` |
|TotalCount |Long |The total number of namespaces. |`2` |


<span id="examples"></span>
## Examples

<span id="request-example"></span>
### Request example

```HTTP
GET https://cdn.byteplusapi.com?Action=ListKvNamespace&Version=2021-03-01&Page=1&Limit=10&OrderBy=2&OrderType=create_time
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230808095102CFDFA3280****",
        "Action": "ListKvNamespace",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Namespaces": [
            {
                "Namespace": "test-kv1",
                "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
                "Description": "test",
                "Creator": "testuser",
                "CreateTime": 1661864175,
                "UpdateTime": 1678288603
            },
            {
                "Namespace": "asdJSJasdad",
                "NamespaceId": "510257916f6b5503b288d064b7154****",
                "Description": "",
                "Creator": "testuser",
                "CreateTime": 1662005890,
                "UpdateTime": 1664337001
            }
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
