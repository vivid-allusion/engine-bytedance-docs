---
title: "CreateSparrow"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-createsparrow"
---

This interface is used to create a function.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=CreateSparrow&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>CreateSparrow<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Name<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Function name. Here are the naming rules:<br><br>  <br><br> <br> <br><br>* You can use uppercase letters, lowercase letters, numbers, and hyphens (\-).<br><br><br> <br> <br><br>* The name should not be longer than 128 characters.<br><br><br>  <br><br>  |  <br><br>test\-sparrow<br><br>  |
|  <br><br>ProjectName<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>The name of the project to which the function belongs, defaulting to `default`.<br><br>  |  <br><br>default<br><br>  |
|  <br><br>Remark<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>The remark for this function.The input requirements are as follows:<br><br>  <br><br> <br> <br><br>* Any characters are allowed.<br><br><br> <br> <br><br>* The length should not exceed 128 characters.<br><br><br>  <br><br>  |  <br><br>This is a test sparrow<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Example<br><br>  |
|---|---|---|---|
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>The ID of the function.<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |

## Examples

### Sample Request

```HTTP
POST https://cdn.byteplusapi.com/?Action=CreateSparrow&Version=2021-03-01
{
  "Name": "test-sparrow"
}
```

### Sample Response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2022011110011401022524308102B1****",
    "Action": "CreateSparrow",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
     "FunctionId": "3gyz993****"
  }
}
```
