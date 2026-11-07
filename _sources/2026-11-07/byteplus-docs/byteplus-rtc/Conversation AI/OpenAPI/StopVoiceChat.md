---
title: "StopVoiceChat"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1404672"
---

After start an agent task, you can stop it by calling this interface.

<span id="0Tyj7FXr"></span>
## HTTP request


* Method：POST

* Endpoint：https://open.byteplusapi.com?Action=StopVoiceChat&Version=2025\-05\-01


<span id="81b4tHeX"></span>
## Request parameters

<span id="3PU0P8Qf"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="y0rub0xO"></span>
### Query


**Action** `String` **`Required`** Example: `StopVoiceChat`

Interface name. The value of this interface: `StopVoiceChat`



**Version** `String` **`Required`** Example: `2025-05-01`

OpenAPI version. The value of this interface: `2025-05-01`


<span id="CjGqGIAD"></span>
### Body


**AppId** `String` **`Required`** Example: `661e****543cf`

The only identifier for your audio & video app. See [get the AppId](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid).



**RoomId** `String` **`Required`** Example: `Room1`

The room ID for the conversation between the agent and the real person.



**TaskId** `String` **`Required`** Example: `task1`

TaskId of the task you need to stop.


<span id="JxxU5RHl"></span>
## Response parameters

This interface does not have any specific return parameters. See [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters) for returned common parameters.

Result returns "success" only when the request succeeds and null when it fails.
