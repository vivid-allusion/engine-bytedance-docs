---
title: "DeleteTranscodesComplete"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-deletetranscodescomplete"
---

The `DeleteTranscodesComplete` event is triggered when all transcoded files of an audio or video file are deleted. This article provides a description of the event parameters and includes examples of the `DeleteTranscodesComplete` event.

<span id="5aeba7cc"></span>
## Parameter


|Parameter |Type |Example |Description |
|---|---|---|---|
|RequestId |String |`202405060***0CF1866` |The unique ID of the request |
|Version |String |`1.0` |The callback version |
|EventType |String |`FileUploadComplete` |The name of the event |
|EventTime |String |`2024-05-06T09:49:33Z` |The time when the event occurred in UTC |
|Data |Data |`-` |The callback content in JSON format |


<span id="0b0c8fa6"></span>
### **Data**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|CallbackArgs |String |The info relayed as\-is from the client to the server, if any |
|Code |String |The error code |
|Message |String |The specific error information |
|Vid |String |The VID of the audio or video file |
|FileId |String |The ID of the transcoded file of the audio or video file. `FileId` being empty means all the transcoded files of the audio or video file are deleted. |
|FileNames |Array of String |The file path |


<span id="66afd40d"></span>
## **Example**

Below is an example of the event that is triggered when all transcoded files of a video is deleted:

```JSON
{
    "Data": {
        "CallbackArgs": "my callback123",
        "Code": "Success",
        "FileId": "",
        "Message": "Success",
        "Vid": "v0c328f30000c0oc02a5nesj082hr***",
        "FileNames": ["e4c13e5505874e5***4b1e74c8616","dr8979hdgfh***"]
    },
    "EventTime": "2021-02-20T07:54:19Z",
    "EventType": "DeleteTranscodesComplete",
    "RequestId": "202102201554191720180012008442***",
    "Version": "1.0"
}
```


Below is an example of the event that is triggered when a specific transcoded file is deleted:

```JSON
{
    "Data": {
        "CallbackArgs": "my callback123",
        "Code": "Success",
        "FileId": "1f282d128c3340d3b1ddaf1dfbdc2***",
        "Message": "Success",
        "Vid": "v0c328f30000c0***nesj082hr3jg",
        "FileNames": ["e4c13e55058***908b94b1e74c8616","74fhgffjgbfj***"]
    },
    "EventTime": "2021-02-20T07:54:19Z",
    "EventType": "DeleteTranscodesComplete",
    "RequestId": "202102201554191720180012008442***",
    "Version": "1.0"
}
```
