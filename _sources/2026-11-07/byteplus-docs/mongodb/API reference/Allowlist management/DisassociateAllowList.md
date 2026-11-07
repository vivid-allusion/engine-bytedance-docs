---
title: "DisassociateAllowList"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/disassociateallowlist"
---

Call the DisassociateAllowList API to disassociate the target MongoDB instance from the specified IP allowlist.

## Request type

Asynchronous request.

## Precautions

After an allowlist is disassociated from an instance, all devices in the allowlist cannot access the instance. Ensure that the IP addresses of devices that still need to access the instance are added to other allowlists of the instance.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AllowListIds |String[] |Yes |["acl\-c2402ba601374808aeb19d06acc2\*\*\*\*"] |Allowlist IDs that need to be disassociated from the instance.<br><br>tip<br><br><br>* You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) API to query the information about all allowlists under the specified region, including allowlist IDs.<br><br>* Multiple allowlist IDs can be input at the same time, which are separated by commas (,).<br><br>* Multiple instance IDs and allowlists cannot be input at the same time, i.e., you can only disassociated multiple instances from the same allowlist at the same time or disassociated one instance from multiple allowlists. |
|InstanceIds |String[] |Yes |["mongo\-shard\-011d2479\*\*\*\*"] |Instance IDs that need to be disassociated from the allowlist.<br><br>tip<br><br><br>* You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs.<br><br>* Multiple instance IDs can be input at the same time, which are separated by commas (,).<br><br>* Multiple instance IDs and allowlists cannot be input at the same time, i.e., you can only disassociated multiple instances from the same allowlist at the same time or disassociated one instance from multiple allowlists. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DisassociateAllowList&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceIds": [
        "mongo-shard-011d2479****"
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
        "RequestId": "202203161718320102252431180280****",
        "Action": "DisassociateAllowList",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
