---
title: "DescribeTagsByResource"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describetagsbyresource"
---

Call the DescribeTagsByResource API to query tags bound to the target Redis instance.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTagsByResource&serviceCode=Redis&version=2020-12-07&groupName=标签管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |[<br><br>"redis\-cnlflix66ohil\*\*\*\*",<br><br>"redis\-cnlfpoc48rz7g\*\*\*\*"<br><br>] |The ID of the instance whose associated tags you want to query.<br><br>> **tip**<br><br><br><br>* > You can specify multiple instance IDs, separated by commas (,). You can specify a maximum of 50 instance IDs.<br><br><br>* > Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query basic information about all Redis instances in the target region, including their instance IDs.<br> |
|PageNumber |Integer |Yes |1 |The page number of the instance tag list. The value cannot exceed the maximum value of the Integer data type. The starting value is 1. |
|PageSize |Integer |Yes |10 |The number of records per page. The value range is between 1 and 1000. |
|TagFilters |Array of [TagFilterObject](https://docs.byteplus.com/en/docs/55/12467#tagfilterobject) |No |Refer to the sample request. |An array of tag key\-value pairs for querying and filtering.<br><br>> **tip**<br><br><br>> If this parameter is left empty, tags will not be used for filtering.<br> |

### TagFilterObject

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |department |The tag key for querying and filtering.<br><br>> **tip**<br><br><br><br>* > When you use tags to filter query results, the tag key (Key) is required, but the tag value (Value) is optional. If you do not specify a tag value, the system searches for all instances associated with the specified tag key.<br><br><br>* > Duplicate tag keys are allowed.<br><br><br>* > Up to 10 tags can be passed in at a time for query filtering.<br> |
|Value |String |No |game |Tag values corresponding to the tag key used for query filtering.<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, no restrictions are placed on tag values, and all instances associated with the specified tag key will be filtered.<br><br><br>* > If an empty string is passed, it filters for instances where the tag value is empty for the corresponding tag key.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |3 |The total number of results that meet the query conditions. |
|TagResources |Array of [TagResource](https://docs.byteplus.com/en/docs/55/12467#tagresource) |Refer to the Sample response. |The tag information associated with the instance. |

### TagResource

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Key |String |department |The tag key associated with the instance. |
|Value |String |game |The value of the tag key associated with the instance. |
|InstanceId |String |redis\-cnlfpoc48rz7g\*\*\*\* |Instance ID. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeTagsByResource&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceIds":[
        "redis-cnlflix66ohil****",
        "redis-cnlfpoc48rz7g****"
    ],
    "TagFilters":[
        {
            "Key":"department",
            "Value":"game"
        },
        {
            "Key":"chargetype",
            "Value":"postpaid"
        }
    ],
    "PageNumber":1,
    "PageSize":10
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230804155514FE4F49ADA2A620583954",
        "Action": "DescribeTagsByResource",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "TagResources": [
            {
                "InstanceId": "redis-cnlflix66ohil****",
                "Key": "department",
                "Value": "game"
            },
            {
                "InstanceId": "redis-cnlfpoc48rz7g****",
                "Key": "chargetype",
                "Value": "prepaid"
            },
            {
                "InstanceId": "redis-cnlfpoc48rz7g****",
                "Key": "department",
                "Value": "game"
            }
        ],
        "Total": 3
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
