---
title: "CreateKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-CreateKvNamespace"
---

This interface is used to create a namespace.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=CreateKvNamespace&Version=2021\-03\-01**

## Usage Constraints

* Up to 10 namespaces can be created under the same Byteplus account.

* The namespace names under the same Byteplus account must be unique.

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>CreateKvNamespace<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Namespace<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Set a recognizable name for the namespace. The input requirements are as follows:<br><br>  <br><br> <br> <br><br>* Length should be between 2 and 64 characters.<br><br><br> <br> <br><br>* It can only contain English letters, numbers, hyphens (\-), and underscores (_).<br><br><br>  <br><br>  |  <br><br>test\-kv1<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>Set a description for the namespace. The input requirements are as follows:<br><br>  <br><br> <br> <br><br>* Any characters are allowed.<br><br><br> <br> <br><br>* The length should not exceed 80 characters.<br><br><br>  <br><br>  |  <br><br>test<br><br>  |
|  <br><br>ProjectName<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>The name of the project to which the namespace belongs, defaulting to `default`.<br><br>  |  <br><br>default<br><br>  |

## Response Parameters

None

## Examples

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=CreateKvNamespace&Version=2021-03-01

{
    "Namespace":"test-kv1",
    "Description":"this is test",
    "ProjectName": "default"
}
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201131150180102252431470****",
        "Action": "CreateKvNamespace",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```
