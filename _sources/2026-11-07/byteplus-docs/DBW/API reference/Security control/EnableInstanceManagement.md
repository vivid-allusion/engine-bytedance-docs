---
title: "EnableInstanceManagement"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/EnableInstanceManagement"
---

Call the EnableInstanceManagement API to enable security control for the database instance.

<span id="bTZ0IWsz"></span>
## Request type

Synchronous request.

<span id="jmINQqZV"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Description** |**Sample** |
|---|---|---|---|---|
|InstanceId |String |Yes |Database instance ID. |mysql\-fcd3ad31\*\*\*\* |
|InstanceType |String |Yes |Database type. The following databases are supported:<br><br><br>* MySQL: RDS for MySQL<br><br>* VeDBMySQL: NDB for MySQL<br><br>* Postgres: RDS for PostgreSQL<br><br>* Mongo: Document Database for MongoDB<br><br>* MSSQL: RDS for SQL Server |MySQL |
|DBAUser |String<br><br> |Yes<br><br> |The User ID of the Instance DBA, that is, the value of UserId in DBAUser of the DescribeManagedUsers interface response.<br><br>For more information about resource roles, see [Role](https://docs.byteplus.com/en/docs/DBW/role-description). |2100067216 |
|OwnerUser |String |Yes |The User ID of the Instance owner, which is the value of UserId in OwnerUser in the response of the DescribeManagedUsers interface.<br><br>For more information about resource roles, see [Role](https://docs.byteplus.com/en/docs/DBW/role-description). |2100067216 |
|Account |String |Yes |Database account. |dbw_lx |
|Password |String |Yes |Database account password. |123qw\*\*\*\* |
|SecurityRuleId<br><br> |String |Yes |Security group ID, which is the ID value in the returned result of the DescribeSecurityGroups interface. |1740264867044012032 |
|ApprovalConfigId |String |Yes |The Approval workflow ID, which is the ConfigId value in the return result of the ListApprovalFlowConfig interface. |1811243361378508800 |
|Source |String |Yes |Data source. The default value of Volcengine data source is Volc. |Volc |


<span id="N5oWP2xy"></span>
## Response parameters

null

<span id="Fb3PFsfK"></span>
## Request example

```JSON
POST /?Action=EnableInstanceManagement&Version=2018-01-01 HTTP/1.1
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


<span id="6JYsuM30"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20250903172426275B961EBDB5F0CD51FA-70ecf4",
        "Action": "EnableInstanceManagement",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id="dsx4260J"></span>
## Error code

For more information, see [Error code](https://docs.byteplus.com/en/docs/DBW/error-codes).
