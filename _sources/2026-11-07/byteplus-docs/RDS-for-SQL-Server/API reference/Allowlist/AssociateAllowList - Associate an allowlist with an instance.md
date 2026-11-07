---
title: "AssociateAllowList - Associate an allowlist with an instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/AssociateAllowList"
---

Call the AssociateAllowList API to associate an allowlist with an instance.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|mwY3iW">必选</span> `Example value: AssociateAllowList`

The operation to perform. The value is `AssociateAllowList`.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|1TzRgJ">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**InstanceIds ** <span data-label="purple">string[] </span><span data-api-tag="require|C0iF5G">必选</span> `Example: [\"mssql-dab1be87****\"]`

A list of instance IDs.



**AllowListIds ** <span data-label="purple">string[] </span><span data-api-tag="require|weonG0">必选</span> `Example: [\"acl-04908986ad034ac0ba1fb1e3a754****\"]`

The ID of the allowlist to be associated with the instance.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=AssociateAllowList&Version=2022-01-01 HTTP/1.1
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251117T073549Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251117/cn-beijing/rds_mssql/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceIds": [
    "mssql-dab1be87****"
  ],
  "AllowListIds": [
    "acl-04908986ad034ac0ba1fb1e3a754****"
  ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20251117154128157065073169F24FD8",
    "Action": "AssociateAllowList",
    "Version": "2022-01-01",
    "Service": "rds_mssql",
    "Region": "cn-beijing"
  },
  "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |
