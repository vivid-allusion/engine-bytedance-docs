---
title: "SparrowBindDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-SparrowBindDomains"
---

This interface is used to bind domains to a function.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

> **注意**

> The edge function only binds domain names that have been added to CDN in the account.

* A function can be associated with a maximum of 100 domain names.

* A domain name can be associated with a maximum of 50 functions.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=SparrowBindDomains&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>SparrowBindDomains<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value<br><br>  |
|---|---|---|---|---|
|  <br><br>Domains<br><br>  |  <br><br>Array<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Enter the domain names that you wish to bind with the function. You can get the available CDN domains list by calling the interface [ListSparrowDomains](https://docs.byteplus.com/docs/byteplus-cdn/reference-ListSparrowDomains).<br><br>  |  <br><br>["test.sparrow1.com","test.sparrow2.com"]<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Enter the ID of the function for which you want to bind to domain.You can get the FunctionId by calling the interface [ListSparrow](https://docs.byteplus.com/docs/byteplus-cdn/reference-Listsparrow).<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |

## Response Parameters

None

## Examples

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=SparrowBindDomains&Version=2021-03-01
{
  "Domains": [
  "test.sparrow1.com",
  "test.sparrow2.com"
  ],
  "FunctionId": "3gyz993****"
}
```
