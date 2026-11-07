---
title: "DescribeVodMostPlayedStatisData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodmostplayedstatisdata"
---

This interface is used to query the video information of the TopN played within a certain time range in the specified space.

<span id="requirements"></span>
## Requirements


* Rate limit: The request rate limit for a single user is **10 requests per second**.

* In HLS protocol videos, when the M3U8 file and TS segments are in the same directory, the BytePlus VOD playback statistics will synchronously count the traffic of the TS segments.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When multiple M3U8 files and their corresponding TS segments are in the same directory (such as the root directory), there may be inaccuracies in the statistics.   </div>
   

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodMostPlayedStatisData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodMostPlayedStatisData` |The API action. For the current API, the value is `DescribeVodMostPlayedStatisData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Space |String |No |`test` |The VOD space name. You can obtain the space name in the following ways:<br><br><br>* View the names of all spaces under the current account on the BytePlus VOD console [Spaces](https://console.byteplus.com/vodpaas/overview/?).<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to get the names of all spaces under the current account. |
|StartTime |String |No |`2023-12-23T16:00:00Z` |The start time. The date format must comply with the RFC3339 standard. |
|EndTime |String |No |`2023-12-24T15:59:59Z` |The end time. The date format must comply with the RFC3339 specification.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Query data within 31 days at the earliest.</div><br> |
|OrderType |String |No |`traffic` |Sort type. The values are as follows:<br><br><br>* `count`: (default) Sort by count.<br><br>* `traffic`: Sort by traffic in descending order. |
|TopN |Long |No |`100` |Return the number of videos. The default value is 100. The maximum is 100. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Space |String |`test` |The VOD space name. |
|StartTime |String |`2023-12-23T16:00:00Z` |The start time, in RFC3339 format. |
|EndTime |String |`2023-12-24T15:59:59Z` |The end time, in RFC3339 format. |
|OrderType |String |`traffic` |Sort type. The values are as follows:<br><br><br>* `count`: Sort by frequency.<br><br>* `traffic`: Sort by traffic in descending order. |
|TopN |Integer |`100` |The number of videos returned. |
|PlayStatInfos |Array of [PlayStatInfos](https://docs.byteplus.com/en/docs/25/8064#playstatinfos) |`-` |The playback information. |


#{.custom\-md\-table\-4}#

<span id="playstatinfos"></span>
### PlayStatInfos


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vid |String |`v02c24g10001***k792ucabrgag` |The video ID. |
|Name |String |`The watermark.dash.mp4` |The video name. |
|Size |Integer |`11135289` |The video size, in bytes. |
|Duration |Float |`107.867` |The video length, in seconds. |
|CreateTime |String |`2022-10-31 16:33:22` |The video creation time. |
|PlayCount |Integer |`2` |The number of plays. |
|Traffic |Integer |`1133` |The traffic, in bytes. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DescribeVodMostPlayedStatisData&Version=2023-01-01&Space=test&StartTime=2023-12-23T16:00:00Z&EndTime=2023-12-24T15:59:59Z&OrderType=traffic&TopN=100
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202312251433***64896865F42EFE9",
        "Action": "DescribeVodMostPlayedStatisData",
        "Version": "2023-01-01",
        "Service": "vod"
    },
    "Result": {
        "Space": "test",
        "StartTime": "2023-12-23T16:00:00Z",
        "EndTime": "2023-12-24T15:59:59Z",
        "OrderType": "traffic",
        "PlayStatInfos": [
            {
                "Vid": "v02c24g10001cald1cbh1vq4cc06mb40",
                "Name": "od(Original_Resolution_Transmuxing),240,360,480,540,720,1080video_stream",
                "Duration": 120.2,
                "Size": 32202259,
                "PlayCount": 736,
                "CreateTime": "2022-06-16 14:42:12",
                "Traffic": 212638450
            },
            {
                "Vid": "v02c24g1000***q4cc06mu9g",
                "Name": "encryption, non-encryptionod,240,360,480,540,720,1080video_stream",
                "Duration": 120.2,
                "Size": 32202259,
                "PlayCount": 288,
                "CreateTime": "2022-06-16 19:54:15",
                "Traffic": 82958589
            },
            {
                "Vid": "v02c24g1000***kiv7mrolf0",
                "Name": "heihei",
                "Duration": 120.2,
                "Size": 32202259,
                "PlayCount": 2,
                "CreateTime": "2022-08-08 17:29:42",
                "Traffic": 32203993.999999996
            },
            {
                "Vid": "v02c24g10001***co9qbmp4en9g",
                "Name": "Origin",
                "Duration": 120.2,
                "Size": 32202259,
                "PlayCount": 32,
                "CreateTime": "2022-06-16 20:06:16",
                "Traffic": 22175704
            },
            {
                "Vid": "v02c24g10001***k792ucabrgag",
                "Name": "watermark.dash.mp4",
                "Duration": 107.867,
                "Size": 11135289,
                "PlayCount": 2,
                "CreateTime": "2022-10-31 16:33:22",
                "Traffic": 1133
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
