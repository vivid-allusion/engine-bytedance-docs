---
title: "UpdateAutoSnapshotPolicy"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/UpdateAutoSnapshotPolicy"
---

Call UpdateAutoSnapshotPolicy interface to modify the automatic snapshot policy information.

<span id="requirements"></span>
## Requirements

After modifying the automatic snapshot policy, the cloud disk that has previously applied the policy will automatically execute the modified automatic snapshot policy.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AutoSnapshotPolicyId |String |Yes |asp\-15c19547\*\*\*\* |The automatic snapshot policy ID that needs to be modified. |
|AutoSnapshotPolicyName |String |No |testName |Automatic snapshot policy name, value selection description is as follows:<br><br><br>* Cannot start with a number, a dash (\-), or auto.<br><br>* Can only contain Chinese, letters, numbers, underscores (_) and underscores (\-).<br><br>   The length should be between 1 and 128 characters. |
|RepeatWeekdays |String |No |1,2 |The repeat date of the automatic snapshot, the unit is days, the period is weeks, and the value selection description is as follows:<br><br><br>* The range of values is `1` to `7`, for example,`1` means Monday.<br><br>* Support setting multiple dates, separated by English commas (,), and up to 7 time points. |
|TimePoints |String |No |1,2,3 |The creation time of the automatic snapshot, the value selection description is as follows:<br><br><br>* Use UTC + 8 time in hours.<br><br>* Value range: `0~ 23`, indicating a total of 24 time points from 00:00 to 23:00, for example, `1` means 01:00.<br><br>* Support setting multiple time points, separated by English commas (,), up to 24 time points. |
|RetentionDays |Integer |No |10 |The storage time of the automatic snapshot, in days, and the value selection description is as follows:<br><br><br>* `-1`: Save permanently until the number of automatic snapshots reaches the upper limit and is automatically deleted.<br><br>* `1~ 65536`: Specifies the number of days to save.<br><br>   Default value: `30` days. |
|Description |String |No |testdescription |Automatic snapshot policy description information. |


<span id="response-parameters"></span>
## Response parameters

Empty.

<span id="sample-request"></span>
## Sample request

```json
POST /?Action=UpdateAutoSnapshotPolicy&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "AutoSnapshotPolicyId": "asp-15c19547****",
    "AutoSnapshotPolicyName": "testName",
    "RepeatWeekdays": "1,2",
    "TimePoints": "1,2,3",
    "RetentionDays": 10,
    "Description": "testdescription"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateAutoSnapshotPolicy",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {}
}
```
