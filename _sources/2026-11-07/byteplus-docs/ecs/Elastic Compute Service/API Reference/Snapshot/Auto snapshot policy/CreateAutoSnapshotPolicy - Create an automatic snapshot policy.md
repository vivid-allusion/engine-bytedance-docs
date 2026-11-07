---
title: "CreateAutoSnapshotPolicy - Create an automatic snapshot policy"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Createautosnapshotpolicy"
---

Call the CreateAutoSnapshotPolicy API to create an automatic snapshot policy.

<span id=".5rOo5oSP5LqL6aG5"></span>
## precautions


* Each volume can create up to 1024 automatic snapshots. When the number of automatic snapshots reaches the limit, the system automatically deletes the oldest automatic snapshot by creation time.

* A single account supports up to 32 automatic snapshot policies per region.

* The scheduled time for the automatic snapshot policy may differ from the actual snapshot creation time; please refer to the actual creation time.

* If the snapshot creation duration exceeds the interval between two automatic snapshots, the system will skip the second scheduled time and not create that snapshot. For example, if you set automatic snapshots at 1:00, 2:00, and 3:00, and the snapshot created at 1:00 takes until 2:30 to finish, the 2:00 snapshot will be skipped, and the next snapshot will be created at 3:00.

* A volume cannot create automatic and manual snapshots simultaneously.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateAutoSnapshotPolicy&groupName=%E8%87%AA%E5%8A%A8%E5%BF%AB%E7%85%A7%E7%AD%96%E7%95%A5&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only the request parameters specific to this API and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|orhaXR">必选</span> `Example: CreateAutoSnapshotPolicy`

Operation to perform: CreateAutoSnapshotPolicy.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|pIPvqe">必选</span> `Example: 2020-04-01`

The version of the API is: 2020\-04\-01.



**AutoSnapshotPolicyName ** <span data-label="purple">string </span><span data-api-tag="require|qFlsMc">必选</span> `Example: testName`

Automatic snapshot policy name guidelines are as follows:


* The first character can only be a Chinese character, letter, or underscore (_).

* Can contain Chinese characters, letters, numbers, underscores (_), hyphens (\-), or periods (.).

* The length must be between 1 and 128 characters.



**TimePoints.N ** <span data-label="purple">string[] </span><span data-api-tag="require|p4OnUc">必选</span> `Example: TimePoints.1=0&TimePoints.2=1`

Time points for automatic snapshot creation are described as follows:


* Use UTC+8 time, measured in hours.

* Value range: 0–23, representing 00:00 to 23:00, a total of 24 time points. For example, 1 means 01:00.

* To create multiple automatic snapshots in a single day, you can specify multiple time points, up to 24.



**RepeatWeekdays.N ** <span data-label="purple">string[] </span>`Optional` `Example: RepeatWeekdays.1=1&RepeatWeekdays.2=7`

By week: Select one or more days from Monday to Sunday to create snapshots. Description as follows:


* The valid range is 1–7, where 1 represents Monday.

* If you need to create multiple automatic snapshots in a week, you can provide several time points, up to a maximum of 7.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When creating an automatic snapshot policy, you must set either the RepeatWeekdays.N parameter or the RepeatDays parameter. You cannot set both RepeatWeekdays.N and RepeatDays at the same time.</div>




**RetentionDays ** <span data-label="purple">integer </span><span data-api-tag="require|iYn74F">必选</span> `Example: 30`

Automatic snapshot retention period, measured in days, as described below:


* \-1: Permanently retained.

* 1–65536: Retained for the specified number of days.



**RepeatDays ** <span data-label="purple">integer </span>`Optional` `Example value: 10`

Create snapshots on a daily basis, with intervals between 1 and 30 days.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When creating snapshots on a daily cycle, the day the automatic snapshot policy is created is considered the first day. Snapshots will not be created for past scheduled times. If all scheduled times on the first day have passed, it is still counted as the first day.</div>


* <div data-tips="true" data-tips-type="tip">When creating an automatic snapshot policy, you must set either the RepeatWeekdays.N or RepeatDays parameter. Setting both parameters at the same time is not supported.</div>




**Tags.N.Key ** <span data-label="purple">string[] </span>`Optional` `Example: Tags.1.Key=tag`

Tag key for the label.


* Tags.N.Key: N indicates the index number of the tag key. Value range: 1\-20.

* Use & to separate multiple tag keys.



**Tags.N.Value ** <span data-label="purple">string[] </span>`Optional` `Example: Tags.1.Value=test`

Tag value of the label.


* Tags.N.Value: N indicates the sequence number of the tag value. Value range: 1\-20.

* Separate multiple tag values with &.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Example value: default`

The project that the automatic snapshot policy belongs to.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The automatic snapshot policy does not inherit the volume’s project; the automatic snapshot policy, the volume, and the snapshot can belong to different projects.</div>


* <div data-tips="true" data-tips-type="warning">If you do not set ProjectName when creating an automatic snapshot policy, the policy will be added to the default project by default.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

Only the response parameters specific to this API are listed below. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AutoSnapshotPolicyId ** <span data-label="purple">string </span>`Example: asp-anj249wubz9kakc8****`

Auto snapshot policy ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=CreateAutoSnapshotPolicy&Version=2020-04-01&TimePoints.1=TimePoints.1%3D0%26TimePoints.2%3D1 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20251124T082339Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251124/ap-southeast-1/storage_ebs/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "AutoSnapshotPolicyName": "testName",
  "RetentionDays": 30
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "202511241623421421290842099C****",
    "Action": "CreateAutoSnapshotPolicy",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "AutoSnapshotPolicyId": "asp-anj249wubz9kakc8****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this API and its business logic. Please refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidRequest |The operation is not permitted due to the request is invalid. |Invalid request. |
|400 |InvalidParameters |The request has invalid parameters. |The request contains invalid parameters. |
|400 |InvalidSnapshotPolicyNameLen |The length of the automatic snapshot policy name is invalid. |The automatic snapshot policy name length is invalid. |
|400 |InvalidSnapshotPolicyNameFormat |The format of the automatic snapshot policy name is invalid. |The format of the automatic snapshot policy name is invalid. |
|400 |ErrInvalidTimePoints |The specified time point is invalid. |The specified time point is invalid. |
|400 |InvalidRepeatDays |The specified period days is invalid. |The specified repeat cycle is invalid. |
|400 |ErrInvalidRepeatWeekDays |The specified repeat weekdays is invalid. |The specified repeat cycle is invalid. |
|400 |ErrorAccountIsOverdue |Account is in arrears, and some snapshot features are unavailable. |Your account is overdue; some snapshot functions are unavailable. |
|403 |AutoSnapshotPolicyQuotaExceed |The number of automatic snapshot policies exceeds quota, please submit ticket to request an increase in quota. |The number of automatic snapshot policies has reached the quota limit. Please request a quota increase. |
|500 |InternalError |An internal error has occurred. |Internal error. Try again. If multiple attempts have failed, submit a support ticket. |
