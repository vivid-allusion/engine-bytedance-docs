---
title: "UpdateSparrow"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateSparrow"
---

This interface is used to update the name or description of a function based on its ID.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=UpdateSparrow&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>UpdateSparrow<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value<br><br>  |
|---|---|---|---|---|
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Enter the ID of the function whose name you want to modify. You can get the FunctionId by calling the interface [ListSparrow](https://docs.byteplus.com/docs/byteplus-cdn/reference-Listsparrow).<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>Name<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>New function name. The name must satisfy the following requirements:<br><br>  <br><br> <br> <br><br>* It can only contain letters, numbers, and hyphens（\-）.<br><br><br> <br> <br><br>* The length must not exceed 128 characters.<br><br><br>  <br><br>  |  <br><br>test\-sparrow2<br><br>  |
|  <br><br>Remark<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>The remark for this function.The input requirements are as follows:<br><br>  <br><br> <br> <br><br>* Any characters are allowed.<br><br><br> <br> <br><br>* The length should not exceed 80 characters.<br><br><br> <br> <br><br>* If this field is not used, it will not be modified. When the value of this field is not filled, the description will be modified to be empty.<br><br><br>  <br><br>  |  <br><br>This is a test sparrow<br><br>  |

## Response Parameters

None

## Examples

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=UpdateSparrow&Version=2021-03-01
{
  "FunctionId": "4356345",
  "Name": "test-sparrow2",
  "Remark": ""
}
```
