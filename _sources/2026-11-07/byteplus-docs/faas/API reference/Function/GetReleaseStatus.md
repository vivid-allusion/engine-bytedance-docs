---
title: "GetReleaseStatus"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GetReleaseStatus"
---

Query function release status.

<span id="请求说明"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=GetReleaseStatus&Version=2024\-06\-06


<span id="请求参数"></span>
## Request parameter


|Parameter |Type |Required or Not |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetReleaseStatus |Interface name. The current API is called `GetReleaseStatus`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |nw\*\*\*\*\*\* |Function ID. |


<span id="请求示例"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=GetReleaseStatus&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "nw******"
}
```


<span id="返回参数"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|FunctionId |String |nwwzoaq1 |Function ID. |
|Status |String |done |Function release status:<br><br><br>* pending: Never released<br><br>* inprogress: Releasing<br><br>* done: Released successfully<br><br>* failed: Release failed |
|StatusMessage |String |Function release finished successfully |Function release status details. This is a supplement to the release status. |
|StableRevisionNumber |Integer |1 |The version number currently running stably online. Generated after the initial release is successful, and before the initial release (status == pending) StableRevisionNumber \-1. |
|NewRevisionNumber |Integer |1 |Version number of the new version being released. When the status is pending, no parameter will return. When the status is inprogress/failed/done, a parameter will return. |
|OldRevisionNumber |Integer |1 |The version number of the old version. When the status is pending, no parameter will return. When the status is inprogress/failed/done, a parameter will return. |
|StartTime |String |2024\-06\-27 07:05:12 |The current release start time. When the status is pending, no parameter will return. When the status is inprogress/failed/done, a parameter will return. |
|TargetTrafficWeight |Integer |100 |Target release traffic percentage. Valid value 0\-100, representing the proportion of traffic of the version you want to release, and full release is 100. |
|CurrentTrafficWeight |Integer |50 |Current released traffic percentage. Valid value 1\-100, representing the proportion of traffic of the version currently being released, and only when the status is inprogress/failed, a parameter will return. |
|ErrorCode |String |function_start_failed |Error codes for release failures:<br><br><br>* function_start_failed: Function start failed<br><br>* function_start_timeout: Function start timeout<br><br>* function_health_check_failed: Function health check failed<br><br>* system_internal_error: System internal error |
|FailedInstanceLogs |String |https://vefaas\-sit.tos\-s3\-ap\-southeast\-1.byteplus.com/release_failed_instance_logs/\*\*\*\*\*\* |The download link for instance logs of failed releases. |
|ReleaseRecordId |String |xozo\*\*\*\*\*\* |Release record ID. |


<span id="返回示例"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetReleaseStatus",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "FunctionId": "nw******",
        "Status": "done",
        "StatusMessage": "Function release finished successfully",
        "StableRevisionNumber": 1,
        "NewRevisionNumber": 1,
        "OldRevisionNumber": 1,
        "StartTime": "2024-06-27 07:05:12",
        "TargetTrafficWeight": 100,
        "CurrentTrafficWeight": 50,
        "ErrorCode": "function_start_failed",
        "FailedInstanceLogs": "https://vefaas-sit.tos-s3-ap-southeast-1.byteplus.com/release_failed_instance_logs/******",
        "ReleaseRecordId": "xozo******"
    }
}
```


<span id="错误码"></span>
## Error code 

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
