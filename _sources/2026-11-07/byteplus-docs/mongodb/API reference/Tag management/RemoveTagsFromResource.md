---
title: "RemoveTagsFromResource"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/removetagsfromresource"
---

Call the RemoveTagsFromResource API to unbind tags for one or more instances.

## Request type

Asynchronous request.

## Precautions

* The RemoveTagsFromResource API is only supported when the instance status is **Running** (that is, in the return result of the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API, the value of `InstanceStatus` for the corresponding instance is `Running`). For more information about the instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* Repeatedly disassociating a tag will override the original result and update the tag value.

* An disassociated tag with no resources will be automatically deleted. For further instructions, refer to [Disassociating or deleting tag](https://docs.byteplus.com/en/docs/mongodb/disassociate-tag).

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceIds |String[] |Yes |["mongo\-shard\-011d2479\*\*\*\*"] |Instance IDs that need to be disassociated from tags.<br><br>tip<br><br><br>* You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs.<br><br>* Multiple instance IDs can be input at the same time, which are separated by commas (,). |
|TagKeys |String[] |No |[ "instancetype", "chargetype" ] |The tag keys to be deleted.<br><br>tip<br><br><br>* Multiple tag keys are supported to be passed in at one time, separated by commas (,). Up to 20 tag keys can be passed in simultaneously.<br><br>* If this parameter is left blank, it means no tags will be associated. |
|All |Boolean |No |false |Whether to disassociate all tags from the specified instance. The value range is as follows:<br><br><br>* `true`: Disassociate all tags from the specified instance.<br><br>* `false` (default): Do not Disassociate all tags from the specified instance.<br><br><br>tip<br><br>The `All` parameter takes effect only when the value of `TagKeys` is empty. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=RemoveTagsFromResource&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceIds": [
        "mongo-replica-36ce163c****"
    ],
    "TagKeys": [
        "instancetype",
        "chargetype"
    ]
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20221213111508C0FBF6787D2E6500****",
        "Action": "RemoveTagsFromResource",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
