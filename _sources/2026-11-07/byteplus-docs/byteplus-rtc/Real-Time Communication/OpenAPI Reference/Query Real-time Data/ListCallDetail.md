---
title: "ListCallDetail"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1186717"
---

You can use this interface to query the uplink and downlink data of a user in a specified room under a certain application within a certain period of time.

<span id="usage-scenario"></span>
## Usage scenario

Specify the `AppId`, `RoomId`, `UserId` and the query time period to query the uplink and downlink data of the specified user in the specified room within the time period.

<span id="requirements"></span>
## Requirements


|Category |Frequency capping |
|---|---|
|Maximum number of queries |10 requests/minute<br><br>10000 times/day |
|The furthest queryable time |6 days |
|Maximum time span of single query |1 hour |
|Data Delay |100 seconds |


<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://open.byteplusapi.com?Action=ListCallDetail&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListCallDetail` |Interface name. The value of this interface: `ListCallDetail` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|StartTime |String |Yes |`2022-05-22T12:00:00+08:00` |Start timestamp for querying in the format of RFC3339 in second |
|EndTime |String |Yes |`2022-05-22T12:59:00+08:00` |End timestamp for querying in the format of RFC3339 in second |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |Yes |`user1,user2` |The list of user IDs to query, up to 20. If the value is invalid, it will be rejected by default. This parameter is valid when `RoomId` is not empty. |
|Direction |String |No |`0` |The direction of data transmission. It can take `0`, `1`, `2`.<br><br><br>* `0` : up and down. Default value.<br><br>* `1` : up<br><br>* `2`: down. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|UserCallDetail |Array of [UserCallDetail](https://docs.byteplus.com/en/docs/12/32201#usercalldetail) |`-` |Information about the index of user's call quality |


<span id="usercalldetail"></span>
### UserCallDetail


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |ID of the queired room |
|UserId |String |`Your_UserId` |ID of the queired user |
|PeerId |String |`Your_Peer_Id` |ID of Peer user, which only exists when the queried userd is on downlink |
|Direction |String |`up` |The direction ofacquired data. |
|CallDetail |Array of [CallDetail](https://docs.byteplus.com/en/docs/12/32201#calldetail) |`-` |Details of this call quality indicator |


<span id="calldetail"></span>
### CallDetail


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Desc |String |`Audio sending bit rate` |Name of the indicator |
|Name |String |`bandwidth` |The field name of the indicator |
|Unit |String |`kbps` |Unit |
|Data |Array of [DataItem](https://docs.byteplus.com/en/docs/12/32201#dataitem) |`-` |Detail about the indicator |


<span id="dataitem"></span>
### DataItem


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |Long |`1652702700000` |The Unix timestamp of the data point for this indicator, in milliseconds. |
|Value |Float |`1` |The value of this indicator's data point |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://open.byteplusapi.com?Action=ListCallDetail&AppId=You****pId&StartTime=2022-05-22T12:00:00+08:00&EndTime=2022-05-22T12:59:00+08:00&RoomId=Your_RoomId&UserId=Your_UserId&Version=2023-11-01
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Service": "rtc",
        "Region": "ap-singapore-1",
        "Version": "2023-11-01"
    },
    "Result": {
        "UserCallDetail": [
            {
                "RoomId": "Your_RoomId",
                "UserId": "Your_UserId",
                "PeerId": "Your_PeerId",
                "Direction": "up",
                "CallDetail": [
                    {
                        "Desc": "Audio sending bit rate",
                        "Name": "bandwidth",
                        "MediaType": "audio",
                        "Data": [
                            {
                                "Time": 1652702700000,
                                "Value": 1
                            },
                            {
                                "Time": 16527027002000,
                                "Value": 2
                            }
                        ]
                    },
                    {
                        "Desc": "Audio upstream packet loss rate",
                        "Name": "fraction_lost",
                        "MediaType": "audio",
                        "Data": [
                            {
                                "Time": 1652702700000,
                                "Value": 1
                            },
                            {
                                "Time": 16527027002000,
                                "Value": 2
                            }
                        ]
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
