---
title: "ListKvKey"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListKvKey"
---

This interface is used to get the list of data in a namespace.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=ListKvKey&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>ListKvKey<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>Namespace<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the namespace to which the data belongs.<br><br>  |  <br><br>test\-kv1<br><br>  |
|  <br><br>NamespaceId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the namespace to which the data belongs. You can get the namespaceId by calling the interface [ListKvNamespace](https://docs.byteplus.com/docs/byteplus-cdn/reference-ListKvNamespace)<br><br>  |  <br><br>46d79a9944ae2fd81f2643e2fe5ef42d\*\*\*\*<br><br>  |
|  <br><br>Page<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Page number<br><br>  |  <br><br>1<br><br>  |
|  <br><br>Limit<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Number of records per page.<br><br> Currently, up to 50 records can be obtained at a time.<br><br>  |  <br><br>10<br><br>  |
|  <br><br>OrderBy<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>The parameter specifies the order in which the data is queried. It accepts the following values:<br><br>  <br><br> <br> <br><br>* 1: Sort the data in descending order.<br><br><br> <br> <br><br>* 2 (default): Sort the data in ascending order.<br><br><br>  <br><br>  |  <br><br>2<br><br>  |
|  <br><br>OrderType<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>The available sorting types are:<br><br>  <br><br> <br> <br><br>* create_time(default): Sort the data based on the time of creation.<br><br><br> <br> <br><br>* update_time: Sort the data based on the time of the last update.<br><br><br>  <br><br>  |  <br><br>create_time<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>NamespaceKeys<br><br>  |  <br><br>KeyDetail<br><br>  |  <br><br>Data details in the namespace.<br><br>  |  <br><br>See explanation below<br><br>  |
|  <br><br>TotalCount<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Total number of data in the namespace.<br><br>  |  <br><br>2<br><br>  |

**KeyDetail**

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Namespace<br><br>  |  <br><br>String<br><br>  |  <br><br>The name of the namespace to which the data belongs.<br><br>  |  <br><br>test\-kv1<br><br>  |
|  <br><br>NamespaceId<br><br>  |  <br><br>String<br><br>  |  <br><br>The ID of the namespace to which the data belongs.<br><br>  |  <br><br>14776510402228\*\*\*\*<br><br>  |
|  <br><br>Key<br><br>  |  <br><br>String<br><br>  |  <br><br>The key.<br><br>  |  <br><br>testkey<br><br>  |
|  <br><br>KeyStatus<br><br>  |  <br><br>Int32<br><br>  |  <br><br>The data status.<br><br>  <br><br> <br> <br><br>* 100: Expired<br><br><br> <br> <br><br>* 200: Normal<br><br><br>  <br><br>  |  <br><br>200<br><br>  |
|  <br><br>DDL<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Data expiration time. After the data expires, the Value in the Key will be inaccessible.<br><br>  <br><br> <br> <br><br>* Displayed in UNIX timestamp format.<br><br><br> <br> <br><br>* 0: Permanent storage.<br><br><br>  <br><br>  |  <br><br>0<br><br>  |
|  <br><br>CreateTime<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Data creation time. Displayed in UNIX timestamp format.<br><br>  |  <br><br>1662005890<br><br>  |
|  <br><br>UpdateTime<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Data update time. Displayed in UNIX timestamp format.<br><br>  |  <br><br>1664337001<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=ListKvKey&Version=2021-03-01
&Namespace=test-kv1
&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****
```

### Sample Response

```JSON
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
                "KeyStatus": 200, // 100 Expired; 200 Normal
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
