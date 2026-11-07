---
title: "DescribeVodRealtimeMediaData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/DescribeVodRealtimeMediaData"
---

This interface is used to query the number of accesses for real\-time snapshots and real\-time audio\-video information retrieval within a specified time range under the specified spatial dimensions.

<span id="requirements"></span>
## Requirements


* **Prerequisites**: The [real-time processing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-real-time-video-processing) feature has been configured in the specified spatial dimension.

* **Billing**: For real\-time processing rates, please refer to [pay-as-you-go pricing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing).

* **Data latency**: 2 hours.

* **Time Range**: The time span for queries should not exceed **93 days**.


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodRealtimeMediaData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodRealtimeMediaData` |The API action. For the current API, the value is `DescribeVodRealtimeMediaData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceList |String |No |`test` |The list of VOD space names. Multiple space names are separated by a comma `,`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, the parameter type is Array of String.</div><br> |
|StartTime |String |Yes |`2024-05-08T00:00:00+08:00` |The start time of the query. It follows the RFC3339 format for UTC time, with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ss.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The start time should be no earlier than 366 days from the current time.</div><br> |
|EndTime |String |Yes |`2024-05-09T00:00:00+08:00` |The end time of the query. It follows the RFC3339 format for UTC time, with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ss.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The query time span does not exceed 93 days.</div><br> |
|ProcessType |String |No |`Snapshot` |Real\-time processing types. The default is all processing types. Supported values:<br><br><br>* `Snapshot`: Real\-time snapshot<br><br>* `Metadata`: Real\-time acquisition of audio and video information |
|Aggregation |Long |No |`3600` |The aggregation time granularity, measured in seconds. The values are as follows:<br><br><br>* `3600`: (default) 1 hour<br><br>* `86400`: 1 day |
|DetailFieldList |String |No |`Space` |List of dimensions that display detailed information. The currently supported values are `Space`, with multiple values separated by a comma `,`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, the parameter type is Array of String.</div><br> |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceList |Array of String |`["test"]` |The VOD space list. |
|StartTime |String |`2024-05-08T00:00:00+08:00` |The start time of the query. It follows the RFC3339 format for the UTC time, with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ss. |
|EndTime |String |`2024-05-09T00:00:00+08:00` |The query end time. It follows the RFC3339 format for UTC time, with a precision to the second, formatted as: yyyy\-MM\-ddTHH:mm:ss. |
|ProcessType |String |`Snapshot` |Real\-time processing types. Supported values:<br><br><br>* `Snapshot`: Real\-time snapshots.<br><br>* `Metadata`: Real\-time acquisition of audio and video information. |
|Aggregation |Long |`86400` |The aggregation time granularity, in seconds. Supported values:<br><br><br>* `3600`: 1 hour<br><br>* `86400`: 1 day |
|DetailFieldList |Array of String |`["Space"]` |The list of dimensions that display detailed information. The currently supported value is `Space`. |
|TotalRealtimeMediaData |Long |`220` |The real\-time processing of the total number of media asset accesses. |
|RealtimeMediaDataList |Array of [RealtimeMediaDataList](https://docs.byteplus.com/en/docs/25/36183#realtimemediadatalist) |`-` |The real\-time processing of media asset information access count list. |
|RealtimeMediaDetailDataList |Array of [RealtimeMediaDetailDataList](https://docs.byteplus.com/en/docs/25/36183#realtimemediadetaildatalist) |`-` |The real\-time processing of media asset information access count detailed list. |


#{.custom\-md\-table\-4}#

<span id="realtimemediadatalist"></span>
### RealtimeMediaDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`2024-05-07T16:00:00Z` |The end time, following the RFC3339 format for UTC time with second precision, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|Count |Long |`220` |The number of visits, measured in occurrences. |


#{.custom\-md\-table\-4}#

<span id="realtimemediadetaildatalist"></span>
### RealtimeMediaDetailDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Space |String |`test` |The VOD space name. |
|Total |Long |`220` |The total number of data entries. |
|RealtimeMediaDataList |Array of [RealtimeMediaDataList](https://docs.byteplus.com/en/docs/25/36183#realtimemediadatalist) |`-` |The real\-time processing of media asset information access count list. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DescribeVodRealtimeMediaData&Version=2023-01-01&SpaceList=test&StartTime=2024-05-08T00:00:00+08:00&EndTime=2024-05-09T00:00:00+08:00&ProcessType=Snapshot&Aggregation=3600&DetailFieldList=Space
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeVodRealtimeMediaData",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "EndTime": "2024-05-09T00:00:00+08:00",
        "SpaceList": [
            "test"
        ],
        "StartTime": "2024-05-08T00:00:00+08:00",
        "Aggregation": 86400,
        "ProcessType": "Snapshot",
        "DetailFieldList": [
            "Space"
        ],
        "RealtimeMediaDataList": [
            {
                "Time": "2024-05-07T16:00:00Z",
                "Count": 220
            }
        ],
        "TotalRealtimeMediaData": 220,
        "RealtimeMediaDetailDataList": [
            {
                "Space": "test",
                "Total": 220,
                "RealtimeMediaDataList": [
                    {
                        "Time": "2024-05-07T16:00:00Z",
                        "Count": 220
                    }
                ]
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
