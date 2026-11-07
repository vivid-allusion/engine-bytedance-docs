---
title: "Common issues when using Database Transmission Service (DTS)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/which_databases_does_DTS_currently_support"
---

The following are common questions before accessing DTS, covering database support, network and access methods, link recovery, cross\-account transmission, and ticket submission essentials.

<span id="hKqYuMT3"></span>
## Supported database types


|Function type |Current supported databases |
|---|---|
|Data migration |MySQL、veDB MySQL、Redis、PostgreSQL、MongoDB、SQL Server |
|Data synchronization |MySQL、veDB MySQL、Redis、PostgreSQL、MongoDB |
|Data subscription |MySQL、PostgreSQL、MongoDB |


<span id="5fZH54dv"></span>
## Network scenarios and access methods


* **Which network scenarios are supported?** 

   The following three network scenarios are currently supported:

   * Public network: Access the database instance through a public IP.

   * Private network: Access the database instance through a private network address.

   * Virtual private cloud (VPC): Access the database instance through Volcengine VPC private network.

* **Which instance access methods are supported?** 

   The following three access methods are currently supported:

   * BytePlus instances: such as BytePlus MySQL and other managed databases.

   * Public network instances: such as self\-built MySQL accessible over the public network.

   * Private network instances: such as self\-built MySQL deployed within the BytePlus VPC.


<span id="rnFzsTH3"></span>
## Link abnormal recovery

Does it support breakpoint resume?

Yes. When the link is interrupted abnormally, DTS can automatically append data during the interruption after the link recovers, without starting over.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If the migration or synchronization task fails due to a fault during transmission, it is recommended to locate and fix the cause before retrying the task. Refer to Retrying a migration task for how to retry a migration task: <a href="https://docs.byteplus.com/en/docs/DTS/retrying_a_migration_task">Retrying a migration task</a>, <a href="https://docs.byteplus.com/en/docs/DTS/retrying_a_synchronization_task?lang=zh">Retrying a synchronization task</a>.</div>


<span id="LVBDaQ6X"></span>
## Cross\-account transmission

Is cross\-account data migration or synchronization supported?

Yes. Database Transmission Service (DTS) supports cross\-account data migration or synchronization to meet data transmission needs in multi\-account environments.

<span id="BwCjFZlP"></span>
## What is the difference between migration tasks and synchronization tasks?


|**Data transmission type** |**Difference** |
|---|---|
|Data migration |Data migration is designed for one\-time data transfer, suitable for database cloud migration, backup, and recovery scenarios. its process includes schema migration, full migration, and incremental migration stages. the task terminates after completely migrating data from the source end database to the target database. |
|Data synchronization |Data synchronization mainly supports long\-term continuous incremental data replication, such as building disaster recovery environments. After starting the synchronization task, full initialization will be automatically completed, and incremental data will continue to synchronize until the task is manually terminated. |


<span id="4jZV33HI"></span>
## What is the concurrency of migration or synchronization tasks?

The concurrency of DTS tasks is up to 64, with a default of 8 and supports dynamic adjustment. For more information, refer to [adjusting full migration speed](https://docs.byteplus.com/en/docs/DTS/adjusting_full_migration_rate) or [adjusting full synchronization speed](https://docs.byteplus.com/en/docs/DTS/adjusting_full_synchronization_rate?lang=zh).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only synchronization tasks with instance types of MySQL, MongoDB, and PostgreSQL support adjusting the full synchronization rate.</div>


<span id="PrxwOlnr"></span>
## Table structure and object restrictions

**Does DTS support the migration or synchronization of tables without primary keys in the source database?** 

Supported, but with significant risks and limitations; not recommended for direct use in production environments. Although Database Transmission Service (DTS) technically allows transmission of tables without primary keys, the lack of unique identifiers causes the following core issues:


* **Data consistency** ** risks**

   * **Data duplication:**  During full or incremental migration, retries or concurrent writes can easily cause duplicate data in tables without primary keys.

   * **Update/delete matching failure:**  During incremental synchronization, DTS struggles to accurately locate specific rows in the target database. This may lead to `UPDATE` or `DELETE` operations failing to execute correctly or mistakenly affecting multiple rows, resulting in inconsistent data between the source end and target.

* **Impact on performance stability**

   * **Sync delay:**  Due to the inability to use primary key indexes for quick positioning, the database must perform full table scans or inefficient lookups when matching rows, causing slower DML operation processing and resulting in sync delay.

   * **Excessive source database pressure:**  Particularly when migrating large tables without primary keys (for example, exceeding **100M**), it imposes significant read pressure on the source database, which may cause the migration task to stall or lead to high source database load affecting business operations.


<span id="xLBrlFjD"></span>
## Task topology and capability boundaries

**Does DTS support migrating or synchronizing data from multiple sources to a single destination?** 

Yes, but it is a complex scenario requiring careful evaluation based on the specific database type and business model. Although DTS supports many\-to\-one data transmission, practical implementation must focus on key issues such as data conflict, table structure differences, and target load.


* **Core risks and challenges: converging multiple sources to the same target typically faces the following issues:** 

   * **Data and primary key conflicts:**  Writing data from multiple source databases into the same target table often leads to primary key duplication or key conflicts.

   * **Structure inconsistency:**  Tables with the same name on different source ends may differ in field types, lengths, or index definitions.

   * **Write contention:**  Multiple tasks writing simultaneously to the target may cause high target database load or lock contention.

   * **Order control:**  It is challenging to ensure the global write order of data across multiple source ends.

* **Scenario processing strategy: Different migration objects require different handling methods:** 

   * **Scenario 1: Converging to the same table/object (high risk)** 

      * **Default behavior:**  In the event of a primary key conflict, DTS typically overwrites the target data with the source data by default.

      * **Mitigation plan:** 

         * **Enable table name mapping:**  Map tables from different source databases to different table names in the target database (for example, `orders_A`, `orders_B`) to achieve complete physical isolation of data.

         * **Business splitting:**  Complete data splitting or routing planning in the business layer beforehand.

   * **Scenario 2: Converging to different tables/objects (low risk)** 

      Each source independently writes data to exclusive tables in the destination; task pipelines are isolated and do not interfere with each other, usually preventing data overwrite issues.


<span id="BfE0pRUp"></span>
## Submit ticket instructions

What information needs to be provided when submitting a ticket after a task error?

Provide the following two key pieces of information from the error prompt to help technical support locate the issue faster:


* Request ID

* Error code
