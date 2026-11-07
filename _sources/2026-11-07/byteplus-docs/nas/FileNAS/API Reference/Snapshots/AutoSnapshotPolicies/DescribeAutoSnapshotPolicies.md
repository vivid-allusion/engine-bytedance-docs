---
title: "DescribeAutoSnapshotPolicies"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DescribeAutoSnapshotPolicies"
---

Call the DescribeAutoSnapshotPolicies interface to query all the automatic snapshot policies you have created in a certain region that meet the query conditions.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AutoSnapshotPolicyId |String |No |asp\-15c19547\*\*\*\* |The automatic snapshot policy ID to query. |
|AutoSnapshotPolicyName |String |No |enas\-18bcb923\*\*\*\* |The name of the automatic snapshot policy to query. |
|PageSize |Integer |No |10 |Number of records per page. An integer between `1` and `100`. Default is`10`. |
|PageNumber |Integer |No |1 |The page number of the policy list, with values not exceeding the maximum value of the Integer data type, starting at `1`. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |2 |Number of automatic snapshot policies. |
|PageSize |Integer |10 |The number of policies per page. |
|PageNumber |Integer |1 |The paginated page number of the automatic snapshot policy list. |
|AutoSnapshotPolicies |Array of [AutoSnapshotPolicy](https://docs.byteplus.com/en/docs/91/25003#autosnapshotpolicy) |See the return example for details |Automatic snapshot policy details. |


<span id="autosnapshotpolicy"></span>
### AutoSnapshotPolicy


|Name |Type |Example |Description |
|---|---|---|---|
|Status |String |Avaliable |Automatic snapshot policy status, value selection description is as follows:<br><br><br>* `Avaliable`: Running.<br><br>* `Creating`: Creating.<br><br>* `Deleting`: Deleting. |
|CreateTime |String |2023\-08\-30 T18:32:25 + 08:00 |Automatic snapshot policy creation time. |
|TimePoints |String |1, 16 |The creation time of the automatic snapshot is described as follows:<br><br><br>* Use UTC + 8 time in hours.<br><br>* Value range: `0~ 23`, indicating a total of 24 time points from 00:00 to 23:00, for example, `1` means 01:00. |
|Description |String |test |Automatic snapshot policy description information. |
|RetentionDays |Integer |30 |The retention time for automatic snapshots, in days, is as follows:<br><br><br>* `-1`: Save permanently until the number of automatic snapshots reaches the upper limit and is automatically deleted.<br><br>* `1~ 65536`: Specifies the number of days to save. |
|RepeatWeekdays |String |1, 3 |The recurring date of the automatic snapshot, in days and weeks, for example, `1` means Monday. |
|FileSystemCount |Integer |1 |Number of file systems for which the policy is enabled. |
|AutoSnapshotPolicyId |String |asp\-61c49dec\*\*\*\* |Automatic Snapshot Policy ID. |
|AutoSnapshotPolicyName |String |policytest2 |Automatic snapshot policy name. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeAutoSnapshotPolicies&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "AutoSnapshotPolicyId": "asp-15c19547****",
    "AutoSnapshotPolicyName": "enas-18bcb923****",
    "PageSize": 10,
    "PageNumber": 1
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeAutoSnapshotPolicies",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "TotalCount": 2,
        "PageSize": 10,
        "PageNumber": 1,
        "AutoSnapshotPolicies": [
            {
                "Status": "Avaliable",
                "CreateTime": "2023-08-30T18:32:25+08:00",
                "TimePoints": "1,16",
                "Description": "test",
                "RetentionDays": 30,
                "RepeatWeekdays": "1,3",
                "FileSystemCount": 1,
                "AutoSnapshotPolicyId": "asp-61c49dec****",
                "AutoSnapshotPolicyName": "policytest2"
            }
        ]
    }
}
```
