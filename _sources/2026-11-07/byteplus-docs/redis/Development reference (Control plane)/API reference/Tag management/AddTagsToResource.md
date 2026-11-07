---
title: "AddTagsToResource"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/addtagstoresource"
---

Call the AddTagsToResource API to associate tags with target Redis instance.

## Request type

Asynchronous request.

## Precautions

* The AddTagsToResource API is only supported when the instance status is **Running** (that is, in the return result of the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API, the `Status` value of the corresponding instance is `Running` ). For more information about the instance status, refer to [Instance Status](https://docs.byteplus.com/en/docs/redis/instance-status).

* When setting tags, the tag key (Key) and tag value (Key) must meet certain rules. For details, see [Tag setting rules](https://docs.byteplus.com/en/docs/redis/associate-tag#.5qCH562-6K6-572u6KeE5YiZ).

* Each tag key must be unique for instance, and can have only one tag value.

* If the key of a newly added tag is the same as a tag key already associated with instance, the new tag value will overwrite the original one. Proceed with caution. For more details, see [Associating or adding tags](https://docs.byteplus.com/en/docs/redis/associate-tag).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=AddTagsToResource&serviceCode=Redis&version=2020-12-07&groupName=标签管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |[<br><br>"redis\-cn0212gzmh2xs\*\*\*\*"<br><br>] |The ID of the instance to add a tag to.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br><br><br>* > Supports passing in multiple instance IDs at once. You can pass a maximum of 20 instance IDs.<br> |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/55/12468#tagobject) |Yes |Refer to the sample request. |An array object of tag keys and tag values to be bound. |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

### TagObject

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |department |The tag key to be associated.<br><br>> **tip**<br><br><br><br>* > When associating tags with an instance, the tag key (Key) is required, and the tag value (Value) is optional. If the tag value is not provided, the tag value for the corresponding tag key will be empty.<br><br><br>* > Supports passing in multiple sets of tag key\-value pairs at once. You can specify up to 20 sets of tag key\-value pairs at a time.<br><br><br>* > Each instance can be associated with up to 50 tags. Tag keys must comply with the setting rules. For details, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/redis/associate-tag#.5qCH562-6K6-572u6KeE5YiZ).<br> |
|Value |String |No |game |The tag value corresponding to the tag to be bound.<br><br>> **tip**<br><br><br><br>* > When associating tags with an instance, the tag key is required, while the tag value is optional. Leaving the tag value blank means the tag value for the corresponding tag key is empty.<br><br><br>* > Supports passing in multiple sets of tag key\-value pairs at once. You can specify up to 20 sets of tag key\-value pairs at a time.<br><br><br>* > Each instance can be associated with up to 50 tags. Tag values must comply with the setting rules. For details, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/redis/associate-tag#.5qCH562-6K6-572u6KeE5YiZ).<br> |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=AddTagsToResource&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceIds":[
        "redis-cn0212gzmh2xs****"
    ],
    "Tags":[
        {
            "Key":"department",
            "Value":"game"
        },
        {
            "Key":"chargetype",
            "Value":"prepaid"
        }
    ]
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022041515420801021204201917601111",
          "Action": "AddTagsToResource",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
