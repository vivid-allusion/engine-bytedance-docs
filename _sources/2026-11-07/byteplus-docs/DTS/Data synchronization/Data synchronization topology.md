---
title: "Data synchronization topology"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology"
---

The data synchronization feature of the Database Transmission Service (DTS) supports multiple synchronization topologies, allowing you to select the appropriate topology for data synchronization based on your business requirements. This topic describes the types of synchronization topologies supported by DTS and their usage instructions.

<span id=".5Y2V5ZCR5ZCM5q2l"></span>
## 

Unidirectional synchronization

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To ensure data consistency, only read operations should be performed on synchronization objects in the target instance of unidirectional synchronization. Write operations are not recommended.</div>


* <div data-tips="true" data-tips-type="tip">In an unidirectional synchronization topology, only a forward synchronization task needs to be configured. For configuration methods, please refer to <a href="https://docs.byteplus.com/en/docs/DTS/configuring_forward_synchronization">Configuring a forward task</a>.</div>



The unidirectional synchronization of DTS supports the following topology types:


* **One\-to\-one unidirectional synchronization**

   Synchronize from a source instance to a target instance. In this scenario, you only need to configure an unidirectional synchronization task.

* **One\-to\-many unidirectional synchronization**

   Synchronize from a source instance to multiple target instances. In this scenario, you need to configure multiple unidirectional synchronization tasks.

   For example, to synchronize from instance A to instances B, C, and D, you need to configure three synchronization tasks (instance A to B, instance A to C, and instance A to D).

* **Many\-to\-one unidirectional synchronization**

   Synchronize from multiple source instances to a target instance. In this scenario, you need to configure multiple unidirectional synchronization tasks.

   For example, to synchronize from instances A, B, and C to instance D, you need to configure three Synchronization tasks (instance A to D, instance B to D, and instance C to D).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To ensure data consistency, the synchronization objects selected in each synchronization task should be different.   </div>
   

* **Cascading unidirectional synchronization**

   A target instance in a synchronization task is also a source instance in another synchronization task. In this scenario, you need to configure multiple unidirectional synchronization tasks.

   For example, to synchronize from instance A to instance B, and then from instance B to instance C, you need to configure two synchronization tasks.


<span id=".5Y-M5ZCR5ZCM5q2l"></span>
## Bidirectional synchronization

Currently, one\-to\-one bidirectional synchronization between MySQL and Redis databases is supported.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In bidirectional synchronization of MySQL, do not perform DDL operations simultaneously on both the source and target database, or the synchronization task may fail. Bidirectional synchronization tasks only support synchronizing DDL operations from the forward task to the target database, and currently do not support synchronizing DDL from the reverse task. If you need to synchronize DDL operations from the reverse task, you can first <a href="https://docs.byteplus.com/en/docs/DTS/Reversing_the_DDL_synchronization_direction_of_the_bidirectional_synchronization_task">adjust the DDL synchronization direction of the bidirectional synchronization task</a> and then perform the DDL operations to ensure data consistency.</div>


* <div data-tips="true" data-tips-type="tip">Due to added conflict resolution logic in Redis bidirectional synchronization, it currently only supports bidirectional synchronization between Volcengine Redis instances.</div>


* <div data-tips="true" data-tips-type="tip">To ensure data consistency, it is recommended that rows with the same primary key value be updated in only one instance. If updated simultaneously, the system will handle it according to the primary key conflict handling method selected when configuring the data synchronization task.</div>


* <div data-tips="true" data-tips-type="tip">In a bidirectional synchronization topology, you need to configure both a forward synchronization task and a reverse synchronization task separately. For configuration methods, refer to <a href="https://docs.byteplus.com/en/docs/DTS/configuring_forward_synchronization">Configuring a forward task</a> and <a href="https://docs.byteplus.com/en/docs/DTS/configuring_reverse_synchronization">Configuring a reverse task</a>.</div>


* <div data-tips="true" data-tips-type="tip">When performing OnlineDDL, forward compatibility must be ensured. For example, do not modify field types or reduce fields, as this may cause synchronization interruptions or data inconsistency. The forward\-compatible table structure DDL list includes: create table, add column, modify column (increase field length), create index, and drop index.</div>


* <div data-tips="true" data-tips-type="tip">It is not recommended to use public networks for bidirectional synchronization, as they are prone to performance bottlenecks.</div>
