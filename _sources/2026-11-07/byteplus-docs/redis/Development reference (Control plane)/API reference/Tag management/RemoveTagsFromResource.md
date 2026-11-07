---
title: "RemoveTagsFromResource"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/removetagsfromresource"
---

Call the RemoveTagsFromResource API to disassociate tags for one or more instances.

## Request type

Asynchronous request.

## Precautions

* The RemoveTagsFromResource API is only supported when the instance status is **Running** (that is, in the return result of the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API, the `Status` value of the corresponding instance is `Running` ). For more information about the instance status, refer to [Instance Status](https://docs.byteplus.com/en/docs/redis/instance-status).

* Repeatedly disassociating tags overwrites the original result, and the tag value will be updated.

* After tags are disassociated, if the number of resources associated with that tag is zero, it will be automatically deleted. For more details, see [Disassociating or deleting tag](https://docs.byteplus.com/en/docs/redis/disassociate-tag).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=RemoveTagsFromResource&serviceCode=Redis&version=2020-12-07&groupName=标签管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["redis\-cn0212gzmh2xs\*\*\*\*"] |The instance ID(s) to disassociate tags from.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br><br><br>* > Supports passing in multiple instance IDs at once. You can pass a maximum of 20 instance IDs.<br> |
|TagKeys |Array of String |No |[<br><br>"instancetype",<br><br>"chargetype"<br><br>] |Tag keys to delete.<br><br>> **tip**<br><br><br>> Supports passing multiple tag keys.<br> |
|All |Boolean |No |false |Whether to disassociate all tags from the target Redis instance. Valid values:<br><br><br>* `true`: disassociate all tags from the target Redis instance.<br><br>* `false` (default value): do not disassociate all tags from the target Redis instance.<br><br><br>> **tip**<br><br><br>> The `All` parameter takes effect only when `TagKeys` is empty.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=RemoveTagsFromResource&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceIds":[
        "redis-cn0212gzmh2xs****"
    ],
    "TagKeys":[
        "instancetype",
        "chargetype"
    ]
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022041515420801021204201917601111",
          "Action": "RemoveTagsFromResource",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
