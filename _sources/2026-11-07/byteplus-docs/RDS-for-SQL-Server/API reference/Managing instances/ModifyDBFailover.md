---
title: "ModifyDBFailover"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifydbfailover"
---

Call the ModifyDBFailover interface to manually switch between master and standby nodes.

<span id="request-type"></span>
## request type

Synchronization request.

<span id="request-parameters"></span>
## request parameters


|**name** |**type** |**Is it required** |**sample value** |**describe** |
|---|---|---|---|---|
|InstanceId |String |Yes |mssql\-3373999a\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances </a>interface to query the instance ID.</div><br> |
|NodeId |String |Yes |mssql\-3373999a\*\*\*\*\-0 |Standby node ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances </a>interface to query the standby node ID.</div><br> |


<span id="return-parameters"></span>
## return parameters

null

<span id="request-example"></span>
## Request example

```sql
POST /?Action=ModifyDBFailover&Version=2022-01-01 HTTP/1.1 
Content-Type: application/json 
Host: rds-mssql.cn-beijing.byteplusapi.com.cn 
X-Date: 20230131T101010Z 
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458**** 
{ 
    "InstanceId":"mssql-3373999a****", 
    "NodeId":"mssql-3373999a****-0" 
}
```


<span id="back-to-example"></span>
## Back to example

```json
{ 
    "ResponseMetadata": { 
        "RequestId": "202505121136416A7BF07596FDEC2F4629-d8e5a7", 
        "Action": "ModifyDBFailover", 
        "Version": "2022-01-01", 
        "Service": "rds_mssql", 
        "Region": "cn-beijing" 
    }, 
    "Result": null 
}
```


<span id="error-code"></span>
## error code

For more details, see [Error Code ](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/error-codes).
