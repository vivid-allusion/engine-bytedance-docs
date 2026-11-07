---
title: "UnbanUserStream"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-80655"
---

When you, as a host, room\-owner or administrator, need to unblock the audio/video stream of a user in the room, you can call `UnbanUserStream` to do this.

<span id="description"></span>
## Description

You can call the `UnbanUserStream`interface, specify the `AppId`you belong to, and unblock the user audio/video stream publishing of the blocked `userId`in the specified `roomId`room.


> * When a user is unbanned from pushing video streams, other users in the room will receive `onVideoStreamBanned` callback.

> * When a user is unbanned from pushing audio streams, other users in the room will receive `onAudioStreamBanned` callback.


<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [Call OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828).

<span id="request-method"></span>
### Request method

POST

<span id="restriction"></span>
### Restriction

QPS must not exceed 20

<span id="request-parameters"></span>
### Request parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/12/docs-69828#request-parameters).

<span id="query"></span>
#### Query


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |`UnbanUserStream` |Interface name. The value of this interface: `UnbanUserStream` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body"></span>
#### Body


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app. |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |Yes |`Your_UserId` |The ID of the users you wish to block their audio/video streams. |
|Token |String |Yes |`Your_Token` |Token of the user you wish to unblock |
|Video |Bool |No |`true` |Whether to block the video stream. When set to true, the video stream will be blocked. |
|Audio |Bool |No |`true` |Whether to block the audio stream. When set to true, the audio stream will be blocked. |


<span id="sample-request"></span>
### Sample request

<span id="query"></span>
#### Query

```postscript
https://open.byteplusapi.com?Action=UnbanUserStream&Version=2020-12-01
```


<span id="body"></span>
#### Body

```json
{
    "AppId": "Your_AppId",
    "RoomId": "Your_RoomId",
    "UserId": "Your_UserId",
    "Token": "Your_Token",
    "Video": true,
    "Audio": false
}
```


<span id="response"></span>
## Response

`Result` returns "success" only when the request succeeds and null when it fails.

<span id="sample-response"></span>
### Sample response

```json
{   "ResponseMetadata": {
        "RequestId": "Your_RequestId",
        "Action": "UnbanUserStream",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "message": "success"
    }
}
```
