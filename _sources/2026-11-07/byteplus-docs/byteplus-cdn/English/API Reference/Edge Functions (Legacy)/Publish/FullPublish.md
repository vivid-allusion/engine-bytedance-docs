---
title: "FullPublish"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-FullPublish"
---

This interface is used to fully publish the function based on the function ID.

## Limits

Request Throttling: You can send a maximum of 20 requests per second. Additionally, for each function, you can send a maximum of 1 request per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=FullPublish&Version=2021\-03\-01**

## **Request Parameters**

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>FullPublish<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the function to which you want publish. You can get the FunctionId by calling the interface [ListSparrow](https://docs.byteplus.com/docs/byteplus-cdn/reference-Listsparrow).<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>Fill in the description information for this release.<br><br>  |  <br><br>test publish<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>TicketId<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Publish id<br><br>  |  <br><br>146023529142213\*\*\*\*<br><br>  |

## **Examples**

### **Sample** Request

```JSON
POST https://cdn.byteplusapi.com/?Action=FullPublish&Version=2021-03-01
{
    "FunctionId": "3246574",
    "Description": "test publish"
}
```

### **Sample Response**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202112072116030102251331430*****",
        "Action": "FullPublish",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TicketId": 146023529142213****
    }
}
```
