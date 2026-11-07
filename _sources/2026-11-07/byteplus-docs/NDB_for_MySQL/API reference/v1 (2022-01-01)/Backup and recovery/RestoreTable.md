---
title: "RestoreTable"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/RestoreTable"
---

Call the RestoreTable to restore the historical database and table of the instance to the original instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RestoreTable&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-dfaa2zic\*\*\*\* |The instance ID of the backup data. |
|BackupId |String |No |snap\-6511\*\*\*\*\-ce0d |Backup file ID. Call the [DescribeBackups](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeBackups) API to query the `BackupID`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Either this parameter or RestoreTime must be specified.</div><br> |
|RestoreTime |String |No |2023\-09\-19T07:21:09Z |Any point in time within the retention cycle of the instance backup, in the yyyy\-MM\-ddTHH:mm:ssZ format (UTC time). Call [DescribeRecoverableTime](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRecoverableTime) to query the recoverable time range for the instance backup.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You must specify either this parameter or the BackupId parameter.</div><br> |
|TableMeta |Array of [TableMetaObject](https://docs.byteplus.com/en/docs/265/57393#tablemetaobject) |Yes |See the request example. |Specifies the databases and tables information to restore during databases and tables recovery.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRecoverableTables">DescribeRecoverableTables</a> to view the recoverable databases and tables of the instance.</div><br> |


<span id="tablemetaobject"></span>
### TableMetaObject


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|DBName |String |Yes |testdb1 |The name of the target database to be restored. |
|NewDBName |String |Yes |testdb2 |The new database name after the restore.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><code>NewDBName</code> (new database name) cannot be the same as <code>DBName</code> (original database name), otherwise the databases and tables recovery will fail.</div><br> |
|Table |Array of [TableObject](https://docs.byteplus.com/en/docs/265/57393#tableobject) |No |See the request example. |Specifies the table in the database to restore.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If <code>Table</code> is empty, all tables in the specified database are restored.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The total number of entire databases and single tables that can be restored at a time cannot exceed 100.</div><br> |


<span id="tableobject"></span>
### TableObject


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|TableName |String |Yes |table1 |The name of the target table to restore. |
|NewTableName |String |Yes |table2 |The name of the new table after the restore. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=RestoreTable&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-dfaa2zic****",
    "BackupId": "snap-6511****-ce0d",
    "TableMeta": [
        {
            "DBName": "testdb3",
            "NewDBName": "testdb3",
            "Table": [
                {
                    "TableName": "auth_operation",
                    "NewTableName": "auth_operation1"
                }
            ]
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202309251609144398CF115AE2B9290462",
        "Action": "RestoreTable",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
