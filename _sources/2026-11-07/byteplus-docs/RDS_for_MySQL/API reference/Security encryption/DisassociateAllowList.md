---
title: "DisassociateAllowList"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/disassociateallowlist1"
---

Call the DisassociateAllowList API to unbind an allowlist.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceIds |String[] |Yes |["mysql\-e26822cf\*\*\*\*"] |The ID of the instance from which the allowlist is to be unbound.<br><br>tip<br><br><br>* You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query basic information of all MySQL instances in the target region, including the instance ID.<br><br>* Supports passing multiple instance IDs at once, allowing the unbinding of a single allowlist from multiple instances in a single call.<br><br>* Does not support passing multiple instance IDs and multiple allowlist IDs simultaneously. |
|AllowListIds |String[] |Yes |["acl\-c2402ba601374808aeb19d06acc2\*\*\*\*"] |The ID of the allowlist to be unbound from the instance.<br><br>tip<br><br><br>* You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) API to query all allowlist information in a specified region, including the allowlist ID.<br><br>* Supports passing multiple allowlist IDs at once, allowing the unbinding of multiple allowlists from an instance in a single call.<br><br>* Does not support passing multiple instance IDs and multiple allowlist IDs simultaneously. |

## Response parameters

null

## Sample request

```json
POST /?Action=DisassociateAllowList&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceIds": [
        "mysql-e26822cf****"
    ],
    "AllowListIds": [
        "acl-c2402ba601374808aeb19d06acc2****"
    ]
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202209161718320102252431180280****",
        "Action": "DisassociateAllowList",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
