---
title: "DescribeClientSessionSnapshot"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/DescribeClientSessionSnapshot"
---

Call the DescribeClientSessionSnapshot API to query the client session snapshot of the instance within the specified time window.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeClientSessionSnapshot&serviceCode=Redis&version=2020-12-07&groupName=)

## Request parameters

Request parameters include instance ID, query time range, paging information, sorting conditions, and filtering conditions.

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn02sg5o56sbs\*\*\*\* |Redis instance ID, which specifies the instance for which to query client session snapshots. This parameter cannot be empty. The server verifies whether the instance exists and belongs to the account. |
|QueryStartTime |String |Yes |2022\-07\-26T12:37:54Z |Query start time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|QueryEndTime |String |Yes |2022\-07\-26T12:38:54Z |Query end time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br><br>* > The time range specified by QueryStartTime and QueryEndTime cannot exceed 5 minutes.<br> |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1000, with a default value of 500. |
|Context |String |No |1658839101000000,69550,0,null |Pagination context. The first query can be empty; the next page is queried with the context from the previous response. If empty or not provided, it indicates the first paginated query. |
|OrderType |String |No |AES |Sort direction. Can be empty. If not empty, it must be a server\-supported sort type. No default value, usually used with OrderBy. |
|OrderBy |String |No |ClientAddr |Sort field. Can be empty. If not empty, it must be an enumerated value supported by ClientSessionOrderBy, such as `ClientAddr`, `SessionAge`, `SessionIdle`, `SessionFlags`, `SessionDb`, `SessionSub`, `SessionPsub`, `SessionMulti`, or `SessionCmd`. |
|Filter |Array of [ClientSessionFilter](https://docs.byteplus.com/en/docs/55/118241#clientsessionfilter) |No |Refer to the sample request. |List of filter conditions used to filter session snapshots by client connection attributes. No filtering occurs if not provided or the list is empty. Each filter item contains FilterKey and FilterValue. |

### ClientSessionFilter

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|FilterKey |String |No |ClientAddr |Filter condition key. Values:<br><br><br>* `ClientId`: Filter by Redis client session ID.<br><br>* `ClientAddr`: Filter by client address and port.<br><br>* `NodeId`: Filter by Proxy node ID. |
|FilterValue |String |No |192.168.1.100:12345 |Value corresponding to the filter condition's key. |

## Response parameters

The returned results include the total number of hits, instance ID, paging context, whether loading is complete, and a list of client session snapshots.

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |The total number of client session entries hit by the query, which is a non\-negative integer. |
|InstanceId |String |redis\-cn02sg5o56sbs\*\*\*\* |The Redis instance ID for this query, matching the InstanceId in the request. |
|Context |String |1658839101000000,69550,0,null |Context cursor used for the next paginated query. Typically an empty string when there is no more data. |
|ListOver |Boolean |true |Pagination end identifier. Values:<br><br><br>* `true`: Indicates no more data.<br><br>* `false`: Indicates that pagination may continue. |
|SessionList |Array of [ClientSessionItem](https://docs.byteplus.com/en/docs/55/118241#clientsessionitem) |Refer to the Sample response. |Client session snapshot list. |

### ClientSessionItem

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|NodeId |String |proxy\-redis\-cn02sg5o56sbs\*\*\*\*\-0 |Proxy node ID, indicating which proxy node the connection lands on. |
|ClientId |Long |111222 |Redis client session ID。 |
|ClientIp |String |192.168.1.100 |Client IP address. |
|SessionDb |Long |0 |The Redis DB number used by the current connection. |
|SessionFd |Integer |222333 |File descriptor used by the socket. |
|ClientAddr |String |192.168.1.100:12345 |Client address and port, for example, `ip:port`. |
|ClientName |String |client\-xxx |Client connection name. May be empty, depending on whether the client side sets the name. |
|InstanceId |String |redis\-cn02sg5o56sbs\*\*\*\* |The Redis instance ID for this query, matching the InstanceId in the request. |
|SessionAge |Long |150 |Connection duration. The unit is seconds. Typically a non\-negative integer. |
|SessionCmd |String |info |The most recently executed command. |
|SessionObl |Long |0 |Output buffer length. In bytes. `0` indicates no output buffer is allocated. |
|SessionOll |Long |100 |The number of objects included in the output list. |
|SessionSub |Integer |0 |Number of subscribed channels. |
|SessionAuth |Integer |1 |Indicates the authentication status. |
|SessionIdle |Long |0 |Connection idle duration. The unit is seconds. Typically a non\-negative integer. |
|SessionOmem |Long |95 |Total memory used by the output buffer and output list. |
|SessionPsub |Integer |0 |Number of subscribed patterns. |
|SessionQbuf |Long |0 |Query buffer length. In bytes. `0` indicates no query buffer is allocated. |
|SessionFlags |String |0 |Client status flag. |
|SessionMulti |Integer |0 |Number of commands executed in the current transaction. |
|SessionEvents |String |fd\-xxx |File descriptor event information |
|SessionQbufFree |Long |100 |Query buffer remaining space. In bytes. `0` indicates no remaining space. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeClientSessionSnapshot&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn02sg5o56sbs****",
    "QueryStartTime": "2025-07-26T12:37:54Z",
    "QueryEndTime": "2025-07-26T12:38:54Z",
    "PageSize": 10,
    "Context": "1658839101000000,69550,0,null",
    "OrderType": "AES",
    "OrderBy": "ClientAddr",
    "Filter": [
        {
            "FilterKey": "ClientAddr",
            "FilterValue": "192.168.1.100:12345"
        }
    ]
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeClientSessionSnapshot",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 1,
        "InstanceId": "redis-cn02sg5o56sbs****",
        "Context": "1658839101000000,69550,0,null",
        "ListOver": true,
        "SessionList": [
            {
                "NodeId": "proxy-redis-cn02sg5o56sbs****-0",
                "ClientId": 111222,
                "ClientIp": "192.168.1.100",
                "SessionDb": 0,
                "SessionFd": 222333,
                "ClientAddr": "192.168.1.100:12345",
                "ClientName": "client-xxx",
                "InstanceId": "redis-cn02sg5o56sbs****",
                "SessionAge": 150,
                "SessionCmd": "info",
                "SessionObl": 0,
                "SessionOll": 100,
                "SessionSub": 0,
                "SessionAuth": 1,
                "SessionIdle": 0,
                "SessionOmem": 95,
                "SessionPsub": 0,
                "SessionQbuf": 0,
                "SessionFlags": "0",
                "SessionMulti": 0,
                "SessionEvents": "fd-xxx",
                "SessionQbufFree": 100
            }
        ]
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
