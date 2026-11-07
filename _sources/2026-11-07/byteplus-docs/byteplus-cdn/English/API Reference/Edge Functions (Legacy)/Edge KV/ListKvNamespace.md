---
title: "ListKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListKvNamespace"
---

This interface is used to get a list of namespaces.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=ListKvNamespace&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>ListKvNamespace<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>Page<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Page number<br><br>  |  <br><br>1<br><br>  |
|  <br><br>Limit<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Number of records per page.<br><br> Currently, up to 50 records can be obtained at a time.<br><br>  |  <br><br>10<br><br>  |
|  <br><br>OrderBy<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>The parameter specifies the order in which the data is queried. It accepts the following values:<br><br>  <br><br> <br> <br><br>* 1: Sort the namespace in descending order.<br><br><br> <br> <br><br>* 2 (default): Sort the namespace in ascending order.<br><br><br>  <br><br>  |  <br><br>2<br><br>  |
|  <br><br>OrderType<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>The available sorting types are:<br><br>  <br><br> <br> <br><br>* create_time(default): Sort the namespace based on the time of creation.<br><br><br> <br> <br><br>* update_time: Sort the namespace based on the time of the last update.<br><br><br>  <br><br>  |  <br><br>create_time<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Namespaces<br><br>  |  <br><br>KvNamespace<br><br>  |  <br><br>List of namespaces<br><br>  |  <br><br>See the explanation below<br><br>  |
|  <br><br>TotalCount<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Total number of namespaces<br><br>  |  <br><br>2<br><br>  |

**KvNamespace**

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Namespace<br><br>  |  <br><br>string<br><br>  |  <br><br>The name of the namespace.<br><br>  |  <br><br>test\-kv1<br><br>  |
|  <br><br>NamespaceId<br><br>  |  <br><br>string<br><br>  |  <br><br>The ID of the namespace.<br><br>  |  <br><br>46d79a9944ae2fd81f2643e2fe5ef42d\*\*\*\*<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>string<br><br>  |  <br><br>The description of the namespace.<br><br>  |  <br><br>test<br><br>  |
|  <br><br>Creator<br><br>  |  <br><br>string<br><br>  |  <br><br>The creator of the namespace.<br><br>  |  <br><br>testuser<br><br>  |
|  <br><br>CreateTime<br><br>  |  <br><br>int64<br><br>  |  <br><br>The creation time. Displayed in UNIX timestamp format.<br><br>  |  <br><br>1661864175<br><br>  |
|  <br><br>UpdateTime<br><br>  |  <br><br>int64<br><br>  |  <br><br>The update time. Displayed in UNIX timestamp format.<br><br>  |  <br><br>1678288603<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=ListKvNamespace&Version=2021-03-01
```

### Sample Response

```JSON
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
