---
title: "DescribeDBAccounts - Query accounts"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeDBAccounts_-_Query_accounts"
---

Call the DescribeDBAccounts API to query database accounts.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span><span data-api-tag="require|fUQtJM">必选</span> `Example value: DescribeDBAccounts`

The operation to perform. The value is `DescribeDBAccounts`.



**Version** <span data-label="purple">string</span><span data-api-tag="require|0QE6YV">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**InstanceId** <span data-label="purple">string</span><span data-api-tag="require|j5z3km">必选</span> `Example: mssql-64504b******`

Instance ID.



**AccountName ** <span data-label="purple">string </span>`Optional` `Example value: test_user`

Account name.



**PageSize ** <span data-label="purple">string </span>`Optional` `Example value: 10`

Page size.



**PageNumber ** <span data-label="purple">string </span>`Optional` `Example value: 1`

Number of pages.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, refer to [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Total ** <span data-label="purple">integer </span>`Example value: 4`

Total number of accounts.



**Account ** <span data-label="purple">object[] </span>`Example value: [ { "AccountName": "test", "AccountPrivileges": [], "AccountStatus": "Available", "AccountType": "Super" } ]`

Account information.


**AccountName ** <span data-label="purple">string </span>`Example value: test`

Account name.



**AccountType ** <span data-label="purple">string </span>`Example value: Normal`

Account type. Possible values:


* `Normal`: Normal account.

* `Super`: Super account.



**AccountStatus ** <span data-label="purple">string </span>`Example value: Available`

Account status. Possible values:


* `Available`: The status is available.

* `Unavailable`: The status is unavailable.



**AccountPrivileges ** <span data-label="purple">object[] </span>`Example value: [ { "AccountPrivilege": "DBOwner", "AccountPrivilegeDetail": "db_owner", "DBName": "testaaaa" } ]`

Account permission information.


**DBName ** <span data-label="purple">string </span>`Example: test_db`

Database name.



**AccountPrivilege ** <span data-label="purple">string </span>`Example: DBOwner`

Permission type. Possible values:


* `DBOwner`: Database owner permission. Grants full management and operational permissions for the database.

* `ReadWrite`: The read and write permission, which supports data query, insertion, update, and deletion operations.

* `ReadOnly`: Read Only permission. Allows querying data only. Writing, modifying, and deleting operations are prohibited.



**AccountPrivilegeDetail ** <span data-label="purple">string </span>`Example value: db_owner`

Account permission details.





<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action= DescribeDBAccounts&Version=2022-01-01 HTTP/1.1
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260112T123840Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260112/cn-beijing/rds_mssql/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
{
    "InstanceId":"mssql-******"   
    "PageSize":10,
    "PageNumber":1,
    
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260204175745FC249218BE5A4533EC0A-******",
        "Action": "DescribeDBAccounts",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Account": [
            {
                "AccountName": "userA",
                "AccountPrivileges": [
                    {
                        "AccountPrivilege": "DBOwner",
                        "AccountPrivilegeDetail": "db_owner",
                        "DBName": "testaaaa"
                    }
                ],
                "AccountStatus": "Available",
                "AccountType": "Super"
            },
            {
                "AccountName": "test",
                "AccountPrivileges": [],
                "AccountStatus": "Available",
                "AccountType": "Normal"
            }
        ],
        "Total": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |
