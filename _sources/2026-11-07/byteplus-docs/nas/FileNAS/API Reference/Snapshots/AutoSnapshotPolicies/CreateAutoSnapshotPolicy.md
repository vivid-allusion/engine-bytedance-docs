---
title: "CreateAutoSnapshotPolicy"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/CreateAutoSnapshotPolicy"
---

Call CreateAutoSnapshotPolicy interface to create an automatic snapshot policy.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* The snapshot function is currently in the free stage, and each file storage instance can create up to 5 automatic snapshots; when the number of automatic snapshots reaches the upper limit, the system will automatically delete the earliest automatic snapshots created.

* There may be some differences between the automatic snapshot policy time you set and the actual snapshot creation time. Please refer to the actual creation time.

* File storage instances cannot create both automatic and manual snapshots at the same time. At an automatic snapshot creation point, if the file system is performing the create snapshot task (manual or automatic snapshot creation), the system will not create an automatic snapshot of that point in time.

   For more information, see [Create an Automatic Snapshot Policy](https://docs.byteplus.com/en/docs/nas/Creating-a-snapshot).


<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AutoSnapshotPolicyName |String |Yes |testName |Automatic snapshot policy name, value selection description is as follows:<br><br><br>* Cannot start with a number, a dash (\-), or `auto`.<br><br>* Can only contain Chinese, letters, numbers, underscores (_) and underscores (\-).<br><br>   The length should be between 1 and 128 characters. |
|RepeatWeekdays |String |Yes |1,2 |The repeat date of the automatic snapshot, the unit is days, the period is weeks, and the value selection description is as follows:<br><br><br>* The range of values is `1` to `7`, for example,`1` means Monday.<br><br>* Support setting multiple dates, separated by English commas (,), and up to 7 time points. |
|TimePoints |String |Yes |1,2,3 |The creation time of the automatic snapshot, the value selection description is as follows:<br><br><br>* Use UTC + 8 time in hours.<br><br>* Value range: `0~ 23`, indicating a total of 24 time points from 00:00 to 23:00, for example, `1` means 01:00.<br><br>* Support setting multiple time points, separated by English commas (,), up to 24 time points. |
|RetentionDays |Integer |No |10 |The storage time of the automatic snapshot, in days, and the value selection description is as follows:<br><br><br>* `-1`: Save permanently until the number of automatic snapshots exceeds the upper limit and is automatically deleted.<br><br>* `1~ 65536`: Specifies the number of days to save.<br><br>   Default value: `30` days. |
|Description |String |No |policytest |Automatic snapshot policy description information. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|AutoSnapshotPolicyId |String |asp\-15c19547\*\*\*\* |Automatic Snapshot Policy ID. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=CreateAutoSnapshotPolicy&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "AutoSnapshotPolicyName": "testName",
    "RepeatWeekdays": "1,2",
    "TimePoints": "1,2,3"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateAutoSnapshotPolicy",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "AutoSnapshotPolicyId": "asp-15c19547****\t"
    }
}
```
