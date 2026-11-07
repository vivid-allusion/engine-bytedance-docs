---
title: "RevokeDBAccountPrivilege - Revoke account privileges"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/RevokeDBAccountPrivilege_-_Revoke_account_privileges"
---

Call the RevokeDBAccountPrivilege operation to revoke privileges from a database account.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span><span data-api-tag="require|xN4eaf">必选</span> `Example value: RevokeDBAccountPrivilege`

The operation to perform. The value is `RevokeDBAccountPrivilege`.



**Version** <span data-label="purple">string</span><span data-api-tag="require|jzwuT9">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**InstanceId** <span data-label="purple">string</span><span data-api-tag="require|aHd908">必选</span> `Example: mssql-64504b******`

Instance ID.



**AccountName** <span data-label="purple">string</span><span data-api-tag="require|b4RQmt">必选</span> `Example: test_user`

Account name.



**DBNames** <span data-label="purple">string</span><span data-api-tag="require|BZ5FP2">必选</span>  `Example value: test_db`

Database name.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action= RevokeDBAccountPrivilege&Version=2022-01-01 HTTP/1.1
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260112T123840Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260112/cn-beijing/rds_mssql/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
{
  "InstanceId": "mssql-64504b******",
  "AccountName": "test_user",
  "DBNames": "test_db"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20260204213323C4262FA002D639665E39-******",
        "Action": "RevokeDBAccountPrivilege",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |
