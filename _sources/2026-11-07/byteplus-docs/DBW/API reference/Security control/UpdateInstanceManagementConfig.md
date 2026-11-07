---
title: "UpdateInstanceManagementConfig"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/UpdateInstanceManagementConfig"
---

Call the UpdateInstanceManagementConfig API to modify security control information.

<span id="qSREdPyF"></span>
## Request type

Synchronous request

<span id="oAlCdUFL"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Description** |**Sample** |
|---|---|---|---|---|
|InstanceId |String |Yes |Database instance ID |mysql\-fcd3ad31\*\*\*\* |
|InstanceType |String |Yes |Database type. The following databases are supported:<br><br><br>* `MySQL`: RDS for MySQL<br><br>* `VeDBMySQL`: NDB for MySQL<br><br>* `Postgres`: Cloud Database PostgreSQL<br><br>* `Mongo`: Document Database for MongoDB<br><br>* `MSSQL`: RDS for SQL Server |MySQL |
|DBAUser |String<br><br> |Yes<br><br> |The User ID of the Instance DBA, that is, the value of `UserId` in `DBAUser` of the [DescribeManagedUsers](https://docs.byteplus.com/en/docs/DBW/DescribeManagedUsers?lang=en) interface response.<br><br>For more information about resource roles, see [Role](https://docs.byteplus.com/en/docs/DBW/role-description). |2100067216 |
|OwnerUser |String |Yes |The User ID of the Instance owner, which is the value of `UserId` in `OwnerUser` in the response of the [DescribeManagedUsers](https://docs.byteplus.com/en/docs/DBW/DescribeManagedUsers?lang=en) interface.<br><br>For more information about resource roles, see [Role](https://docs.byteplus.com/en/docs/DBW/role-description). |2100067216 |
|Source |String |Yes |Data source: The default value is `Volc`. |Volc |
|Account |String |No |Database account. |dbw_lx |
|Password |String |No |Database password. |123qw\*\*\*\* |
|SecurityRuleId |String |No |Security group ID: The `ID` value in the result returned by the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/DBW/DescribeSecurityGroups?lang=en) API. |1740264867044012032 |
|ApprovalConfigId |String |No |Approval workflow ID, which is the `ConfigId` value in the result returned by the [ListApprovalFlowConfig](https://docs.byteplus.com/en/docs/DBW/ListApprovalFlowConfig?lang=en) interface. |1811243361378508800 |


<span id="DHP8ENDs"></span>
## Response parameters

null

<span id="36Eav8BW"></span>
## Request example

```JSON
POST /?Action=UpdateInstanceManagementConfig&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "mysql-fcd3ad31****",
    "InstanceType": "MySQL",
    "DBAUser": "2100067216",
    "OwnerUser": "2100067216",
    "Account": "dbw_lx",
    "Password": "123qw****",
    "SecurityRuleId": "1740264867044012032",
    "ApprovalConfigId": "1811243361378508800",
    "Source": "Volc"
}
```


<span id="GCIIJYmZ"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025090411153116DD9869FCC91A118381-273c02",
        "Action": "UpdateInstanceManagementConfig",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id="wKjR5Gvu"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
