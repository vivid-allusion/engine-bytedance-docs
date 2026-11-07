---
title: "ModifyDBInstanceName - Modify instance name"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifydbinstancename"
---

Call the ModifyDBInstanceName API to modify the instance name.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Example value: ModifyDBInstanceName`

The action to perform. Set the value to `ModifyDBInstanceName`.



**Version ** <span data-label="purple">string   </span>`Example value: 2022-01-01`

The API version is `2022-01-01`.



**InstanceId ** <span data-label="purple">string   </span>`Example value: mssql-dab1be87****`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the instance ID.</div>




**InstanceNewName ** <span data-label="purple">string   </span>`Example value: name123`

Instance name. The naming rules for the instance name are as follows:


* Cannot start with digits or hyphen (\-).

* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).

* The length must be between 1 and 128 characters.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=ModifyDBInstanceName&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId":"mssql-dab1be87****",
    "InstanceNewName":"name123"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202505121136416A7BF07596FDEC2F4629-d8e5a7",
        "Action": "ModifyDBInstanceName",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the error codes related to the business logic for this API. For common error codes, see the [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value for parameter {parameter1} is invalid. |
