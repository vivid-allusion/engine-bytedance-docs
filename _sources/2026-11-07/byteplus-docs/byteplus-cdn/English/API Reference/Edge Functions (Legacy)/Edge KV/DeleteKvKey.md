---
title: "DeleteKvKey"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DeleteKvKey"
---

This interface is used to delete specific data in a namespace.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=DeleteKvKey&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>DeleteKvKey<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Namespace<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the namespace to which the data belongs.<br><br>  |  <br><br>test\-kv1<br><br>  |
|  <br><br>NamespaceId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the namespace to which the data belongs. You can get the namespaceId by calling the interface [ListKvNamespace](https://docs.byteplus.com/docs/byteplus-cdn/reference-ListKvNamespace)<br><br>  |  <br><br>46d79a9944ae2fd81f2643e2fe5ef42d\*\*\*\*<br><br>  |
|  <br><br>Key<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The key to the data to be deleted.<br><br>  |  <br><br>testkey<br><br>  |

## Response Parameters

None

## Examples

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=DeleteKvKey&Version=2021-03-01

{
    "Namespace":"test-kv1",
    "NamespaceId":"46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key":"testkey"
}
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201131150180102252431470****",
        "Action": "DeleteKvKey",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```
