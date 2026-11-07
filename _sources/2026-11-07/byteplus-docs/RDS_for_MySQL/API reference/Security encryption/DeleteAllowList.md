---
title: "DeleteAllowList"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleteallowlist1"
---

Call the DeleteAllowList API to delete an allowlist.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-c2402ba601374808aeb19d06acc2\*\*\*\* |The allowlist ID.<br><br>tip<br><br>You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) API to query all allowlist information in the specified region, including the allowlist ID. |
|ProjectName |String |No |default |The project to which it belongs.<br><br>tip<br><br>If the AK/SK used to call the API belongs to a sub\-account that only has permissions for a specific project, this request parameter needs to be passed. |

## Response parameters

null

## Sample request

```json
POST /?Action=DeleteAllowList&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "AllowListId": "acl-c2402ba601374808aeb19d06acc2****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2022091617331801022509900806A5****",
        "Action": "DeleteAllowList",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
