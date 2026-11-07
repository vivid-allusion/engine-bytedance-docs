---
title: "DescribeRegions"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describeregions"
---

Call the DescribeRegions API to query the list of regions available for Cache for Redis.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeRegions&serviceCode=Redis&version=2020-12-07&groupName=地域和可用区)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|RegionId |String |No |cn\-beijing |Region ID.<br><br>> **tip**<br><br><br>> If this parameter is blank, the query returns all available region resources under the current account.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Regions |Array of [RegionInfo](https://docs.byteplus.com/en/docs/55/12483#regioninfo) |Refer to the Sample response. |List of region information. |

### RegionInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|RegionId |String |cn\-beijing |Region ID. |
|RegionName |String |China (Beijing) |Region name. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeRegions&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "RegionId":"cn-beijing"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022041515063901019405910012651265",
        "Action": "DescribeRegions",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
 "Result": {
     "Regions":[
         { 
               "RegionId": "cn-beijing", 
               "RegionName": "华北2（北京）"
         }
     ] 
  }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
