---
title: "SendRoomUnicast"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-79118"
---

Calls `SendRoomUnicast` to send a text message or a binary message to a specified user in an RTC room.

<span id="usage-scenario"></span>
## Usage scenario

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


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=SendRoomUnicast&Version=2020\-12\-01


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
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app. |
|RoomId |String |Yes |`You_RoomId` |The ID of the room where the user receives the message |
|From |String |Yes |`from_server_id` |The only identifier of the business server.<br><br>Under an `AppID` , it cannot be repeated with the `user_ID` used by real users for real\-time message communication;<br><br>It is recommended to send messages with a fixed `ID` .<br><br><br>* The length of a string is no longer than 128 characters.<br><br>* A string can contain following characters:<br><br>   * `a~z`<br><br>   * `A~Z`<br><br>   * `0~9`<br><br>   * `@` `.` `_` `-` |
|To |String |Yes |`to_user_id` |ID set when the user calls the [login](https://docs.byteplus.com/en/docs/12/docs-70080#login) interface to receive messages, which can be used to receive out\-of\-room messages. |
|Binary |Boolean |Yes |`flase` |* `true`: binary message;<br><br>* `false`: text message. |
|Message |String |Yes |`hello` |Peer\-to\-peer message.<br><br>&nbsp;<br><br>If the message is a binary one, it needs to be Base64 encoded. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Message |String |`success` |Only return the message `Success` when the request is successful, empty if it fails. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=SendRoomUnicast&Version=2020-12-01
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "SendRoomUnicast",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "message": "Success"
    }
}
```


&nbsp;
