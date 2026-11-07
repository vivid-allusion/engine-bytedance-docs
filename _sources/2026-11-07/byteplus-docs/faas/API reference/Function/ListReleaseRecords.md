---
title: "ListReleaseRecords"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/ListReleaseRecords"
---

Query function release records.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=ListReleaseRecords&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListReleaseRecords |Interface name. The current API is called `ListReleaseRecords`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |nu\*\*\*\*\*\* |Function ID. |
|PageNumber |Integer |No |1 |Paging parameter, the current page number is default 1. |
|PageSize |Integer |No |10 |Paging parameter, the size per page is default 10. |
|Filters |Array of [Filter](https://docs.byteplus.com/en/docs/faas/ListReleaseRecords#filter) |No |\- |Query filter criteria. |
|OrderBy |Object of [OrderBy](https://docs.byteplus.com/en/docs/faas/ListReleaseRecords#orderby) |No |\- |Query sorting parameters. |


<span id="filter"></span>
### Filter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Name |String |No |Id |Filter key enumeration:<br><br><br>* Id (Release Record ID)<br><br>* Status (release status)<br><br>* SourceRevisionNumber (historic version number)<br><br>* TargetRevisionNumber (target version number)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Filtered values do not support fuzzy queries.</div><br> |
|Values |Array of String |No |["7d2\*\*\*\*\*\*"] |The filter value of the query is an array. |


<span id="orderby"></span>
### OrderBy


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |CreateTime |The Key name for sorting:<br><br><br>* CreateTime: Creation time<br><br>* FinishTime: Finish time |
|Ascend |Boolean |No |true |Whether the sorted results are sorted in ascending order.<br><br><br>* true: Ascending order<br><br>* false (default): Descending order |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=ListReleaseRecords&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "nu******",
    "PageNumber": 1,
    "PageSize": 10,
    "Filters": [
        {
            "Name": "Id",
            "Value": [
                "7d2******"
            ]
        }
    ],
    "OrderBy": {
        "Key": "CreationTime",
        "Ascend": false
    }
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [ReleaseRecord](https://docs.byteplus.com/en/docs/faas/ListReleaseRecords#releaserecord) |\- |Function release record list. |
|Total |Integer |1 |The total amount of data in the response list. |


<span id="releaserecord"></span>
### ReleaseRecord


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |cyts\*\*\*\*\*\* |The Release Record ID. |
|Status |String |finished |Release status:<br><br><br>* rolling: Releasing<br><br>* finished: Finished<br><br>* rollbacking: In rollbacks<br><br>* rollbacked: Rollbacked<br><br>* failed: Failed |
|FinishTime |String |2024\-06\-14 15:31:07.143863491 +0800 CST m=+88714.902440914 |Finish time. |
|FunctionId |String |nu\*\*\*\*\*\* |Function ID. |
|Description |String |Support xxx feature |Release information description. |
|CreationTime |String |2024\-06\-14 15:31:07.143863441 +0800 CST m=+88714.902440864 |Creation time. |
|LastUpdateTime |String |2024\-06\-14 15:31:07.143863491 +0800 CST m=+88714.902440914 |Update time. |
|SourceRevisionNumber |Integer |9 |Released historic version number. |
|TargetRevisionNumber |Integer |10 |Target version number of the release. |


<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListReleaseRecords",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Items": [
            {
                "Id": "cyt******",
                "Status": "finished",
                "FinishTime": "2024-06-14 15:31:07.143863491 +0800 CST m=+88714.902440914",
                "FunctionId": "nu******",
                "Description": "Support xxx feature",
                "CreationTime": "2024-06-14 15:31:07.143863441 +0800 CST m=+88714.902440864",
                "LastUpdateTime": "2024-06-14 15:31:07.143863491 +0800 CST m=+88714.902440914",
                "SourceRevisionNumber": 9,
                "TargetRevisionNumber": 10
            }
        ],
        "Total": 1
    }
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
