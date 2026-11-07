---
title: "ListCallDetail"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-172151"
---

You can use this interface to query the uplink and downlink data of a user in a specified room under a certain application within a certain period of time.

<span id="description"></span>
## Description

Specify the `AppId`, `RoomId`, `UserId` and the query time period to query the uplink and downlink data of the specified user in the specified room within the time period.

<span id="restriction"></span>
## Restriction


|Category |Frequency capping |
|---|---|
|Maximum number of queries |10 requests/minute<br><br>10000 times/day |
|The furthest queryable time |6 days |
|Maximum time span of single query |1 hour |
|Data Delay |100 seconds |


<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [Call OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828).

<span id="request-method"></span>
### Request method

GET

<span id="request-parameters"></span>
### Request parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters ](https://docs.byteplus.com/en/docs/12/docs-69828#request-parameters).


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListCallDetail` |Interface name. The value of this interface: `ListCallDetail` |
|Version |String |Yes |`2020-12-01` |Interface version. The value of this interface: `2020-12-01` |
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|StartTime |String |Yes |`2022-05-22T12:00:00+08:00` |Start timestamp for querying in the format of RFC3339 in second |
|EndTime |String |Yes |`2022-05-22T12:59:00+08:00` |End timestamp for querying in the format of RFC3339 in second |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |Yes |`"user1","user2"` |The list of user IDs to query, up to 20. If the value is invalid, it will be rejected by default. This parameter is valid when `RoomId` is not empty. |
|Direction |String |No |`0` |The direction of data transmission. It can take `0`, `1`, `2`.<br><br><br>* `0` : up and down. Default value.<br><br>* `1` : up<br><br>* `2`: down. |


<span id="request-parameter"></span>
### Request Parameter

```postscript
http://open.byteplusapi.com?Action=ListCallDetail&AppId=Your_AppId&StartTime=2022-05-22T12:00:00+08:00&EndTime=2022-05-22T12:59:00+08:00&RoomId=Your_RoomId&UserId=Your_UserId&Version=2020-12-01
```


<span id="return-parameter"></span>
### Return parameter

See [BaseResponse](https://docs.byteplus.com/en/docs/12/docs-69835#baseresponse) for the structure of return results. The structure of `BaseResponse.Result` is as follows:


|Parameter |Type |Description |
|---|---|---|
|UserCallDetail |Array of [UserCall](https://docs.byteplus.com/en/docs/12/14238#usercall) |Information about the index of user's call quality |


> The return value Result only returns the above parameters when the request is successful, and it is empty when the request fails


**UserCall** 


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |ID of the queired room |
|UserId |String |`Your_UserId` |ID of the queired user |
|PeerId |String |`Your_Peer_Id` |ID of Peer user, which only exists when the queried userd is on downlink |
|Direction |String |`up` |The direction ofacquired data. |
|CallDetail |Array of [Detail](https://docs.byteplus.com/en/docs/12/14238#detail) | |Details of this call quality indicator |


**Detail** 


|Parameter |Type |Example |Description |
|---|---|---|---|
|Desc |String |`Audio sending bit rate` |Name of the indicator |
|Name |String |`bandwidth` |The field name of the indicator |
|MediaType |String |`audio` |The media type of this indicator. It can takes`audio` or `video`. |
|Data |Array of [DataItem](https://docs.byteplus.com/en/docs/12/14238#dataitem) | |Detail about the indicator |


**DataItem** 


|Parameter |Type |Example |Description |
|---|---|---|---|
|Time |Int |`1652702700000` |The Unix timestamp of the data point for this indicator, in milliseconds. |
|Value |Float |`1` |The value of this indicator's data point |


<span id="response"></span>
## Response

<span id="sample-response"></span>
### Sample response

```json
{
   "ResponseMetadata": {
     "RequestId": "Your_RequestId",
     "Service": "rtc",
     "Region": "ap-singapore-1",
     "Version": "2020-12-01"
   },
   "Result": {
     "UserCallDetail": [
       {
         "RoomId": "Your_RoomId",
         "UserId": "Your_UserId",
         "PeerId": "Your_PeerId",
         "Direction": "up",
         "CallDetail": [
           {"Desc":"Audio sending bit rate",
            "Name": "bandwidth",
            "MediaType": "audio",
            "Data":[
               {"Time": 1652702700000,
                 "Value": 1},
               {"Time": 16527027002000,
                 "Value": 2}]
           },
           {"Desc":"Audio upstream packet loss rate",
            "Name": "fraction_lost",
            "MediaType": "audio",
            "Data":[
               {"Time": 1652702700000,
                 "Value": 1},
               {"Time": 16527027002000,
                 "Value": 2}]
           }
         ]
       }
     ]
   }
}
```
