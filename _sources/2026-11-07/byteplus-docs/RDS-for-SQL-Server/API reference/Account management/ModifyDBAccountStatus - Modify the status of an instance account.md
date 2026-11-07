---
title: "ModifyDBAccountStatus - Modify the status of an instance account"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/ModifyDBAccountStatus_-_Modify_the_status_of_an_instance_account"
---

Call the ModifyDBAccountStatus operation to enable or disable an instance account.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span><span data-api-tag="require|VsHvUW">必选</span> `Example value: ModifyDBAccountStatus`

The operation to perform. The value is `ModifyDBAccountStatus`.



**Version** <span data-label="purple">string</span><span data-api-tag="require|ARK67M">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**InstanceId** <span data-label="purple">string</span><span data-api-tag="require|fuJ6Pw">必选</span> `Example value: mssql-abc****`

Instance ID.



**AccountName** <span data-label="purple">string</span><span data-api-tag="require|ixMUQZ">必选</span> `Example value: user1`

Account name.



**AccountStatus** <span data-label="purple">string</span> <span data-api-tag="require|HlhTQR">必选</span>`Example value: Enable`

Modify the account status to enabled or disabled. Possible values:


* `Enable`: Enable the account.

* `Disable`: Disable the account.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=ModifyDBAccountStatus&Version=2022-01-01 HTTP/1.1
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260112T123840Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260112/cn-beijing/rds_mssql/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "mssql-abc****",
  "AccountName": "user1",
  "AccountStatus": "Enable"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20260112203903021005048049******",
    "Action": "ModifyDBAccountStatus",
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
