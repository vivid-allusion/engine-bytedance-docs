---
title: "DeleteKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DeleteKvNamespace"
---

This interface is used to delete a namespace.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=DeleteKvNamespace&Version=2021\-03\-01**

## Request Parameters

### Query Parameter

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>DeleteKvNamespace<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

## Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Namespace<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the namespace to be deleted.<br><br>  |  <br><br>test\-kv1<br><br>  |
|  <br><br>NamespaceId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the namespace to be deleted. You can get the namespaceId by calling the interface [ListKvNamespace](https://docs.byteplus.com/docs/byteplus-cdn/reference-ListKvNamespace)<br><br>  |  <br><br>46d79a9944ae2fd81f2643e2fe5ef42d\*\*\*\*<br><br>  |

## Response Parameters

None

## Examples

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=DeleteKvNamespace&Version=2021-03-01

{
    "Namespace":"test-kv1",
    "NamespaceId":"46d79a9944ae2fd81f2643e2fe5ef42d****"
}
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201131150180102252431470****",
        "Action": "DeleteKvNamespace",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```
