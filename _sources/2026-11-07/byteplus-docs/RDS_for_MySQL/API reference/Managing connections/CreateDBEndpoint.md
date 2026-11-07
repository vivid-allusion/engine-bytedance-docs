---
title: "CreateDBEndpoint"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbendpoint"
---

## Request type

Asynchronous request.

## Precautions

Connection endpoints can only be created for double\-node and multiple\-node instances. Multiple node instances only support creating 3 customized read/write direct endpoints.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBEndpoint&serviceCode=rds_mysql&version=2022-01-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-e26822cf\*\*\*\* |Instance ID. |
|EndpointType |String |Yes |Custom |Connection endpoint type. The value is `Custom`, which indicates a customized endpoint. |
|ReadWriteMode |String |No |ReadOnly |The read/write mode for the connection endpoint. Values:<br><br><br>* `ReadWrite`: read/write.<br><br>* `ReadOnly`: read\-only.<br><br><br>> **tip**<br><br><br>> When used as a request parameter, the default value is `ReadWrite`.<br> |
|EndpointName |String |No |EndpointName |Instance endpoint name.<br><br><br>* It cannot start with a digit or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length must be between 1 and 64 characters. |
|Description |String |No |This is a description of the connection endpoint. |Remarks. |
|Nodes |String |No |Primary,mysql\-3c25f219\*\*\*\*\-r5b3f |A list of Node IDs configured for the Connection endpoint. Required when EndpointType is Custom.<br><br>> **tip**<br><br><br><br>* > To add the primary node to the Endpoint, enter Primary instead of the primary Node ID.<br><br><br>* > Separate multiple Node IDs with commas (,).<br> |
|AutoAddNewNodes |Boolean |No |true |When the endpoint type is read/write or read\-only, setting whether the new node joins automatically is supported. Values:<br><br><br>* `true`: Joins automatically.<br><br>* `false`: Does not join automatically (Default). |
|ConnectionMode |String |No |Proxy |The connection mode of the endpoint. Values:<br><br><br>* `Proxy`: proxy endpoint (default).<br><br>* `Direct`: direct endpoint.<br><br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail) API to query the status of the database proxy of the instance.<br><br><br>   * > If the database proxy of the instance is enabled, the value can be `Proxy` or `Direct`.<br><br><br>   * > If the database proxy of the instance is disabled, the value can only be `Direct`.<br><br><br>* > The connection endpoint type of a multiple\-node instance cannot be modified.<br> |
|IdleConnectionReclaim |Boolean |No |true |Whether to enable the wait_timeout feature for the proxy endpoint. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br>> **tip**<br><br><br>> When the ConnectionMode parameter is set to Proxy, it is a required field. If set to Direct, this parameter takes no effect.<br> |
|ConnectionPoolType |String |No |Direct |The connection pool type of the proxy endpoint. Values:<br><br><br>* `Transaction`: transaction\-level connection pool. Default value.<br><br>* `Direct`: direct connection mode.<br><br><br>> **tip**<br><br><br><br>* > Single\-node instances do not support this feature.<br><br><br>* > When the ConnectionMode parameter is set to Proxy, it is a required field. If set to Direct, this parameter takes no effect.<br> |
|ReadWriteSpliting |Boolean |No |true |Enable read\-write separation? Values:<br><br><br>* `yes`: yes. Default value.<br><br>* `false`: no.<br><br><br>> **tip**<br><br><br>> When the ConnectionMode parameter is set to Proxy, it is a required field. If set to Direct, this parameter takes no effect.<br> |
|ReadOnlyNodeDistributionType |String |No |LoadSchedule |Read weight distribution mode. This parameter is required when read/write separation is set to `true`. As a request parameter for the CreateDBEndpoint and ModifyDBEndpoint APIs, the value range is as follows:<br><br><br>* `LoadSchedule`: load scheduling.<br><br>* `RoundRobinCustom`: round robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: round robin scheduling with automatic weight assignment. As a response parameter for the DescribeDBInstanceDetail API, the value range is as follows:<br><br>* `Default`: automatic assignment based on specification weights.<br><br>* `Custom`: custom weight assignment.<br><br>* `RoundRobin`: round robin scheduling.<br><br>* `LoadSchedule`: load scheduling.<br><br>* `RoundRobinCustom`: round robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: round robin scheduling with automatic weight assignment.<br><br><br>> **tip**<br><br><br><br>* > Multiple node instances only support `RoundRobinAuto`.<br><br><br>* > Single\-node instances do not support this feature.<br><br><br>* > When the `ConnectionMode` parameter is set to `Proxy`, it is a required field. If set to `Direct`, this parameter takes no effect.<br> |
|ReadOnlyNodeWeight |Array of [NodeWeightObject](https://docs.byteplus.com/en/docs/40/15478#nodeweightobject) |No |See the request example. |Custom read weight allocation policy.<br><br>> **tip**<br><br><br>> When the `ConnectionMode` parameter is set to `Proxy`, it is a required field. If set to `Direct`, this parameter takes no effect.<br> |
|ReadOnlyNodeMaxDelayTime |Integer |No |40 |The latency threshold for the read\-only node. The value can be an integer from 1 to 3,600. The default value is 30. The unit is seconds.<br><br>> **tip**<br><br><br>> When the `ConnectionMode` parameter is set to `Proxy`, it is a required field. If set to `Direct`, this parameter takes no effect.<br> |
|MultiStatementsMode |String |No |Loose |The Multi\-Statements mode of the proxy endpoint. Values:<br><br><br>* `Strict`: strict mode. Default value.<br><br>* `Loose`: loose mode.<br><br><br>> **tip**<br><br><br><br>* > Single\-node instances do not support this feature.<br><br><br>* > When the `ConnectionMode` parameter is set to `Proxy`, it is a required field. If set to `Direct`, this parameter takes no effect.<br> |
|OverloadProtection |Boolean |No |false |Whether overload protection is enabled. Values:<br><br><br>* `yes`: yes. Default value.<br><br>* `false`: no.<br><br><br>> **tip**<br><br><br>> When the `ConnectionMode` parameter is set to `Proxy`, it is a required field. If set to `Direct`, this parameter takes no effect.<br> |
|MasterProtectorTimeout |Integer |No |60 |Overload protection timeout. The value range is an integer from 60 to 7,200. The default value is 60, and the unit is seconds.<br><br>> **tip**<br><br><br>> When the `ConnectionMode` parameter is set to `Proxy`, it is a required field. If set to `Direct`, this parameter takes no effect.<br> |
|MasterNodeRouting |Boolean |No |false |Specifies whether to enable primary node routing. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br>> **tip**<br><br><br>> When the `ConnectionMode` parameter is set to `Proxy`, it is a required field. If set to `Direct`, this parameter takes no effect.<br> |
|ImplicitTransSplit |Boolean |No |false |Indicates whether to enable transaction splitting. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br>> **tip**<br><br><br>> When the `ConnectionMode` parameter is set to `Proxy`, it is a required field. If set to `Direct`, this parameter takes no effect.<br> |
|EnableConnectionPersistent |Boolean |No |true |Whether to enable connection persistence for the connection endpoint. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br>> **tip**<br><br><br>> When the `ConnectionMode` parameter is set to `Proxy`, it is a required field. If set to `Direct`, this parameter takes no effect.<br> |
|CustomRouteStrategy |Object of [CustomRouteStrategy](https://docs.byteplus.com/en/docs/40/15478#customroutestrategy) |No |See the request example. |SQL forwarding rules for the connection endpoint. |
|ConsistentReadConfig |Object of [ConsistentReadConfig](https://docs.byteplus.com/en/docs/40/15478#consistentreadconfig) |No |See the request example. |Set the consistency level. |

### NodeWeightObject

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|NodeId |String |No |mysql\-050b3e08\*\*\*\*\-2 |Read\-only node requires passing in NodeId; primary node does not require it. |
|NodeType |String |No |Primary |Node type.<br><br><br>* `Primary`: primary node.<br><br>* `ReadOnly`: read\-only node. |
|Weight |Integer |No |100 |The read weight of the node. The step size is 100, and the valid value range is 0~10000.<br><br>> **tip**<br><br><br>> The read weight of a single node can be set to 0, but the sum of read weights for all nodes must be greater than or equal to 100.<br> |

### CustomRouteStrategy

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|KeywordRouteStrategy |Array of [KeywordRouteStrategy](https://docs.byteplus.com/en/docs/40/15478#keywordroutestrategy) |No |Refer to the sample. |Custom routing policy. |

### KeywordRouteStrategy

|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|NodeType |String |No |Primary |Target for the SQL forwarding rule. Values:<br><br><br>* `Primary`: primary node.<br><br>* `Secondary`: secondary node.<br><br>* `ReadOnly`: read\-only node.<br><br><br>> **tip**<br><br><br><br>* > For a double\-node instance, you can select the primary node or the read\-only node.<br><br><br>* > For a multiple node instance, you can select the primary node or the secondary node.<br> |
|SQLKeyword |String |Yes |Select |Keywords of the forwarding rule. The rules for setting SQL keywords are as follows:<br><br><br>* Each rule can contain a maximum of 20 keywords.<br><br>* The maximum length is 64 characters, and it can contain English letters, digits, underscores `_`, `@`, `#`, `:=`, and Chinese characters.<br><br><br>> **tip**<br><br><br><br>* > SQL keywords are case\-sensitive. Changes in the case of keywords may cause rules to fail silently.<br><br><br>* > When you configure SQL forwarding rules through the API, the keyword can be an empty string or spaces. In this case, all SQL statements are matched, meaning all requests are forwarded to the target node.<br> |

### ConsistentReadConfig

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|EnableConsistentRead |Boolean |No |true |Whether to enable consistency read. Values are as follows:<br><br><br>* `true`: enabled.<br><br>* `false`: disabled. |
|ConsistentReadMode |String |No |Session |The consistency read level.<br><br><br>* `Eventual` (default): Eventual consistency.<br><br>* `Session`: Session consistency.<br><br>* `Global`: Global consistency. |
|ConsistentReadTimeoutMs |Long |No |20 |The consistency read wait timeout. The default value is 10 ms. The value range is 0~60,000, and the unit is ms (milliseconds). When this parameter is set to 0, no waiting is required. |
|ConsistentReadTimeoutAction |String |No |TransMaster |Set the method used by the proxy to handle read requests when the read\-only node fails to catch up with the target position within the timeout period. Values are as follows:<br><br><br>* `TransMaster` (default): Forward to the primary node.<br><br>* `Error`: Return an error. |

## Response parameter

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|InstanceId |String |mysql\-3c25f219\*\*\*\* |Instance ID. |
|EndpointId |String |mysql\-3c25f219\*\*\*\*\-custom\-eeb5 |Endpoint ID. |

## Sample

### Sample request

```json
POST /?Action=CreateDBEndpoint&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-3c25f219****",
    "EndpointName": "自定义终端",
    "EndpointType": "Custom",
    "Nodes": "Primary",
    "ReadWriteMode": "ReadWrite",
    "AutoAddNewNodes": true,
    "CustomRouteStrategy": {
        "KeywordRouteStrategy": [
            {
                "SQLKeyword": "select",
                "NodeType": "ReadOnly"
            }
        ]
    }
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230302225000051F23B8DD57341993BE",
        "Action": "CreateDBEndpoint",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "EndpointId": "mysql-f23648f2****-custom-eeb5",
        "InstanceId": "mysql-f23648f2****"
    }
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
