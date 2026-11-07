---
title: "ListUserInfo"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-156027"
---

In an audio & video application, you may need to query the information of specific or all users in a room over a period of time. You can use `ListUserInfo` to do this.

<span id="description"></span>
## Description

You can call the `ListUserInfo` interface, specify the `AppId` , `RoomId` and the time period to be queried, and get the relevant information of the specified or all users in the room.

<span id="restriction"></span>
## Restriction


|Category |Frequency capping |
|---|---|
|Maximum number of queries |10 per second |
|The farthest queryable time |Fourteen days |
|Maximum time span of single query |6 hours (If the time span you set is over 6 hours, the end time of the query task will be automatically adjusted to the starting time plus 6 hours.) |
|Data delay |100 seconds |


<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [Call OpenAPI](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828).

<span id="request-method"></span>
### Request method

GET

<span id="request-parameters"></span>
### Request parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters ](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters).


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListUserInfo` |Interface name, this interface value: `ListUserInfo` |
|Version |String |Yes |`2020-12-01` |Interface version, this interface value: `2020-12-01` |
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|StartTime |String |Yes |`2006-01-02T15:04:05+08:00` |Start timestamp for querying in the format of RFC3339 in second |
|EndTime |String |Yes |`2006-01-02T15:04:05+08:00` |End timestamp for querying in the format of RFC3339 in second |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room |
|PageNum |Int |No |`1` |Sequence number for paging. The default value is `1` |
|PageSize |Int |No |`20` |The number of rooms per page. The maximum is 100, and the default value is `20`. If the value input exceeds 100, it will be adjusted to 100. |
|UserId |String |No |`Your_UserId` |The list of user IDs to be queried. Every user ID is separated by commas, and up to 10 can be specified. If the input value is invalid, it is rejected by default. When empty, query the information of all users in the room. |
|ExcludeServerUser |Bool |No |`true` |Whether to exclude Linux users. The default value is`true`, which means Linux users are excluded. |


<span id="request-example"></span>
### Request example

```postscript
http://open.byteplusapi.com?Action=ListUserInfo&AppId=Your_AppId&StartTime=2022-09-09T09:00:00 08:00&EndTime=2022-09-09T12:00:00 08:00&RoomId=Your_RoomId&Version=2020-12-01
```


<span id="return-parameters"></span>
### Return Parameters

The structure of `BaseResponse.Result` is as follows:

**Result**


|Parameter |Type |Example |Description |
|---|---|---|---|
|Total |int |`2` |The total number of users queried |
|PageNum |int |`1` |Sequence number for paging |
|PageSize |int |`20` |The number of rooms per page |
|UserList |Array of [UserListItem](https://docs.byteplus.com/en/docs/12/14240#userlistitem) | |User information |


<span id="userlistitem"></span>
#### UserListItem  


|Parameter |Type |Example |Description |
|---|---|---|---|
|CallId |String |`Your_CallId` |ID of a calling, the only identifier of a calling |
|RoomId |String |`Your_RoomId` |Queried Room ID |
|UserId |String |`Your_UserId` |Queried User ID |
|CreatedAt |String |`2006-01-02T15:04:05+08:00` |Timestamp when user first enters the room in the format of RFC3339 in seconds under the CallId |
|LeaveAt |String |`2006-01-02T15:04:05+08:00` |Timestamp when user last leaves the room in the format of RFC3339 in second under the CallId. If the user is online when you query, the return value is empty. |
|Access |String |`wifi` |Network type of user under the CallId. Enumeration values: `2g` , `3g` , `4g` , `5g` , `wifi` , `unknown` . |
|OS |String |`ios` |Device platform of user under the CallId. Enumeration values: `android` , `ios` , `linux` , `mac` , `windows` , `web` , `unknown`. |
|DeviceType |String |`iPhone 11` |Device type of user under the CallId |
|SdkVersion |String |`3.30.101` |SDK version of user under the CallId |
|Pub |Bool |`True` |Whether the user published a stream under the CallId |
|Finished |Bool |`True` |Whether the user leaves the room under the CallId |
|Duration |Int |`100` |The total online time of the user from the first time entering the room to the last time leaving the room under the CallId(Time intervals will be accumulated if the user enters and leaves the room multiple times). The duration is based on the real\-time status of user when queried. The unit of duration is second. |
|Record |Array of [Record](https://docs.byteplus.com/en/docs/12/14240#record) |/ |The record of entering and leaving of a user under the CallId |


<span id="record"></span>
#### Record  


|Parameter |Type |Example |Description |
|---|---|---|---|
|Time |String |`2022-10-31T19:22:57+08:00` |Timestamp when a user enters or leaves in the format of RFC3339 in seconds. |
|Type |String |`join_room` |The user entering or leaving the room. It can takes value: `join_room` or `leave_room`. |


<span id="response"></span>
## Response

<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_RequestID",
        "Action": "ListUserInfo",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Total": 1,
        "PageNum": 1,
        "PageSize": 20,
        "UserList": [
            {
                "CallId": "Your_CallId",
                "RoomId": "Your_RoomId",
                "UserId": "Your_UserId",
                "CreatedAt": "2022-10-31T19:22:57+08:00",
                "LeaveAt": "2022-10-31T19:23:29+08:00",
                "Access": "wifi",
                "OS": "linux",
                "DeviceType": "iPhone 11",
                "SdkVersion": "3.37.0517.1420",
                "Pub": false,
                "Duration": 22,
                "Finished": true,
                "Record": [
                    {
                        "Time": "2022-10-31T19:22:57+08:00",
                        "Type": "join_room"
                    },
                    {
                        "Time": "2022-10-31T19:23:08+08:00",
                        "Type": "leave_room"
                    },
                    {
                        "Time": "2022-10-31T19:23:18+08:00",
                        "Type": "join_room"
                    },
                    {
                        "Time": "2022-10-31T19:23:29+08:00",
                        "Type": "leave_room"
                    }
                ]
            }
        ]
    }
}
```
