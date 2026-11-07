---
title: "GetRoomOnlineUsers"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1188355"
---

By specifying the AppId and room ID, you can query the user information in the room, including the total number of existing users, the total number of invisible users, the type of user terminal device, etc.

<span id="Requirements"></span>
## Requirements

Request frequency: When the request parameter `Property` is `false`, the QPS must not exceed **40**; when the request parameter `Property` is `true`, the QPS must not exceed **1**.

<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://open.byteplusapi.com?Action=GetRoomOnlineUsers&Version=2023\-11\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="Query"></span>
### Query


|**Parameter**  |**Data Type**  |**Required**  |**Sample Value**  |**Description**  |
|---|---|---|---|---|
|Action |String |Yes |`GetRoomOnlineUsers` |Interface name. The value of this interface: `GetRoomOnlineUsers` |
|Version |String |Yes |`2023-11-01` |OpenAPI version. The value of this interface: `2023-11-01` |
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. |
|Property |Boolean |No |`false` |Whether to return other detailed information except the user ID;<br><br><br>* true: Return. In addition to the user ID, information such as device type and platform type will also be returned.<br><br>* false: Do not return, only return the user ID. |
|RoleType |Integer |No |`0` |Filter the type of user to be queried, which only takes effect when `Property` is `true`:<br><br><br>* 0 (default value): Do not distinguish the type, and return visible and invisible users.<br><br>   > The upper limit of the total number of visible and invisible users that can be returned is 200. If the total number of users exceeds the upper limit, visible users will be returned first.<br><br>* 1: Only return visible users.<br><br>* 2: Only return invisible users. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|RoomExists |Boolean |`true` |Whether the queried room exists.<br><br><br>* `true`: Exist.<br><br>* `false`: Not exist.<br><br><br>When the value of `RoomExist` is false, no other fields will be returned. |
|TotalUser |Integer |`6` |The total number of users found.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This field is only returned when <code>Property</code> is <code>false</code>.</div><br> |
|TotalInvisibleUser |Integer |`3` |The total number of invisible users found. A maximum of 10,000 invisible users will be returned.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This field is only returned when <code>Property</code> is <code>false</code>.</div><br> |
|VisibleUserList |Array of [VisibleUserList](https://docs.byteplus.com/en/docs/12/21041#visibleuserlist) |`["normal_user_1"]` |List of visible users |
|InvisibleUserList |Array of [InvisibleUserList](https://docs.byteplus.com/en/docs/12/21041#invisibleuserlist) |`["silent_user_1"]` |List of invisible users |


<span id="visibleuserlist"></span>
### VisibleUserList


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|UserId |String | |User ID. |
|PlatformType |Integer | |SDK types:<br><br><br>* 1: Native<br><br>* 2: Web<br><br>* 4: Douyin Mini Program |
|DeviceType |String | |The types of operating systems of user terminal devices:<br><br><br>* android<br><br>* ios<br><br>* mac<br><br>* windows<br><br>* linux<br><br>* harmony |
|MediaProcessingType |Integer |`21` |Backend processing business types.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This field will only be returned when the user is a backend processing robot.</div><br><br><br>The values are as follows:<br><br><br>* 11: Local recording<br><br>* 21: Single\-stream cloud recording<br><br>* 22: Mixing\-stream cloud recording<br><br>* 23: Multi\-stream push<br><br>* 24: Single\-stream push<br><br>* 25: Relay online media stream<br><br>* 27: WebRecord<br><br>* 28: Video frame extraction<br><br>* 29: Audio segment<br><br>* 30: Push to WTN (public stream)<br><br>* 34: Conversational AI |


<span id="invisibleuserlist"></span>
### InvisibleUserList


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|UserId |String | |User ID. |
|PlatformType |Integer | |SDK Types:<br><br><br>* 1: Native<br><br>* 2: Web<br><br>* 4: Douyin Mini Program |
|DeviceType |String | |The types of operating systems of user terminal devices:<br><br><br>* android<br><br>* ios<br><br>* mac<br><br>* windows<br><br>* linux<br><br>* harmony |
|MediaProcessingType |Integer |`21` |Audio Segment |


<span id="sample-request"></span>
## Sample request

```json
GET https://open.byteplusapi.com?Action=GetRoomOnlineUsers&Version=2023-11-01&AppId=You****pId&RoomId=Your_RoomId
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "GetRoomOnlineUsers",
        "Version": "2023-11-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "RoomExist": true,
        "TotalUser": 6,
        "TotalInvisibleUser": 3,
        "VisibleUserList": [
            "normal_user_1",
            "normal_user_2",
            "normal_user_3"
        ],
        "InvisibleUserList": [
            "silent_user_1",
            "silent_user_2",
            "silent_user_3"
        ]
    }
}
```
