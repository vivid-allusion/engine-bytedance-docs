---
title: "DisableInstanceManagement"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DisableInstanceManagement"
---

Call the DisableInstanceManagement API to disable security control.

<span id="9eDRyVVa"></span>
## Request type

Synchronous request.

<span id="L7RsTOVz"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Description** |**Sample** |
|---|---|---|---|---|
|InstanceId |String |Yes |Database instance ID |mysql\-fcd3ad31\*\*\*\* |
|InstanceType<br><br> |String |Yes |Database type: The database types currently supported are as follows:<br><br><br>* `MySQL`: RDS for MySQL<br><br>* `VeDBMySQL`: NDB for MySQL<br><br>* `Postgres`: Cloud Database PostgreSQL<br><br>* `Mongo`: Document Database for MongoDB<br><br>* `MSSQL`: RDS for SQL Server |MySQL<br><br> |
|PreCheck<br><br> |Bool |Yes<br><br> |Whether to verify the ticket status. The values are as follows:<br><br><br>* `true`: Only the ticket status is verified, and the security control will not be disabled.<br><br>* `false`: If the verification is passed, the security control will be directly disabled.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The verification fails when the ticket status is Not started, Pre\-checking, Approving, or Wait for execution, or In progress.</div><br> |true |
|Source |String |Yes |Data source. The default value is `Volc`. |Volc |


<span id="iOMqHer9"></span>
## Response parameters


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|StatusList |Object[] |The return result of disabling security control. |See the return example.<br><br> |


<span id="dbthItCR"></span>
## Request example

```JSON
POST /?Action=DisableInstanceManagement&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceType": "MySQL",
    "InstanceId": "mysql-fcd3ad31****",
    "Source": "Volc",
    "PreCheck": true
}
```


<span id="3n4UnN9f"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025090411191075168428392D2A0D1475-5da7a7",
        "Action": "DisableInstanceManagement",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "StatusList": [
            {
                "Disabled": true,
                "InstanceId": "mysql-fcd3ad31****",
                "InstanceType": "MySQL",
                "Reason": "None"
            }
        ]
    }
}
```


<span id="0oLXoYaF"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
