---
title: "RestartDBInstance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/restartdbinstance"
---

Call the RestartDBInstance interface to restart the instance.

<span id="request-type"></span>
## request type

Synchronization request.

<span id="request-parameters"></span>
## request parameters


|**name** |**type** |**Is it required** |**sample value** |**describe** |
|---|---|---|---|---|
|InstanceId |String |Yes |mssql\-dab1be87\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances </a>interface to query the instance ID.</div><br> |


<span id="return-parameters"></span>
## return parameters

null

<span id="request-example"></span>
## Request example

```json
POST /?Action=RestartDBInstance&Version=2022-01-01 HTTP/1.1 
Content-Type: application/json 
Host: rds-mssql.cn-beijing.byteplusapi.com.cn 
X-Date: 20230131T101010Z 
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458**** 
{ 
    "InstanceId": "mssql-dab1be87****" 
}
```


<span id="back-to-example"></span>
## Back to example

```json
{ 
    "ResponseMetadata": { 
        "RequestId": "202409121945533F5BF46BC9700311825D-35381b", 
        "Action": "RestartDBInstance", 
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
