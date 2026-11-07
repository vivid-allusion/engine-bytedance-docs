---
title: "ModifyDBEndpoint"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpoint"
---

## Request type

Asynchronous request.

## Precautions

* Only custom endpoints can be modified.

* You can only modify the endpoint name and description of a custom direct endpoint.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBEndpoint&serviceCode=rds_mysql&version=2022-01-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-e26822cf\*\*\*\* |Instance ID. |
|EndpointId |String |Yes |mysql\-e26822cf\*\*\*\*\-cluster |Instance ID. |
|ReadWriteMode |String |No |ReadOnly |The read/write mode for the connection endpoint. Values:<br><br><br>* `ReadWrite`: read/write.<br><br>* `ReadOnly`: read\-only.<br><br><br>> **tip**<br><br><br>> When used as a request parameter, the default value is `ReadWrite`.<br> |
|EndpointName |String |No |Endpoint name |Instance endpoint name. The rules for the endpoint name are as follows:<br><br><br>* It cannot start with a digit or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length must be between 1 and 64 characters. |
|Description |String |No |Endpoint description |Endpoint description. The length is 1~255 characters. |
|Nodes |String |No |Primary,mysql\-e26822cf\*\*\*\*\-r90ab |Node list for endpoint configuration.<br><br>> **tip**<br><br><br><br>* > No node ID is needed for the primary node. Use the primary string.<br><br><br>* > **Double node instance**<br><br><br>   * > A proxy endpoint in read/write mode can be associated with only the primary node or with the primary node and up to 10 read\-only nodes; in Read\-only mode, it can only be associated with 1 to 10 read\-only nodes.<br><br><br>   * > For a direct endpoint, it can only be associated with the primary node in read/write mode, and only with 1 read\-only node in read\-only mode.<br><br><br>* > **Multiple node instances**<br><br><br>   * > The default endpoint is associated with all nodes of the instance, and the write endpoint is only associated with the primary node. Adjusting the associated nodes for the default and write endpoints is not supported.<br><br><br>   * > The read\-only endpoint is associated with all secondary nodes by default, and it can be associated with a minimum of one and a maximum of all secondary nodes. When adjusting the nodes associated with the read\-only endpoint of a multiple node instance, disable the **Associate all secondary nodes** function. After a secondary node is switched to the primary node, it will automatically be disassociated from the read\-only endpoint.<br><br><br>   * > Once a secondary node associated with the read\-only endpoint of a multiple node instance is switched to the primary node, the number of secondary nodes associated with the read\-only endpoint is reduced by one. If you need to maintain the original number of secondary nodes in the read\-only endpoint, you need to manually add a new secondary node. It is recommended to configure enough secondary nodes for the endpoint to handle business traffic.<br><br><br>* > To ensure high availability in read\-only mode, it is recommended to associate the read\-only endpoint with at least two secondary nodes (for multiple node instances) or two read\-only nodes (for double node instances).<br> |
|AutoAddNewNodes |Boolean |No |true |When the endpoint type is read/write or read\-only, setting whether the new node joins automatically is supported. Values:<br><br><br>* `true`: Joins automatically.<br><br>* `false`: Does not join automatically (Default).<br><br><br>> **tip**<br><br><br><br>* > The "Automatically add new nodes" feature for the connection endpoint of a multiple\-node instance cannot be adjusted. The "Automatically add new nodes" feature is enabled by default for the default endpoint and read\-only endpoint, and disabled for the write endpoint.<br><br><br>* > Single\-node instances do not support this feature.<br> |
|ReadWriteSpliting |Boolean |No |true |Enable read/write separation. Values:<br><br><br>* `true`: enable read/write separation.<br><br>* `false`: disable read/write separation (default).<br><br><br>> **tip**<br><br><br><br>* > This parameter is supported when ReadWriteMode is `ReadWrite`, but not when it is `ReadOnly`. This parameter only takes effect on the Default_endpoint.<br><br><br>* > Single\-node instances do not support this feature.<br> |
|ReadOnlyNodeMaxDelayTime |Integer |No |30 |The maximum latency threshold for the read\-only node. When the read\-only node latency exceeds this value, read traffic does not go to that node. The value can be an integer from 1 to 3,600. The default value is 30. The unit is seconds.<br><br>> **tip**<br><br><br>> This parameter can be set for a Read/Write endpoint after Read/Write separation is enabled.<br> |
|ReadOnlyNodeDistributionType |String |No |LoadSchedule |Read weight distribution mode. This parameter is required when read/write separation is set to `true`. As a request parameter for the CreateDBEndpoint and ModifyDBEndpoint APIs, the value range is as follows:<br><br><br>* `LoadSchedule`: load scheduling.<br><br>* `RoundRobinCustom`: round robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: round robin scheduling with automatic weight assignment. As a response parameter for the DescribeDBInstanceDetail API, the value range is as follows:<br><br>* `Default`: automatic assignment based on specification weights.<br><br>* `Custom`: custom weight assignment.<br><br>* `RoundRobin`: round robin scheduling.<br><br>* `LoadSchedule`: load scheduling.<br><br>* `RoundRobinCustom`: round robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: round robin scheduling with automatic weight assignment.<br><br><br>> **tip**<br><br><br><br>* > Multiple node instances only support `RoundRobinAuto`.<br><br><br>* > Single\-node instances do not support this feature.<br><br><br>* > When the `ConnectionMode` parameter is set to `Proxy`, it is a required field. If set to `Direct`, this parameter takes no effect.<br> |
|ReadOnlyNodeWeight |Array of [NodeWeightObject](https://docs.byteplus.com/en/docs/40/15474#nodeweightobject) |No |[<br><br>{<br><br>"NodeType" : "Primary",<br><br>"Weight" : 100<br><br>},<br><br>{<br><br>"NodeId" : "mysql\-e26822cf\*\*\*\*\-r84eb",<br><br>"Weight" : 100<br><br>},<br><br>{<br><br>"NodeId" : "mysql\-e26822cf\*\*\*\*\-r90ab",<br><br>"Weight" : 200<br><br>}<br><br>] |Custom read weight allocation, which means passing the read request weights of the primary and read\-only nodes. Increments by 100 up to a maximum of 10,000. When ReadOnlyNodeDistributionType is set to `Custom`, this parameter must be provided.<br><br>> **tip**<br><br><br><br>* > The primary node requires NodeType to be Primary, and the read\-only node requires NodeID.<br><br><br>* > The weights cannot all be set to 0.<br> |
|IdleConnectionReclaim |Boolean |No |true |Indicates whether to enable Wait_timeout.<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled (Default).<br><br><br>> **tip**<br><br><br>> Single\-node instances do not support this feature.<br> |
|ConnectionPoolType |String |No |Direct |The connection pool type of the proxy endpoint. Values:<br><br><br>* `Transaction`: transaction\-level connection pool. Default value.<br><br>* `Direct`: direct connection mode.<br><br><br>> **tip**<br><br><br><br>* > Single\-node instances do not support this feature.<br><br><br>* > When the ConnectionMode parameter is set to Proxy, it is a required field. If set to Direct, this parameter takes no effect.<br> |
|MultiStatementsMode |String |No |Loose |The Multi\-Statements mode of the proxy endpoint. Values:<br><br><br>* `Strict`: strict mode. Default value.<br><br>* `Loose`: loose mode.<br><br><br>> **tip**<br><br><br><br>* > Single\-node instances do not support this feature.<br><br><br>* > When the `ConnectionMode` parameter is set to `Proxy`, it is a required field. If set to `Direct`, this parameter takes no effect.<br> |
|OverloadProtection |Boolean |No |false |Whether overload protection is enabled. Values:<br><br><br>* `yes`: yes. Default value.<br><br>* `false`: no.<br><br><br>> **tip**<br><br><br><br>* > Only proxy endpoints support the overload protection feature.<br><br><br>* > The overload protection feature is effective only when read/write separation for the connection endpoint is enabled and the primary node is not the only node of the current connection endpoint.<br><br><br>* > Single\-node instances do not support this feature.<br> |
|MasterProtectorTimeout |Integer |No |60 |Overload protection timeout. The value range is an integer from 60 to 7,200. The default value is 60, and the unit is seconds.<br><br>> **tip**<br><br><br><br>* > Only proxy endpoints support the overload protection feature.<br><br><br>* > This setting is effective only when OverloadProtection is set to `true`.<br> |
|MasterNodeRouting |Boolean |No |false |Specifies whether to enable primary node routing. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br>> **tip**<br><br><br><br>* > Only the proxy endpoint supports this setting.<br><br><br>* > Multiple\-node and single\-node instances do not support this feature.<br> |
|ImplicitTransSplit |Boolean |No |false |Indicates whether to enable transaction splitting. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br>> **tip**<br><br><br>> Only the proxy endpoint supports this setting.<br> |
|ConnectAllSlaveNodes |Boolean |No |false |Indicates whether to associate all secondary nodes. Values:<br><br><br>* `yes`: yes. Default value.<br><br>* `false`: no.<br><br><br>> **tip**<br><br><br><br>* > Only read\-only endpoints of multiple node instances support this configuration.<br><br><br>* > To disable this function, the instance must have at least two secondary nodes.<br> |
|EnableConnectionPersistent |Boolean |No |false |Whether to enable connection persistence for the connection endpoint. Values:<br><br><br>* `true`: yes.<br><br>* `false`: No (default).<br><br><br>> **tip**<br><br><br>> Only the proxy endpoint supports this setting.<br> |
|CustomRouteStrategy |Object of [CustomRouteStrategy](https://docs.byteplus.com/en/docs/40/15474#customroutestrategy) |No |See the request example. |Customized routing and forwarding rules |
|ConsistentReadConfig |Object of [ConsistentReadConfig](https://docs.byteplus.com/en/docs/40/15474#consistentreadconfig) |No |See the request example. |Set the consistency level. |

### NodeWeightObject

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|NodeId |String |No |mysql\-050b3e08\*\*\*\*\-2 |Read\-only node requires passing in NodeId; primary node does not require it. |
|NodeType |String |No |Primary |Node type.<br><br><br>* `Primary`: primary node.<br><br>* `ReadOnly`: read\-only node. |
|Weight |Integer |No |100 |The read weight of the node. The step size is 100, and the valid value range is 0~10000.<br><br>> **tip**<br><br><br>> The read weight of a single node can be set to 0, but the sum of read weights for all nodes must be greater than or equal to 100.<br> |

### CustomRouteStrategy

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|KeywordRouteStrategy |Array of [KeywordRouteStrategy](https://docs.byteplus.com/en/docs/40/15474#keywordroutestrategy) |No |Refer to the sample. |Custom routing policy. |

### KeywordRouteStrategy

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|NodeType |String |No |Primary |Target for the SQL forwarding rule. Values:<br><br><br>* `Primary`: primary node.<br><br>* `Secondary`: secondary node.<br><br>* `ReadOnly`: read\-only node.<br><br><br>> **tip**<br><br><br><br>* > For a double\-node instance, you can select the primary node or the read\-only node.<br><br><br>* > For a multiple node instance, you can select the primary node or the secondary node.<br> |
|SQLKeyword |String |Yes |Select |Keywords of the forwarding rule. The rules for setting SQL keywords are as follows:<br><br><br>* Each rule can contain a maximum of 20 keywords.<br><br>* The maximum length is 64 characters, and it can contain English letters, digits, underscores `_`, `@`, `#`, `:=`, and Chinese characters.<br><br><br>> **tip**<br><br><br><br>* > SQL keywords are case\-sensitive. Changes in the case of keywords may cause rules to fail silently.<br><br><br>* > When you configure SQL forwarding rules through the API, the keyword can be an empty string or spaces. In this case, all SQL statements are matched, meaning all requests are forwarded to the target node.<br> |

### ConsistentReadConfig

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|EnableConsistentRead |Boolean |No |true |Whether to enable consistency read. Values are as follows:<br><br><br>* `true`: Enabled.<br><br>* `false`: disabled. |
|ConsistentReadMode |String |No |Session |The consistency read level.<br><br><br>* `Eventual` (default): Eventual consistency.<br><br>* `Session`: Session consistency.<br><br>* `Global`: Global consistency. |
|ConsistentReadTimeoutMs |Long |No |20 |The consistency read wait timeout. The default value is 10 ms. The value range is 0~60,000, and the unit is ms (milliseconds). When this parameter is set to 0, no waiting is required. |
|ConsistentReadTimeoutAction |String |No |TransMaster |Set the method used by the proxy to handle read requests when the read\-only node fails to catch up with the target position within the timeout period. Values are as follows:<br><br><br>* `TransMaster` (default): Forward to the primary node.<br><br>* `Error`: Return an error. |

## Response parameter

null

## Sample

### Sample request

```json
POST /?Action=ModifyDBEndpoint&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-3c25f219bdbf",
    "EndpointId": "mysql-3c25f219bdbf-custom-e020",
    "EndpointName": "自定义终端",
    "Nodes": "Primary,mysql-e26822cf****-r90ab",
    "AutoAddNewNodes": true,
    "ReadWriteMode": "ReadWrite",
    "ReadOnlyNodeMaxDelayTime": 30,
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
        "RequestId": "20230111155941DE19D8CD8EB9198A3133",
        "Action": "ModifyDBEndpoint",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
