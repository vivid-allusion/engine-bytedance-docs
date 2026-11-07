---
title: "DescribeVodSnapshotData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodsnapshotdata"
---

This interface is used to query the usage of the screenshot function within a specified time range under the specified spatial dimensions.

<span id="requirements"></span>
## Requirements


* Billing: For screenshot billing prices, please refer to [Pay-As-You-Go pricing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing).

* Data Latency: **4 hours**.

* Permission Explanation: When using a sub\-account to request the API, the API will verify permissions based on the sub\-account and only return data that the sub\-account is authorized to access. For more details, see [Creating a sub-account](https://docs.byteplus.com/en/docs/byteplus-vod/docs-creating-iam-users).


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodSnapshotData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodSnapshotData` |The API action. For the current API, the value is `DescribeVodSnapshotData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceList |String |No |`test` |List of the Video on Demand (VOD) space names. Multiple space names are separated by a comma `,`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, this parameter type is Array of String.</div><br> |
|StartTime |String |No |`2021-04-13T00:00:00+08:00` |The start time of the query. It follows the RFC3339 format for UTC time, with a precision of seconds. The format is: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |No |`2021-04-14T00:00:00+08:00` |The end time of the query. It follows the RFC3339 format for UTC time with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The query time span does not exceed 93 days.</div><br> |
|SnapshotType |String |No |`Sprite` |The screenshot types. The values are as follows:<br><br><br>* `Poster`: Static snapshots<br><br>* `Sample`: Sampled snapshots<br><br>* `Dynpost`: Dynamic snapshots<br><br>* `Animated`: Looped dynamic snapshots<br><br>* `AIDynpost`: The smart cover (AI dynamic snapshots)<br><br>* `Sprite`: Sprite snapshots |
|TaskStageList |String |No |`busy` |The task type. Separate multiple task types with a comma `,`. The values are as follows:<br><br><br>* `free`: Idle task<br><br>* `busy`: Nomal task<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, the parameter type is Array of String.</div><br> |
|Aggregation |Long |No |`3600` |The aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `86400`: (default) 1 day<br><br>* `3600`: 1 hour |
|DetailFieldList |String |No |`Space` |Detailed field list. Values are as follows:<br><br><br>* `Space`: The name of the Video on Demand (VOD) space.<br><br>* `TaskStage`: The task type.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the parameter is not empty, more detailed usage data will be returned.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If it is a POST request, this parameter type is Array of String.</div><br> |
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
|SnapshotType |String |`Sprite` |The screenshot type. The values are as follows:<br><br><br>* `Poster`: Static snapshots<br><br>* `Sample`: Sampled snapshots<br><br>* `Dynpost`: Dynamic snapshots<br><br>* `Animated`: Looped dynamic snapshots<br><br>* `AIDynpost`: The smart cover (AI dynamic snapshots)<br><br>* `Sprite`: Sprite snapshots |
|TaskStageList |Array of String |`["busy","free"]` |The task type list. The values are as follows:<br><br><br>* `free`: Idle task<br><br>* `busy`: Normal task |
|Aggregation |Long |`3600` |The aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `3600`: 1 hour<br><br>* `86400`: 1 day |
|DetailFieldList |Array of String |`["TaskStage"]` |Detailed field list. The values are as follows:<br><br><br>* `Space`: The name of the on\-demand space<br><br>* `TaskStage`: The type of the task |
|TotalSnapshotData |Long |`100` |The total number of screenshots for the selected time period. |
|SnapshotDataList |Array of [SnapshotDataList](https://docs.byteplus.com/en/docs/25/36077#snapshotdatalist) |`-` |The specific data on screenshot usage. |
|SnapshotDetailDataList |Array of [SnapshotDetailDataList](https://docs.byteplus.com/en/docs/25/36077#snapshotdetaildatalist) |`-` |The screenshot usage for various task types. |


#{.custom\-md\-table\-4}#

<span id="snapshotdatalist"></span>
### SnapshotDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`2022-04-13T00:00:00+08:00` |The start time of the data time range. It follows the RFC3339 format for UTC time, with second precision, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|Count |Long |`100` |The number of screenshots. |


#{.custom\-md\-table\-4}#

<span id="snapshotdetaildatalist"></span>
### SnapshotDetailDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Space |String |`test` |The VOD space name. |
|Total |String |`1000` |The number of screenshots. |
|TaskStage |String |`busy` |The task type. The values are as follows:<br><br><br>* `free`: Idle task<br><br>* `busy`: Normal task |
|SnapshotDataList |Array of [SnapshotDataList](https://docs.byteplus.com/en/docs/25/36077#snapshotdatalist) |`-` |The specific data on screenshot usage. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DescribeVodSnapshotData&Version=2023-01-01&SpaceList=test&StartTime=2021-04-13T00:00:00+08:00&EndTime=2021-04-14T00:00:00+08:00&SnapshotType=Sprite&TaskStageList=busy&Aggregation=3600&DetailFieldList=Space&RegionList=cn-north-1
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104***100232280022D30",
        "Action": "DescribeVodSnapshotData",
        "Version": "2023-01-01",
        "Service": "vod"
    },
    "Result": {
        "SpaceList": [
            "test"
        ],
        "StartTime": "2021-04-13T00:00:00+08:00",
        "EndTime": "2021-04-14T00:00:00+08:00",
        "TaskStageList": [
            "busy",
            "free"
        ],
        "DetailFieldList": [
            "TaskStage"
        ],
        "Aggregation": 3600,
        "TotalSnapshotData": 100,
        "SnapshotDataList": [
            {
                "Time": "2022-04-13T00:00:00+08:00",
                "Count": 100
            }
        ],
        "SnapshotDetailDataList": [
            {
                "TaskStage": "busy",
                "SnapshotDataList": [
                    {
                        "Time": "2022-04-13T00:00:00+08:00",
                        "Count": 50
                    }
                ]
            },
            {
                "TaskStage": "free",
                "SnapshotDataList": [
                    {
                        "Time": "2022-04-13T00:00:00+08:00",
                        "Count": 50
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
