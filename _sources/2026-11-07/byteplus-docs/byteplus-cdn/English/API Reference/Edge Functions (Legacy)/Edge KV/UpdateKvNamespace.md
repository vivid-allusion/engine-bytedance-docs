---
title: "UpdateKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateKvNamespace"
---

This interface is used to modify the name or description of a namespace.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=UpdateKvNamespace&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>UpdateKvNamespace<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Namespace<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the namespace for which the name or description will be modified.<br><br>  |  <br><br>test\-kv1<br><br>  |
|  <br><br>NamespaceId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the namespace to which the description will be modified. You can get the namespaceId by calling the interface [ListKvNamespace](https://docs.byteplus.com/docs/byteplus-cdn/reference-ListKvNamespace).<br><br>  |  <br><br>46d79a9944ae2fd81f2643e2fe5ef42d\*\*\*\*<br><br>  |
|  <br><br>NewNamespace<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The new name for the namespace.If you wish to modify the description of the namespace without changing its name, you can simply enter the current namespace name as the value for this parameter.The input requirements are as follows:<br><br>  <br><br> <br> <br><br>* Length should be between 2 and 64 characters.<br><br><br> <br> <br><br>* It can only contain English letters, numbers, hyphens (\-), and underscores (_).<br><br><br>  <br><br>  |  <br><br>test\-kv2<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>The new description information for the namespace. If this parameter is not specified, the original description will be retained. The input requirements are as follows:<br><br>  <br><br> <br> <br><br>* Any characters are allowed.<br><br><br> <br> <br><br>* The length should not exceed 80 characters.<br><br><br>  <br><br>  |  <br><br>test<br><br>  |

## Response Parameters

None

## Examples

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=UpdateKvNamespace&Version=2021-03-01

{
    "Namespace":"test-kv1",
    "NamespaceId":"46d79a9944ae2fd81f2643e2fe5ef42d****",
    "NewNamespace": "test-kv2",
    "Description":"test"
}
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201131150180102252431470****",
        "Action": "UpdateKvNamespace",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```
