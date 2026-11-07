---
title: "DescribeVodEnhanceImageData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodenhanceimagedata"
---

This interface is used to query the usage of the video enhancement function within a certain time range under specified spatial dimensions.

<span id="requirements"></span>
## Requirements


* Billing: For the billing price of video enhancement, please refer to [Pay-As-You-Go pricing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing).

* Data latency: **4 hours**.

* Time Range: The time span for queries should not exceed **93 days**.

* Permission Explanation: When using a sub\-account to request an interface, the interface will perform permission verification according to the sub\-account and only return the data that the sub\-account is authorized to access. For more details, see [Creating a sub-account](https://docs.byteplus.com/en/docs/byteplus-vod/docs-creating-iam-users).


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodEnhanceImageData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodEnhanceImageData` |The API action. For the current API, the value is `DescribeVodEnhanceImageData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceList |String |No |`test` |The list of VOD space names. Multiple space names are separated by a comma `,`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, this parameter type is Array of String.</div><br> |
|StartTime |String |No |`2022-04-12T16:00:00Z` |The start time of the query. It follows the RFC3339 format in UTC time, with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |No |`2022-04-13T16:00:00Z` |The start time of the query. Follows the RFC3339 format for UTC time with second precision, formatted as: yyyy\-MM\-ddTHH:mm:ssZ.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The time span of a single query must not exceed 93 days.</div><br> |
|TaskStageList |String |No |`busy` |The task type. Separate multiple task types with a comma `,`. The values are as follows:<br><br><br>* `free`: Idle task<br><br>* `busy`: Normal task<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, this parameter type is Array of String.</div><br> |
|Aggregation |Long |No |`3600` |The aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `86400`: (default) 1 day<br><br>* `3600`: 1 hour |
|TaskTypeList |String |No |`SR` |The type of the task. Multiple task types can be specified, separated by a comma `,`. Default is all types. Supported values are as follows:<br><br><br>* `SR`: Smart resolution;<br><br>* `VFI`: Video frame interpolation;<br><br>* `SDREnhance`: SDR enhancement;<br><br>* `SDR2HDR`: SDR to HDR conversion;<br><br>* `AudioDenoise`: Noise reduction. |
|TimeZone |String |No |`Etc/GMT+12` |The time zone ID, see [Time zones](https://docs.byteplus.com/en/docs/byteplus-vod/reference-time-zones). |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceList |Array of String |`["test"]` |The list of VOD spaces. |
|StartTime |String |`2021-04-13T00:00:00+08:00` |The start time of the query. It follows the RFC3339 format for UTC time, with a precision to the second, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |`2021-04-14T00:00:00+08:00` |The query end time. It follows the RFC3339 format for UTC time with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|TaskStageList |Array of String |`["busy","free"]` |The task type list. The values are as follows:<br><br><br>* `free`: Idle task<br><br>* `busy`: Normal task |
|Aggregation |Long |`3600` |The aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `3600`: 1 hour<br><br>* `86400`: 1 day |
|TaskTypeList |Array of String |`SR` |The type of the task.<br><br><br>* `SR`: Smart resolution;<br><br>* `VFI`: Video frame interpolation;<br><br>* `SDREnhance`: SDR enhancement;<br><br>* `SDR2HDR`: SDR to HDR conversion;<br><br>* `AudioDenoise`: Noise reduction. |
|EnhanceImageList |Array of [EnhanceImageList](https://docs.byteplus.com/en/docs/25/36078#enhanceimagelist) |`-` |Detailed usage data for video quality enhancement. |
|TotalEnhanceImagData |Long |`100` |Total video quality enhancement usage in milliseconds for the selected time period. |


#{.custom\-md\-table\-4}#

<span id="enhanceimagelist"></span>
### EnhanceImageList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`2022-04-13T00:00:00Z` |The timestamp. |
|SR |Long |`20000` |The duration of smart resolution (SR) tasks processed during the specified time period, measured in milliseconds. |
|VFI |Long |`20` |The duration of video frame interpolation (VFI) tasks processed during the specified time period, measured in milliseconds. |
|SDR2HDR |Long |`20` |The duration of SDR to HDR conversion tasks processed during the specified time period, measured in milliseconds. |
|SDREnhance |Long |`20` |The duration of SDR enhancement tasks processed during the specified time period, measured in milliseconds. |
|AudioDenose |Long |`3600` |The duration of audio denoising tasks processed during the specified time period, measured in milliseconds. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DescribeVodEnhanceImageData&Version=2023-01-01&SpaceList=test&StartTime=2022-04-12T16:00:00Z&EndTime=2022-04-13T16:00:00Z&SnapshotType=&TaskStageList=busy&Aggregation=3600&DetailFieldList=
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20180604110***0100232280022D30",
        "Action": "DescribeVodEnhanceImageData",
        "Version": "2023-01-01",
        "Service": "vod"
    },
    "Result": {
        "SpaceList": [
            "test"
        ],
        "StartTime": "2022-04-12T16:00:00Z",
        "EndTime": "2022-04-13T16:00:00Z",
        "Aggregation": 3600,
        "TotalEnhanceImagData": 100,
        "EnhanceImageList": [
            {
                "Time": "2022-04-13T:00:00Z",
                "SR": 20,
                "VFI": 20,
                "SDREnhance": 20,
                "SDR2HDR": 20
            },
            {
                "Time": "2022-04-13T:00:00Z",
                "SR": 20,
                "FrameInterpolation": 20,
                "SDREnhance": 20,
                "SDRToHDR": 20,
                "AudioDenose": 3600
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
