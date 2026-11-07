---
title: "DescribeVodSpaceSubtitleStatisData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodspacesubtitlestatisdata"
---

This interface is used to query the usage of the smart subtitling feature within a specified spatial dimension over a certain time period.

<span id="requirements"></span>
## Requirements


* Billing: For the pricing of the intelligent subtitle billing, please refer to [[Pay-As-You-Go pricing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing).

* Data Delay: **2 hours**.

* Time Range: The time span for queries should not exceed **93 days**.

* Permission Explanation: When using a sub\-account to request the interface, the interface will perform permission verification according to the sub\-account and only return the data that the sub\-account has permission to access. For more details, see [Creating a sub-account](https://docs.byteplus.com/en/docs/byteplus-vod/docs-creating-iam-users).


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodSpaceSubtitleStatisData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodSpaceSubtitleStatisData` |The API action. For the current API, the value is `DescribeVodSpaceSubtitleStatisData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceList |String |No |`test` |The list of on\-demand space names. Multiple space names are separated by commas `,`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, this parameter type is Array of String.</div><br> |
|StartTime |String |Yes |`2022-04-18T20:00:00Z` |The query start time. It follows the RFC3339 format for UTC time with second precision, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |Yes |`2022-04-18T22:00:00Z` |The end time of the query. It follows the RFC3339 format in UTC time, with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The time span of a single query can not exceed 93 days.</div><br> |
|SubtitleType |String |No |`MT` |Subtitle Type. Default is select all. The values are as follows:<br><br><br>* `ASR`: Voice Transcription<br><br>* `MT`: Machine Translation<br><br>* `ES`: Extracted subtitles |
|TaskStageList |String |No |`busy,free` |The task type. Separate multiple task types with a comma `,`. The values are as follows:<br><br><br>* `busy`: Normal task<br><br>* `free`: Idle task<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, the parameter type is Array of String.</div><br> |
|Aggregation |Long |No |`3600` |The aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `3600`: (default) 1 hour.<br><br>* `86400`: 1 day. |
|DetailFieldList |String |No |`TaskStage` |Detailed field list. The values are as follows:<br><br><br>* `TaskStage`: The task type.<br><br>* `Space`: The VOD space name.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the parameter is not empty, more detailed usage data will be returned.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If it is a POST request, the parameter type is Array of String.</div><br> |
|TimeZone |String |No |`Etc/GMT+12` |The time zone ID, see [Time zones](https://docs.byteplus.com/en/docs/byteplus-vod/reference-time-zones). |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceList |Array of String |`["test"]` |The list of VOD space names. |
|StartTime |String |`2022-04-18T20:00:00Z` |The query start time. It follows the RFC3339 format for UTC time, with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |`2022-04-18T22:00:00Z` |The query's end time. It follows the RFC3339 format for UTC time, with a precision to the second, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|SubtitleType |String |`MT` |The subtitle type. The values are as follows:<br><br><br>* `ASR`: Speech transcription<br><br>* `MT`: Machine translation<br><br>* `ES`: Extracted subtitles |
|TaskStageList |Array of String |`["busy","free"]` |The task type. The values are as follows:<br><br><br>* `busy`: Normal task;<br><br>* `free`: Idle task. |
|Aggregation |Long |`3600` |The aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `3600`: 1 hour<br><br>* `86400`: 1 day |
|DetailFieldList |Array of String |`["TaskStage"]` |Detailed field list. The values are as follows:<br><br><br>* `TaskStage`: The task type<br><br>* `Space`: The VOD space name |
|TotalSubtitleUsageData |Long |`100` |The total subtitle usage for the selected time period. |
|SubtitleUsageDataList |Array of [SubtitleUsageDataList](https://docs.byteplus.com/en/docs/25/8057#subtitleusagedatalist) |`-` |The specific data for subtitle usage. |
|SubtitleUsageDataDetailList |Array of [SubtitleUsageDataDetailList](https://docs.byteplus.com/en/docs/25/8057#subtitleusagedatadetaillist) |`-` |The subtitle usage for various types of tasks. |


#{.custom\-md\-table\-4}#

<span id="subtitleusagedatalist"></span>
### SubtitleUsageDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`2022-04-18T20:00:00Z` |The start time of the data time range. It follows the RFC3339 format for UTC time with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|Usage |Long |`100` |Usage, measured in milliseconds or characters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the <code>SubtitleType</code> is set to <code>ASR</code> or <code>ES</code>, the unit for <code>Usage</code> is milliseconds.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the <code>SubtitleType</code> is set to <code>MT</code>, the unit for <code>Usage</code> is characters.</div><br> |


#{.custom\-md\-table\-4}#

<span id="subtitleusagedatadetaillist"></span>
### SubtitleUsageDataDetailList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Space |String |`test` |The VOD space name. |
|TaskStage |String |`busy` |The task type. The values are as follows:<br><br><br>* `busy`: Normal task<br><br>* `free`: Idle task |
|SubtitleUsageDataList |Array of [SubtitleUsageDataList](https://docs.byteplus.com/en/docs/25/8057#subtitleusagedatalist) |`-` |The specific data for subtitle usage. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DescribeVodSpaceSubtitleStatisData&Version=2023-01-01&SpaceList=test&StartTime=2022-04-18T20:00:00Z&EndTime=2022-04-18T22:00:00Z&SubtitleType=MT&TaskStageList=busy,free&Aggregation=3600&DetailFieldList=TaskStage&RegionList=
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20221123122***0380DAD1333",
        "Action": "DescribeVodSpaceSubtitleStatisData",
        "Version": "2023-01-01",
        "Service": "vod"
    },
    "Result": {
        "SpaceList": [
            "test"
        ],
        "StartTime": "2022-04-18T20:00:00Z",
        "EndTime": "2022-04-18T22:00:00Z",
        "TaskStageList": [
            "busy",
            "free"
        ],
        "SubtitleType": "MT",
        "DetailFieldList": [
            "TaskStage"
        ],
        "Aggregation": 3600,
        "TotalSubtitleUsageData": 100,
        "SubtitleUsageDataList": [
            {
                "Time": "2022-04-18T20:00:00Z",
                "Usage": 100
            }
        ],
        "SubtitleUsageDetailDataList": [
            {
                "TaskStage": "busy",
                "SubtitleUsageDataList": [
                    {
                        "Time": "2022-04-18T20:00:00Z",
                        "Usage": 100
                    }
                ]
            },
            {
                "TaskStage": "free",
                "SubtitleUsageDataList": [
                    {
                        "Time": "2022-04-18T20:00:00Z",
                        "Usage": 100
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
