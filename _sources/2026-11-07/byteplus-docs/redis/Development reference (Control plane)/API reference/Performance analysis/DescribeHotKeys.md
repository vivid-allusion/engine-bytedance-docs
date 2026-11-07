---
title: "DescribeHotKeys"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describehotkeys"
---

Call the DescribeHotKeys API to query hot key details of the target Redis instance within a specified time range.

## Request type

Synchronous request.

## Precautions

You can only view the details of the top 1000 hot keys in a specified Redis instance within the past 15 days. For more details, refer to [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeHotKeys&serviceCode=Redis&version=2020-12-07&groupName=性能分析)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn02sg5o56sbs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|PageSize |Integer |Yes |50 |The number of records per page, an integer between 1 and 1000. |
|QueryStartTime |String |No |2023\-03\-27T15:30:00Z |Query start time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br><br>* > Only supports viewing hot key distribution for the last 15 days.<br><br><br>* > If this parameter is left empty, the actual query start time defaults to 1 hour before the current time.<br><br><br>   > For example, if the current time is 2023\-03\-26 16:30:00, and `QueryStartTime` is left blank, the actual query start time will be 2023\-03\-26 16:30:00.<br>   <br><br>* > The query end time must be later than the query start time, and the time interval should not exceed 15 days.<br> |
|QueryEndTime |String |No |2023\-03\-27T15:31:00Z |Query end time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the actual query end time defaults to the current time.<br><br><br>* > The query end time must be later than the query start time, and the time interval should not exceed 15 days.<br> |
|KeyType |String |No |list |Specifies the data type used to filter hot key query results. Supports the following data types:<br><br><br>* `string`<br><br>* `list`<br><br>* `set`<br><br>* `zset`<br><br>* `hash`<br><br><br>> **tip**<br><br><br>> If this parameter is left blank, data type filtering is not used.<br> |
|ShardIds |Array of String |No |["server\-redis\-cn02sg5o56sbs\*\*\*\*\-0"] |Specify a list of shard IDs used to filter the results of the hot key query.<br><br>> **tip**<br><br><br><br>* > Up to 40 shard IDs can be passed simultaneously. Pass multiple shard IDs as an array.<br><br><br>* > If this parameter is left blank, shard ID filtering is not used.<br><br><br>* > You can call the [DescribeDBInstanceShards](https://docs.byteplus.com/en/docs/redis/describedbinstanceshards) API to query the details of each shard under the target Redis instance, including the shard ID (that is, the `ShardId` field in the Response).<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of query results. |
|InstanceId |String |redis\-cn02sg5o56sbs\*\*\*\* |Instance ID. |
|HotKey |Array of [HotKeyInfo](https://docs.byteplus.com/en/docs/55/38014#hotkeyinfo) |Refer to the Sample response. |Hot key details list. |

### HotKeyInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ActionType |String |Read |Request type that triggers hot key detection. Values:<br><br><br>* `Read`: read request.<br><br>* `Write`: write request. |
|CreateTime |String |2023\-03\-27T15:30:35Z |Collection time of hot keys, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|DBName |String |0 |The name of the database to which the hot key belongs. |
|NodeId |String |server\-redis\-cn02sg5o56sbs\*\*\*\*\-0\-0 |The node ID of the hot key. |
|KeyInfo |String |key:000000000015 |Name of the hot key. |
|KeyType |String |string |Data type of hot keys. |
|QueryCount |String |15000 |Access count of the hot key. |
|ShardId |String |server\-redis\-cn02sg5o56sbs\*\*\*\*\-0 |Shard ID of the hot key |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeHotKeys&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn02sg5o56sbs****",
    "QueryStartTime": "2023-03-27T15:30:00Z",
    "QueryEndTime": "2023-03-27T15:31:00Z",
    "PageSize": 50,
    "ShardIds": [
        "server-redis-cn02sg5o56sbs****-0"
    ]
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeHotKeys",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 1,
        "InstanceId": "redis-cn02sg5o56sbs****",
        "HotKey": [
            {
                "ActionType": "Read",
                "DBName": "0",
                "NodeId": "server-redis-cn02sg5o56sbs****-0-0",
                "KeyInfo": "key:000000000015",
                "KeyType": "string",
                "ShardId": "server-redis-cn02sg5o56sbs****-0",
                "CreateTime": "2023-03-27T15:30:35Z",
                "QueryCount": "15000"
            }
        ]
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
