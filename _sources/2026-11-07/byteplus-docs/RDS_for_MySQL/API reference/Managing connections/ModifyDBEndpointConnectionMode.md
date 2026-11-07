---
title: "ModifyDBEndpointConnectionMode"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpointconnectionmode"
---

## Request type

Asynchronous request.

## Precautions

* The endpoint type can be changed only when the database proxy service for the instance is enabled.

* The connection endpoint type can be modified only for double\-node instances.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBEndpointConnectionMode&serviceCode=rds_mysql&version=2022-01-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-25651c34\*\*\*\* |Instance ID. |
|EndpointId |String |Yes |mysql\-25651c34\*\*\*\*\-cluster |Connect endpoint ID. |
|ConnectionMode |String |Yes |Proxy |The connection mode of the endpoint. Values:<br><br><br>* `Proxy`: proxy endpoint (default).<br><br>* `Direct`: direct endpoint.<br><br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail) API to query the status of the database proxy of the instance.<br><br><br>   * > If the database proxy of the instance is enabled, the value can be `Proxy` or `Direct`.<br><br><br>   * > If the database proxy of the instance is disabled, the value can only be `Direct`.<br><br><br>* > The connection endpoint type of a multiple\-node instance cannot be modified.<br> |
|CreateDBEndpointReq |Object of [CreateDBEndpointReq](https://docs.byteplus.com/en/docs/40/54517#createdbendpointreq) |Yes |See the request example. |The configuration of the connection endpoint after conversion. |

### CreateDBEndpointReq

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|EndpointType |String |Yes |Custom |Connection endpoint type. Value:<br><br><br>* `Custom`: customized endpoint.<br><br>* `Cluster`: default endpoint. |
|InstanceId |String |Yes |mysql\-e26822cf\*\*\*\* |Instance ID. |
|Nodes |String |Yes |Primary |A list of node IDs configured for the connection endpoint.<br><br>> **tip**<br><br><br><br>* > To add the primary node to the Endpoint, enter Primary instead of the primary Node ID.<br><br><br>* > Separate multiple Node IDs with commas (,).<br><br><br>* > A direct endpoint can be connected to only one node.<br> |
|Description |String |No |This is a description of the connection endpoint. |Remarks. |
|EndpointName |String |No |TestEndpoint |Instance endpoint name.<br><br><br>* It cannot start with a digit or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length must be between 1 and 64 characters.<br><br><br>> **tip**<br><br><br>> If this parameter is not specified, the endpoint name will not be modified.<br> |
|ConnectionPoolType |String |No |Direct |Sets the connection pool type for the endpoint when it is converted to a proxy endpoint. Values:<br><br><br>* `Transaction`: transaction\-level connection pool. Default value.<br><br>* `Direct`: direct connection mode. |
|IdleConnectionReclaim |Boolean |No |true |Specifies whether to enable the wait_timeout feature for the endpoint when converting it to a proxy endpoint. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value. |
|AutoAddNewNodes |Boolean |No |false |Specifies whether to automatically add new nodes to the endpoint when it is converted to a proxy endpoint. Values:<br><br><br>* `true`: Joins automatically. Default value.<br><br>* `false`: Does not join automatically. |
|ReadWriteMode |String |No |ReadWrite |The read/write mode for the connection endpoint. Values:<br><br><br>* `ReadWrite`: read/write.<br><br>* `ReadOnly`: read\-only.<br><br><br>> **tip**<br><br><br><br>* > When used as a request parameter, the default value is `ReadWrite`.<br><br><br>* > This parameter is valid only when EndpointType is set to `Custom`.<br> |
|ReadWriteSpliting |Boolean |No |false |Sets whether to enable read/write separation for the endpoint when converting to a proxy endpoint. Values:<br><br><br>* `yes`: yes. Default value.<br><br>* `false`: no. |
|MultiStatementsMode |String |No |Loose |Sets the multi\-statements mode for the endpoint when converting it to a proxy endpoint. Values:<br><br><br>* `Strict`: strict mode. Default value.<br><br>* `Loose`: loose mode. |
|OverloadProtection |Boolean |No |false |When converting to a proxy endpoint, set whether to enable the overload protection feature for the endpoint. Values:<br><br><br>* `yes`: yes. Default value.<br><br>* `false`: no. |
|MasterProtectorTimeout |Integer |No |100 |Set the overload protection timeout for the endpoint when converting it to a proxy endpoint. The value range is an integer from 60 to 7,200. The default value is 60, and the unit is seconds. |
|ReadOnlyNodeDistributionType |String |No |RoundRobinCustom |Sets the read weight allocation mode for the endpoint when converting to a proxy endpoint. This parameter is required when read/write separation is set to `true`. As a request parameter for the CreateDBEndpoint and ModifyDBEndpoint APIs, the value range is as follows:<br><br><br>* `LoadSchedule`: load scheduling.<br><br>* `RoundRobinCustom`: round robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: round robin scheduling with automatic weight assignment. As a response parameter for the DescribeDBInstanceDetail API, the value range is as follows:<br><br>* `Default`: automatic assignment based on specification weights.<br><br>* `Custom`: custom weight assignment.<br><br>* `RoundRobin`: round robin scheduling.<br><br>* `LoadSchedule`: load scheduling.<br><br>* `RoundRobinCustom`: round robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: round robin scheduling with automatic weight assignment. |
|ReadOnlyNodeWeight |Array of [NodeWeightObject](https://docs.byteplus.com/en/docs/40/54517#nodeweightobject) |No |See the request example. |The read weight allocation policy for the customized endpoint when it is converted to a proxy endpoint. |
|MasterNodeRouting |Boolean |No |true |Specifies whether to enable primary node routing. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br>> **tip**<br><br><br>> Only the proxy endpoint supports this setting.<br> |
|ReadOnlyNodeMaxDelayTime |Integer |No |40 |The latency threshold for the read\-only node. The value can be an integer from 1 to 3,600. The default value is 30. The unit is seconds. |
|ImplicitTransSplit |Boolean |No |false |When converting to a proxy endpoint, set whether to enable the transaction separation feature for the endpoint. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value. |
|CustomRouteStrategy |Object of [CustomRouteStrategy](https://docs.byteplus.com/en/docs/40/54517#customroutestrategy) |No |See the request example. |SQL forwarding rules for the connection endpoint. |
|ConsistentReadConfig |Object of [ConsistentReadConfig](https://docs.byteplus.com/en/docs/40/54517#consistentreadconfig) |No |See the request example. |Set the consistency level. |

### NodeWeightObject

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|NodeId |String |No |mysql\-050b3e08\*\*\*\*\-2 |Read\-only node requires passing in NodeId; primary node does not require it. |
|NodeType |String |No |Primary |Node type.<br><br><br>* `Primary`: primary node.<br><br>* `ReadOnly`: read\-only node. |
|Weight |Integer |No |100 |The read weight of the node. The step size is 100, and the valid value range is 0~10000.<br><br>> **tip**<br><br><br>> The read weight of a single node can be set to 0, but the sum of read weights for all nodes must be greater than or equal to 100.<br> |

### CustomRouteStrategy

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|KeywordRouteStrategy |Array of [KeywordRouteStrategy](https://docs.byteplus.com/en/docs/40/54517#keywordroutestrategy) |No |Refer to the sample. |Custom routing policy. |

### KeywordRouteStrategy

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
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

null

## Sample

### Request example 1 Converting a connection endpoint to a direct endpoint

```json
POST /?Action=ModifyDBEndpointConnectionMode&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-25651c34****",
    "EndpointId": "mysql-25651c34****-cluster",
    "ConnectionMode": "Direct",
    "CreateDBEndpointReq": {
        "InstanceId": "mysql-25651c34****",
        "EndpointType": "Cluster",
        "Nodes": "Primary"
    }
}
```

### Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "20250606170159831A107E095666D8676C-157121",
        "Action": "ModifyDBEndpointConnectionMode",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```

### Request example 2 Converting a direct endpoint to a proxy endpoint

```json
POST /?Action=ModifyDBEndpointConnectionMode&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-25651c34****",
    "EndpointId": "mysql-25651c34****-cluster",
    "ConnectionMode": "Proxy",
    "CreateDBEndpointReq": {
        "InstanceId": "mysql-25651c34****",
        "EndpointType": "Cluster",
        "Nodes": "Primary,mysql-25651c34****-r399d"
    }
}
```

### Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "20250606170252D33B79CAF18434F0B6DC-1db1c3",
        "Action": "ModifyDBEndpointConnectionMode",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
