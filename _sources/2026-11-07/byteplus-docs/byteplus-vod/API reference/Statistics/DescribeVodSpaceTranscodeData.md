---
title: "DescribeVodSpaceTranscodeData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodspacetranscodedata"
---

This interface is used to query the usage of the transcoding function within a specified time range under the specified spatial dimensions.

<span id="requirements"></span>
## Requirements


* Billing: For transcoding billing rates, please refer to [Pay-As-You-Go pricing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing).

* Data latency: **2 hours**.

* Time Range: The time span for queries should not exceed **93 days**.

* Permission Explanation: When using a sub\-account to request an interface, the interface will perform permission verification based on the sub\-account and only return the data that the sub\-account has permission to access. For more details, see [Creating a sub-account](https://docs.byteplus.com/en/docs/byteplus-vod/docs-creating-iam-users).


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodSpaceTranscodeData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodSpaceTranscodeData` |The API action. For the current API, the value is `DescribeVodSpaceTranscodeData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceList |String |No |`test` |List of VOD space names. Separate multiple space names with a comma `,`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, the parameter type is Array of String.</div><br> |
|StartTime |String |Yes |`2022-04-18T20:00:00Z` |The start time of the query. The date format must comply with the RFC3339 specification. |
|EndTime |String |Yes |`2022-04-18T22:00:00Z` |The query end time. The date format must comply with the RFC3339 standard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The time span for a single query can not exceed 93 days.</div><br> |
|TranscodeType |String |No |`Normal` |The transcoding type. The default is to select all. The values are as follows:<br><br><br>* `Slice`: Speed\-up transcoding.<br><br>* `Normal`: Standard transcoding.<br><br>* `LowCost`: Low\-cost transcoding.<br><br>* `ByteHD`: Low\-bitrate\-HD. |
|Specification |String |No |`Audio` |The container format. The values are as follows:<br><br><br>* `Audio`: The audio format.<br><br>* `ConvertFormat`: Remuxing Original Footage.<br><br>* `H.264_240p`<br><br>* `H.264_360p`<br><br>* `H.264_480p`<br><br>* `H.264_540p`<br><br>* `H.264_720p`<br><br>* `H.264_2k`<br><br>* `H.264_4k`<br><br>* `H.265_240p`<br><br>* `H.265_360p`<br><br>* `H.265_480p`<br><br>* `H.265_540p`<br><br>* `H.265_720p`<br><br>* `H.265_2k`<br><br>* `H.265_4k`<br><br>* `H.266_240p`<br><br>* `H.266_360p`<br><br>* `H.266_480p`<br><br>* `H.266_540p`<br><br>* `H.266_720p`<br><br>* `H.266_2k`<br><br>* `H.266_4k` |
|TaskStageList |String |No |`busy` |The task type. Separate multiple task types with a comma `,`. The values are as follows:<br><br><br>* `busy`: Normal task.<br><br>* `free`: Idle task.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, this parameter type is Array of String.</div><br> |
|Aggregation |Long |No |`3600` |The aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `3600`: (Default) 1 hour<br><br>* `86400`: 1 day |
|DetailFieldList |String |No |`TaskStage` |Detailed field list, whether to return more detailed data based on query conditions. Separate multiple fields with a comma, ','. The values are as follows:<br><br><br>* `TaskStage`: The task type.<br><br>* `Space`: The name of the VOD space.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, the parameter type is Array of String.</div><br> |
|TimeZone |String |No |`Etc/GMT+12` |The time zone ID, see [Time zones](https://docs.byteplus.com/en/docs/byteplus-vod/reference-time-zones). |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceList |Array of String |`["test"]` |The list of VOD space names. |
|StartTime |String |`2022-04-18T20:00:00Z` |The query start time. It follows the RFC3339 format in UTC time with a precision to the second, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |`2022-04-18T22:00:00Z` |The query end time. It follows the RFC3339 format in UTC time, with a precision to the second, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|TranscodeType |String |`Normal` |The transcoding types. The values are as follows:<br><br><br>* `Slice`: Speed\-up transcoding.<br><br>* `Normal`: Standard transcoding.<br><br>* `LowCost`: Low\-cost transcoding.<br><br>* `ByteHD`: Low\-bitrate transcoding. |
|Specification |String |`Audio` |The packaging format. The values are as follows:<br><br><br>* `Audio`: The audio format.<br><br>* `ConvertFormat`: Original Resolution Transmuxing.<br><br>* `H.264_240p`<br><br>* `H.264_360p`<br><br>* `H.264_480p`<br><br>* `H.264_540p`<br><br>* `H.264_720p`<br><br>* `H.264_2k`<br><br>* `H.264_4k`<br><br>* `H.265_240p`<br><br>* `H.265_360p`<br><br>* `H.265_480p`<br><br>* `H.265_540p`<br><br>* `H.265_720p`<br><br>* `H.265_2k`<br><br>* `H.265_4k`<br><br>* `H.266_240p`<br><br>* `H.266_360p`<br><br>* `H.266_480p`<br><br>* `H.266_540p`<br><br>* `H.266_720p`<br><br>* `H.266_2k`<br><br>* `H.266_4k` |
|TaskStageList |Array of String |`busy` |The task type. The values are as follows:<br><br><br>* `busy`: Normal task.<br><br>* `free`: Idle task. |
|Aggregation |Long |`3600` |The aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `3600`: 1 hour<br><br>* `86400`: 1 day |
|DetailFieldList |Array of String |`["TaskStage"]` |Display dimensions for detailed information are as follows:<br><br><br>* `TaskStage`: The task type.<br><br>* `Space`: The VOD space name. |
|TotalTranscodeData |Long |`100` |The total transcoding duration for the selected time period. The unit is milliseconds. |
|TotalTranscodeDataList |Array of [TotalTranscodeDataList](https://docs.byteplus.com/en/docs/25/8056#totaltranscodedatalist) |`-` |The transcoding duration for various encapsulation formats. |
|TranscodeDataDetailList |Array of [TranscodeDataDetailList](https://docs.byteplus.com/en/docs/25/8056#transcodedatadetaillist) |`-` |The transcoding duration for various task types. |


#{.custom\-md\-table\-4}#

<span id="totaltranscodedatalist"></span>
### TotalTranscodeDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`Audio` |The encapsulation format. The values are as follows:<br><br><br>* `Audio`: The audio format.<br><br>* `ConvertFormat`: Original Resolution Transmuxing.<br><br>* `H.264_240p`<br><br>* `H.264_360p`<br><br>* `H.264_480p`<br><br>* `H.264_540p`<br><br>* `H.264_720p`<br><br>* `H.264_2k`<br><br>* `H.264_4k`<br><br>* `H.265_240p`<br><br>* `H.265_360p`<br><br>* `H.265_480p`<br><br>* `H.265_540p`<br><br>* `H.265_720p`<br><br>* `H.265_2k`<br><br>* `H.265_4k`<br><br>* `H.266_240p`<br><br>* `H.266_360p`<br><br>* `H.266_480p`<br><br>* `H.266_540p`<br><br>* `H.266_720p`<br><br>* `H.266_2k`<br><br>* `H.266_4k` |
|Value |Long |`100` |The transcoding duration, in milliseconds. |


#{.custom\-md\-table\-4}#

<span id="transcodedatadetaillist"></span>
### TranscodeDataDetailList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Space |String |`test` |The VOD space name. |
|Total |Long |`11` |The transcoding duration. The unit is milliseconds. |
|TaskStage |String |`free` |The task type. The values are as follows:<br><br><br>* `busy`: Normal task.<br><br>* `free`: Idle task. |
|TranscodeUsageList |Array of [TranscodeUsageList](https://docs.byteplus.com/en/docs/25/8056#transcodeusagelist) |`-` |The detailed data on transcoding usage. |


#{.custom\-md\-table\-4}#

<span id="transcodeusagelist"></span>
### TranscodeUsageList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`2022-04-18T20:00:00Z` |The start time of the data time range. It follows the RFC3339 format for UTC time with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|TranscodeItemList |Array of [TranscodeItemList](https://docs.byteplus.com/en/docs/25/8056#transcodeitemlist) |`-` |The transcoding project list. |


#{.custom\-md\-table\-4}#

<span id="transcodeitemlist"></span>
### TranscodeItemList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`Audio` |The encapsulation format. The values are as follows:<br><br><br>* `Audio`: The audio format.<br><br>* `ConvertFormat`: Original Resolution Transmuxing.<br><br>* `H.264_240p`<br><br>* `H.264_360p`<br><br>* `H.264_480p`<br><br>* `H.264_540p`<br><br>* `H.264_720p`<br><br>* `H.264_2k`<br><br>* `H.264_4k`<br><br>* `H.265_240p`<br><br>* `H.265_360p`<br><br>* `H.265_480p`<br><br>* `H.265_540p`<br><br>* `H.265_720p`<br><br>* `H.265_2k`<br><br>* `H.265_4k`<br><br>* `H.266_240p`<br><br>* `H.266_360p`<br><br>* `H.266_480p`<br><br>* `H.266_540p`<br><br>* `H.266_720p`<br><br>* `H.266_2k`<br><br>* `H.266_4k` |
|Value |Long |`100` |The transcoding duration, in milliseconds. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DescribeVodSpaceTranscodeData&Version=2023-01-01&SpaceList=test&StartTime=2022-04-18T20:00:00Z&EndTime=2022-04-18T22:00:00Z&TranscodeType=Normal&Specification=Audio&TaskStageList=busy&Aggregation=3600&DetailFieldList=TaskStage
```


<span id="sample-response"></span>
### Sample response

```json
HTTP/1.1 200 OK
Content-Length: 190
Content-Type: application/json

{
    "ResponseMetadata": {
        "RequestId": "20221123122***0380DAD1333",
        "Action": "DescribeVodSpaceTranscodeData",
        "Version": "2023-01-01",
        "Service": "vod"
    },
    "Result": {
        "SpaceList": ["test"],
        "StartTime":   "2022-04-18T20:00:00Z",
        "EndTime":     "2022-04-18T22:00:00Z",
        "Aggredation": 3600,
        "Specification": "Audio",
        "TranscodeType": "Normal",
        "TaskStageList": ["busy", "free"],
        "DetailFieldList": ["TaskStage"],
        "TotalTranscodeData": 100,
        "TotalTranscodeDataList": [
             {
          "Name": "Audio",
          "Value": 100
             }
        ],
        "TranscodeDataDetailList":[
            {
                "TaskStage": "busy",
                "Total": 11,
                "TranscodeUsageList": [
                {
                    "Time": "2022-04-18T20:00:00Z",
                    "TranscodeItemList": [
                       {
                          "Name": "Audio",
                          "Value": 100
                       }
                    ]
                }
              ]
           },
          {
            "TaskStage": "free",
            "Total": 11,
            "TranscodeUsageList": [
                {
                    "Time": "2022-04-18T20:00:00Z",
                    "TranscodeItemList": [
                       {
                          "Name": "Audio",
                          "Value": 100
                       }
                    ]
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
