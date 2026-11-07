---
title: "Optimization of Master-Slave Replication Latency for High-Concurrency Small Transactions"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Optimization_of_Master-Slave_Replication_Latency_for_High-Concurrency_Small_Transactions"
---

This topic describes the feature for optimizing master\-replica replication latency of high\-concurrency small transactions provided by RDS for MySQL.

<span id="Rhf5Rcbb"></span>
## Background

When a large number of small transactions are continuously written on the primary node, the standby node needs to frequently receive, write and replay replication logs. If every small transaction triggers a log flush, position notification and scheduling distribution separately, the replication link on the standby node will incur high overhead from system calls and thread scheduling, which tends to reduce replication throughput or raise replication latency. The high\-concurrency small transaction replication latency optimization reduces redundant flushing and repeated scheduling overhead on the standby replication link to improve the standby node's efficiency in processing small transactions.

<span id="ThmYEEgt"></span>
## Supported version

MySQL 8.0, and the kernel minor version is MySQL 8.0.43_20260615 and above.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id="F76g1JRN"></span>
## Feature description

The high\-concurrency small transaction replication latency optimization feature of RDS for MySQL optimizes the replication link on secondary nodes by adopting small transaction batching and batch scheduling. After this feature is enabled, the secondary node aggregates multiple small transactions according to configured thresholds without splitting transaction boundaries. It cuts the overhead incurred when the SQL thread distributes tasks to worker threads one by one, reducing replication latency for small transactions and boosting replication throughput. It is mainly applicable to scenarios where the primary node continuously generates massive small transactions and the secondary node needs to reduce replication latency.

This optimization does not alter the basic replication semantics of transaction content and transaction sequence. When transactions reach boundaries or configured thresholds, or when control events such as log rotation and heartbeat are encountered, the system triggers necessary flushing and visibility updates to ensure the secondary node keeps replication progress advancing steadily.

<span id="z2bx1F1s"></span>
## Instructions

<span id="yiiNc2Or"></span>
### Parameter description

MySQL provides the following configurable parameters for setting up the high\-concurrency small transaction replication latency optimization feature.


|**Parameter name** |**Default value** |**Whether an instance restart is required for the change to take effect** |**Value range** |**Scope** |**Description** |
|---|---|---|---|---|---|
|loose_replica_package_transaction_limit_size |0 |No |0~131072<br><br> |Global<br><br> |Enable or disable the high\-concurrency small transaction replication latency optimization feature, and configure the small transaction batching threshold on secondary nodes in bytes (Byte). Values are as follows:<br><br><br>* `0`: Disabled.<br><br>* `1~131072`: Enabled: Small transactions will be batched with the configured threshold. The recommended value is 131072. |
|loose_replica_event_arena_max_size |268435456 |No<br><br> |0~17179869184 |Global<br><br> |It is used to configure the maximum reserved space for SQL thread event memory pool optimization on secondary nodes, with the unit being Byte. Values are as follows:<br><br><br>* `0`: Disable the event memory pool optimization and adopt the conventional memory allocation mode.<br><br>* `1~17179869184`: Set the maximum reserved space of the event memory pool.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter only takes effect when <code>loose_replica_package_transaction_limit_size</code> \> 0.</div><br> |


<span id="CrXFBR2X"></span>
### Examples


* Enable the latency optimization for high\-concurrency small transactions:

   ```SQL
   SET GLOBAL loose_replica_package_transaction_limit_size = 131072;
   ```
   

* Disable the latency optimization for high\-concurrency small transactions:

   ```SQL
   SET GLOBAL loose_replica_package_transaction_limit_size = 0;
   ```
   

* Set the maximum reserved space for the SQL thread event memory pool optimization on secondary nodes:

   ```SQL
   SET GLOBAL loose_replica_event_arena_max_size = 268435456;
   ```
   


<span id="apjlLBsw"></span>
## Performance data

The actual performance of the high\-concurrency small transaction replication latency optimization is associated with primary write concurrency, single transaction size, secondary node specifications, replication parallelism and parameter values. Run the sysbench write\-only script on the primary node with the concurrent thread count set to 128 to simulate peak business write traffic. The test result shows that the replication TPS of the secondary node increases by approximately 40%.
