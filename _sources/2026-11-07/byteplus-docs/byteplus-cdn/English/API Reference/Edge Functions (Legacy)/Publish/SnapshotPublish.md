---
title: "SnapshotPublish"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-SnapshotPublish"
---

This interface is used to roll back the function to a specified version.

## Limits

Request Throttling: You can send a maximum of 20 requests per second. Additionally, for each function, you can send a maximum of 1 request per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=SnapshotPublish&Version=2021\-03\-01**

## **Request parameters**

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>SnapshotPublish<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the function to which you want rollback. You can get the FunctionId by calling the interface [ListSparrow](https://docs.byteplus.com/docs/byteplus-cdn/reference-Listsparrow).<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>VersionTag<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The specified version number to be published.You can get the VersionTag by calling the interface [ListVersions](https://docs.byteplus.com/docs/byteplus-cdn/reference-ListVersions) .<br><br>  |  <br><br>1.0.1<br><br>  |
|  <br><br>PublishType<br><br>  |  <br><br>Int32<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Publish type：<br><br>  <br><br> <br> <br><br>* 200: FullPublish<br><br><br> <br> <br><br>* 100: CanaryPublish<br><br><br>  <br><br>  |  <br><br>200<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>Fill in the description information for this release.<br><br>  |  <br><br>test publish<br><br>  |

## **Response data**

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>TicketId<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Publish id<br><br>  |  <br><br>278335600748419\*\*\*\*<br><br>  |

## **Example**

### Request Example

```JSON
POST https://cdn.byteplusapi.com/?Action=SnapshotPublish&Version=2021-03-01
{
    "FunctionId": "3gyz993****",
    "PublishType": 200,
    "VersionTag": "1.0.1"
}
```

### **Response Example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202112072116030102251331430*****",
        "Action": "SnapshotPublish",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TicketId": 278335600748419****
    }
}
```
