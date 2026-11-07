---
title: "DescribeFatLogs"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/DescribeFatLogs"
---

Call the DescribeFatLogs API to query Fatlog log details of Server or Proxy nodes in the target Redis instance within a specified time range.

## Request type

Synchronous request.

## Precautions

* The fatlog threshold is fixed at 500 KB, meaning only query statements with returned result data exceeding 500 KB are recorded as fatlogs.

* You can view the details of fatlogs within the last 3 days. For more details, refer to [Querying fatlog](https://docs.byteplus.com/en/docs/redis/query-fat-log).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeFatLogs&serviceCode=Redis&version=2020-12-07&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn02sg5o56sbs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|NodeIds |Array of String |No |["proxy\-redis\-cn02sg5o56sbs\*\*\*\*\-1", "proxy\-redis\-cn02sg5o56sbs\*\*\*\*\-0"] |Node IDs for querying fatlog logs.<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, fatlog details for all nodes within the target instance will be queried by default.<br><br><br>* > Supports querying multiple node IDs simultaneously.<br><br><br>* > Call the [DescribeNodeIds](https://docs.byteplus.com/en/docs/redis/describenodeids) API to query all node ID information for target Redis instance.<br><br><br>* > The total string length of `NodeIds` cannot exceed 1024 bytes. It is recommended to pass no more than 8 node IDs.<br> |
|PageSize |Integer |Yes |50 |The number of records per page. The value range is between 1 and 1000. |
|QueryStartTime |String |No |2026\-03\-17T07:10:00Z |Query start time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br>> If this parameter is left empty, the actual query start time defaults to 3 days before the current time. For example, if the current time is 2026\-03\-04 16:30:00, and `QueryStartTime` is left blank, the actual query start time will be 2026\-03\-01 16:30:00.<br> |
|QueryEndTime |String |No |2026\-03\-17T07:11:00Z |Query end time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the actual query end time defaults to the current time.<br><br><br>* > The query end time must be later than the query start time.<br> |
|Context |String |No |[1658839101000000,69550,0,null] |The context of fatlog query results, used when more fatlog records need to be loaded.<br><br>> **tip**<br><br><br>> After calling the DescribeFatLogs API, you can determine whether there are any remaining fatlog records to load based on the value of the response parameter `ListOver`:<br><br><br><br>* > If the value of `ListOver` is `false`, it indicates that there are remaining fatlog records matching the query criteria that have not been loaded yet. You can call the DescribeFatLogs API again and use the `Context` value in the response parameter from the previous API call to view the remaining fatlog records.<br><br><br>* > If the value of `ListOver` is `true`, all fatlog records matching the query conditions have been fully loaded.<br> |
|FatLogType |String |No |proxy |Fatlog type. Values:<br><br><br>* `proxy`: Proxy node.<br><br>* `server`: Server node.<br><br><br>> **tip**<br><br><br>> If no value is passed, the type of Fatlog is not specified, and both proxy and server are returned.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Context |String |[1658839101000000,69550,0,null] |The context of fatlog query results, used when more fatlog records need to be loaded. |
|FatLogs |Array of [FatLogItem](https://docs.byteplus.com/en/docs/55/105060#fatlogitem) |Refer to the Sample response. |Fatlog details. |
|InstanceId |String |redis\-cn02sg5o56sbs\*\*\*\* |Instance ID. |
|ListOver |Boolean |true |Whether all fatlog entries have been fully loaded. Valid values:<br><br><br>* `true`: All loaded.<br><br>* `false`: Not all loaded.<br><br><br>> **tip**<br><br><br>> If `ListOver` returns `false`, call DescribeProxyFatLogs again and pass the value returned by `Context` in the request parameters to query the details of the uncompleted fatlogs.<br> |
|Total |Integer |1 |Total number of query results. |

### FatLogItem

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ActionType |String |Read |Request type. Values:<br><br><br>* `Read`: read request.<br><br>* `Write`: write request. |
|ClientAddress |String |172.22. ** *.* ** :47502 |Client address that initiated the query request.<br><br>> **tip**<br><br><br>> The server node's fatlog is forwarded by the proxy node, and the returned client address includes the proxy address.<br> |
|ClientName |String | |Client name. |
|Cmd |String |GET bigkey |The executed statement. |
|CmdLength |String |614411 |Statement length. Unit: Byte. |
|ExecutionStartTime |String |2026\-03\-17T07:10:22Z |The execution start time of the fatlog query statement, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|InstanceId |String |redis\-cn02sg5o56sbs\*\*\*\* |Instance ID. |
|LogId |String | |Log ID. |
|NodeId |String |proxy\-redis\-redis\-cn02sg5o56sbs\*\*\*\*\-0 |The ID of the node to which the fatlog belongs. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeFatLogs&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn02sg5o56sbs****",
    "NodeIds": [
        "proxy-redis-cn02sg5o56sbs****-0"
    ],
    "QueryStartTime": "2026-03-17T07:10:00Z",
    "QueryEndTime": "2026-03-17T07:11:00Z",
    "PageSize": 50,
    "FatLogType":"proxy"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeFatLogs",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "Context": "[1658839101000000,69550,0,null]",
        "FatLogs": [
            {
                "Cmd": "GET bigkey",
                "NodeId": "proxy-redis-redis-cn02sg5o56sbs****-0",
                "CmdLength": "614411",
                "InstanceId": "redis-cn02sg5o56sbs****",
                "ClientAddress": "172.22.***.***:47502",
                "ExecutionStartTime": "2026-03-17T07:10:22Z"
            }
        ],
        "InstanceId": "redis-cn02sg5o56sbs****",
        "ListOver": true,
        "Total": 1,
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
