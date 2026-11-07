---
title: "ListRoomInfo"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1186715"
---

In an audio & video application, you may need to query the list of the rooms where audio or video calls are being made and related information of these rooms.

<span id="description"></span>
## Description

You can call the `ListRoomInfo` interface, specify the `AppId` ` and the time period to be queried to get the list of the rooms and related information of these rooms.

> When the creation time of a room is within the span to be queried, the relevant information of the room will be shown.


<span id="restriction"></span>
## Restriction


|Category |Frequency capping |
|---|---|
|Maximum number of queries |10 per second |
|The farthest queryable time |Fourteen days |
|Maximum time span of single query |24 hours (If the time span you set is over 24 hours, the end time of the query task will be automatically adjusted to the starting time plus 24 hours.) |
|Data delay |20 seconds |


<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [Call OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828).

<span id="request-method"></span>
### Request method

GET

<span id="request-parameter"></span>
### Request Parameter

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters ](https://docs.byteplus.com/en/docs/12/docs-69828#request-parameters).

<span id="query"></span>
#### Query


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListRoomInfo` |Interface name. The value of this interface: `ListRoomInfo` |
|Version |String |Yes |`2023-11-01` |Interface version. The value of this interface:`2023-11-01` |
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|StartTime |String |Yes |`2006-01-02T15:04:05+08:00` |Start timestamp for querying in the format of RFC3339 in second |
|EndTime |String |Yes |`2006-01-02T15:04:05+08:00` |End timestamp for querying in the format of RFC3339 in second |
|RoomId |String |No |`Your_RoomId` |The ID of the room. It's the only identifier of a room |
|PageNum |Int |No |`1` |Sequence number for paging. The default value is `1` |
|PageSize |Int |No |`20` |The number of rooms per page. The maximum is 100, and the default value is `20`. If the value input exceeds 100, it will be adjusted to 100. |


<span id="request-example"></span>
### Request example

```postscript
http://open.byteplusapi.com?Action=ListRoomInfo&AppId=Your_AppId&StartTime=2022-09-09T10:00:00 08:00&EndTime=2022-09-09T13:00:00 08:00&Version=2023-11-01
```


<span id="return-parameter"></span>
### Return Parameter


|Parameter |Type |Example |Description |
|---|---|---|---|
|Total |Int |`2` |The total number of rooms quried. If there are multiple calls under the same RoomId, they will be recorded as multiple rooms. |
|PageNum |Int |`1` |Sequence number for paging |
|PageSize |Int |`20` |The number of rooms per page |
|HasMore |Bool |`false` |Whether there is follow\-up data |
|RoomList |Array of [RoomListItem](https://docs.byteplus.com/en/docs/12/32202#roomlistitem) |`-` |Room information |


<span id="roomlistitem"></span>
#### RoomListItem  


|Parameter |Type |Example |Description |
|---|---|---|---|
|CallId |String |`Your_CallId` |ID of a calling, the only identifier of a calling |
|RoomId |String |`Your_RoomId` |Room ID returned |
|CreatedTime |String |`2022-04-17T22:38:13+08:00` |Timestamp when room is created in the format of RFC3339 in second |
|DestroyTime |String |`2022-04-17T22:38:13+08:00` |Timestamp when room is destroyed in the format of RFC3339 in second |
|ActiveUserNum |Int |`0` |Number of users currently in the room |
|IsFinished |Bool |`true` |Whether the room is destroyed |


<span id="response"></span>
## Response

<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_RequestID",
        "Action": "ListRoomInfo",
        "Version": "2023-11-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Total": 2,
        "PageNum": 1,
        "PageSize": 20,
        "HasMore": false,
        "RoomList": [
            {
                "CallId": "test_call1",
                "RoomId": "test_room1",
                "CreateTime": "2022-10-31T19:17:47+08:00",
                "DestroyTime": "2022-10-31T19:18:05+08:00",
                "ActiveUserNum": 0,
                "IsFinished": true
            },
            {
                "CallId": "test_call2",
                "RoomId": "test_room1",
                "CreateTime": "2022-10-31T19:18:09+08:00",
                "DestroyTime": "2022-10-31T19:18:25+08:00",
                "ActiveUserNum": 0,
                "IsFinished": true
            }
        ]
    }
}
```
