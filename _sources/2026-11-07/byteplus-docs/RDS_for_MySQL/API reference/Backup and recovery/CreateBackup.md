---
title: "CreateBackup"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/createbackup1"
---

Call the CreateBackup API to create a backup.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* An instance can run only one backup task at a time.

* This API does not support creating log backups.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateBackup&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-e26822cf\*\*\*\* |Instance ID. |
|BackupMethod |String |No |Physical |The supported backup types vary based on the instance's storage type:<br><br><br>* If the instance's storage type is local disk, Physical backup `Physical` (the default) or Logical backup `Logical` can be selected.<br><br>* If the instance's storage type is volume, you can only select `Snapshot` backup. |
|BackupType |String |No |Full |Backup method.<br><br><br>* Range:<br><br>   * If the backup type is physical backup `Physical` or snapshot backup `Snapshot`, the backup method is full backup `Full` (default value) or incremental backup frequency `HighFrequencyIncrement`.<br><br>   * If you select logical backup `Logical` as the backup type, the backup method must be full database backup `DumpAll`. This parameter is not required for a backup set of specified databases and tables. You only need to specify the databases and tables in the BackupMeta parameter. |
|BackupMeta |Array of [BackupMeta](https://docs.byteplus.com/en/docs/40/15426#backupmeta) |No |See the request example. |Specifies the databases and tables information to be backed up when creating a logical database & table backup.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when performing a logical backup (BackupMethod=Logical) for specified databases and tables (when the BackupType parameter is not specified). This parameter is invalid for other backup types and backup methods.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Quantity limit: When creating a backup for specified databases and tables, the maximum number of databases is 5,000, and the maximum number of tables per database is 5,000.</div><br> |
|BackupName |String |No |Manual backup 001 |Set the backup name. Naming rules are as follows:<br><br><br>* Cannot start with a hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length must be between 1 and 128 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a backup name is not set, the backup ID is used as the backup name.</div><br> |


<span id="backupmeta"></span>
### BackupMeta


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|DBName |String |Yes |db1 |Specify the database to be backed up. |
|TableNames |Array of String |No |["table1","table2"] |Specify the tables in the database to be backed up. If this field is empty, it defaults to a full database backup. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|BackupId |String |2c587b3e5b6e409ca38a2c99462a\*\*\*\* |ID of the newly created backup. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6LLTE="></span>
### Sample request 1

Create a full physical backup

```json
POST /?Action=CreateBackup&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-ce48081d****",
    "BackupType": "Full",
    "BackupMethod": "Physical"
}
```


<span id=".6L-U5Zue56S65L6LLTE="></span>
### Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "20230111114312146C48B77B8FB071C1FD",
        "Action": "CreateBackup",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupId": "986533aae3ac4e27af6ec1cd2aeeca1d"
    }
}
```


<span id=".6K-35rGC56S65L6LLTI="></span>
### Sample request 2

Create a full database backup

```json
POST /?Action=CreateBackup&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-ce48081d****",
    "BackupMethod": "Logical",
    "BackupType": "DumpAll"
}
```


<span id=".6L-U5Zue56S65L6LLTI="></span>
### Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "20230111114312146C48B77B8FB071C1FD",
        "Action": "CreateBackup",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupId": "2c587b3e5b6e409ca38a2c99462a****"
    }
}
```


<span id=".6K-35rGC56S65L6LLTM="></span>
### Sample request 3

Create a database & table backup

```json
POST /?Action=CreateBackup&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-ce48081d****",
    "BackupMethod": "Logical",
    "BackupMeta": [
        {
            "DBName": "testdb",
            "Tables": [
                ""
            ]
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6LLTM="></span>
### Sample response 3

```json
{
    "ResponseMetadata": {
        "RequestId": "20230111114312146C48B77B8FB071C1FD",
        "Action": "CreateBackup",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupId": "e2a7f1ea55fb43b281b5fcaf3f5e****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
