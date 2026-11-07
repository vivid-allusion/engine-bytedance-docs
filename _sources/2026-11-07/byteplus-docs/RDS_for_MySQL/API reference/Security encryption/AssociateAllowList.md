---
title: "AssociateAllowList"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/associateallowlist1"
---

Call the AssociateAllowList API to bind an allowlist.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceIds |String[] |Yes |["mysql\-668a3c88\*\*\*\*"] |The ID of the instance to be bound to the allowlist.<br><br>tip<br><br><br>* You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query basic information of all MySQL instances in the target region, including the instance ID.<br><br>* Supports passing multiple instance IDs at once, separated by commas (,). A maximum of 200 instance IDs can be passed in a single request.<br><br>* Does not support passing multiple instance IDs and allowlists simultaneously, meaning you can only either bind multiple instances to the same allowlist at once or bind one instance to multiple allowlists at a time. |
|AllowListIds |String[] |Yes |["acl\-c2402ba601374808aeb19d06acc2\*\*\*\*","acl\-b2a5bf3e471c433096232082c199\*\*\*\*"] |The ID of the allowlist to be bound to the instance.<br><br>tip<br><br><br>* You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) API to query all allowlist information in the specified region, including the allowlist ID.<br><br>* Supports passing multiple allowlist IDs at once, separated by commas (,). A maximum of 100 allowlist IDs can be passed in a single request.<br><br>* Does not support passing multiple instance IDs and allowlists simultaneously, meaning you can only either bind multiple instances to the same allowlist at once or bind one instance to multiple allowlists at a time. |

## Response parameters

null

## Sample request

```json
POST /?Action=AssociateAllowList&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceIds": [
        "mysql-668a3c88****"
    ],
    "AllowListIds": [
        "acl-63f61303c8ca430ebffb4eccd12d****",
        "acl-69482646126a48608062962e47c2****"
    ]
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220916164600010225243081008D****",
        "Action": "AssociateAllowList",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
