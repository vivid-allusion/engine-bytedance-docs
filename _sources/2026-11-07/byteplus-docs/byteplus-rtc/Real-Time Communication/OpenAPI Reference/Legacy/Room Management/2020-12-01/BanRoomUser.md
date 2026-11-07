---
title: "BanRoomUser"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-336038"
---

In your audio and video application, you may need to ban a room or specific user in the room to dismiss the room or remove specific user. You can use the `BanRoomUser` OpenAPI to do this.

<span id="description"></span>
## Description

You can call `BanRoomUser` interface, specify your `AppId` and `RoomId` to ban a room, or specify `AppId`, `RoomId` and `UserId` to remove specific user in the room.

After the OpenAPI is called, the banned user gets an error code of `-1006`; if the banned user is visible, other users in the same RTC room receive `onUserLeave`.

<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [Call OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828).

<span id="restriction"></span>
### Restriction


|Category |Frequency capping |
|---|---|
|Maximum number of queries |20 per second |


<span id="request-method"></span>
### Request method

POST

<span id="request-parameters"></span>
### Request parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters ](https://docs.byteplus.com/en/docs/12/docs-69828#request-parameters).

<span id="query"></span>
#### Query


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |`BanRoomUser` |Interface name. The value of this interface: `BanRoomUser` |
|Version |String |Yes |`2020-12-01` |Interface version. The value of this interface: `2020-12-01` |


<span id="body"></span>
#### Body


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |No |`Your_UserId` |ID of the user you want to ban |
|ForbiddenInterval |Int |No |`0` |Ban length in seconds. The value's range is `[60,259200]`.<br><br>If the value takes empty or `0`, it means that the user is allowed to re\-enter the room.<br><br>If the value is greater than `0` and less than `60`, it will be automatically changed to `60`.<br><br>If the value is greater than `259200`, it will be automatically changed to `259200`. |


<span id="sample-request"></span>
### Sample request

<span id="query"></span>
#### Query

```postscript
https://open.byteplusapi.com?Action=BanRoomUser&Version=2020-12-01
```


<span id="body"></span>
#### Body

```json
{
     "AppId" : "Your_AppId",
     "RoomId" : "Your_RoomId",
     "UserId" : "Your_UserId",
     "ForbiddenInterval" : 0
}
```


<span id="response"></span>
## Response

`Result` returns "success" only when the request succeeds and null when it fails.

<span id="sample-response"></span>
### Sample response

<span id="normal-return-example"></span>
### Normal return example

```json
{
     "ResponseMetadata": {
         "RequestId": "Your_RequestId",
         "Action": "BanRoomUser",
         "Version": "2020-12-01",
         "Service": "rtc",
         "Region": "ap-singapore-1"
     },
     "Result": {
         "message": "success"
     }
}
```
