---
title: "DescribePlannedEventImpactDetail"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/DescribePlannedEventImpactDetail"
---

Call the DescribePlannedEventImpactDetail API to query impact information about planned events.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribePlannedEventImpactDetail&serviceCode=Redis&version=2020-12-07&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|EventId |String |Yes |event\-cq01ojqnj86l\*\*\*\* |ID of the planned event. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Impact |Object of [PlannedEventImpactDetail](https://docs.byteplus.com/en/docs/55/121039#plannedeventimpactdetail) |Refer to the Sample response. |Impact of planned events. |

### PlannedEventImpactDetail

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ImpactItem |Object of [ImpactItem](https://docs.byteplus.com/en/docs/55/121039#impactitem) |Refer to the Sample response. |Impact details for planned events. Returned when node\-level impact exists. |
|NotGenerated |Boolean |false |Whether impact has been generated for the event. Values:<br><br><br>* `true`: Not generated.<br><br>* `false`: Generated. |

### ImpactItem

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AffectedText |String |The proxy's existing connections were disconnected (recovered), and the client has re\-established the connection. |Impact on the node. |
|InvolvedNodes |Array of [ImpactNode](https://docs.byteplus.com/en/docs/55/121039#impactnode) |Refer to the Sample response. |Details of affected nodes. |
|UnaffectedText |String |Proxies not on the maintenance list maintained uninterrupted connections and read/write operations with server nodes. |Description for unaffected nodes. |
|SuggestedActions |Array of String |["Ensure the client connection pool is configured for automatic reconnection.","Requests may temporarily fail during reconnection, configure a retry strategy.","No changes to backend data nodes, data read/write links are intact.","Schedule maintenance windows during off\-peak business hours."] |Recommendations for addressing impacts on planned events.<br><br>> **tip**<br><br><br>> Returned if the planned event has not been executed; not returned if canceled or successfully executed.<br> |

### ImpactNode

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Count |Integer |2 |Number of affected nodes. |
|NodeIds |Array of String |[<br><br>"proxy\-0", "proxy\-1"<br><br>] |Affected node ID. |
|RoleName |String |Proxy node |Node name, corresponding to the Type parameter value:<br><br><br>* Primary node<br><br>* Secondary node<br><br>* Proxy node |
|Type |String |ProxyNode |Node type.<br><br><br>* `PrimaryNode`: Primary node<br><br>* `SecondaryNode`: Secondary node<br><br>* `ProxyNode`: Proxy node. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribePlannedEventImpactDetail&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "EventId":"event-cq01ojqnj86l****"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribePlannedEventImpactDetail",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-north-1"
    },
    "Result": {
        "Impact": {
            "ImpactItem": {
                "AffectedText": "该 Proxy 存量连接曾断开（已完成恢复），客户端已重新建立连接",
                "InvolvedNodes": [
                    {
                        "Count": 2,
                        "NodeIds": [
                            "proxy-0",
                            "proxy-1"
                        ],
                        "RoleName": "Proxy 节点",
                        "Type": "ProxyNode"
                    }
                ],
                "UnaffectedText": "不在维护列表的Proxy与数据节点连接、读写全程未受影响"
            },
            "NotGenerated": false
        }
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
