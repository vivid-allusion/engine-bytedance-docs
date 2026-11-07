---
title: "Solutions for modification of instance specifications"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/solutions-for-spec-modification"
---

You can flexibly change the configurations of MongoDB sharding instance based on business fluctuations, including upgrading or downgrading node specifications, increasing or decreasing node and storage space. This topic describes the configuration adjustment solutions supported by MongoDB.

<span id=".6LS555So6K-05piO"></span>
## Billing information

For details on the billing rules for changing instance configurations, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/mongodb/pay-as-you-go#.5Y-Y5pu06YWN572u) and [Subscription](https://docs.byteplus.com/en/docs/mongodb/subscription#.5Y-Y5pu06YWN572u).

<span id=".5Y-Y6YWN5b2x5ZON"></span>
## Impact of configuration change


* The change configuration process may last for several minutes or even hours. During this period, the instance will enter the **Scaling** state, and no other operations on the instance are allowed (such as viewing instance details, managing accounts, or backups).

* During the change configuration process, there may be 1 to 2 brief disconnections, each lasting about 30 seconds. Exercise caution during operations. It is recommended to perform change configuration operations during off\-peak business hours and ensure the application supports automatic reconnection.

* After completing the change configuration, some parameter values will vary with the instance specifications. Please assess the impact of these changes on your business. For more information, refer to [Supported parameter](https://docs.byteplus.com/en/docs/mongodb/supported-parameter).


<span id=".5Y-Y6YWN6aKE5qOA5p-l"></span>
## Pre\-check for configuration change

Before performing instance configuration modification operation, the Document Database for MongoDB will pre\-check the health status of the instance to ensure that all health monitoring indicators of the instance meet the requirements for configuration change, reducing the possibility of abnormalities caused by configuration changes. If a relevant error occurs during the instance configuration change pre\-check phase, refer to the suggestions in [What should I do if an error occurs during the pre-check stage of changing the instance configuration](https://docs.byteplus.com/en/docs/mongodb/change-instance-config-faq#knmitzxI) to resolve it.

<span id=".5Y-Y6YWN5pa55qGI"></span>
## Specification modification solutions

Different types of MongoDB instances support different specification modification solutions. Refer to the table below for details.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Changing disk types is not supported during specification modification.</div>


* <div data-tips="true" data-tips-type="warning">FlexPL volume instances do not support storage space reduction.</div>




<Tabs>
<Tab zoneid="BPSAEn7jZG" title="Replica set instance">
<TabTitle>Replica set instance</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-replica-set-instance-spec">Modifying replica set instance specification</a>.</div>



|Configuration change type |Operation and limits |
|---|---|
|Upgrade |Support upgrading node specifications.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If read\-only nodes exist in the instance, their specifications will also be upgraded when node specifications are upgraded.</div><br> |
||Support increasing storage space.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When increasing storage space, the modified storage space capacity must be greater than or equal to 1.2 times the used space to ensure the instance operates normally.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After storage space is changed, the storage space of each node in the instance will be modified, rather than the total storage space of all nodes becoming the modified storage space.</div><br> |
||**Does not support increasing the number of nodes** (Replica set instances adopt a 3\-node high availability architecture by default). |
||Support increasing the number of read\-only nodes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each instance can add up to 5 read\-only nodes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For replica set instances, changing the number of read\-only nodes is mutually exclusive with other configuration change operations of the instance. That is, when changing the node specification or storage space, changing the number of read\-only nodes simultaneously is not supported. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node">Adding or deleting read\-only nodes</a>.</div><br> |
|Downgrade |Support downgrading node specifications.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If read\-only nodes exist in the instance, their specifications will also be downgraded when node specifications are downgraded.</div><br> |
||Support decreasing storage space.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When decreasing storage space, the modified storage space capacity must be greater than or equal to 1.2 times the used space to ensure the instance operates normally.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After storage space is changed, the storage space of each node in the instance will be modified, rather than the total storage space of all nodes becoming the modified storage space.</div><br> |
||**Does not support decreasing the number of nodes** (Replica set instances adopt a 3\-node high availability architecture by default). |
||Support decreasing the number of read\-only nodes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can reduce to 0 read\-only nodes, which means deleting all read\-only nodes in the instance.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For replica set instances, changing the number of read\-only nodes is mutually exclusive with other configuration change operations of the instance. That is, when changing the node specification or storage space, changing the number of read\-only nodes simultaneously is not supported. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node">Adding or deleting read\-only nodes</a>.</div><br> |





</Tab>
<Tab zoneid="lDrmMciIGe" title="Sharding cluster instance">
<TabTitle>Sharding cluster instance</TabTitle>


|Component type |Configuration change type |Operation and limits |
|---|---|---|
|[Modifying Mongos node configuration](https://docs.byteplus.com/en/docs/mongodb/modify-mongos-config) |Upgrade |Support upgrading Mongos node specifications. |
|||Support increasing the number of Mongos nodes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The number of Mongos nodes can be increased to a maximum of 32.</div><br> |
||Downgrade |Support downgrading Mongos node specifications. |
|||Support decreasing the number of Mongos nodes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The number of Mongos nodes can only be decreased when it is greater than or equal to 3. The minimum number of Mongos nodes that can be retained after reduction is 2.</div><br> |
|[Modifying shard configuration](https://docs.byteplus.com/en/docs/mongodb/modify-shard-config) |Upgrade |Support upgrading node specifications of a single shard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If read\-only nodes exist in the shard, upgrading specification of the single shard node will also upgrade specifications of all read\-only nodes within that shard.</div><br> |
|||Support increasing the storage space of a single shard. |
|||Support upgrading node specifications of all shard in batches.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only when there is <strong>no read\-only node</strong> in a sharding cluster instance and the configurations (including node specifications and storage space) of all Shard are the same, is the function of batch modifying Shard configurations supported.</div><br> |
|||Support increasing storage space for all shards in batches.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When increasing storage space, the modified storage space capacity must be greater than or equal to 1.2 times the used space to ensure the instance operates normally.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only when there is <strong>no read\-only node</strong> in a sharding cluster instance and the configurations (including node specifications and storage space) of all Shard are the same, is the function of batch modifying Shard configurations supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you modify the storage space for multiple shards in batches, the storage space of each individual shard will change, rather than the total storage space of all shards becoming the new configured space.</div><br> |
|||Support increasing the number of shards (each shard fixedly contains 3 nodes), up to a maximum of 32 shards. |
|||Support increasing the number of read\-only nodes in a single shard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each shard can add up to 5 read\-only nodes. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node">Adding or deleting read\-only nodes</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Changes to the number of read\-only nodes are mutually exclusive with other configuration changes for Shard. Therefore, you cannot simultaneously change node specifications or storage space for Shard when modifying the number of read\-only nodes. To change other configurations of Shard, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-shard-config">Modifying Shard configuration</a>.</div><br> |
||Downgrade |Support downgrading node specifications of a single shard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If read\-only nodes exist in the shard, downgrading specification of the single shard node will also downgrade specifications of all read\-only nodes within that shard.</div><br> |
|||Support decreasing the storage space of a single shard. |
|||Support downgrading node specifications of all shard in batches.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only when there is <strong>no read\-only node</strong> in a sharding cluster instance and the configurations (including node specifications and storage space) of all Shard are the same, is the function of batch modifying Shard configurations supported.</div><br> |
|||Support decreasing storage space for all shards in batches.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When decreasing storage space, the modified storage space capacity must be greater than or equal to 1.2 times the used space to ensure the instance operates normally.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only when there is <strong>no read\-only node</strong> in a sharding cluster instance and the configurations (including node specifications and storage space) of all Shard are the same, is the function of batch modifying Shard configurations supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you modify the storage space for multiple shards in batches, the storage space of each individual shard will change, rather than the total storage space of all shards becoming the new configured space.</div><br> |
|||**Does not support decreasing the number of shards**. |
|||Support decreasing the number of read\-only nodes in a single shard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can reduce to 0 read\-only nodes, which means deleting all read\-only nodes in the current shard. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node">Adding or deleting read\-only nodes</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Changes to the number of read\-only nodes are mutually exclusive with other configuration changes for Shard. Therefore, you cannot simultaneously change node specifications or storage space for Shard when modifying the number of read\-only nodes. To change other configurations of Shard, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-shard-config">Modifying Shard configuration</a>.</div><br> |
|[Modifying ConfigServer node configuration](https://docs.byteplus.com/en/docs/mongodb/modify-configserver-config) |Upgrade |Support upgrading ConfigServer node specifications. |
|||Support increasing storage space.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When increasing storage space, the modified storage space capacity must be greater than or equal to 1.2 times the used space to ensure the instance operates normally.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After storage space is changed, the storage space of each node in ConfigServer will be modified, rather than the total storage space of all nodes becoming the modified storage space.</div><br> |
|||**Does not support increasing the number of ConfigServer nodes** (ConfigServer fixedly contains 3 nodes). |
||Downgrade |Support downgrading ConfigServer node specifications. |
|||Support decreasing storage space.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When decreasing storage space, the modified storage space capacity must be greater than or equal to 1.2 times the used space to ensure the instance operates normally.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After storage space is changed, the storage space of each node in ConfigServer will be modified, rather than the total storage space of all nodes becoming the modified storage space.</div><br> |
|||**Does not support decreasing the number of ConfigServer nodes** (ConfigServer fixedly contains 3 nodes). |





</Tab>
</Tabs>
