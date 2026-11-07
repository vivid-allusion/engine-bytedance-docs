---
title: "DescribeSlowLogs"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describeslowlogs"
---

Call the DescribeSlowLogs API to query slow log details of the target Redis instance within a specified time range.

## Request type

Synchronous request.

## Precautions

* You can only view the details of slow logs within the last three days.

* Block\-type commands whose execution time, communication time, and wait time exceed the thresholds will not be logged in the slow log. For more information, refer to [Querying slow log](https://docs.byteplus.com/en/docs/redis/query-slow-log).

   |Command group |Commands |
   |---|---|
   |Lists |BLPOP, BRPOP, BRPOPLPUSH |
   |SortedSets |BZPOPMIN, BZPOPMAX |
   |Streams |XREAD, XREADGROUP |

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeSlowLogs&serviceCode=Redis&version=2020-12-07&groupName=日志管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn02sg5o56sbs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|PageSize |Integer |Yes |50 |The number of records per page. The value range is between 1 and 1000. |
|NodeIds |Array of String |No |["proxy\-redis\-cn02sg5o56sbs\*\*\*\*\-1", "proxy\-redis\-cn02sg5o56sbs\*\*\*\*\-0"] |The node ID for which to query slow logs.<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the slow log details for all nodes within the target instance are queried by default.<br><br><br>* > Call the [DescribeNodeIds](https://docs.byteplus.com/en/docs/redis/describenodeids) API to query all node ID information for target Redis instance.<br><br><br>* > The total string length of `NodeIds` cannot exceed 1024 bytes. It is recommended to pass no more than 8 node IDs.<br> |
|SlowLogType |String |No |Proxy |Type of slow log. Valid values:<br><br><br>* `Server`: Server node slow log.<br><br>* `Proxy`: Proxy node slow log.<br><br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, slow logs for all node types are returned by default.<br><br><br>* > If both `NodeIds` and `SlowLogType` are provided, the `NodeIds` value takes precedence.<br> |
|QueryStartTime |String |No |2022\-07\-26T12:37:54Z |Query start time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br>> If this parameter is left empty, the actual query start time defaults to 3 days before the current time. For example, if the current time is 2022\-08\-01 16:30:00, and `QueryStartTime` is not specified, the actual query start time will be 2022\-07\-29 16:30:00.<br> |
|QueryEndTime |String |No |2022\-07\-26T12:38:54Z |Query end time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the actual query end time defaults to the current time.<br><br><br>* > The query end time must be later than the query start time.<br> |
|DBName |String |No |0 |The database where slow logs are located. Different slow log types support different database value ranges, specifically:<br><br><br>* Proxy node slow logs: Any integer between 0 and 256.<br><br>* Server node slow logs: The database for server node slow logs is empty, thus only `-` is supported as a value.<br><br><br>> **tip**<br><br><br>> If this parameter is left blank, the slow logs on all databases will be returned by default.<br> |
|Context |String |No |[1658839101000000,69550,0,null] |The context of slow log query results, used to load more slow logs.<br><br>> **tip**<br><br><br>> After calling the DescribeSlowLogs API, you can use the value of the return parameter `ListOver` to determine if there are any unloaded slow log records remaining:<br><br><br><br>* > If the value of `ListOver` is `false`, it indicates that there are still slow log entries matching the query conditions that have not been fully loaded. You can call the DescribeSlowLogs API again and use the `Context` value from the returned parameters of the previous API call to view the remaining slow log entries.<br><br><br>* > If the value of `ListOver` is `true`, it indicates that all slow log entries matching the query conditions have been fully loaded.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of query results. |
|InstanceId |String |redis\-cn02sg5o56sbs\*\*\*\* |Instance ID. |
|ListOver |Boolean |true |Whether the slow log content is fully loaded. Valid values:<br><br><br>* `true`: All loaded.<br><br>* `false`: Not all loaded.<br><br><br>> **tip**<br><br><br>> If `ListOver` returns `false`, you can call DescribeSlowLogs again. Pass the value returned by `Context` in the request parameters to query the details of the remaining slow logs.<br> |
|Context |String |[1658839101000000,69550,0,null] |The context of slow log query results, used to load more slow logs. |
|SlowQuery |Array of [SlowQueryInfo](https://docs.byteplus.com/en/docs/55/12529#slowqueryinfo) |Refer to the Sample response. |Slow log details. |

### SlowQueryInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |redis\-cn02sg5o56sbs\*\*\*\* |Instance ID. |
|NodeId |String |proxy\-redis\-redis\-cn02sg5o56sbs\*\*\*\*\-0 |The ID of the node to which the slow log belongs. |
|DBName |String |0 |Database name.<br><br>> **tip**<br><br><br>> Only slow logs on proxy nodes will return this information. For server node slow logs, this value is empty by default (i.e., `-`).<br> |
|UserName |String |default |Account name.<br><br>> **tip**<br><br><br>> Only slow logs on proxy nodes will return this information. For server node slow logs, this value is empty by default (i.e., `-`).<br> |
|ExecutionStartTime |String |2022\-07\-26T12:37:38Z |The execution start time of the slow query statement, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|QueryText |String |INFO |Slow query statement. |
|QueryTimes |Long |22073438 |Slow query statement execution duration, in microseconds (us). |
|HostAddress |String |172.22. ** *.* ** :47502 |The client address that issued the slow query request.<br><br>> **tip**<br><br><br>> Only slow logs on proxy nodes will return this information. For server node slow logs, this value is empty by default (i.e., `-`).<br> |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeSlowLogs&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId":"redis-cn02sg5o56sbs****",
    "NodeIds":[
        "proxy-redis-cn02sg5o56sbs****-0",
        "proxy-redis-cn02sg5o56sbs****-1"
    ],
    "QueryStartTime":"2022-07-26T12:37:54Z",
    "QueryEndTime":"2022-07-26T12:38:54Z",
    "PageSize":50
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022072620484801022508421701070107",
        "Action": "DescribeSlowLogs",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "Context": "[1658839101000000,69550,0,null]",
        "InstanceId": "redis-cn02sg5o56sbs****",
        "ListOver": true,
        "SlowQuery": [
            {
                "DBName": "0",
                "ExecutionStartTime": "2022-07-26T12:37:38Z",
                "HostAddress": "172.22.***.***:47502",
                "InstanceId": "redis-redis-cn02sg5o56sbs****",
                "NodeId": "proxy-redis-redis-cn02sg5o56sbs****-0",
                "QueryText": "INFO",
                "QueryTimes": 22073438,
                "UserName": "default"
            }
        ],
        "Total": 1
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
