---
title: "DeleteAllowList"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/deleteallowlist"
---

Call the DeleteAllowList API to delete the target allowlist.

## Request type

Asynchronous request.

## Precautions

The allowlist can be deleted only after all the instances in the target allowlist are disassociated from it. You can call the [DisassociateAllowList](https://docs.byteplus.com/en/docs/mongodb/disassociateallowlist) API to disassociate an instance from the allowlist.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-c2402ba601374808aeb19d06acc2\*\*\*\* |Allowlist ID.<br><br>tip<br><br>You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) API to query the information of all allowlists in a specified region, including the allowlist ID. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DeleteAllowList&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "AllowListId": "acl-c2402ba601374808aeb19d06acc2****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2022031617331801022509900806A5****",
        "Action": "DeleteAllowList",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
