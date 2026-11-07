---
title: "DeleteMediaComplete"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-deletemediacomplete"
---

The `DeleteMediaComplete` event provides a callback notification to confirm the completion of an audio or video file deletion task. This document details the event's parameters and data structure, including a full JSON example, to help you correctly parse and handle this event in your application.

<span id="56c024a5"></span>
## Parameter


|Parameter |Type |Example |Description |
|---|---|---|---|
|RequestId |String |`202405060***0CF1866` |The unique ID of the request |
|Version |String |`1.0` |The callback version |
|EventType |String |`FileUploadComplete` |The name of the event |
|EventTime |String |`2024-05-06T09:49:33Z` |The time when the event occurred in UTC |
|Data |Data |`-` |The callback content in JSON format |


<span id="3413619a"></span>
### **Data**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|CallbackArgs |String |The information relayed as\-is from the client to the server, if any |
|Code |String |The error code |
|Message |String |The specific error information |
|Vid |String |The VID of the deleted file |
|FileNames |Array of String |The file path |


<span id="5390746f"></span>
## **Example**

Below is an example of the event that is triggered when the deletion of a file is completed:

```JSON
{
    "Data": {
        "CallbackArgs": "my callback123",
        "Code": "Success",
        "Message": "Success",
        "Vid": "v0c328f30000c0oc02a5nesj082hr***",
        "FileNames": ["e4c13e550587***4b1e74c8616","443sfydyh***4dfg789"]
    },
    "EventTime": "2021-02-20T07:54:35Z",
    "EventType": "DeleteMediaComplete",
    "RequestId": "202102201554341720180012009369***",
    "Version": "1.0"
}
```
