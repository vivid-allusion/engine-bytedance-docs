---
title: "DisassociateAllowList - Disassociate an instance from an allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DisAssociateAllowList"
---

Call the DisassociateAllowList API to disassociate an instance from an allowlist.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|CvFgIV">必选</span> `Example value: DisassociateAllowList`

The operation to perform. The value is DisassociateAllowList.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|I7tG7s">必选</span> `Example value: 2022-01-01`

The API version is 2022\-01\-01.



**InstanceIds ** <span data-label="purple">string[] </span><span data-api-tag="require|TkyPYR">必选</span> `Example value: ["mssql-bf173671********", "mssql-37e2ccd4****" ]`

A list of Instance IDs.



**AllowListIds ** <span data-label="purple">string[] </span><span data-api-tag="require|6ofk9J">必选</span> `Example value: ["acl-ba7e0e2ab5f04a9f94dc397**********"]`

The ID of the allowlist from which to disassociate an instance.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DisassociateAllowList&Version=2022-01-01 HTTP/1.1
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251117T072449Z
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
    "RequestId": "2025111715245924402409308406AB28",
    "Action": "DisassociateAllowList",
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
