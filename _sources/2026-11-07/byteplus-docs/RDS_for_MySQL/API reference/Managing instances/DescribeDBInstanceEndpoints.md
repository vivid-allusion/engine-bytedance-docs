---
title: "DescribeDBInstanceEndpoints"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceEndpoints"
---

Call the DescribeDBInstanceEndpoints API to query the list of connection addresses of the instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f83edc2e\*\*\*\* |Instance ID. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Endpoints |Object[] |Please refer to the return example. |Connection information of the instance |
|Addresses |Object[] |Please refer to the return example. |Address list. |
|DNSVisibility |Boolean |false |* `false`: Private network resolution of Volcano Engine (default).<br><br>* `true`: Private network and public network resolution of Volcano Engine. |
|Domain |String |mysql1d797b6f\*\*\*\*.rds.ivolces.com |Connect to the domain name. |
|EipId |String |eip\-13g6t81tglmgw3n6nu4vt\*\*\*\* |The ID of the EIP, which is only valid for the Public address. |
|IPAddress |String |10. ** *.* ** .3 |IP address. |
|InternetProtocol |String |IPv4 |IP protocol version. The value is `IPv4`. |
|NetworkType |String |Private |Network address type, with the following values:<br><br><br>* `Private`: Private network address.<br><br>* `Public`: Public network address. |
|Port |String |3306 |Port. |
|SubnetId |String |subnet\-2bzr8zdx5o8ao2dx0efq4\*\*\*\* |Subnet ID, only valid for Private addresses. |
|EipLocked |Boolean |false |Whether the EIP used to connect to the terminal has been shut down due to arrears. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|AutoAddNewNodes |String |Enable |When the terminal type is a read\-write terminal or a read\-only terminal, it supports setting whether a new node is automatically joined. Value:<br><br><br>* `Enable`: Automatically joined<br><br>* `Disable`: Not automatically joined (default). |
|ConnectionInfoTags |String[] |["Default"] |Connect the terminal tabs. |
|ConnectionMode |String |Proxy |Connection terminal type. Values:<br><br><br>* `Proxy`: Proxy terminal.<br><br>* `Direct`: Direct terminal.<br><br><br>tip<br><br><br>* If the database proxy function of the instance is enabled, the value can be `Proxy` or `Direct`.<br><br>* If the database proxy function of the instance is not enabled, the value can only be `Direct`.<br><br><br>You can call the [DescribeDBInstanceDetail](https://www.volcengine.com/docs/6313/170653) interface to query the opening status of the database proxy function of the instance. |
|ConnectionPoolType |String |Direct |The connection pool type of the proxy terminal. Values:<br><br><br>* `Transaction`: Transaction\-level connection pool. Default value.<br><br>* `Direct`: Direct connection mode. |
|Description |String |This is a description of connecting to the terminal. |The description information of connecting to the terminal. |
|EnableReadOnly |String |Enable |Whether global read\-only is enabled, value:<br><br><br>* `Enable`: Enabled.<br><br>* `Disable`: Not enabled. |
|EnableReadWriteSplitting |String |Enable |Whether read\-write separation has been enabled, with possible values:<br><br><br>* `Enable`: Enabled.<br><br>* `Disable`: Not enabled. |
|EndpointId |String |mysql\-050b3e08\*\*\*\* |Instance connection terminal ID. |
|EndpointName |String |Custom connection terminal |Instance connection terminal name. |
|EndpointType |String |Custom |Terminal type. The value is `Custom`, a custom terminal. |
|IdleConnectionReclaim |Boolean |true |Whether the idle connection recycling function is enabled.<br><br><br>* `true`: Enabled.<br><br>* `false`: Not enabled.<br><br><br>tip<br><br>This field will only be returned by the proxy terminal. |
|ImplicitTransSplit |Boolean |false |Whether to enable transaction separation. Value:<br><br><br>* `true`: Yes.<br><br>* `false`: No.<br><br><br>tip<br><br>Only the proxy terminal will return this field. |
|MasterNodeRouting |Boolean |false |Whether to enable the master node route. Value:<br><br><br>* `true`: Yes.<br><br>* `false`: No.<br><br><br>tip<br><br>This field will only be returned by the proxy terminal. |
|MasterProtectorTimeout |Integer |60 |Overload protection timeout. The value range is an integer between 60 and 7200, and the unit is seconds.<br><br>tip<br><br>Only the proxy terminal will return this field. |
|MultiStatementsMode |String |Loose |The Multi\-Statements mode of the proxy terminal. Values:<br><br><br>* `Strict`: Strict mode. Default value.<br><br>* `Loose`: Loose mode. |
|OverloadProtection |Boolean |false |Whether to turn on overload protection. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No.<br><br><br>tip<br><br>This field will only be returned by the proxy terminal. |
|ReadOnlyNodeDistributionType |String |LoadSchedule |Read the weight distribution mode. This parameter needs to be passed in when the read\-write separation setting is set to `true`. When used as a request parameter in the CreateDBEndpoint and ModifyDBEndpoint interfaces, the value range is as follows:<br><br><br>* `LoadSchedule`: Load scheduling.<br><br>* `RoundRobinCustom`: Round\-robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: Round\-robin scheduling with automatically assigned weights.<br><br><br>When used as a return parameter in the DescribeDBInstanceDetail interface, the value range is as follows:<br><br><br>* `Default`: Automatically assign weights according to the specification.<br><br>* `Custom`: Customize the weight distribution.<br><br>* `RoundRobin`: Round\-robin scheduling.<br><br>* `LoadSchedule`: Load scheduling.<br><br>* `RoundRobinCustom`: Round\-robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: Round\-robin scheduling with automatically assigned weights. |
|ReadOnlyNodeMaxDelayTime |Integer |40 |The read\-only node delay threshold. The value range is from 1 to 3600, and the default value is 30, with the unit being seconds. |
|ReadOnlyNodeWeight |Object[] |Please refer to the return example. |The list of nodes configured in the connection terminal and the corresponding read\-only weights. |
|NodeId |String |mysql\-050b3e08\*\*\*\*\-2 |The read\-only node needs to pass in the NodeId, while the master node does not need to pass in. |
|NodeType |String |Primary |Node types.<br><br><br>* `Primary`: Primary node.<br><br>* `ReadOnly`: Read\-only node. |
|Weight |Integer |100 |The read weight of the node, increasing by 100, with a maximum value of 10000.<br><br>tip<br><br>The weights cannot all be set to 0. |
|ReadWriteMode |String |ReadOnly |Read/Write Modes:<br><br><br>* `ReadWrite`: Read and write.<br><br>* `ReadOnly`: Read only. |
|EnableConnectionPersistent |Boolean |false |Whether to enable connection persistence. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |

## Sample request

```json
POST /?Action=DescribeDBInstanceEndpoints&Version=2022-01-01
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json
X-Date: 20180614T114308Z
Authorization: HMAC-SHA256 Credential=AKIAIAGMBG4SXSQQ****/20180614/ap-southeast-1/rds_mysql/request, SignedHeaders=accept;content-type;host;x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c8701d16****
{
    "InstanceId": "mysql-f83edc2e****"
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
