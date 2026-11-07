---
title: "ModifyBackupPolicy"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifybackuppolicy"
---

Call the ModifyBackupPolicy interface to modify the automatic backup policy of the RDS for SQL Server instance, such as the backup cycle, backup execution time window, and so on.

<span id="request-type"></span>
## request type

Synchronization request.

<span id="request-parameters"></span>
## request parameters


|**name** |**type** |**Is it required** |**sample value** |**describe** |
|---|---|---|---|---|
|InstanceId |String |Yes |mssql\-bbe31c86\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> interface to query the instance ID.</div><br> |
|BackupTime |String |Yes |19:00Z\-20:00Z |The time window to start executing the backup task, with an interval of 1 hour. Format: HH: mmZ\-HH: mmZ (UTC time). |
|FullBackupPeriod |String |Yes |Monday,Wednesday |Full backup cycle. Multiple values are separated by English commas (,). The values are as follows:<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday. |
|BackupRetentionPeriod |Integer |Yes |7 |Data backup retention days, value: 7 to 30. |


<span id="return-parameters"></span>
## return parameters


|**name** |**type** |**sample value** |**describe** |
|---|---|---|---|
|InstanceId |String |mssql\-1be522b5\*\*\*\* |Instance ID. |


<span id="request-example"></span>
## Request example

```json
POST /?Action=ModifyBackupPolicy&Version=2022-01-01 HTTP/1.1 
Content-Type: application/json 
Host: rds-mssql.cn-beijing.byteplusapi.com.cn 
X-Date: 20230131T101010Z 
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458**** 

{ 
    "InstanceId":"mssql-bbe31c86d8ed", 
    "BackupTime":"19:00Z-20:00Z", 
    "FullBackupPeriod": "Monday,Wednesday", 
    "BackupRetentionPeriod":8 
}
```


<span id="back-to-example"></span>
## Back to example

```json
{ 
    "ResponseMetadata": { 
        "RequestId": "20230823161820C950B0CCB0F1175BFD5F", 
        "Action": "ModifyBackupPolicy", 
        "Version": "2022-01-01", 
        "Service": "rds_mssql", 
        "Region": "cn-beijing" 
    }, 
    "Result": { 
        "InstanceId":"mssql-1be522b5****" 
    } 
}
```


<span id="error-code"></span>
## **error code**

For more details, see [Error Code](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/error-codes).
