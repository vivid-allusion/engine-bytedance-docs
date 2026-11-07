---
title: "AddTagsToResource"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/addtagstoresource"
---

Call the AddTagsToResource API to associate tags to the target MongoDB instance.

## Request type

Asynchronous request.

## Precautions

* The AddTagsToResource API is only supported when the instance status is **Running** (that is, in the return result of the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API, the `InstanceStatus` value of the corresponding instance is `Running`). For more information about the instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* When setting tags, the tag key (Key) and the tag value (Key) need to meet certain rules. For detailed information, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/mongodb/associate-tag#.5qCH562-6K6-572u6KeE5YiZ).

* The tag keys of multiple tags under the same instance cannot be repeated, and each tag key can only have one tag value.

* If the newly bound tag key coincides with the tag key already bound to the instance, the new tag value will overwrite the original tag value. Please operate with caution. For more instructions, refer to [Associating or adding tag](https://docs.byteplus.com/en/docs/mongodb/associate-tag).

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceIds |String[] |Yes |["mongo\-shard\-011d2479\*\*\*\*"] |Instance IDs that need to be bound to tags.<br><br>tip<br><br><br>* You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs.<br><br>* Multiple instance IDs can be input at the same time, which are separated by commas (,). A maximum of 20 instance IDs can be input at the same time. |
|Tags |Object[] |Yes | |An array object of tag keys and tag values to be associated. |
|Key |String |Yes |instancetype |The tag key corresponding to the tag needs to be associated with.<br><br>tip<br><br><br>* When associating tags with an instance, the tag key (Key) is required, and the tag value (Value) is optional. Not filling in the tag value means that the tag value corresponding to the tag key is empty.<br><br>* Supports passing in multiple sets of tag key\-value objects at a time, with multiple sets of tag key\-value objects separated by English commas (,). Up to 20 sets of tag key\-value pairs can be passed in at the same time.<br><br>* A single instance can be associated with a maximum of 50 tags. The tag key must meet the setting rules. For specific rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/mongodb/associate-tag#.5qCH562-6K6-572u6KeE5YiZ). |
|Value |String |No |replica |The tag value corresponding to the tag needs to be associated with.<br><br>tip<br><br><br>* When associating tags with an instance, the tag key (Key) is required, and the tag value (Value) is optional. Not filling in the tag value means that the tag value corresponding to the tag key is empty.<br><br>* It is supported to pass in multiple sets of tag key\-value objects at a time, and multiple sets of tag key\-value objects are separated by English commas (,). Up to 20 sets of tag key\-value pairs can be passed in at the same time.<br><br>* A single instance can be associated with up to 50 tags. The tag key needs to meet the setting rules. For specific rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/mongodb/associate-tag#.5qCH562-6K6-572u6KeE5YiZ). |

## Response parameters

The current API has no specified response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Request sample

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=AddTagsToResource&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceIds": [
        "mongo-replica-36ce163c****"
    ],
    "Tags": [
        {
            "Key": "instancetype",
            "Value": "shard"
        },
        {
            "Key": "chargetype",
            "Value": "prepaid"
        }
    ]
}
```

## Response sample

```json
{
    "ResponseMetadata": {
        "RequestId": "202212091735327549DDD37A541ADE****",
        "Action": "AddTagsToResource",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
