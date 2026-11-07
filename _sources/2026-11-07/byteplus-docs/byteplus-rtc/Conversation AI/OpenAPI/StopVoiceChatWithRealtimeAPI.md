---
title: "StopVoiceChatWithRealtimeAPI"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1316258"
---

You can call this interface to end a task started by `StopVoiceChatWithRealtimeAPI`.

<span id="v0X58EJ4"></span>
## HTTP request


* Method：POST

* Endpoint：https://open.byteplusapi.com?Action=StopVoiceChatWithRealtimeAPI&Version=2025\-05\-01


<span id="bw6frcqt"></span>
## Request parameters

<span id="JbSmosP4"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="6uMIVhXD"></span>
### Query


**Action** `String` **`Required`** Example: `StopVoiceChatWithRealtimeAPI`

Interface name. The value of this interface: `StopVoiceChatWithRealtimeAPI`



**Version** `String` **`Required`** Example: `2025-05-01`

OpenAPI version. The value of this interface: `2025-05-01`


<span id="UScQgiyS"></span>
### Body


**AppId** `String` **`Required`** Example: `661e****543cf`

The only identifier for your audio & video app.



**RoomId** `String` **`Required`** Example: `Room1`

Room ID. It's the only identifier of a room.



**TaskId** `String` **`Required`** Example: `Task1`

TaskId. You must set the TaskId for each task.


<span id="ZMPElyyF"></span>
## Response parameters

This interface does not have any specific return parameters. See [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) for returned common parameters.

Result returns "success" only when the request succeeds and null when it fails.
