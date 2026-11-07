---
title: "SendRoomUnicast"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1164062"
---

> This API interface is for the latest version, and new features will be updated here. It is recommended to use the latest version. For documentation of older versions, please refer to [legacy](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-v3wedfo4dj).


Calls `SendRoomUnicast` to send a text message or a binary message to a specified user in an RTC room.

<span id="usage"></span>
## Usage

<span id="prerequisites"></span>
### Prerequisites

For Native SDK 3.60 and above, and Web SDK 4.66 and above, ensure that the **RTS advanced feature** is enabled in the [RTC console > Settings > RTS real-time messaging](https://console.byteplus.com/rtc/cloudRTC?&tab=RTSMode) before calling this API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this feature is enabled while the SDK is running, you must reinitialize the engine for the configuration to take effect.</div>


<span id="interface-behavior"></span>
### Interface Behavior

After the message is successfully sent, the user receives the message via the following callback:


| |Android |iOS |Windows |
|---|---|---|---|
|Text message |[onRoomMessageReceived](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#onroommessagereceived) |[rtsRoom:onRoomMessageReceived:message](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroommessagereceived-message) |[OnRoomMessageReceived](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70096#onroommessagereceived) |
|Binary message |[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#onroombinarymessagereceived) |[rtsRoom:onRoomBinaryMessageReceived:message:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroombinarymessagereceived-message) |[OnUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70096#onuserbinarymessagereceived) |


<span id="make-a-call"></span>
### Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [call OpenAPI](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828) .

<span id="caution"></span>
## Caution


* QPS: For each AppId, the sum of the upper limits of the call frequencies of `SendUnicast`, `SendRoomUnicast`, `SendBroadcast` and `BatchSendRoomUnicast` is **500** times per second.

* The size of one message cannot exceed 64KB.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=SendRoomUnicast&Version=2023\-07\-20


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`SendRoomUnicast` |Interface name. The value of this interface: `SendRoomUnicast` |
|Version |String |Yes |`2023-07-20` |OpenAPI version. The value of this interface: `2023-07-20` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app. |
|RoomId |String |Yes |`You_RoomId` |The ID of the room where the user receives the message |
|From |String |Yes |`from_server_id` |The only identifier of the business server;<br><br>It is customized by you according to the [ID naming specification when calling OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828#taskid) ;<br><br>Under an `AppID` , it cannot be repeated with the `user_ID` used by real users for real\-time message communication;<br><br>It is recommended to send messages with a fixed `ID` . |
|To |String |Yes |`to_user_id` |ID set when the user calls the [login](https://docs.byteplus.com/en/docs/12/docs-70080#login) interface to receive messages, which can be used to receive out\-of\-room messages. |
|Binary |Boolean |Yes |`flase` |* `true`: binary message;<br><br>* `false`: text message. |
|Message |String |Yes |`hello` |Peer\-to\-peer message.<br><br>If the message is a binary one, it needs to be Base64 encoded. |


<span id="response-parameters"></span>
## Response parameters

See [BaseResponse](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#response) for the structure of return results.

`Result` returns `success` when the request succeeds and specific error message when it fails.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Message |String |`Success` |The message'Success' is returned when the request is successful, indicating that the server level successfully received the message, and a specific error message is returned when it fails. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=SendRoomUnicast&Version=2023-07-20
{
    "AppId": "You****pId",
    "From": "from_server_id",
    "To": "to_user_id",
    "RoomId": "You_RoomId",
    "Message": "hello",
    "Binary": false
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "SendRoomUnicast",
        "Version": "2023-07-20",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Message": "Success"
    }
}
```


&nbsp;
