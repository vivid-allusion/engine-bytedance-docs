---
title: "DescribeBackupEncryptionStatus - Query the backup encryption policy of an instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackupencryptionstatus"
---

Call the DescribeBackupEncryptionStatus API to query the backup encryption policy of an instance.

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


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|DataEncryptionStatus |String |On |Indicates whether encryption is enabled for data backup. Values:<br><br><br>* `On`: enabled.<br><br>* `Off`: disabled. |
|LogEncryptionStatus |String |On |Specifies whether to enable encryption for log backup. Values:<br><br><br>* `On`: enabled.<br><br>* `Off`: disabled. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeBackupEncryptionStatus&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-0d458bb5****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024051511492825FD41C99A9BDE8B9D7F-1b2940",
        "Action": "DescribeBackupEncryptionStatus",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "DataEncryptionStatus": "Off",
        "LogEncryptionStatus": "On"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
