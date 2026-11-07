---
title: "DescribeBigKeys"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describebigkeys"
---

Call the DescribeBigKeys API to query large key details of the target Redis instance within a specified time range.

## Request type

Synchronous request.

## Precautions

You can only view the details of the top 100 keys with the highest memory usage or the most elements in a specified Redis instance within the past 15 days. For more details, refer to [Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBigKeys&serviceCode=Redis&version=2020-12-07&groupName=性能分析)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn02sg5o56sbs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|PageSize |Integer |Yes |50 |Number of records on each page. Value range is any integer between 1 and 100. |
|QueryStartTime |String |No |2023\-03\-27T15:30:00Z |Query start time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br><br>* > Only supports viewing big key distribution for the last 15 days.<br><br><br>* > If this parameter is left empty, the actual query start time defaults to 24 hours before the current time.<br><br><br>   > For example, if the current time is 2023\-03\-27 16:30:00, and `QueryStartTime` is left blank, the actual query start time will be 2023\-03\-26 16:30:00.<br>   <br><br>* > The query end time must be later than the query start time, and the time interval should not exceed 24 hours.<br> |
|QueryEndTime |String |No |2023\-03\-27T15:31:00Z |Query end time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the actual query end time defaults to the current time.<br><br><br>* > The query end time must be later than the query start time, and the time interval should not exceed 24 hours.<br> |
|KeyType |String |No |list |Specify the data type used to filter big key query results. Supported data types:<br><br><br>* `string`<br><br>* `list`<br><br>* `set`<br><br>* `zset`<br><br>* `hash`<br><br><br>> **tip**<br><br><br>> If this parameter is left blank, data type filtering is not used.<br> |
|OrderBy |String |No |ValueSize |Specify the sorting condition for query results. The following sorting conditions are supported:<br><br><br>* `ValueSize` (default): Sort big key query results by memory usage.<br><br>* `ValueLen`: Sort big key query results by the number of elements. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of query results. |
|InstanceId |String |redis\-cn02sg5o56sbs\*\*\*\* |Instance ID. |
|BigKey |Array of [BigKeyInfo](https://docs.byteplus.com/en/docs/55/12480#bigkeyinfo) |Refer to the Sample response. |Big key details. |

### BigKeyInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DBName |String |2 |The name of the database to which the big key belongs. |
|KeyInfo |String |key:000000000015 |Name of the big key. |
|KeyType |String |string |Data type of the big key. |
|ValueLen |String |1 |Number of elements contained in the big key.<br><br>> **tip**<br><br><br><br>* > The number of elements for string type big keys defaults to 1.<br><br><br>* > Non\-string type big keys return the specific number of elements.<br> |
|ValueSize |String |10241 |Memory usage of the big key, unit: Byte.<br><br>> **tip**<br><br><br><br>* > String\-type big keys return specific memory usage.<br><br><br>* > Non\-string type big keys have empty memory usage by default.<br> |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeBigKeys&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId":"redis-cn02sg5o56sbs****",
    "QueryStartTime":"2023-03-20T12:37:54Z",
    "QueryEndTime":"2023-03-20T12:38:54Z",
    "PageSize":50
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202207262048480102250842170107xxxx",
        "Action": "DescribeBigKeys",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "BigKey": [
            {
                "DBName": "2",
                "KeyInfo": "key:000000000015",
                "KeyType": "string",
                "ValueLen": "1",
                "ValueSize": "10241"
            }
        ],
        "InstanceId": "redis-cn02sg5o56sbs****",
        "Total": 1
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
