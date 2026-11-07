---
title: "CreateDBAccount - Create an account"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/CreateDBAccount_-_Create_an_account"
---

Call the CreateDBAccount API to create a database account.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span><span data-api-tag="require|XnMPhF">必选</span> `Example value: CreateDBAccount`

The action to be performed. The value is `CreateDBAccount`.



**Version** <span data-label="purple">string</span><span data-api-tag="require|SfPGjk">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**AccountPrivileges ** <span data-label="purple">object[] </span>`Optional` `Example: [ { "AccountPrivilege": "DBOwner", "AccountPrivilegeDetail": "db_owner", "DBName": "testaaaa" } ]`

Account permissions.


**DBName** <span data-label="purple">string</span><span data-api-tag="require|WQ2Joz">必选</span> `Example value: test_db`

Database name.



**AccountPrivilege** <span data-label="purple">string</span><span data-api-tag="require|tMYPSC">必选</span> `Example value: DBOwner`

Permission type. Possible values:


* `DBOwner`: Database owner permission. Grants full management and operational permissions for the database.

* `ReadWrite`: The read and write permission, which supports data query, insertion, update, and deletion operations.

* `ReadOnly`: Read Only permission. Allows querying data only. Writing, modifying, and deleting operations are prohibited.



**AccountPrivilegeDetail ** <span data-label="purple">string </span>`Optional` `Example: db_owner`

Account permission details.




**InstanceId** <span data-label="purple">string</span><span data-api-tag="require|quIZqn">必选</span> `Example value: mssql-c913e4******`

Instance ID.



**AccountName** <span data-label="purple">string</span> <span data-api-tag="require|rcT3ds">必选</span>`Example: test_user`

Account name.



**AccountPassword** <span data-label="purple">string</span><span data-api-tag="require|LPv1mO">必选</span> `Example: Pass*******`

Account password.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=CreateDBAccount&Version=2022-01-01 HTTP/1.1
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260313T075938Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260313/cn-beijing/rds_mssql/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "mssql-c913e4******",
  "AccountName": "test_user",
  "AccountPassword": "Pass******"
  "AccountPrivileges": [
                    {
                        "AccountPrivilege": "DBOwner",
                        "AccountPrivilegeDetail": "db_owner",
                        "DBName": "test"
                    }
]
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2026031315574523824CBD482A655AA586-******",
        "Action": "CreateDBAccount",
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
|400 |OperationFailed |Opration Failed: %s |Operation failed: |
