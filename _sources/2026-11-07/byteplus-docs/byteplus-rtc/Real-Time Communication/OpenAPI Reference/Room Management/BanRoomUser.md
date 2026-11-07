---
title: "BanRoomUser"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1188353"
---

You can call `BanRoomUser` interface, specify your `AppId` and `RoomId` to ban a room, or specify `AppId`, `RoomId` and `UserId` to remove specific user in the room.

<span id="usage-scenario"></span>
## Usage scenario


* By specifying the `AppId` and `RoomId`, you can ban the specified room. If `ForbiddenInterval` is empty or `0`, all users in the room will be kicked out, but they will be allowed to re\-enter the room immediately. If `ForbiddenInterval` is greater than `0`, all users will be kicked out of the room, and no users will be allowed to re\-enter the room within the specified time period.

* By specifying the `AppId`, `RoomId`, and `UserId`, you can ban a user in a specified room. If `ForbiddenInterval` is empty or `0`, the user will be kicked out of the specified room, but they will be allowed to re\-enter the room immediately. If `ForbiddenInterval` is greater than `0`, the user will be kicked out of the room, and they will not be allowed to re\-enter the room within the specified time period.

* By specifying the `AppId` and `UserId`, you can ban the user corresponding to this `UserId` in all rooms. If `ForbiddenInterval` is empty or `0`, all users corresponding to `UserId` will be kicked out of the rooms, but they will be allowed to re\-enter the rooms immediately. If `ForbiddenInterval` is greater than `0`, all users corresponding to `UserId` will be kicked out of the rooms, and they will not be allowed to re\-enter the rooms within the specified time period.

* By specifying the `AppId` and `IP`, you can ban all users who enter the room using this public IP. If `ForbiddenInterval` is empty or `0`, all users corresponding to the IP will be kicked out of the rooms, but users using this IP will be allowed to re\-enter the rooms immediately. If `ForbiddenInterval` is greater than `0`, all users corresponding to the IP will be kicked out of the rooms, and they will not be allowed to re\-enter the rooms within the specified time period.

* Preemptive banning is supported. At least one of `RoomId`, `UserId`, and `IP` must have a non\-empty value.


After the OpenAPI is called, the banned user gets an error code of `-1006`; if the banned user is visible, other users in the same RTC room receive `onUserLeave`.

<span id="requirements"></span>
## Requirements

<span id="restriction"></span>
## Restriction

QPS must not exceed 40.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=BanRoomUser&Version=2023\-11\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`BanRoomUser` |Interface name. The value of this interface: `BanRoomUser` |
|Version |String |Yes |`2023-11-01` |OpenAPI version. The value of this interface: `2023-11-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|RoomId |String |No |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |No |`Your_UserId` |ID of the user you want to ban |
|IP |String |No |`Your_IP` |public IP you want to ban.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When this parameter is filled in, RoomId and UserId must be left empty.</div><br><br><br>Repeatedly calling this interface to ban the same IP will not cause the request to fail, but `BaseResponse.Result` will return `User IP has been banned`. |
|ForbiddenInterval |Integer |No |`0` |Ban length in seconds. The value's range is `[60,259200]`.<br><br>If the value takes empty or `0`, it means that the user is allowed to re\-enter the room.<br><br>If the value is greater than `0` and less than `60`, it will be automatically changed to `60`.<br><br>If the value is greater than `259200`, it will be automatically changed to `259200`. |


<span id="response-parameters"></span>
## Response parameters

Result returns "success" only when the request succeeds and null when it fails.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Message |String |`success` |The message "success" is returned only if the request succeeds, but empty if it fails. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=BanRoomUser&Version=2023-11-01
{
    "AppId": "You****pId",
    "RoomId": "Your_RoomId",
    "UserId": "Your_UserId",
    "ForbiddenInterval": 0
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "BanRoomUser",
        "Version": "2023-11-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "message": "success"
    }
}
```


&nbsp;
