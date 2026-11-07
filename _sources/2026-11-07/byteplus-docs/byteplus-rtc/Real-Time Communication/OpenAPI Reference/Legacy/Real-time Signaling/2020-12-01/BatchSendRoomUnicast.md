---
title: "BatchSendRoomUnicast"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104962"
---

In your audio & video application, when you need to send peer\-to\-peer messages from the business server level to a number of users in a specified RTC room simultaneously, you can use the OpenAPI `BatchSendRoomUnicast` to do this.

<span id="usage-scenario"></span>
## Usage scenario

You can call the `BatchSendRoomUnicast` interface, specify the `AppId`, and send peer\-to\-peer messages to the specified users in the room corresponding to the `roomId` simultaneously.


> * The message can be either a text message or a binary message.

> * The size of text message cannot exceed 20 KB, and the size of binary message cannot exceed 20 KB.

> * This interface supports sending peer\-to\-peer messages to up to 600 users at a time.


After the message is successfully sent, the user receives the message via the following callback:

After the message is successfully sent, the user receives the message via the following callback:


| |Android |iOS |Windows |
|---|---|---|---|
|Text message |[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#onusermessagereceivedoutsideroom) |[rtcEngine:onUserMessageReceived:message](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onusermessagereceived-message) |[OnUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70096#onusermessagereceivedoutsideroom) |
|Binary message |[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#onuserbinarymessagereceivedoutsideroom) |[rtcEngine:onUserBinaryMessageReceivedOutsideRoom:message](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onuserbinarymessagereceived-message) |[OnUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70096#onuserbinarymessagereceivedoutsideroom) |


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=BatchSendRoomUnicast&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`BatchSendRoomUnicast` |Interface name. The value of this interface: `BatchSendRoomUnicast` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app. |
|RoomId |String |Yes |`You_RoomId` |The ID of the room. It's the only identifier of a room. |
|From |String |Yes |`from_server_id` |The only identifier of the business server.<br><br>Under an `AppID` , it cannot be repeated with the `user_ID` used by real users for real\-time message communication;<br><br>It is recommended to send messages with a fixed `ID` .<br><br><br>* The length of a string is no longer than 128 characters.<br><br>* A string can contain following characters:<br><br>   * `a~z`<br><br>   * `A~Z`<br><br>   * `0~9`<br><br>   * `@` `.` `_` `-` |
|To |Array of String |Yes |`[user1, user2]` |ID of users receiving messages |
|Binary |Boolean |Yes |`flase` |* `true`: binary message;<br><br>* `false`: text message. |
|Message |String |Yes |`hello` |Peer\-to\-peer message<br><br>&nbsp;<br><br>If the message is a binary one, it needs to be Base64 encoded. |


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
POST https://open.byteplusapi.com?Action=BatchSendRoomUnicast&Version=2020-12-01
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "BatchSendRoomUnicast",
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
