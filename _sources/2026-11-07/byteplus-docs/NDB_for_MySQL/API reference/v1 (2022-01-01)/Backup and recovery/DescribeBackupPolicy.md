---
title: "DescribeBackupPolicy"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeBackupPolicy"
---

Call the DescribeBackupPolicy to query the instance data backup policy.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBackupPolicy&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-gzwdsf9b\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |vedbm\-gzwdsf9b\*\*\*\* |Instance ID. |
|BackupTime |String |18:00Z\-20:00Z |The time window for running the backup task is 2 hours. Format: HH:mmZ\-HH:mmZ (UTC time). |
|FullBackupPeriod |String |Friday,Monday,Saturday |Full backup cycle. Separate multiple values with a comma (,). Value:<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday. |
|BackupRetentionPeriod |Integer |7 |Number of days to retain data backup. |
|ContinueBackup |Boolean |true |Specifies whether to enable continuous backup. The value must be `true`. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeBackupPolicy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-gzwdsf9b****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202307191407166A09199F8080EF9ED490",
        "Action": "DescribeBackupPolicy",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupRetentionPeriod": 7,
        "BackupTime": "18:00Z-20:00Z",
        "ContinueBackup": true,
        "FullBackupPeriod": "Friday,Monday,Saturday,Sunday,Thursday,Tuesday,Wednesday",
        "IncrementBackupPeriod": 20,
        "InstanceId": "vedbm-gzwdsf9b****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
