---
title: "DescribeRecoverableTables"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRecoverableTables"
---

Call the DescribeRecoverableTables to query the recoverable libraries and tables of the instance.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-6jvx8d7w\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|BackupId |String |No |snap\-63f4\*\*\*\*\-8dff |Backup file ID. Call the [DescribeBackups](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeBackups) API to query the `BackupID`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Either this parameter or the <code>RestoreTime</code> parameter is required.</div><br> |
|RestoreTime |String |No |2023\-05\-09T15:07:25Z |Any point in time within the retention cycle of the instance backup, in the yyyy\-MM\-ddTHH:mm:ssZ format (UTC time). Call [DescribeRecoverableTime](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRecoverableTime) to query the recoverable time range for the instance backup.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You must specify either this parameter or the <code>BackupId</code> parameter.</div><br> |
|DBName |String |No |db_test |Database name.<br><br><br>* If this parameter is specified, the system returns all restorable tables in the specified database.<br><br>* If this parameter is not specified, the system returns a list of restorable databases. |
|PageSize |Integer |Yes |1000 |Number of records per page. The value ranges from 1 to 1,000. |
|PageNumber |Integer |Yes |1 |The page number must be greater than or equal to 1 and must not exceed the maximum value of an integer. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DBTableInfos |Array of [DBTableInfoObject](https://docs.byteplus.com/en/docs/265/57392#dbtableinfoobject) |Refer to the return example. |Restorable database and table information for the instance. |


<span id="dbtableinfoobject"></span>
### DBTableInfoObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Database |String |test_db |Database name. |
|Tables |Array of String |["table1","table2","table3"] |Table information for the specified database. |
|DatabaseRecoverable |Boolean |true |Whether the entire database can be restored. Valid values:<br><br><br>* `true`: the entire database can be restored.<br><br>* `false`: at least one table in the target database cannot be restored. |
|TablesInfo |JSON Map |{"table6": {"TableRecoverable": false}，"table7": {"TableRecoverable": false}} |Information about the tables that cannot be restored in the target database.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is returned when the <code>DatabaseRecoverable</code> parameter is set to <code>false</code>.</div><br> |


<span id="tablesinfo"></span>
### TablesInfo


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TableRecoverable |Boolean |false |Indicates whether the target table is restorable. The value is fixed to `false`, meaning the table cannot be restored. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Request example 1

```JSON
POST /?Action=DescribeRecoverableTables&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20230828T084117Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkOD******/20230828/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c87******
{
    "InstanceId":"vedbm-dfaa2zic****",
    "RestoreTime":"2023-09-25T08:18:10Z",
    "PageSize":1000,
    "PageNumber":1,
    "DBName":"testdb1"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example 1

Specify the `DBName` parameter

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023092516270861B6A9D5989B6B1DA2E8",
        "Action": "DescribeRecoverableTables",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "DBTableInfos": [
            {
                "Database": "testdb3",
                "DatabaseRecoverable": false,
                "Tables": [
                    "table1",
                    "table2",
                    "table3",
                    "table4",
                    "table5"
                ],
                "TablesInfo": {
                    "table6": {
                        "TableRecoverable": false
                    },
                    "table7": {
                        "TableRecoverable": false
                    },
                    "table8": {
                        "TableRecoverable": false
                    }
                }
            }
        ]
    }
}
```


<span id=".6K-35rGC56S65L6LLTI="></span>
### Request example 2

```JSON
POST /?Action=DescribeRecoverableTables&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId":"vedbm-dfaa2zic****",
    "RestoreTime":"2023-09-25T08:18:10Z",
    "PageSize":1000,
    "PageNumber":1,
    "DBName":"testdb1"
}
```


<span id=".6L-U5Zue56S65L6LLTI="></span>
### Response example 2

Do not specify the `DBName` parameter

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023092516262161B6A9D5989B6B1D87DC",
        "Action": "DescribeRecoverableTables",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "DBTableInfos": [
            {
                "Database": "testdb1",
                "DatabaseRecoverable": true
            },
            {
                "Database": "testdb2",
                          "DatabaseRecoverable": true
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
