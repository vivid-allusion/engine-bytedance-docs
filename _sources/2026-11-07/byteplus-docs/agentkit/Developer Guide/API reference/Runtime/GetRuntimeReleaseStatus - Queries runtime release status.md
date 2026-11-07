---
title: "GetRuntimeReleaseStatus - Queries runtime release status"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetRuntimeReleaseStatus_-_Queries_runtime_release_status"
---

You can call this operation to query the runtime release status.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|nO2XKy">必选</span> `Sample value: GetRuntimeReleaseStatus`

The action that you want to perform. Value: GetRuntimeReleaseStatus.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|JODoZ2">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|JTAO0k">必选</span> `Sample value: r-yefj305tds75z4k3****`

ID of the runtime.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CurrentTrafficWeight ** <span data-label="purple">integer </span>`Sample value: 60`

The current traffic percentage for the release. This indicates the traffic proportion of the version currently being released. This parameter is returned only when `status` is `inprogress or failed`.


* Value: 0–100.



**ErrorCode ** <span data-label="purple">string </span>`Sample value: function_start_failed`

Error codes displayed when release fails:


* function_start_failed: Function startup failed

* function_start_timeout: Function startup timeout

* function_health_check_failed: Function health check failed

* system_internal_error: Internal system error



**FailedInstanceLogs ** <span data-label="purple">string </span>`Sample value: https://xx.tos-s3-cn.volces.com/release_failed_instance_logs/******`

The download link for logs of instances that failed to release.



**NewVersionNumber ** <span data-label="purple">integer </span>`Sample value: 4`

The target version number for the release.



**OldVersionNumber ** <span data-label="purple">integer </span>`Sample value: 3`

The previously released version number.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not returned when <code>status</code> is <code>pending</code>. It is returned when status is <code>inprogress, failed, or done</code>.</div>




**ReleaseRecordId ** <span data-label="purple">string </span>`Sample value: 5oivgbdpp4ji****`

Release record​ ID.



**RuntimeId ** <span data-label="purple">string </span>`Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



**StableVersionNumber ** <span data-label="purple">integer </span>`Sample value: 2`

The version number currently running in the stable online environment. This value is generated after the first successful release. Before the first release (status=pending), StableVersionNumber is \-1.



**StartTime ** <span data-label="purple">string </span>`Sample value: 2026-02-10 07:05:12`

The start time of the current release.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not returned when <code>status</code> is <code>pending</code>. It is returned when status is <code>inprogress, failed, or done</code>.</div>




**Status ** <span data-label="purple">string </span>`Sample value: done`

Runtime release status:


* pending: No release has been performed.

* inprogress: A release is in progress.

* done: The release succeeded.

* failed: The release failed.



**StatusMessage ** <span data-label="purple">string </span>`Sample value: Runtime release finished successfully`

Detailed information about the runtime release status.



**TargetTrafficWeight ** <span data-label="purple">integer </span>`Sample value: 60`

The target traffic percentage for the release.


* Value range: 1\-100.

* If the value is 100: Full release.

* If the value is less than 100: Grey release.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetRuntimeReleaseStatus&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "RuntimeId": "r-yefj305tds75z4k3****",
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20260212164514578DDADB7457C5C9****",
        "Action": "GetRuntimeReleaseStatus",
        "Version": "2025-10-30",
        "Service": "agentkit",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RuntimeId": "r-yefj305tds75z4k3****",
        "Status": "done",
        "StatusMessage": "",
        "StableVersionNumber": 2,
        "NewVersionNumber": 4,
        "OldVersionNumber": 3,
        "StartTime": "2026-02-10 07:05:12",
        "TargetTrafficWeight": 60,
        "CurrentTrafficWeight": 60,
        "ErrorCode": "",
        "FailedInstanceLogs": "",
        "ReleaseRecordId": "n6tfbaejc25****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidResourceStatus |The status of the specified resource does not support this request. |The current status of the resource does not support this operation. |
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The parameter RuntimeId cannot be empty. |
