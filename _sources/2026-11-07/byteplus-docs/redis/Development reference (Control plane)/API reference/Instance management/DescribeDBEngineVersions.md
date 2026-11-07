---
title: "DescribeDBEngineVersions"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describedbengineversions"
---

Call the DescribeDBEngineVersions API to query list of minor versions supported by Redis major versions.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBEngineVersions&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|EngineVersion |String |No |7.0 |Redis database major version number, valid values are as follows:<br><br><br>* `7.0`: Redis 7.0.<br><br>* `6.0`: Redis 6.0.<br><br>* `5.0`: Redis 5.0.<br><br><br>> **tip**<br><br><br>> If this parameter is left blank, the list of minor versions supported by all major Redis database versions is queried by default.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DBEngineVersions |Array of [DBEngineVersion](https://docs.byteplus.com/en/docs/55/91373#dbengineversion) |Refer to the Sample response. |Database version list. |

### DBEngineVersion

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Engine |String |Redis |Database engine. |
|EngineVersion |String |7.0 |Database engine version. |
|ServerVersions |Array of [VersionInfo](https://docs.byteplus.com/en/docs/55/91373#versioninfo) |Refer to the Sample response. |List of server versions supported by the current major version. |
|ProxyVersions |Array of [VersionInfo](https://docs.byteplus.com/en/docs/55/91373#versioninfo) |Refer to the Sample response. |List of proxy versions supported by the current major version. |

### VersionInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Version |String |7.512.0 |Server version number. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBEngineVersions&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "EngineVersion": "7.0"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420800210023228002****",
        "Action": "DescribeDBEngineVersions",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "DBEngineVersions": [
            {
                "Engine": "Redis",
                "EngineVersion": "7.0",
                "ProxyVersions": [
                    {
                        "Version": "1.512.0"
                    }
                ],
                "ServerVersions": [
                    {
                        "Version": "7.512.0"
                    }
                ]
            }
        ]
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
