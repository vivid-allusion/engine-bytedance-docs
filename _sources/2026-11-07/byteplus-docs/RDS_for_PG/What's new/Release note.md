---
title: "Release note"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/release_notes"
---

This topic lists product feature updates and related documentation for RDS for PostgreSQL.

> **tip**

> Some of the features described in this topic are still in the beta phase. If you need to use them, [submit a ticket](https://console.byteplus.com/workorder/create) to apply.

**2026**

## October 2026

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|Support PostgreSQL 18<br><br> |Support PostgreSQL 18, further enriching the capability matrix of RDS for PostgreSQL. |2026\-10\-15<br><br> |All |[Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) |
|SQL throttling |PostgreSQL instances support SQL template and keyword\-level throttling capabilities. You can configure throttling rules through API interfaces to enhance the stability and availability of databases and business systems. |2026\-10\-15 |All |[SQL throttling](https://docs.byteplus.com/en/docs/RDS_for_PG/SQL-throttling) |
|Upgrade pgvector extension to version 0.8.2<br><br> |After version upgrade, you can use the updated vector extension capabilities in PostgreSQL instances to improve compatibility and availability in vector data processing scenarios. |2026\-10\-15<br><br> |All |[Searching based on high-dimensional vector similarity (pg_vector)](https://docs.byteplus.com/en/docs/RDS_for_PG/searching_based_on_high-dimensional_vector_similarity-pg_vector?lang=en) |

## August 2026

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|supports stopping and starting instances (invitation\-only) |Support stopping instances while preserving information such as instance data and network configuration, saving instance usage costs without affecting data. Start the instance when needed to quickly resume operation. |2026\-08\-27<br><br> |All |[Stopping and starting an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/Stopping_and_starting_an_instance) |

## July 2026

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|Support viewing abnormal state events of PostgreSQL instances in the event center of Cloud Monitor |Subscribe to events and tasks executed by PostgreSQL instances via Cloud Monitor, helping you keep track of instance status in real time for troubleshooting. |2026\-07\-30<br><br> |All |[Viewing an event](https://docs.byteplus.com/en/docs/RDS_for_PG/Viewing_an_event?lang=en) |
|Supports viewing slow log through the Database Workshop |View the instance slow query SQL list through Database Workshop and further analyze the slow log information of primary and standby nodes to help you quickly locate issues. |2026\-07\-30 |All |[Viewing and downloading logs](https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_and_downloading_logs) |

## June 2026

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|Supports effective_cache_size parameter |Supports setting the estimated disk buffer usage for a single query by the query optimizer. |2026\-06\-03 |All |[List of modifiable parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_modifiable_parameters?lang=en) |
|Supports restricting the instance scope managed by IAM users based on tags |Supports binding corresponding tags to different PostgreSQL instances, and then granting permissions to different IAM users by tag through IAM custom permission policies, restricting IAM users to view or manage only the PostgreSQL instances under specified tags |2026\-06\-03 |All |[Limit the instance scope of IAM user management by tags](https://docs.byteplus.com/en/docs/RDS_for_PG/Limiting_the_instance_scope_of_IAM_user_management_by_tags) |

## March 2026

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|Support up to 12,000 GB of storage space (beta) |When the instance CPU cores are 8 or more, it supports configuring up to 12,000 GB of storage space for the instance. |2026\-03\-30 |All<br><br> |[Product specifications](https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications)<br><br> |
|Support pgjwt extension |Support pgjwt extension, a PostgreSQL\-based JSON Web Token (JWT) extension that allows you to generate and verify JWTs directly within the database. |2026\-03\-30 |All<br><br> |[Database-native JWT generation and verification (pgjwt)](https://docs.byteplus.com/en/docs/RDS_for_PG/JWT) |
|Support pgmq extension |Support pgmq extension, a PostgreSQL\-based lightweight message queue extension. Its API design is similar to Amazon SQS and RSMQ, providing users with simple yet powerful message processing capabilities. |2026\-03\-30 |All |[Native message queue (pgmq)](https://docs.byteplus.com/en/docs/RDS_for_PG/pgmq) |
|Support safeupdate extension |Support the safeupdate extension, a lightweight PostgreSQL extension designed to enhance database operation security by enforcing that `UPDATE` and `DELETE` statements must include a `WHERE` clause. |2026\-03\-30 |All |[DML statement security protection (safeupdate)](https://docs.byteplus.com/en/docs/RDS_for_PG/safeupdate) |
|Support pg_graphql extension |Support pg_graphql extension, which provides a complete GraphQL service engine within the database. |2026\-03\-30 |All |[Native GraphQL service engine (pg_graphql)](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_graphql) |
|Support hypopg extension |Support hypopg extension, which allows creating hypothetical indexes in memory. |2026\-03\-30 |All |[Memory hypothetical index (hypopg)](https://docs.byteplus.com/en/docs/RDS_for_PG/hypopg) |
|Support index_advisor extension |Support index_advisor extension, which automatically analyzes given SQL queries and recommends optimal indexes to improve query performance. |2026\-03\-30 |All |[Intelligent index recommendation (index_advisor)](https://docs.byteplus.com/en/docs/RDS_for_PG/index_advisor) |
|Support pg_uuidv7 extension |Support pg_uuidv7 extension, embedding a high\-precision Unix timestamp in the high\-order bytes of the UUID, with the low\-order bytes filled by random numbers to ensure uniqueness. |2026\-03\-30 |All |[Time-ordered globally unique identifier (pg_uuidv7)](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_uuidv7) |
|Support postgresql\-hll extension |Support the postgresql\-hll extension and introduce a custom data type `hll` to solve large\-scale data cardinality estimation (count distinct) issues, such as billions or more, with minimal storage space and very fast computation speed. |2026\-03\-30 |All |[HyperLogLog algorithm extension (postgresql-hll)](https://docs.byteplus.com/en/docs/RDS_for_PG/postgresql) |

## February 2026

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|Support changing the virtual private cloud and subnet used by the instance (beta) |To enhance user experience, RDS for PostgreSQL supports changing the virtual private cloud and subnet used by instances without recreating the instance. |2026\-02\-03<br><br> |All<br><br> |[Change the virtual private cloud of the instance](https://docs.byteplus.com/en/docs/RDS_for_PG/Modifying_an_instance_virtual_private_cloud) |

**2025**

## December 2025

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|Support cloud disk storage type (invitation\-only) |You can create instances with Cloud ESSD FlexPL or Cloud ESSD PL0 storage types. They support maximum storage spaces of 32,000 GB and 16,000 GB, respectively. |2025\-12\-02 |China (Guangzhou), Asia Pacific (Johor), Asia Pacific (Jakarta) |[Product specifications](https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications) |
|Support event monitoring |Integrate with Cloud monitor (VCM) to monitor events such as "Active and standby switching (task switching)", "Active and standby switching (failover)", and "Instance backup failed", and support configuring alarm rules. |2025\-12\-02 |All |[Viewing an event](https://docs.byteplus.com/en/docs/RDS_for_PG/Viewing_an_event) |
|Supports viewing and downloading WAL backup |Support viewing and downloading WAL backup to check write actions locally, verify wal integrity, analyze replication/recovery issues, and assess write performance. |2025\-12\-02 |All |[Downloading WAL backup](https://docs.byteplus.com/en/docs/RDS_for_PG/Downloading_WAL_backup) |

## October 2025

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|Support SSL encryption |Support enabling SSL encryption for instances and supports updating SSL certificates. |2025\-10\-13 |All |[Configuring SSL encryption](https://docs.byteplus.com/en/docs/RDS_for_PG/Configuring_SSL_encryption) |
|Upgrade "Historical event" to "Task center" |Upgrades “Historical event” to “Task center”. In Task center, you can view and manage all Actions performed on instances. |2025\-10\-13 |All |[Task center](https://docs.byteplus.com/en/docs/RDS_for_PG/historical_events) |
|Support for configuration adjustment evaluation |Support estimating changes and giving possible impacts when modifying instance configuration. |2025\-10\-13 |All |[Regular modification of specification](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification) |
|Support an incremental backup method with high\-frequency incremental data |Support a high\-frequency incremental backup method to meet backup needs in different scenarios and reduce the overall cost of backup usage. |2025\-10\-13 |All |[Customizing backup policies](https://docs.byteplus.com/en/docs/RDS_for_PG/customizing_backup_policies) |
|Support more monitoring monitor and alarm metrics |More monitoring metrics are added under the dimensions of resource monitoring, engine monitoring, and deployment monitoring to facilitate a more comprehensive grasp of the instance state. |2025\-10\-13 |All |[Monitoring metrics](https://docs.byteplus.com/en/docs/RDS_for_PG/monitoring_metrics) |
|Provide private network address accessible across domains (trial) |Provide private network addresses with cross\-region access, enriching the business scenarios supported by instances connection. |2025\-10\-13 |All |[Obtaining cross-regional private network address](https://docs.byteplus.com/en/docs/RDS_for_PG/Obtaining_cross-regional_private_network_address) |

## July 2025

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|Support for major kernel version upgrades of the database (invitation for testing) |RDS for PostgreSQL provides the ability to upgrade a major version of an instance, allowing you to upgrade a lower version of PostgreSQL instance that meets the conditions to a higher version, and support cross\-version upgrades. |2025\-07\-31 |All |[Upgrading database major version](https://docs.byteplus.com/en/docs/RDS_for_PG/upgrading_major_engine_version) |
|Enhanced allowlist management capabilities |Support setting the allowlist as the default allowlist; support binding ECS security groups by "Associated ECSIP" and "Inbound IP", which is closer to the actual usage scenario. |2025\-07\-31 |All |* [Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_ip_address_allowlist)<br><br>* [Modifying an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_an_allowlist) |
|Enhanced allowlist management capabilities |It provides copy, synchronization and batch disassociating instance functions for allowlist to improve product experience. |2025\-07\-31 |All |* [Disassociating allowlists](https://docs.byteplus.com/en/docs/RDS_for_PG/disassociating_an_allowlist)<br><br>* [Copying an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/Copying_an_allowlist) |
|Support for specifying an allowlist when creating an instance. |Support for specifying an allowlist to associate with when creating an instance. |2025\-07\-31 |All |* [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance)<br><br>* [Restoring to a new instanceRestoring to new instance](https://docs.byteplus.com/en/docs/RDS_for_PG/recovery_from_a_backup_set) |
|Added monitoring metrics for databases & tables |Add the monitoring indicator "DBMaxTableSize, which monitors the size of the largest table under the database in units of the database. |2025\-07\-31 |All |[Monitoring metrics](https://docs.byteplus.com/en/docs/RDS_for_PG/monitoring_metrics) |
|Enhance the management of operations events |Enhance the ability to manage operation and maintenance events, and support modifying the switching time of operation and maintenance events to be executed. |2025\-07\-31 |All |[Modifying the switching time of the operation and maintenance event](https://docs.byteplus.com/en/docs/RDS_for_PG/Modifying_the_switching_time) |

## June 2025

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|Support for creating parameter templates and applying them to instances |Support for creating custom parameter templates and applying parameter templates to single or batch instances to quickly adjust the parameter configuration of the instance. |2025\-06\-04 |All |* [Apply parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Applying_a_parameter_template)<br><br>* [Manage parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Managing_a_parameter_template) |
|Support for cloning databases |Support cloning existing databases to quickly create new databases with the same structure as existing databases. |2025\-06\-04 |All |[Cloning a database](https://docs.byteplus.com/en/docs/RDS_for_PG/Clone) |
|Support for specifying backup objects and backup types when creating backups |When creating a backup, it supports selecting the backup object as the entire instance or a specified database, and supports creating physical and logical backups of the entire instance. |2025\-06\-04 |All |[Creating a data backup](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_manual_backup) |
|Support for creating logical backups and downloads |Support creating logical backups for specified databases and downloading logical backups locally. |2025\-06\-04 |All |* [Creating a data backup](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_manual_backup)<br><br>* [Downloading data backup files](https://docs.byteplus.com/en/docs/RDS_for_PG/Downloading_a_data_backup) |
|Support restoring from logical backups to existing instances |Support restoring from logical backups to existing instances |2025\-06\-04 |All |[Restoring to existing instance](https://docs.byteplus.com/en/docs/RDS_for_PG/Restoring_to_an_existing_instance) |
|Add monitoring metrics for slow queries |Add a monitoring indicator of "incremental change trend of slow query in nearly n seconds", which supports user\-defined statistical time of the indicator. |2025\-06\-04 |All |[Monitoring metrics](https://docs.byteplus.com/en/docs/RDS_for_PG/monitoring_metrics) |

## April 2025

|Function name |Function description |Release date |Release region |Related document |
|---|---|---|---|---|
|Support PostgreSQL 17 |Support PostgreSQL 17, further enriching the capability matrix of RDS for PostgreSQL. |2025\-04\-22 |All |[Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) |
|Support pg_repack 1.5.2 |Provide the pg_repack plug\-in of version 1.5.2. |2025\-04\-22 |All |[Cleaning space (pg_repack)](https://docs.byteplus.com/en/docs/RDS_for_PG/cleaning_space-pg_repack) |
|Support pg_vector 0.8.0 |Provide the pg_vector extension 0.8.0 in PostgreSQL 13 and above instances, adding three new vector data types, two vector operators, two parameters for ivfflat index queries, and three parameters for HNSW index queries. |2025\-04\-22 |All |[Searching based on high-dimensional vector similarity (pg_vector)](https://docs.byteplus.com/en/docs/RDS_for_PG/searching_based_on_high-dimensional_vector_similarity-pg_vector) |
|Support pg_partman extension |Support the pg_partman extension, providing time\-based and sequence\-based table partition set management capabilities. |2025\-04\-22 |All |[Time-based and sequence-based table partition set management (pg_partman)](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_partman) |
|Support for pg_jobmon extension |Support for pg_jobmon extension, which provides a non\-transactional transaction and function logging mechanism for retaining log information when a transaction or function fails. |2025\-04\-22 |All |[Logging extensions (pg_jobmon)](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_jobmon) |
|Enhanced the ability to export instance lists |Enhanced the ability to export instance lists, supporting:<br><br><br>* Export instance lists in multiple ranges to meet business needs in more scenarios.<br><br>* Export the endpoint address of the instance. |2025\-04\-22 |All |[Exporting the instance list](https://docs.byteplus.com/en/docs/RDS_for_PG/exporting_an_instance_list) |
|Adjust the number limit of batch creation of instances |Adjust the number limit of batch creation of instances, and increase the number of instances when creating instances in batches to 20. |2025\-04\-22 |All |[Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) |
|Support displaying operation and maintenance events in the console |Add the display of operation and maintenance events in the console, which can easily view the operation and maintenance events that are expected to be executed in the current region, such as version upgrades and host operation and maintenance. |2025\-04\-22 |All |[Viewing operation and maintenance events](https://docs.byteplus.com/en/docs/RDS_for_PG/view_operation_and_maintenance_events) |

## March 2025

|Function name |Function description |Release date |Release region |Related document |
|---|---|---|---|---|
|Release the first Java SDK based on Open API V2 |Release the first Java SDK based on Open API V2, with version number 0.1.157. SDKs for Python (1.0.130) and Go (v1.0.187) are released simultaneously. |2025\-03\-20 |All regions |[SDK overview](https://docs.byteplus.com/en/docs/RDS_for_PG/sdk_overview) |
|Asia Pacific (Jakarta) region officially available |RDS for PostgreSQL is officially available for sale in Asia Pacific (Jakarta) starting from Beijing time on March 12, 2025. |2025\-03\-12 |Asia Pacific (Jakarta) |[Endpoints](https://docs.byteplus.com/en/docs/RDS_for_PG/request_structure#.5pyN5Yqh5Zyw5Z2A) |
|Support pg_bigm extension |Support pg_bigm extension, which supports creating a 2\-gram GIN index to speed up the full\-text search process. |2025\-03\-10 |All |[Full-text search (pg_bigm)](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_bigm) |
|Support pg_ivm extension |Support pg_ivm extension, which provides the incremental view maintenance (IVM) function. |2025\-03\-10 |All |[Incremental view maintenance (pg_ivm)](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_ivm) |

## February 2025

|Function name |Function description |Release date |Release region |Related document |
|---|---|---|---|---|
|Support pg_hint_plan extension |Support pg_hint_plan extension, providing the ability to change the established execution plan through annotation hints. |2025\-02\-19 |All |[Changing the given execution plan through annotation hints (pg_hint_plan)](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_hint_plan) |
|Support pg_profile extension |Support pg_profile extension, providing the ability to count resource\-intensive activities. |2025\-02\-19 |All |[Resource-intensive activity statistics (pg_profile)](https://docs.byteplus.com/en/docs/RDS_for_PG/pg_profile) |
|Enhanced replication slot management capabilities |Enhanced replication slot management capabilities, support for deleting active replication slots, and support for batch deletion of replication slots. |2025\-02\-19 |All |[- Deleting replication slot](https://docs.byteplus.com/en/docs/RDS_for_PG/delete_replication_slot)<br><br>[Deleting replication slots in batches](https://docs.byteplus.com/en/docs/RDS_for_PG/deleting_replication_slots_in_a_batch) |

**2024**

## December 2024

|Function name |Function description |Release date |Release region |Related document |
|---|---|---|---|---|
|Add monitoring metrics related to slow queries, deadlocks, and lock waits |Provide monitoring items for instantaneous slow queries, the queries with lock waiting time exceeding 1h, 2pc transactions, database deadlocks, and the data return\-to\-scan ratio. |2024\-12\-25 |All |[Monitoring metrics](https://docs.byteplus.com/en/docs/RDS_for_PG/monitoring_metrics) |
|Support PostgreSQL 15 and PostgreSQL 16 |Support PostgreSQL 15 and PostgreSQL 16, further enriching the capability matrix of RDS for PostgreSQL. |2024\-12\-11 |All |[Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) |
|Support zhparser extension |Support zhparser extension, providing Chinese word segmentation capability. Support zhparser extension, providing Chinese word segmentation capability. |2024\-12\-11 |All |[Chinese word segmentation (zhparser)](https://docs.byteplus.com/en/docs/RDS_for_PG/chinese_word_segmentation-zhparser) |
|Support wal2json extension |Support wal2json extension, supporting the output of logical log files in JSON format for viewing or downstream system consumption. |2024\-12\-11 |All |[Logical log conversion (wal2json)](https://docs.byteplus.com/en/docs/RDS_for_PG/logical_log_conversion-wal2json) |
|Support orafce extension |Support orafce extension, providing compatibility with Oracle database. |2024\-12\-11 |All |[Compatibility extension (orafce)](https://docs.byteplus.com/en/docs/RDS_for_PG/compatibility_extension-orafce) |
|Support pg_jieba extension |Support pg_jieba extension, providing a PostgreSQL extension for Chinese word segmentation full\-text search. |2024\-12\-11 |All |[Chinese search (pg_jieba)](https://docs.byteplus.com/en/docs/RDS_for_PG/chinese_search-pg_jieba) |
|Optimize the display of the list of modifiable parameters |Optimize the display of the list of modifiable parameters and provide parameter type information. |2024\-12\-11 |All |[List of modifiable parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_modifiable_parameters) |
|Provided IP addresses for instances |Provide IP addresses for instances to meet users' needs for connecting to instances in different business scenarios. |2024\-12\-11 |All |[Viewing instance connection information](https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_access_address_and_port) |
|Provide SQL throttling capabilities (beta) |In order to cope with high\-concurrency business peaks, SQL throttling capabilities are provided to limit and manage the resource consumption of specific SQL statements. |2024\-12\-11 |All |[SQL throttling (beta)](https://docs.byteplus.com/en/docs/RDS_for_PG/SQL_throttle) |
|Related product updates \- DBW |The one\-click diagnostic function can help you more intuitively view the full picture of the performance of the cloud database PostgreSQL version database instance and confirm whether the instance has any abnormalities. |2024\-12\-05 |All |[Diagnosis (PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/one-click-diagnosis-management) |

## October 2024

|Function name |Function description |Release date |Release region |Related document |
|---|---|---|---|---|
|China (Hong Kong) is officially available |RDS for PostgreSQL is officially available for sale in China (Hong Kong) starting from Beijing time on October 30, 2024. |2024\-10\-30 |China (Hong Kong) |[Endpoints](https://docs.byteplus.com/en/docs/RDS_for_PG/request_structure#.5pyN5Yqh5Zyw5Z2A) |
|Support for managing WAL log space |Support for clearing WAL logs for instances, providing the ability to have more granular control over instance storage space. |2024\-10\-24 |All |[Clear WAL](https://docs.byteplus.com/en/docs/RDS_for_PG/clearing_wal_logs) |
|Support for calling interfaces related to allowlist in Terraform |Ecotool\-Terraform adds support for the interfaces to the allowlist, which allows you to query, create, bind, unbind, and delete allowlists in Terraform. |2024\-10\-24 |All |[About Terraform](https://docs.byteplus.com/en/docs/RDS_for_PG/terraform) |
|Support for using a preset alarm template when creating an alarm policy |Support for using a preset alarm template when creating an alarm policy. The preset template contains the basic information, alarm objects, and alarm rules of the alarm policy, and the preset alarm template can be applied with one click to simplify the operation process. |2024\-10\-24 |All |[Creating an alarm strategy](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_alert_policies) |
|Add monitoring metrics related to error logs |Provide alarm metrics related to error logs and optimize the display of error logs. |2024\-10\-24 |All |[Monitoring metrics](https://docs.byteplus.com/en/docs/RDS_for_PG/monitoring_metrics) |
|Support yearly and monthly billing |Added yearly and monthly billing options to provide richer choices for different business scenarios. |Oct.24 2024 |All |Yearly or monthly subscription |
|Public sale for the first time |RDS for PostgreSQL is sold publicly for the first time. |Oct.21 2024 |All |About RDS for PostgreSQL |

## August 2024

|Function name |Function description |Release date |Release region |Related document |
|---|---|---|---|---|
|Asia Pacific (Johor) is officially available |The RDS for PostgreSQL is officially available for sale in Asia Pacific (Johor) from October 30, 2024, Beijing time. |August.30 2024 |Asia Pacific (Johor) |[Endpoints](https://docs.byteplus.com/en/docs/RDS_for_PG/request_structure#.5pyN5Yqh5Zyw5Z2A) |

## July 2024

|Function name |Function description |Release date |Release region |Related document |
|---|---|---|---|---|
|Support PostgreSQL 14 |Support PostgreSQL 14, further enriching the capability matrix of RDS for PostgreSQL. |2024\-07\-30 |All |[Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) |
|Support WAL log management capability |Provide WAL log management capability, support viewing and managing replication slots in instances, and further enhance instance stability. |2024\-07\-30 |All |[WAL management](https://docs.byteplus.com/en/docs/RDS_for_PG/wal_management) |
|Support pg_vector 0.6.2 |Provide the pg_vector extension 0.6.2 in PostgreSQL 12 and above instances to support parallel construction of HNSW indexes and index construction progress query. |2024\-07\-30 |All |[Searching based on high-dimensional vector similarity (pg_vector)](https://docs.byteplus.com/en/docs/RDS_for_PG/searching_based_on_high-dimensional_vector_similarity-pg_vector) |
|Support pg_cron 1.6.2 |Provide the pg_cron extension 1.6.2 to improve the reliability and stability of the extension. |2024\-07\-30 |All |[Task scheduler expanding (pg_cron)](https://docs.byteplus.com/en/docs/RDS_for_PG/task_scheduler_expanding-pg_cron) |
|Provide more monitoring metrics |29 new monitoring metrics are added, and dashboards are provided for 25 of them to help you understand the details of instance status and business status. |2024\-07\-30 |All |[Monitoring metrics](https://docs.byteplus.com/en/docs/RDS_for_PG/monitoring_metrics) |

## June 2024

|Function name |Function description |Release date |Release region |Related document |
|---|---|---|---|---|
|Support restarting read\-only nodes |When restarting an instance, you can select the restart range, and you can choose to restart all nodes or specify read\-only nodes. |2024\-06\-12 |All |[Restarting an instance or read-only node(s)](https://docs.byteplus.com/en/docs/RDS_for_PG/restarting_an_instance) |
|Support database audit |RDS for PostgreSQL has completed the connection with the Database Workshop, providing database audit capabilities with a white screen of the database interactive platform. |2024\-06\-12 |All |[Observation diagnosis](https://docs.byteplus.com/en/docs/RDS_for_PG/observation_diagnosis) |

## April 2024

|Feature |Description |Release time |Release region |Related documents |
|---|---|---|---|---|
|Product released |RDS for PostgreSQL is released in beta stage for the first time. |2024/4/1 |All |About RDS for PostgreSQL |

**2023**

## December 2023

**2021**

## December 2021
