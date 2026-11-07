---
title: "DescribeVodPlayedStatisData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodplayedstatisdata"
---

This interface is used to query the playback information of videos within a specified space and time range.

<span id="requirements"></span>
## Requirements


* Data latency: About 8 hours.

* Known limitation: This interface currently does not support retrieving playback information for the day a domain name is added. For example, if you add a domain name on December 3, 2024, you will only be able to access playback information from December 4 onwards.

* In HLS protocol videos, when the M3U8 file and TS segments are in the same directory, BytePlus VOD's playback statistics will synchronize the traffic statistics of the TS segments.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When multiple M3U8 files and their corresponding TS segments are in the same directory (such as the root directory), there may be inaccuracies in the statistics.</div>


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodPlayedStatisData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodPlayedStatisData` |The API action. For the current API, the value is `DescribeVodPlayedStatisData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Space |String |No |`test` |The name of the VOD space. You can obtain the name of the space in the following ways:<br><br><br>* View the names of all spaces under the current account on the BytePlus VOD console [Spaces](https://console.byteplus.com/vodpaas/overview/?).<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|StartTime |String |No |`2023-12-23T16:00:00Z` |The start time, in RFC3339 format. |
|EndTime |String |No |`2023-12-24T15:59:59Z` |End time, RFC3339 format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Query data from at least the past 31 days.</div><br> |
|VidList |String |No |`["v03c24g100***v0vp0ml6d3g", "v02c24g1000***v0ss463b0vg",v02c24g1***tkhs1v0tk8qog730]` |The list of queried Vids, maximum of 100.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a GET request, connect with English commas <code>,</code>.</div><br> |
|OrderType |String |No |`count_up` |The sorting type. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Space |String |`test` |The space. |
|EndTime |String |`2023-12-24T15:59:59Z` |The end time of the query, RFC3339; the query time span does not exceed 93 days. |
|VidList |Array of String |`["v03c24g10001c\*\*\*v0vp0ml6d3","v02c24g10001\*\*\*9s1v0ss463b","v02c24g10001\*\*\*v0tk8qog730"]` |The list of queried Vids, with multiple Vids separated by commas. |
|OrderType |String |`count_up` |The sorting type. |
|StartTime |String |`2023-12-23T16:00:00Z` |The query start time, RFC3339. |
|PlayStatInfos |Array of [BusinessDescribeVodPlayedStatisDataItem](https://docs.byteplus.com/en/docs/25/8063#businessdescribevodplayedstatisdataitem) | | |


#{.custom\-md\-table\-4}#

<span id="businessdescribevodplayedstatisdataitem"></span>
### BusinessDescribeVodPlayedStatisDataItem


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vid |String |`v02c24g10001***v0tk8qog730` |Video ID. |
|Name |String |`title` |Video name. |
|Size |Long |`121809370` |Video size, in bytes. |
|Traffic |Long |`0` |Traffic, in bytes. |
|Duration |Double |`158.583` |Video length, in seconds. |
|PlayCount |Long |`0` |Play counts. |
|CreateTime |String |`0` |Video creation time. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DescribeVodPlayedStatisData&Version=2023-01-01&Space=test&StartTime=2023-12-23T16:00:00Z&EndTime=2023-12-24T15:59:59Z&VidList=["v03c24g100***v0vp0ml6d3g", "v02c24g1000***v0ss463b0vg",v02c24g1***tkhs1v0tk8qog730]&OrderType=count_up
```


<span id="sample-response"></span>
### Sample response

```json
HTTP/1.1 200 OK
Content-Length: 190
Content-Type: application/json

{
  "ResponseMetadata":{
    "RequestId": "201806041******0232280022D30",
    "Action": "DescribeVodPlayedStatisData",
    "Version": "2023-01-01",
    "Service": "vod"
  },
  "Result":{
    "Space": "test",
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "VidList": ["1232131", "1324324"]
    "PlayStatInfos": [
      {
        "Vid": "1232131",
        "Name": "test",
        "Duration": 12,
        "Size": 100,
        "PlayCount": 5,
        "CreateTime": "2022-04-11T00:00:00Z",
        "Traffic": 20
      },
      {
        "Vid": "1324324",
        "Name": "test",
        "Duration": 12,
        "Size": 100,
        "PlayCount": 5,
        "CreateTime": "2022-04-11T00:00:00Z",
        "Traffic": 20
      }
    ],
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
