---
title: "Instance configuration modification"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/change-instance-config-faq"
---

This topic summarizes the instance configuration modification FAQs for Document Database for MongoDB.

<span id="UbSnTg7r"></span>
### Does Document Database for MongoDB support increasing or decreasing nodes or shards?

Document Database for MongoDB supports two instance types, and different types of MongoDB instances support different instance configuration changing solution. For more information on the instance configuration changing solution supported by MongoDB, refer to [Instance configuration modification](https://docs.byteplus.com/en/docs/mongodb/change-instance-config).

<span id="knmitzxI"></span>
### What should I do if an error occurs during the pre\-check stage of changing the instance configuration?

Before performing [instance configuration](https://docs.byteplus.com/en/docs/mongodb/change-instance-config) modification operation, the Document Database for MongoDB will pre\-check the health status of the instance to ensure that all health monitoring indicators of the instance meet the requirements for configuration change, reducing the possibility of abnormalities caused by configuration changes.

If error occurs during the pre\-check phase of instance specification modification, refer to the suggestions in the table below to resolve it.


|Error code |Problem cause |Solution |
|---|---|---|
|`Oplog window is too small for replica set %s.` |Oplog time window is insufficient. |1. Refer to the suggestions in [What should be done after receiving event monitoring alarm for the oplog window being insufficient](https://docs.byteplus.com/en/docs/mongodb/instance-management-faq#.5pS25Yiw5a6e5L6LLW9wbG9nLeS_neeVmeeql-i_h-Wwj-eahOS6i-S7tuebkeaOp-WRiuitpuWQjuivpeWmguS9leWkhOeQhu-8nw==) and first try modifying the `replication.oplogSizeMB` parameter value.<br><br>2. If the issue cannot be resolved after modifying the above parameter, please [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support for further problem location. |
|`Insufficient connections: node %s has %d available, below the minimum limit of %d.` |Available connections on the node is insufficient. |1. Adjust the parameter value of `net.maxIncomingConnections` appropriately according to the actual number of connections required by the business. For parameter modification methods, refer to [Modifying instance parameters](https://docs.byteplus.com/en/docs/mongodb/modify-parameter).<br><br>2. If the issue cannot be resolved after modifying the above parameter, please [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support for further problem location. |
|`Replica set member %s is unhealthy.` |Unhealthy nodes are present in the replica set. |[Submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support for assistance. |
|`Primary not found in replica set %s.` |Primary node not found in the replica set. ||
|`Replication lag detected: member %s has latency %s.` |Replication latency for the node exceeds 300s. ||
|`Too many logical sessions: node %s has %d active sessions, exceeding the limit %d.` |Number of logical sessions on the node exceeds the limit. ||
|`Health check for the instance encountered an error.` |Instance health check failed.<br><br> ||


<span id="43y5spqX"></span>
### Why does the instance experience performance jitter (such as increased business access latency) when adding shards?

After you add shards to the instance through the scaling operation, for the need of automatic data balancing, the MongoDB Balancer will immediately start the relocation process. After the relocation is completed, the data on the original shard will be deleted. It should be noted that, under the default settings, MongoDB does not limit the amount of data migrated and the interval time. Therefore, during the period from the start of sharding until the data is fully balanced, if there is a large amount of data in your MongoDB instance, the [primary shard](https://www.mongodb.com/docs/manual/core/sharded-cluster-shards/#primary-shard) is very likely to experience an increase in load. In such a situation, latency\-sensitive businesses are likely to perceive it obviously, such as an abnormal increase in CPU usage, an exacerbation of business access latency, and a slowdown in page response speed.

If the above problems occur while adding a Shard to your MongoDB instance, you can try using the following 2 parameters to limit the instance's data migration and cleanup speed.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Adjusting the following parameters can alleviate performance fluctuation issues caused by load balancing in the short term. However, this will also significantly prolong the time required for new shards to complete data balancing, necessitating a comprehensive trade\-off based on actual business scenarios.</div>


* <div data-tips="true" data-tips-type="default">It is highly recommended that you closely monitor the table data volume of the MongoDB instance and enable the sharding feature for the instance in advance. At the same time, to prevent any impact on the online business, it is recommended to perform the sharding expansion operation during the business off\-peak period. For more suggestions on the use of the sharding cluster, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/ug-for-sharding-cluster">User guide for MongoDB sharding cluster</a>.</div>


* <div data-tips="true" data-tips-type="default">For collections requiring sharding, it is recommended to create an index on the shard key beforehand. Prioritize selecting fields as shard keys that have diverse values, balanced write patterns, and are aligned with queries to ensure data distribution and efficient queries.</div>


* <div data-tips="true" data-tips-type="default">Before upgrading, we recommend that you <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical personnel, provide the target specification details, and have the technical team evaluate whether this configuration change will trigger a data migration. They will also confirm the estimated upgrade duration and any potential impact.</div>


* <div data-tips="true" data-tips-type="default">For precautions regarding instance specification upgrades, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/solutions-for-spec-modification?lang=en">Solutions for modification of instance specifications</a>. For the procedure and precautions on adding shards, refer to<a href="https://docs.byteplus.com/en/docs/mongodb/modify-shard-config?lang=en"> Modifying shard configuration</a>.</div>




|**Parameter name** |**Description** |
|---|---|
|[rangeDeleterBatchDelayMS](https://www.mongodb.com/docs/v6.0/reference/parameters/#mongodb-parameter-param.rangeDeleterBatchDelayMS) |The interval between each deletion batch during the cleanup phase of range migration. Unit: milliseconds. Changes take effect immediately, with no instance restart required. For the specific procedure, refer to [Modifying instance parameters](https://docs.byteplus.com/en/docs/mongodb/modify-parameter?lang=en).<br><br><br>* **Parameter setting suggestions**<br><br>   * If the MongoDB instance has a low load and you want to complete the deletion operation quickly, you can appropriately reduce the interval time (for example, set it to 10\-50 milliseconds).<br><br>   * If the MongoDB instance has limited resources, to avoid generating excessive instantaneous load, especially when it is carried out simultaneously with other critical operations in a production environment, you can appropriately increase the interval time (for example, set it to 100\-500 milliseconds).<br><br><br> |
|[rangeDeleterBatchSize](https://www.mongodb.com/docs/v6.0/reference/parameters/#mongodb-parameter-param.rangeDeleterBatchSize) |This parameter specifies the maximum number of documents to be deleted in each batch during the cleanup phase of range migration. Changes take effect immediately, with no instance restart required **.**  For the specific procedure, refer to[ Modifying instance parameters](https://docs.byteplus.com/en/docs/mongodb/modify-parameter?lang=en).<br><br><br>* **Parameter setting suggestions**<br><br>   * If the amount of data to be processed is large and the MongoDB instance has sufficient resources, you can appropriately increase the number of documents deleted each time (for example, set it to 1000\-2000) to improve the deletion efficiency.<br><br>   * If the MongoDB instance has limited resources, you can appropriately reduce the number of documents deleted each time (for example, set it to 100\-500) to avoid imposing excessive load on the system.<br><br><br> |


In the event that performance instability remains unresolved after the aforementioned parameter adjustments, or if write operations fail, proceed with the following mitigation steps.


* View Balancer running status

   First, [connect to the Mongos node of the sharding cluster instance using the MongoDB Shell tool](https://docs.byteplus.com/en/docs/mongodb/ug-connect-instance-via-mongo-shell?lang=en), then execute the following commands.

   ```JavaScript
   sh.isBalancerRunning()
   ```
   

   If the response is `false` (or `inBalancerRound` in the response is `false`), it indicates that the Balancer is not currently running, and you can proceed to the next step.

   If the response is `true` (or `inBalancerRound` in the response is `true`), it indicates that the Balancer is currently performing data migration. Do not forcibly stop it at this time. Try again later.

* Stop Balancer to pause data migration

   After confirming the Balancer is not running, execute the following command.

   ```JavaScript
   sh.stopBalancer()
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more information about <code>sh.isBalancerRunning()</code>, refer to <a href="https://www.mongodb.com/docs/manual/reference/method/sh.isBalancerRunning/">sh.isBalancerRunning()</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the problem is resolved, if you need to re\-enable the Balancer, execute the <code>sh.setBalancerState(true)</code> command to restore automatic data balancing.   </div>
   

* [Submit a ticket](https://console.byteplus.com/workorder/create) for technical support. At this time, the on\-site instance state, monitoring data, and log records are at their most comprehensive, facilitating rapid root cause identification.
