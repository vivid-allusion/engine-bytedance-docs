---
title: "ListQuality"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-124667"
---

You can use this interface to query the offline quality of audio and video calls of an application within a certain period of time.

To query offline quality data accross dimensions such as geographical distribution, device platform, and network type, it is recommended to call the [ListQualityDistribution](https://docs.byteplus.com/en/docs/12/docs-163728) interface.

<span id="usage-scenario"></span>
## Usage scenario

Specify the `AppId`, the indicator type and the query time period to query the indicator data within the time period.

<span id="requirements"></span>
## Requirements


|Category |Frequency capping |
|---|---|
|Maximum number of queries |10 times/minute<br><br>60 times/day |
|The farthest queryable time |30 days |
|Maximum time span of single query |7 days |
|Data Granularity |1 day or 5 minutes |
|Data Delay |8 Hours |


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=ListQuality&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListQuality` |Interface name. The value of this interface: `ListQuality` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|StartTime |String |Yes |`2021-07-24T00:00:00+08:00` |Start timestamp for querying in the format of RFC3339 in second |
|EndTime |String |Yes |`2021-07-25T00:00:00+08:00` |End timestamp for querying in the format of RFC3339 in second |
|Indicator |Array of String |Yes |`["stall_rate","join_room_success_rate"]` |The name of the indicator to be queried. Multiple indicators can be queried at the same time. For optional value, see [Indicator](https://docs.byteplus.com/en/docs/12/docs-1167931#listquality). |
|AggregateGranularity |String |Yes |`1d` |The aggregation of returning the granularity of time. The values can take `1d` and `5min`. |
|ProductType |String |No |`native` |The product type to be queried. The values can take `native` and `web`.<br><br><br>* `native`: The default value. The BytePlusRTC SDK of `android`, `iOS`, `linux`, `mac` or `windows`.<br><br>* `web`: the BytePlusRTC SDK of `Web`. |
|OS |Array of String |No |`iOS` |The value can take: `android`, `iOS`, `linux`, `mac`or`windows`<br><br>&nbsp;<br><br>This parameter is not valid when `ProductType` = `web` |
|Access |Array of String |No |`2g` |Network type. The value can takes: `2g`, `3g`, `4g`, `5g` or `wifi`<br><br>&nbsp;<br><br>This parameter is not valid when `ProductType` = `web` |
|RoomId |String |No |`Your_RoomId` |Room ID. If not filled, it means to query the overall offline indicators under the `AppId`. |
|UserId |Array of String |No |`["user1","user2"]` |The list of user IDs to query, up to 20. If the value is invalid, it will be rejected by default. This parameter is valid when `RoomId` is not empty. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AggregateGranularity |String |`1d` |The granularity of returned data |
|Indicators |Array of [Indicator](https://docs.byteplus.com/en/docs/12/14237#indicator) |`AudioStallDuration` |Specific data of indicator |


<span id="indicator"></span>
### Indicator


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`5s_join_room_success_rate` |Name of the indicator |
|Unit |String |`%` |Unit of the indicator |
|Data |Array of [Data](https://docs.byteplus.com/en/docs/12/14237#data) |`-` |Specific value of the indicator and corresponding time |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2021-07-24T00:00:00+08:00` |The time of Indicator to be aggregated, that is, the starting time of period corresponding to the indicator value. The granularity at which aggregation times are returned can be selected by setting `AggregateGranularity`. The format is RFC3339 specification. |
|Value |Double |`99.99` |Indicator value, floating point number, with two decimal places. |
|StreamId |String |`stream1` |The public stream ID to be queried; separate multiple StreamIds with commas.<br><br>If left blank, it queries all public streams under AppId. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=ListQuality&Version=2020-12-01
{
    "AppId": "You****pId",
    "StartTime": "2021-07-24T00:00:00+08:00",
    "EndTime": "2021-07-28T00:00:00+08:00",
    "Indicator": [
        "stall_rate",
        "join_room_success_rate"
    ],
    "ProductType": "native",
    "Aggregate Granularity": "1d",
    "OS": [
        "ios",
        "linux"
    ],
    "Access": [
        "2g",
        "3g"
    ],
    "RoomId": "Your_RoomId",
    "UserId": "Your_UserId"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "ListQuality",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Aggregate Granularity": "1d",
        "Indicators": [
            {
                "Name": "5s_join_room_success_rate",
                "Unit": "%",
                "Data": [
                    {
                        "TimeStamp": "2021-07-24T00:00:00+08:00",
                        "Value": 98.68
                    },
                    {
                        "TimeStamp": "2021-07-25T00:00:00+08:00",
                        "Value": 98.2
                    }
                ]
            },
            {
                "Name": "10s_join_room_success_rate",
                "Unit": "%",
                "Data": [
                    {
                        "TimeStamp": "2021-07-24T00:00:00+08:00",
                        "Value": 99.68
                    },
                    {
                        "TimeStamp": "2021-07-25T00:00:00+08:00",
                        "Value": 99.2
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
