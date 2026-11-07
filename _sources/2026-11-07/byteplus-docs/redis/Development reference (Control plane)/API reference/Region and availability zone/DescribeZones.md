---
title: "DescribeZones"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describezones"
---

Call the DescribeZones API to query the list of availability zones available for Cache for Redis in a specified region.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeZones&serviceCode=Redis&version=2020-12-07&groupName=地域和可用区)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|RegionId |String |Yes |cn\-beijing |Region ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeRegions](https://docs.byteplus.com/en/docs/redis/describeregions) API to query all available region resources for Redis instances, including region IDs.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Zones |Array of [ZoneInfo](https://docs.byteplus.com/en/docs/55/12482#zoneinfo) |Refer to the Sample response. |Availability Zone list. |

### ZoneInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ZoneId |String |cn\-beijing\-a |Availability Zone ID. |
|ZoneName |String |Availability zone A |Availability Zone name. |
|ZoneStatus |Integer |1 |Availability Zone status, with the following values:<br><br><br>* `1`: The target Availability Zone is available for purchase.<br><br>* `2`: The target Availability Zone is sold out and unavailable for purchase. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeZones&Version=2020-12-07 HTTP/1.1
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
    "RequestId": "20250103160848EDBD027396F29CF2FBA3-b02bdc",
    "Action": "DescribeZones",
    "Version": "2020-12-07",
    "Service": "Redis",
    "Region": "cn-beijing"
  },
  "Result": {
    "Zones": [
      {
        "ZoneId": "cn-beijing-a",
        "ZoneName": "可用区A",
        "ZoneStatus": 1
      },
      {
        "ZoneId": "cn-beijing-b",
        "ZoneName": "可用区B",
        "ZoneStatus": 1
      },
      {
        "ZoneId": "cn-beijing-c",
        "ZoneName": "可用区C",
        "ZoneStatus": 1
      },
      {
        "ZoneId": "cn-beijing-d",
        "ZoneName": "可用区D",
        "ZoneStatus": 1
      }
    ]
  }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
