---
title: "ResetDBAccount - Reset a database account password"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/ResetDBAccount_-_Reset_a_database_account_password"
---

Call the ResetDBAccount operation to reset a database account password.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span><span data-api-tag="require|8t94LO">必选</span> `Example value: ResetDBAccount`

The operation to be performed. The value is `ResetDBAccount`.



**Version** <span data-label="purple">string</span><span data-api-tag="require|cv9Tci">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**InstanceId** <span data-label="purple">string</span><span data-api-tag="require|AuouDs">必选</span> `Example: mssql-64504b******`

Instance ID.



**AccountName** <span data-label="purple">string</span><span data-api-tag="require|rUbNlx">必选</span> `Example: test_user`

Account name.



**AccountPassword** <span data-label="purple">string</span><span data-api-tag="require|fR01Um">必选</span> `Example value: Pass******`

Account password.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action= ResetDBAccount&Version=2022-01-01 HTTP/1.1
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260112T123840Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260112/cn-beijing/rds_mssql/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
    "InstanceId": "mssql-******",
    "AccountName": "test_user",
    "AccountPassword": "Pass******"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026020422375360E7756251CA49B3614F-******",
        "Action": "ResetDBAccount",
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
|400 |OperationFailed |Opration Failed: %s |Operation failed: |
|403 |InstanceStatusNotSupported |The current operation is unsupported because the instance status is Recycled. |The instance status does not support the current operation. |
|404 |InstanceNotFound |Instance not found. |Instance not found. |
