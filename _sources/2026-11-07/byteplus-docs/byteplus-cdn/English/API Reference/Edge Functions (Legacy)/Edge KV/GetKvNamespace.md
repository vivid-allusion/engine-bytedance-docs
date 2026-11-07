---
title: "GetKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-GetKvNamespace"
---

This interface is used to query detailed information about a namespace.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=GetKvNamespace&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>GetKvNamespace<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>Namespace<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the namespace for which you want to view detailed information.<br><br>  |  <br><br>test\-kv1<br><br>  |
|  <br><br>NamespaceId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the namespace to which you want to view detailed information. You can get the namespaceId by calling the interface [ListKvNamespace](https://docs.byteplus.com/docs/byteplus-cdn/reference-ListKvNamespace).<br><br>  |  <br><br>46d79a9944ae2fd81f2643e2fe5ef42d\*\*\*\*<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Namespace<br><br>  |  <br><br>KvNamespace<br><br>  |  <br><br>Namespace details<br><br>  |  <br><br>See the explanation below<br><br>  |

**KvNamespace**

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Namespace<br><br>  |  <br><br>string<br><br>  |  <br><br>The name of the namespace.<br><br>  |  <br><br>test\-kv1<br><br>  |
|  <br><br>NamespaceId<br><br>  |  <br><br>string<br><br>  |  <br><br>The ID of the namespace.<br><br>  |  <br><br>46d79a9944ae2fd81f2643e2fe5ef42d\*\*\*\*<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>string<br><br>  |  <br><br>The description of the namespace.<br><br>  |  <br><br>test<br><br>  |
|  <br><br>Creator<br><br>  |  <br><br>string<br><br>  |  <br><br>The creator of the namespace.<br><br>  |  <br><br>testuser<br><br>  |
|  <br><br>CreateTime<br><br>  |  <br><br>int64<br><br>  |  <br><br>The creation time. Displayed in UNIX timestamp format.<br><br>  |  <br><br>1661864175<br><br>  |
|  <br><br>UpdateTime<br><br>  |  <br><br>int64<br><br>  |  <br><br>The update time. Displayed in UNIX timestamp format.<br><br>  |  <br><br>1678288603<br><br>  |
|  <br><br>ProjectName<br><br>  |  <br><br>string<br><br>  |  <br><br>The name of the project to which the namespace belongs.<br><br>  |  <br><br>default<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=GetKvNamespace&Version=2021-03-01
&Namespace=test-kv1
&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****
```

### Sample Response

```JSON
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
