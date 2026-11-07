---
title: "DeleteBackup"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deletebackup"
---

Call the DeleteBackup interface to delete the backup file of the RDS for SQL Server instance.

<span id="request-type"></span>
## request type

Synchronization request.

<span id="request-parameters"></span>
## request parameters


|**name** |**type** |**Is it required** |**sample value** |**describe** |
|---|---|---|---|---|
|InstanceId |String |Yes |mssql\-bbe31c86\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> interface to query the instance ID.</div><br> |
|BackupId |String |Yes |8862c436c2bd401684a30da3dfed\*\*\*\* |Backup ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackups">DescribeBackups</a> interface to query the backup ID.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Deleting backups when <code>CreateType</code> is <code>System</code> is not supported.</div><br> |


<span id="return-parameters"></span>
## return parameters


|**name** |**type** |**sample value** |**describe** |
|---|---|---|---|
|BackupId |String |ca155ac99fcb4eed86617041bfe0\*\*\*\* |Backup task ID. |
|InstanceId |String |mssql\-1be522b5\*\*\*\* |Instance ID. |


<span id="request-example"></span>
## Request example

```json
POST /?Action=DeleteBackup&Version=2022-01-01 HTTP/1.1 
Content-Type: application/json 
Host: rds-mssql.cn-beijing.byteplusapi.com.cn 
X-Date: 20230131T101010Z 
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458**** 

{ 
    "InstanceId":"mssql-bbe31c86****", 
    "BackupId":"8862c436c2bd401684a30da3dfedb6d7" 
}
```


<span id="back-to-example"></span>
## Back to example

```json
{ 
    "ResponseMetadata": { 
        "RequestId": "20230823161820C950B0CCB0F1175BFD5F", 
        "Action": "DeleteBackup", 
        "Version": "2022-01-01", 
        "Service": "rds_mssql", 
        "Region": "cn-beijing" 
    }, 
    "Result": { 
        "BackupId": "2198ffde72d44d0ea9a5a465eb2e****", 
        "InstanceId":"mssql-1be522b5****" 
    } 
}
```


<span id="error-code"></span>
## **error code**

For more details, see [Error Code](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/error-codes).
