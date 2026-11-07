---
title: "SendUnicast"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1164061"
---

> This API interface is for the latest version, and new features will be updated here. It is recommended to use the latest version. For documentation of older versions, please refer to [legacy](https://docs.byteplus.com/en/docs/12/docs-v3wedfo4dj).


Send out\-of\-room peer\-to\-peer messages from the business server to a client.

<span id="usage-guide"></span>
## Usage Guide

<span id="prerequisites"></span>
## Prerequisites


1. For Native SDK 3.60 and above, and Web SDK 4.66 and above, ensure that the **RTS advanced feature** is enabled in the [RTC console](https://console.byteplus.com/rtc/cloudRTC?&tab=RTSMode) before calling this interface.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If this feature is enabled while the SDK is running, you must reinitialize the engine for the configuration to take effect.   </div>
   

2. Before sending a message, you need to call the `login` interface to complete the login and obtain the `user_Id` for receiving real\-time messages.


<span id="interface-behavior"></span>
## Interface Behavior

After the message is successfully sent, the user receives the message via the following callback:


| |Android |iOS |Windows |
|---|---|---|---|
|Text message |[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#onusermessagereceivedoutsideroom) |[rtcEngine:onUserMessageReceivedOutsideRoom:message](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onusermessagereceivedoutsideroom-message) |[OnUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#onusermessagereceivedoutsideroom) |
|Binary message |[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#onuserbinarymessagereceivedoutsideroom) |[rtcEngine:onUserBinaryMessageReceivedOutsideRoom:message](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onuserbinarymessagereceivedoutsideroom-message) |[OnUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#onuserbinarymessagereceivedoutsideroom) |


<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [call OpenAPI](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828) .

<span id="requirements"></span>
## Requirements

QPS: For each AppId, the sum of the upper limits of the call frequencies of `SendUnicast`, `SendRoomUnicast`, `SendBroadcast` and `BatchSendRoomUnicast` is **500** times per second.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=SendUnicast&Version=2023\-07\-20


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`SendUnicast` |Interface name. The value of this interface: `SendUnicast` |
|Version |String |Yes |`2023-07-20` |OpenAPI version. The value of this interface: `2023-07-20` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app. |
|From |String |Yes |`from_server_id` |The only identifier of the business server;<br><br>It is customized by you according to the [ID naming specification when calling OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828#taskid) ;<br><br>Under an `AppID` , it cannot be repeated with the `user_ID` used by real users for real\-time message communication;<br><br>It is recommended to send messages with a fixed `ID` . |
|To |String |Yes |`to_user_id` |ID set when the user calls the [login](https://docs.byteplus.com/en/docs/12/docs-70080#login) interface to receive messages, which can be used to receive out\-of\-room messages |
|Binary |Boolean |Yes |`flase` |* `true`: binary message;<br><br>* `false`: text message. |
|Message |String |Yes |`hello` |Peer\-to\-peer message.<br><br>If the message is a binary one, it needs to be Base64 encoded. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Message |String |`Success` |The message'Success' is returned when the request is successful, indicating that the server level successfully received the message, and a specific error message is returned when it fails. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=SendUnicast&Version=2023-07-20
{
    "AppId": "You****pId",
    "From": "from_server_id",
    "To": "to_user_id",
    "Message": "hello",
    "Binary": true
}
```


<span id="sample-response"></span>
### Sample response

See [BaseResponse](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1164065#baseresponse) for the structure of return results.

`Result` returns `success` when the request succeeds and specific error message when it fails.

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "SendUnicast",
        "Version": "2023-07-20",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "message": "Success"
    }
}
```


&nbsp;
