---
title: "SparrowUnBindDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-SparrowUnBindDomains"
---

This interface is used to unbind domains to a function.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=SparrowUnBindDomains&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>SparrowUnBindDomains<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Domains<br><br>  |  <br><br>Array<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Enter the domain names which you want to unbind.<br><br>  |  <br><br>["test.sparrow1.com","test.sparrow2.com"]<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Enter the ID of the function for which you want to unbind to domain.<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |

## Response Parameters

None

## Examples

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=SparrowUnBindDomains&Version=2021-03-01
{
  "Domains": [
  "test.sparrow1.com",
  "test.sparrow2.com"
  ],
  "FunctionId": "3gyz993****"
}
```
