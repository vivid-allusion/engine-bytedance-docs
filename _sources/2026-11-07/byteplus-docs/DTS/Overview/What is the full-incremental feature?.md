---
title: "What is the full-incremental feature?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/architecture_principles"
---

Database Transmission Service (DTS) supports the full\-incremental feature. This feature can help you mix, deduplicate, and concurrently migrate or synchronize full and incremental data to the destination during data migration and synchronization, thereby increasing the data transmission rate and reducing the possibility of data rollback. This topic introduces the advantages, flow chart, and performance comparison of the full\-incremental feature.

<span id="XvtMNK9D"></span>
## Flow chart

<span id=".5pWw5o2u6L-B56e7"></span>
### Data migration

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fabc1160a5ec75449a29196c2b973e6f.png) </span>


&nbsp;

* **Schema migration**: Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database.

* **Full migration + Incremental migration**: While fully reading the source table content, it parses and replays the target database incremental logs and reads incremental data. DTS writes the deduplicated full and incremental mixed data to the destination at the same time.

* **Post\-schema migration**: To ensure the performance of data migration and the stability of the migration task, some database migration object will be created after the full and incremental migrations are complete. The objects requiring post\-schema migration are in MySQL: triggers and events.


<span id=".5pWw5o2u5ZCM5q2l"></span>
### Data synchronization

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bccb3252d1596812eeeb71d408a46a31.png) </span>


&nbsp;

* **Schema initialization**: Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database.

* **Full initialization + Incremental initialization**: While fully reading the source table content, it parses and replays the target database incremental logs and reads incremental data. DTS writes the deduplicated full and incremental mixed data to the destination at the same time.


<span id=".5LyY5Yq_"></span>
## Advantages


* **More flexible**: You can flexibly configure the synchronization type, data filtering range, and conflict strategy of different tables in the same task.

* **Freedom from data dependencies**: Enables the migration or synchronization of larger tables without reliance on Kafka, effectively addressing concerns about data delays due to extended full\-data operations.

* **Improved efficiency**: Significantly improves data freshness and greatly reduces the possibility of data fallback. When the migration or synchronization task is started, the incremental data starts to be fully written to the destination. Full and incremental migration or synchronization are performed simultaneously.

* **Time saving**: Reduces the cutover time required for large databases by eliminating the step of catching up with incremental data after full data migration or synchronization.

* **Simplified process**: When modifying the objects of a data migration or synchronization task, it reduces the waiting time. Since full and incremental data changes are synchronized concurrently, only schema changes need to be completed after initiating a modification to proceed to the next round of data changes.


<span id=".5oCn6IO95a-55q-U"></span>
## Performance comparison

During the incremental migration or incremental synchronization phase, DTS developers compare the performance of transmitting the same data for synchronization tasks using and not using the full\-incremental feature. The results show that using the full\-incremental feature for data transmission is more efficient. The specific data is shown in the following table.

The specifications of the Volcanic Engine RDS for MySQL instance and the DTS data synchronization task are as follows.


* The specifications of the Volcanic Engine RDS for MySQL instance are as follows:

   * Compatible version: RDS for MySQL 5.7

   * Node specification: 8 Cores 16 GB (rds.mysql.d1.n.8c16g)

   * Storage space: 500 GB.

* DTS synchronization task:

   * Link specification: Compact

   * Synchronization topology: Unidirectional synchronization

   * Instance access method of source and target databases: Volcanic Engine RDS for MySQL

   * Synchronization type: Schema initialization + Full initialization + Incremental synchronization

   * Conflict strategy: Conflict overwrite



|**Data type** |**Source** |**Destination** |**Disable the full\-incremental feature** |**Enable the full\-incremental feature** |
|---|---|---|---|---|
|**Single row 250b** |China (Beijing) |China (Beijing) |* RPS: 25k<br><br>* Traffic: 5mb/s |* RPS: 45k<br><br>* Traffic: 9.15mb/s |
||China (Beijing) |China (Guangzhou) |* RPS: 22k<br><br>* Traffic: 4.3mb/s |* RPS: 32.2k<br><br>* Traffic: 6.4mb/s |
|**Single row 500b** |China (Beijing) |China (Beijing) |* RPS: 16k<br><br>* Traffic: 7.2mb/s |* RPS: 37.3k<br><br>* Traffic: 16.5mb/s |
||China (Beijing) |China (Guangzhou) |* RPS: 12.7k<br><br>* Traffic: 5.6 mb/s |* RPS: 28.2k<br><br>* Traffic: 12.5mb/s |
||China (Beijing) |Asia Pacific (Johor) |* RPS: 15.2k<br><br>* Traffic: 6.6mb/s |* RPS: 18.1k<br><br>* Traffic: 8mb/s |
|**Single row 1k** |China (Beijing) |China (Beijing) |* RPS: 16k<br><br>* Traffic: 12.2mb/s |* RPS: 34k<br><br>* Traffic: 25mb/s |
||China (Beijing) |China (Guangzhou) |* RPS: 13k<br><br>* Traffic: 9.5mb/s |* RPS: 26.5k<br><br>* Traffic: 19.9mb/s |
||China (Beijing) |Asia Pacific (Johor) |* RPS: 15.1k<br><br>* Traffic: 11 mb/s |* RPS: 15.5k<br><br>* Traffic: 11.39mb/s |
|**Single row 100k** |China (Beijing) |China (Beijing) |* RPS: 2k<br><br>* Traffic: 126mb/s |* RPS: 2k<br><br>* Traffic: 128mb/s |
||China (Beijing) |China (Guangzhou) |* RPS: 1.95k<br><br>* Traffic: 123mb/s |* RPS: 2k<br><br>* Traffic: 128mb/s |
||China (Beijing) |Asia Pacific (Johor) |* RPS: 1.8k<br><br>* Traffic: 113mb/s |* RPS: 1.3k<br><br>* Traffic: 82mb/s |
|**Single row 500k** |China (Beijing) |China (Beijing) |* RPS: 0.4k<br><br>* Traffic: 127.5mb/s |* RPS: 0.47k<br><br>* Traffic: 148.7mb/s |
||China (Beijing) |China (Guangzhou) |* RPS: 0.4k<br><br>* Traffic: 127mb/s |* RPS: 0.25k<br><br>* Traffic: 103mb/s |
||China (Beijing) |Asia Pacific (Johor) |* RPS: 0.36k<br><br>* Traffic: 113mb/s |* RPS: 0.35k<br><br>* Traffic: 117.6mb/s |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The full\-incremental feature is currently in the invitation test stage. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support.

* Currently, the full\-incremental feature is only supported for MySQL\-to\-MySQL migration and synchronization tasks.

* When the full\-incremental feature is enabled for the task, the full and incremental data will be migrated or synchronized to the destination concurrently. Therefore, configuring delay isolation for incremental migration or incremental synchronization tasks separately is not supported.

* The created task does not support changing the transmission architecture of the task. To use the full\-incremental feature, you need to re\-create the task or copy it based on the original task. For how to copy a task, refer to [Copying a migration task](https://docs.byteplus.com/en/docs/DTS/replicating_a_migration_task) or [Copying a synchronization task](https://docs.byteplus.com/en/docs/DTS/replicating_a_synchronization_task).


<span id=".55u45YWz5paH5qGj"></span>
## Related document

You can enable the full\-incremental feature in data migration and data synchronization tasks for RDS for MySQL creation. Related documents are shown below.


* [Creating a data migration task for RDS for MySQL](https://docs.byteplus.com/en/docs/DTS/creating_mysql_data_migration_tasks)

* [Creating a data synchronization task for RDS for MySQL](https://docs.byteplus.com/en/docs/DTS/creating_mysql_data_synchronization_tasks)
