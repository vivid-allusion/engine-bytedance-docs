---
title: "RestoreToExistedInstance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretoexistedinstance"
---

Call the RestoreToExistedInstance API to restore data to an existing database instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Cross\-major\-version instance restoration is not supported. For example: Restore a MySQL 5.7 instance to a MySQL 8.0 instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RestoreToExistedInstance&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|SourceDBInstanceId |String |Yes |mysql\-e7fda57b\*\*\*\* |The ID of the source instance for the backup data. |
|BackupId |String |No |effc1de81b8a4c8e886fef2c3e06\*\*\*\* |Backup file ID. You can query the BackupID by calling [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You must specify either this parameter or the RestoreTime parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Physical backups can only restore to the original instance.</div><br> |
|RestoreTime |String |No |2022\-01\-01T10:10:10Z |Any point in time within the backup retention period of the source instance, formatted as `yyyy-MM-ddTHH:mm:ssZ` (UTC time). You can call [DescribeRecoverableTime](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describerecoverabletime1) to check if restoration to this point in time is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must specify either this parameter or the BackupId parameter.</div><br> |
|RestoreType |String |No |TABLE_LEVEL |The restore type. Currently, only `TABLE_LEVEL` is supported, which indicates a table\-level restoration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field will be deprecated.</div><br> |
|TableMeta |Array of [TableMetaObject](https://docs.byteplus.com/en/docs/40/15425#tablemetaobject) |No |[<br><br>  {<br><br>    "DBName" : "db",<br><br>    "NewDBName" : "db_new",<br><br>    "Table":<br><br>      [<br><br>        {<br><br>          "TableName" : "table",<br><br>          "NewTableName" : "table_new"<br><br>        }<br><br>      ]<br><br>  }<br><br>] |Specifies the databases and tables information to restore during databases and tables recovery.<br><br>This parameter is required when RestoreType is `TABLE_LEVEL`. |
|FastMode |Boolean |No |true |Whether to enable fast recovery mode. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value. |


<span id="tablemetaobject"></span>
### TableMetaObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|DBName |String |Yes |testdb1 |Specifies the DB to restore. |
|NewDBName |String |No |testdb2 |New DB name. Naming rules are as follows:<br><br><br>* The name must be unique.<br><br>* 2 to 64 characters in length.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* It cannot contain certain reserved words, including root and admin. Refer to the [List of forbidden keywords](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_forbidden_keywords) for forbidden reserved words.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Its value can be the same as DBName when restoring only a table.</div><br> |
|Table |Array of [Table](https://docs.byteplus.com/en/docs/40/15425#table) |No |[<br><br>{<br><br>"TableName" : "table1",<br><br>"NewTableName" : "table2"<br><br>}<br><br>] |The tables in the database to restore. If this parameter is empty, the entire database is restored. |


<span id="table"></span>
### Table


|Parameter |Type |Is it required? |Example |Description |
|---|---|---|---|---|
|TableName |String |Yes |table1 |Specifies the table to restore. |
|NewTableName |String |No |table2 |The new name of the table. Naming rules are as follows:<br><br><br>* The name must be unique.<br><br>* 2 to 64 characters in length.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* It cannot contain certain reserved words, including root and admin. Refer to the [List of forbidden keywords](https://apihub.bytedance.net/project/2544/branch/dev-1724929119/6313/66162) for forbidden reserved words. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=RestoreToExistedInstance&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "SourceDBInstanceId": "mysql-c8cfcccd****",
    "BackupId": "effc1de81b8a4c8e886fef2c3e06****",
    "RestoreType": "TABLE_LEVEL",
    "TableMeta": [
        {
            "DBName": "db",
            "NewDBName": "db_new",
            "Table": []
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023120412152879A7CDBA12D1A212B90D",
        "Action": "RestoreToExistedInstance",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
