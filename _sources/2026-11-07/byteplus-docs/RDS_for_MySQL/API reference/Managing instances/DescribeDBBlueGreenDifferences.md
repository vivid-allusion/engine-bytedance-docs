---
title: "DescribeDBBlueGreenDifferences"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBBlueGreenDifferences"
---

Call the DescribeDBBlueGreenDifferences interface to query the differences between the blue instance and the green instance in the blue\-green deployment.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f83edc2e\*\*\*\* |The ID of the blue instance in blue\-green deployment. |
|GreenEndpoints |Object[] |No |Please refer to the request example. |Connection information of the instance. |
|Addresses |Object[] |No |Please refer to the return example. |Address list. |
|DNSVisibility |Boolean |No |false |* `false`: Private network resolution of Volcano Engine (default).<br><br>* `true`: Private network and public network resolution of Volcano Engine. |
|Domain |String |No |mysql1d797b6f\*\*\*\*.rds.ivolces.com |Connect to the domain name. |
|EipId |String |No |eip\-13g6t81tglmgw3n6nu4vt\*\*\*\* |The ID of the EIP, which is only valid for the Public address. |
|IPAddress |String |No |10. ** *.* ** .3 |IP address. |
|InternetProtocol |String |No |IPv4 |IP protocol version. The value is `IPv4`. |
|NetworkType |String |No |Private |Network address type, with the following values:<br><br><br>* `Private`: Private network address.<br><br>* `Public`: Public network address. |
|Port |String |No |3306 |Port. |
|SubnetId |String |No |subnet\-2bzr8zdx5o8ao2dx0efq4\*\*\*\* |Subnet ID, only valid for Private addresses. |
|EipLocked |Boolean |No |false |Whether the EIP used to connect to the terminal has been shut down due to arrears. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|AutoAddNewNodes |String |No |Enable |When the terminal type is a read\-write terminal or a read\-only terminal, it supports setting whether a new node is automatically joined. Value:<br><br><br>* `Enable`: Automatically joined<br><br>* `Disable`: Not automatically joined (default). |
|ConnectionInfoTags |String[] |No |["Default"] |Connect the terminal tabs. |
|ConnectionMode |String |No |Proxy |Connection terminal type. Values:<br><br><br>* `Proxy`: Proxy terminal.<br><br>* `Direct`: Direct terminal.<br><br><br>tip<br><br><br>* If the database proxy function of the instance is enabled, the value can be `Proxy` or `Direct`.<br><br>* If the database proxy function of the instance is not enabled, the value can only be `Direct`.<br><br><br>You can call the [DescribeDBInstanceDetail](https://www.volcengine.com/docs/6313/170653) interface to query the opening status of the database proxy function of the instance. |
|ConnectionPoolType |String |No |Direct |The connection pool type of the proxy terminal. Values:<br><br><br>* `Transaction`: Transaction\-level connection pool. Default value.<br><br>* `Direct`: Direct connection mode. |
|Description |String |No |This is a description of connecting to the terminal. |The description information of connecting to the terminal. |
|EnableReadOnly |String |No |Enable |Whether global read\-only is enabled, value:<br><br><br>* `Enable`: Enabled.<br><br>* `Disable`: Not enabled. |
|EnableReadWriteSplitting |String |No |Enable |Whether read\-write separation has been enabled, with possible values:<br><br><br>* `Enable`: Enabled.<br><br>* `Disable`: Not enabled. |
|EndpointId |String |No |mysql\-050b3e08\*\*\*\* |Instance connection terminal ID. |
|EndpointName |String |No |Custom connection terminal |Instance connection terminal name. |
|EndpointType |String |No |Custom |Terminal type. The value is `Custom`, a custom terminal. |
|IdleConnectionReclaim |Boolean |No |true |Whether the idle connection recycling function is enabled.<br><br><br>* `true`: Enabled.<br><br>* `false`: Not enabled.<br><br><br>tip<br><br>This field will only be returned by the proxy terminal. |
|ImplicitTransSplit |Boolean |No |false |Whether to enable transaction separation. Value:<br><br><br>* `true`: Yes.<br><br>* `false`: No.<br><br><br>tip<br><br>Only the proxy terminal will return this field. |
|MasterNodeRouting |Boolean |No |false |Whether to enable the master node route. Value:<br><br><br>* `true`: Yes.<br><br>* `false`: No.<br><br><br>tip<br><br>This field will only be returned by the proxy terminal. |
|MasterProtectorTimeout |Integer |No |60 |Overload protection timeout. The value range is an integer between 60 and 7200, and the unit is seconds.<br><br>tip<br><br>Only the proxy terminal will return this field. |
|MultiStatementsMode |String |No |Loose |The Multi\-Statements mode of the proxy terminal. Values:<br><br><br>* `Strict`: Strict mode. Default value.<br><br>* `Loose`: Loose mode. |
|OverloadProtection |Boolean |No |false |Whether to turn on overload protection. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No.<br><br><br>tip<br><br>This field will only be returned by the proxy terminal. |
|ReadOnlyNodeDistributionType |String |No |LoadSchedule |Read the weight distribution mode. This parameter needs to be passed in when the read\-write separation setting is set to `true`. When used as a request parameter in the CreateDBEndpoint and ModifyDBEndpoint interfaces, the value range is as follows:<br><br><br>* `LoadSchedule`: Load scheduling.<br><br>* `RoundRobinCustom`: Round\-robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: Round\-robin scheduling with automatically assigned weights.<br><br><br>When used as a return parameter in the DescribeDBInstanceDetail interface, the value range is as follows:<br><br><br>* `Default`: Automatically assign weights according to the specification.<br><br>* `Custom`: Customize the weight distribution.<br><br>* `RoundRobin`: Round\-robin scheduling.<br><br>* `LoadSchedule`: Load scheduling.<br><br>* `RoundRobinCustom`: Round\-robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: Round\-robin scheduling with automatically assigned weights. |
|ReadOnlyNodeMaxDelayTime |Integer |No |40 |The read\-only node delay threshold. The value range is from 1 to 3600, and the default value is 30, with the unit being seconds. |
|ReadOnlyNodeWeight |Object[] |No |Please refer to the return example. |The list of nodes configured in the connection terminal and the corresponding read\-only weights. |
|NodeId |String |No |mysql\-050b3e08\*\*\*\*\-2 |The read\-only node needs to pass in the NodeId, while the master node does not need to pass in. |
|NodeType |String |No |Primary |Node types.<br><br><br>* `Primary`: Primary node.<br><br>* `ReadOnly`: Read\-only node. |
|Weight |Integer |No |100 |The read weight of the node, increasing by 100, with a maximum value of 10000.<br><br>tip<br><br>The weights cannot all be set to 0. |
|ReadWriteMode |String |No |ReadOnly |Read/Write Modes:<br><br><br>* `ReadWrite`: Read and write.<br><br>* `ReadOnly`: Read only. |
|EnableConnectionPersistent |Boolean |No |false |Whether to enable connection persistence. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|BlueInfoDifference |Object |Please refer to the return example. |Details of the blue instance in blue\-green deployment. |
|Nodes |Object[] |Please refer to the return example. |The node information of the instance. |
|CreateTime |String |2024\-10\-29T08:45:28.000Z |The creation time of the node (UTC time). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|DelayReplicationTime |Long |1000 |The delay replication time of the read\-only node, with a value ranging from 0 to 604800, and the unit is seconds. |
|InstanceId |String |mysql\-h441603c\*\*\*\* |Instance ID. |
|Memory |Integer |2 |Memory size, in units of GiB. |
|NodeId |String |mysql\-h441603c\*\*\*\*\-01 |Node ID. |
|NodeSpec |String |rds.mysql.d1.n.2c4g |Node Specifications. For details about node specifications, see [Product Specifications](https://docs.byteplus.com/en/docs/6313/74505). |
|NodeStatus |String |Running |Node status, with possible values:<br><br><br>* `Running`: In operation.<br><br>* `Creating`: In the process of being created.<br><br>* `Deleting`: In the process of being deleted.<br><br>* `Restarting`: In the process of restarting.<br><br>* `Restoring`: In the process of restoration.<br><br>* `Updating`: In the process of being updated.<br><br>* `Upgrading`: In the process of being upgraded.<br><br>* `Error`: Error. |
|NodeType |String |Primary |Node type. Values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: Secondary node.<br><br>* `ReadOnly`: Read\-only node. |
|RegionId |String |cn\-beijing |Region ID. You can call [DescribeRegions](https://docs.byteplus.com/en/docs/6313/170644) to query and use this parameter to specify the region where the instance is to be created. |
|SyncDelay |Long |28 |The delay time between the node and the master node. The unit is milliseconds (ms). |
|UpdateTime |String |2024\-10\-31T08:45:28.000Z |The node updates the local time. |
|VCPU |Integer |1 |The number of CPU cores of the node. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|Endpoints |Object[] |Please refer to the return example. |Connection information of the instance. |
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
|ProxyDetail |Object |Please refer to the return example. |Proxy configuration information of the instance. |
|DBProxyStatus |String |Shutdown |The status of the database proxy function of the instance. Values:<br><br><br>* `Creating`: The proxy is being started.<br><br>* `Running`: The proxy is running.<br><br>* `Shutdown`: The proxy has been shut down.<br><br>* `Deleting`: The proxy is being shut down. |
|ProxyResourceInfo |Object |Please refer to the return example. |The resource information of the database proxy service of the instance. |
|MaxProxyCpuNum |Integer |1024 |The maximum number of cores that the user can configure for the database proxy service. |
|MinProxyCpuNum |Integer |2 |The minimum number of cores that a user can configure for the database proxy service. |
|CurrentProxyCpuNum |Integer |2 |The number of cores of the current instance database proxy service. |
|ChargeDetail |Object |Please refer to the return example. |Billing information for the instance. |
|ChargeType |String |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: Pay\-as\-you\-go (post\-payment).<br><br>* `PrePaid`: Annual and monthly subscription (pre\-payment). |
|AutoRenew |Boolean |true |Whether to automatically renew in the prepaid scenario.<br><br><br>* `true`: Automatically renew upon expiration.<br><br>* `false`: Do not automatically renew upon expiration. |
|PeriodUnit |String |Month |The purchase cycle in the prepaid scenario.<br><br><br>* `Month`: The purchase cycle is monthly.<br><br>* `Year`: The purchase cycle is yearly.<br><br><br>tip<br><br>When this parameter is used as a request parameter, the default value is `Month`. |
|Period |Integer |1 |The purchase duration in the prepaid scenario.<br><br>tip<br><br><br>* When this parameter is used as a request parameter, the default value is `1`.<br><br>* When the value of PeriodUnit is `Year`, the value range of Period is 1~3.<br><br>* When the value of PeriodUnit is `Month`, the value range of Period is 1~9. |
|ChargeStatus |String |Normal |Billing status of the instance. Values:<br><br><br>* `Normal`: Normal.<br><br>* `Overdue`: Arrears.<br><br>* `Unpaid`: Waiting for payment. |
|ChargeStartTime |String |2025\-07\-22T13:10:15.000Z |The billing start time of the instance (UTC time). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|ChargeEndTime |String |2025\-08\-22T15:59:59.000Z |The billing end time (UTC time) of the yearly and monthly subscribed instances. The format is `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br>tip<br><br>If the queried instance is a pay\-as\-you\-go instance, this field will be returned as empty. |
|OverdueTime |String |2025\-08\-23T04:00:00.000Z |The time (UTC time) when the instance is shut down due to arrears (pay\-as\-you\-go) or expiration (yearly/monthly subscription). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|OverdueReclaimTime |String |2025\-08\-29T15:59:59.000Z |The expected release time (UTC time) after the instance is shut down due to arrears (pay\-as\-you\-go) or expiration (yearly or monthly subscription). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|TempModifyStartTime |String |2022\-01\-01T10:10:10.000Z |The start time of the temporary upgrade (UTC time). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br>tip<br><br>For instances that are not in the temporary upgrade period, this field will not be returned. |
|TempModifyEndTime |String |2022\-01\-01T10:10:09.000Z |The restoration time (UTC time) of the temporary upgrade. The format is `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br>tip<br><br>For instances not in the temporary upgrade period, this field is not returned. |
|Scene |String | |辅助字段，可以不暴露 |
|ParamDifference |Boolean |true |Whether there is a difference in parameter configuration between the blue instance and the green instance. Value:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|AllowSimpleInfos |Object[] |Please refer to the return example. |The difference information of the whitelists bound by the green instance and the blue instance. |
|AllowListId |String |acl\-f244c112cfc149c482d718187fb1\*\*\*\* |The ID of the whitelist. |
|AllowListDesc |String |## This is a description of the whitelist. |Description information of the whitelist. |
|AllowListName |String |Test whitelist |The name of the whitelist. |
|AllowListType |String |IPv4 |The types of the whitelist. |
|GreenInfoDifference |Object |Please refer to the return example. |Details of the green instance in blue\-green deployment. |
|Nodes |Object[] |Please refer to the return example. |The node information of the instance. |
|CreateTime |String |2024\-10\-29T08:45:28.000Z |The creation time of the node (UTC time). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|DelayReplicationTime |Long |1000 |The delay replication time of the read\-only node, with a value ranging from 0 to 604800, and the unit is seconds. |
|InstanceId |String |mysql\-h441603c\*\*\*\* |Instance ID. |
|Memory |Integer |2 |Memory size, in units of GiB. |
|NodeId |String |mysql\-h441603c\*\*\*\*\-01 |Node ID. |
|NodeSpec |String |rds.mysql.d1.n.2c4g |Node Specifications. For details about node specifications, see [Product Specifications](https://docs.byteplus.com/en/docs/6313/74505). |
|NodeStatus |String |Running |Node status, with possible values:<br><br><br>* `Running`: In operation.<br><br>* `Creating`: In the process of being created.<br><br>* `Deleting`: In the process of being deleted.<br><br>* `Restarting`: In the process of restarting.<br><br>* `Restoring`: In the process of restoration.<br><br>* `Updating`: In the process of being updated.<br><br>* `Upgrading`: In the process of being upgraded.<br><br>* `Error`: Error. |
|NodeType |String |Primary |Node type. Values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: Secondary node.<br><br>* `ReadOnly`: Read\-only node. |
|RegionId |String |cn\-beijing |Region ID. You can call [DescribeRegions](https://docs.byteplus.com/en/docs/6313/170644) to query and use this parameter to specify the region where the instance is to be created. |
|SyncDelay |Long |28 |The delay time between the node and the master node. The unit is milliseconds (ms). |
|UpdateTime |String |2024\-10\-31T08:45:28.000Z |The node updates the local time. |
|VCPU |Integer |1 |The number of CPU cores of the node. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|Endpoints |Object[] |Please refer to the return example. |Connection information of the instance. |
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
|ProxyDetail |Object |Please refer to the return example. |Proxy configuration information of the instance. |
|DBProxyStatus |String |Shutdown |The status of the database proxy function of the instance. Values:<br><br><br>* `Creating`: The proxy is being started.<br><br>* `Running`: The proxy is running.<br><br>* `Shutdown`: The proxy has been shut down.<br><br>* `Deleting`: The proxy is being shut down. |
|ProxyResourceInfo |Object |Please refer to the return example. |The resource information of the database proxy service of the instance. |
|MaxProxyCpuNum |Integer |1024 |The maximum number of cores that the user can configure for the database proxy service. |
|MinProxyCpuNum |Integer |2 |The minimum number of cores that a user can configure for the database proxy service. |
|CurrentProxyCpuNum |Integer |2 |The number of cores of the current instance database proxy service. |
|ChargeDetail |Object |Please refer to the return example. |Billing information for the instance. |
|ChargeType |String |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: Pay\-as\-you\-go (post\-payment).<br><br>* `PrePaid`: Annual and monthly subscription (pre\-payment). |
|AutoRenew |Boolean |true |Whether to automatically renew in the prepaid scenario.<br><br><br>* `true`: Automatically renew upon expiration.<br><br>* `false`: Do not automatically renew upon expiration. |
|PeriodUnit |String |Month |The purchase cycle in the prepaid scenario.<br><br><br>* `Month`: The purchase cycle is monthly.<br><br>* `Year`: The purchase cycle is yearly.<br><br><br>tip<br><br>When this parameter is used as a request parameter, the default value is `Month`. |
|Period |Integer |1 |The purchase duration in the prepaid scenario.<br><br>tip<br><br><br>* When this parameter is used as a request parameter, the default value is `1`.<br><br>* When the value of PeriodUnit is `Year`, the value range of Period is 1~3.<br><br>* When the value of PeriodUnit is `Month`, the value range of Period is 1~9. |
|ChargeStatus |String |Normal |Billing status of the instance. Values:<br><br><br>* `Normal`: Normal.<br><br>* `Overdue`: Arrears.<br><br>* `Unpaid`: Waiting for payment. |
|ChargeStartTime |String |2025\-07\-22T13:10:15.000Z |The billing start time of the instance (UTC time). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|ChargeEndTime |String |2025\-08\-22T15:59:59.000Z |The billing end time (UTC time) of the yearly and monthly subscribed instances. The format is `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br>tip<br><br>If the queried instance is a pay\-as\-you\-go instance, this field will be returned as empty. |
|OverdueTime |String |2025\-08\-23T04:00:00.000Z |The time (UTC time) when the instance is shut down due to arrears (pay\-as\-you\-go) or expiration (yearly/monthly subscription). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|OverdueReclaimTime |String |2025\-08\-29T15:59:59.000Z |The expected release time (UTC time) after the instance is shut down due to arrears (pay\-as\-you\-go) or expiration (yearly or monthly subscription). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|TempModifyStartTime |String |2022\-01\-01T10:10:10.000Z |The start time of the temporary upgrade (UTC time). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br>tip<br><br>For instances that are not in the temporary upgrade period, this field will not be returned. |
|TempModifyEndTime |String |2022\-01\-01T10:10:09.000Z |The restoration time (UTC time) of the temporary upgrade. The format is `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br>tip<br><br>For instances not in the temporary upgrade period, this field is not returned. |
|Scene |String | |辅助字段，可以不暴露 |
|ParamDifference |Boolean |true |Whether there is a difference in parameter configuration between the blue instance and the green instance. Value:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|AllowSimpleInfos |Object[] |Please refer to the return example. |The difference information of the whitelists bound by the green instance and the blue instance. |
|AllowListId |String |acl\-f244c112cfc149c482d718187fb1\*\*\*\* |The ID of the whitelist. |
|AllowListDesc |String |## This is a description of the whitelist. |Description information of the whitelist. |
|AllowListName |String |Test whitelist |The name of the whitelist. |
|AllowListType |String |IPv4 |The types of the whitelist. |

## Sample request

```json
POST /?Action=DescribeDBBlueGreenDifferences&Version=2022-01-01
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json
X-Date: 20180614T114308Z
Authorization: HMAC-SHA256 Credential=AKIAIAGMBG4SXSQQ****/20180614/ap-southeast-1/rds_mysql/request, SignedHeaders=accept;content-type;host;x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c8701d16****
{
    "InstanceId": "mysql-f83edc2e****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025072419293530F5681E45B67F0F0EAF-a2c310",
        "Action": "DescribeDBBlueGreenDifferences",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "BlueInfoDifference": {
            "ChargeDetail": {
                "AutoRenew": false,
                "ChargeEndTime": "",
                "ChargeStartTime": "",
                "ChargeStatus": "Normal",
                "ChargeType": "PostPaid",
                "Number": 1,
                "OverdueReclaimTime": "",
                "OverdueTime": "",
                "Period": 0,
                "PeriodUnit": "Year"
            },
            "Endpoints": [
                {
                    "Address": [
                        {
                            "AddressAffinity": false,
                            "DNSVisibility": false,
                            "Domain": "mysqlf83edc2e****.rds.cn-guangzhou.ivolces.com",
                            "EipId": "",
                            "IPAddress": "192.168.3.205",
                            "IPv6Address": "",
                            "InternetProtocol": "IPv4",
                            "NetworkType": "Private",
                            "Port": "3306",
                            "SubnetId": "subnet-3rf442t6a54w016nf3pg9****",
                            "UpgradeDomainSuffix": "rds.cn-guangzhou.ivolces.com"
                        }
                    ],
                    "Addresses": [
                        {
                            "AddressAffinity": false,
                            "DNSVisibility": false,
                            "Domain": "mysqlf83edc2e****.rds.cn-guangzhou.ivolces.com",
                            "EipId": "",
                            "IPAddress": "192.168.3.205",
                            "IPv6Address": "",
                            "InternetProtocol": "IPv4",
                            "NetworkType": "Private",
                            "Port": "3306",
                            "SubnetId": "subnet-3rf442t6a54w016nf3pg9****",
                            "UpgradeDomainSuffix": "rds.cn-guangzhou.ivolces.com"
                        }
                    ],
                    "ConnectionInfoTags": [
                        "Default"
                    ],
                    "ConnectionMode": "Direct",
                    "Description": "",
                    "EnableReadOnly": "Disable",
                    "EnableReadWriteSplitting": "Disable",
                    "EndpointId": "mysql-f83edc2e****-cluster",
                    "EndpointName": "",
                    "EndpointType": "Cluster",
                    "ReadOnlyNodeMaxDelayTime": 30,
                    "ReadOnlyNodeWeight": [
                        {
                            "NodeId": "",
                            "NodeType": "Primary",
                            "Weight": 100
                        }
                    ],
                    "ReadWriteMode": "ReadWrite"
                }
            ],
            "Nodes": [
                {
                    "CreateTime": "2025-07-23T03:40:54.000Z",
                    "DelayReplicationTime": 0,
                    "InstanceId": "mysql-f83edc2e****",
                    "Memory": 1,
                    "NodeId": "mysql-f83edc2e****-me954-0",
                    "NodeSpec": "rds.mysql.d1.n.1c1g",
                    "NodeStatus": "Running",
                    "NodeType": "Primary",
                    "RegionId": "cn-guangzhou",
                    "ShardId": "",
                    "SubInstanceId": "mysql-f83edc2e****-me954",
                    "SyncDelay": 0,
                    "UpdateTime": "",
                    "VCPU": 1,
                    "ZoneId": "cn-guangzhou-a"
                },
                {
                    "CreateTime": "2025-07-23T03:40:54.000Z",
                    "DelayReplicationTime": 0,
                    "InstanceId": "mysql-f83edc2e****",
                    "Memory": 1,
                    "NodeId": "mysql-f83edc2e****-s8e03-0",
                    "NodeSpec": "rds.mysql.d1.n.1c1g",
                    "NodeStatus": "Running",
                    "NodeType": "Secondary",
                    "RegionId": "cn-guangzhou",
                    "ShardId": "",
                    "SubInstanceId": "mysql-f83edc2e****-s8e03",
                    "SyncDelay": 0,
                    "UpdateTime": "",
                    "VCPU": 1,
                    "ZoneId": "cn-guangzhou-a"
                },
                {
                    "CreateTime": "2025-07-23T06:17:13.000Z",
                    "DelayReplicationTime": 0,
                    "InstanceId": "mysql-f83edc2e****",
                    "Memory": 2,
                    "NodeId": "mysql-f83edc2e****-r8386",
                    "NodeSpec": "rds.mysql.d1.n.1c2g",
                    "NodeStatus": "Running",
                    "NodeType": "ReadOnly",
                    "RegionId": "cn-guangzhou",
                    "ShardId": "",
                    "SubInstanceId": "mysql-f83edc2e****-r8386",
                    "SyncDelay": 0,
                    "UpdateTime": "",
                    "VCPU": 1,
                    "ZoneId": "cn-guangzhou-a"
                },
                {
                    "CreateTime": "2025-07-24T06:06:31.000Z",
                    "DelayReplicationTime": 0,
                    "InstanceId": "mysql-f83edc2e****",
                    "Memory": 4,
                    "NodeId": "mysql-f83edc2e****-r9dcf",
                    "NodeSpec": "rds.mysql.d1.n.2c4g",
                    "NodeStatus": "Running",
                    "NodeType": "ReadOnly",
                    "RegionId": "cn-guangzhou",
                    "ShardId": "",
                    "SubInstanceId": "mysql-f83edc2e****-r4974",
                    "SyncDelay": 0,
                    "UpdateTime": "",
                    "VCPU": 2,
                    "ZoneId": "cn-guangzhou-a"
                }
            ],
            "ParamDifference": true,
            "ProxyDetail": {
                "Charged": false,
                "DBProxyStatus": "Shutdown",
                "ProxyResourceInfo": {
                    "CurrentProxyCpuNum": 0,
                    "MaxProxyCpuNum": 1024,
                    "MinProxyCpuNum": 2
                }
            }
        },
        "GreenInfoDifference": {
            "AllowSimpleInfos": [
                {
                    "AllowListDesc": "这是一段白名单的描述信息。",
                    "AllowListId": "acl-f244c112cfc149c482d718187fb1****",
                    "AllowListName": "测试白名单",
                    "AllowListType": "IPv4"
                }
            ],
            "ChargeDetail": {
                "AutoRenew": false,
                "ChargeEndTime": "",
                "ChargeStartTime": "",
                "ChargeStatus": "Normal",
                "ChargeType": "PostPaid",
                "Number": 1,
                "OverdueReclaimTime": "",
                "OverdueTime": "",
                "Period": 0,
                "PeriodUnit": "Year"
            },
            "Endpoints": [
                {
                    "Address": [
                        {
                            "AddressAffinity": false,
                            "DNSVisibility": false,
                            "Domain": "mysql06c7db72****.rds.cn-guangzhou.ivolces.com",
                            "EipId": "",
                            "IPAddress": "192.168.3.206",
                            "IPv6Address": "",
                            "InternetProtocol": "IPv4",
                            "NetworkType": "Private",
                            "Port": "3306",
                            "SubnetId": "subnet-3rf442t6a54w016nf3pg9****",
                            "UpgradeDomainSuffix": "rds.cn-guangzhou.ivolces.com"
                        }
                    ],
                    "Addresses": [
                        {
                            "AddressAffinity": false,
                            "DNSVisibility": false,
                            "Domain": "mysql06c7db72****.rds.cn-guangzhou.ivolces.com",
                            "EipId": "",
                            "IPAddress": "192.168.3.206",
                            "IPv6Address": "",
                            "InternetProtocol": "IPv4",
                            "NetworkType": "Private",
                            "Port": "3306",
                            "SubnetId": "subnet-3rf442t6a54w016nf3pg9****",
                            "UpgradeDomainSuffix": "rds.cn-guangzhou.ivolces.com"
                        }
                    ],
                    "ConnectionInfoTags": [
                        "Default"
                    ],
                    "ConnectionMode": "Direct",
                    "Description": "",
                    "EnableReadOnly": "Enable",
                    "EnableReadWriteSplitting": "Disable",
                    "EndpointId": "mysql-06c7db72****-cluster",
                    "EndpointName": "",
                    "EndpointType": "Cluster",
                    "ReadOnlyNodeMaxDelayTime": 30,
                    "ReadOnlyNodeWeight": [
                        {
                            "NodeId": "",
                            "NodeType": "Primary",
                            "Weight": 100
                        }
                    ],
                    "ReadWriteMode": "ReadWrite"
                }
            ],
            "Nodes": [
                {
                    "CreateTime": "2025-07-24T03:48:24.000Z",
                    "DelayReplicationTime": 0,
                    "InstanceId": "mysql-06c7db72****",
                    "Memory": 1,
                    "NodeId": "mysql-06c7db72****-me2e1-0",
                    "NodeSpec": "rds.mysql.d1.n.1c1g",
                    "NodeStatus": "Running",
                    "NodeType": "Primary",
                    "RegionId": "cn-guangzhou",
                    "ShardId": "",
                    "SubInstanceId": "mysql-06c7db72****-me2e1",
                    "SyncDelay": 0,
                    "UpdateTime": "",
                    "VCPU": 1,
                    "ZoneId": "cn-guangzhou-a"
                },
                {
                    "CreateTime": "2025-07-24T03:48:25.000Z",
                    "DelayReplicationTime": 0,
                    "InstanceId": "mysql-06c7db72****",
                    "Memory": 1,
                    "NodeId": "mysql-06c7db72****-s6d85-0",
                    "NodeSpec": "rds.mysql.d1.n.1c1g",
                    "NodeStatus": "Running",
                    "NodeType": "Secondary",
                    "RegionId": "cn-guangzhou",
                    "ShardId": "",
                    "SubInstanceId": "mysql-06c7db72****-s6d85",
                    "SyncDelay": 0,
                    "UpdateTime": "",
                    "VCPU": 1,
                    "ZoneId": "cn-guangzhou-a"
                },
                {
                    "CreateTime": "2025-07-24T03:48:23.000Z",
                    "DelayReplicationTime": 0,
                    "InstanceId": "mysql-06c7db72****",
                    "Memory": 1,
                    "NodeId": "mysql-06c7db72****-r271e",
                    "NodeSpec": "rds.mysql.d1.n.1c1g",
                    "NodeStatus": "Running",
                    "NodeType": "ReadOnly",
                    "RegionId": "cn-guangzhou",
                    "ShardId": "",
                    "SubInstanceId": "mysql-06c7db72****-r271e",
                    "SyncDelay": 0,
                    "UpdateTime": "2025-07-24T08:08:53.000Z",
                    "VCPU": 1,
                    "ZoneId": "cn-guangzhou-a"
                },
                {
                    "CreateTime": "2025-07-24T03:48:23.000Z",
                    "DelayReplicationTime": 0,
                    "InstanceId": "mysql-06c7db72****",
                    "Memory": 1,
                    "NodeId": "mysql-06c7db72****-r1932",
                    "NodeSpec": "rds.mysql.d1.n.1c1g",
                    "NodeStatus": "Running",
                    "NodeType": "ReadOnly",
                    "RegionId": "cn-guangzhou",
                    "ShardId": "",
                    "SubInstanceId": "mysql-06c7db72****-r1932",
                    "SyncDelay": 0,
                    "UpdateTime": "2025-07-24T08:08:53.000Z",
                    "VCPU": 1,
                    "ZoneId": "cn-guangzhou-a"
                }
            ],
            "ParamDifference": true,
            "ProxyDetail": {
                "Charged": false,
                "DBProxyStatus": "Shutdown",
                "ProxyResourceInfo": {
                    "CurrentProxyCpuNum": 0,
                    "MaxProxyCpuNum": 1024,
                    "MinProxyCpuNum": 2
                }
            }
        }
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
