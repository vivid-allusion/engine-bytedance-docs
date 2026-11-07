---
title: "DescribeBackupDecryptionKey - Query the encryption key for a backup"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackupdecryptionkey"
---

Call the DescribeBackupDecryptionKey API to query the encryption key for a backup.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If you receive the error "The instance version is too low to support the requested operation" when calling this API, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical staff to upgrade the instance.

* MySQL 8.4 instances do not support backup encryption.


<span id=".6LCD6K-V"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-0d458bb5\*\*\*\* |Instance ID. |
|BackupId |String |Yes |* BackupId example: f1f2284117a344a38370c37b841fec75<br><br>* FileName example: binlog\-1683420632178737071\-binlog.000044 |Data backup ID or the file name of the log backup.<br><br>If you are querying the key for data backup encryption, the value of this field is the BackupId of the backup file, which you can obtain by calling the [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups) API. If you are querying the key for log backup encryption, the value of this field is the FileName of the backup file, which you can obtain by calling the [DescribeBinlogFiles](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebinlogfiles) API. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|DecryptionKey |String |889a48446dece6e4a9c8033ade4e5903 |Key. |
|Iv |String |ec81a486bada45c0 |Initialization vector.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is returned only when querying the key for a log backup.</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeBackupDecryptionKey&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-0d458bb5****",
    "BackupId": "binlog_mysql-0d458bb5****-mb27f-0_1715747255925159171-binlog.000020"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024051513250710A7B3BCF7ECB986A033-e2f1e9",
        "Action": "DescribeBackupDecryptionKey",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "DecryptionKey": "aa7e7d668764ae9abf420a7de01004ad",
        "Iv": "ec81a486bada45c0"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
