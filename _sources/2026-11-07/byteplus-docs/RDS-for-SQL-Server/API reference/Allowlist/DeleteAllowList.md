---
title: "DeleteAllowList"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DeleteAllowList"
---

Deletes an allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request Type

Sync request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-ba7e0e2ab5f04a9f94dc397a9\*\*\*\* |Allowlist ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeAllowLists">DescribeAllowLists</a> operation to view the allowlist ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

null

<span id=".6K-35rGC56S65L6L"></span>
## Request Example

```json
POST /?Action=DeleteAllowList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "AllowListId": "acl-ba7e0e2ab5f04a9f94dc397a9a******"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response Example

```json
{
    "ResponseMetadata": {
        "RequestId": "20250514173402BA0207B322DEED8433D2-bafab1",
        "Action": "DeleteAllowList",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Codes

For more information, see [Error Codes](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/error-codes).
