---
title: "Next-generation architecture"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-architecture-of-bytehouse"
---

ByteHouse Cloud Data Warehouse Edition, based on the next\-generation cloud\-native architecture and combining a shared\-nothing compute layer with a shared\-everything storage layer, effectively avoids the re\-sharding issues in traditional MPP architectures. By utilizing HDFS and object storage as the storage layer, ByteHouse supports deployment on cloud platforms, thus implementing the cloud\-native architecture.

<span id="2759448e"></span>
# Product architecture

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3243c51aab224560bda3e1f37437536e~tplv-goo7wpa0wc-image.image) </span>

<span id="bcd03489"></span>
# Core components

<span id="aa1e4802"></span>
## Control layer


|Component |Component Introduction |Related Documents |
|---|---|---|
|**Environmental Management** |Environmental management supports users in building multiple independent operating environments under SaaS services (such as test and production environments), where resources in different environments are independently isolated; at the same time, permissions are set for the environment, and only authorized users can access it, enhancing business security. |[Manage environment](https://docs.byteplus.com/docs/bytehouse/manage-environment) |
|**Data Management & Development** |* Database management: Manages objects such as visual databases, tables, and materialized views, and allows for the creation, change, and deletion of table structures and partitions, making operations more convenient.<br><br>* SQL Query & Development: Provides a powerful SQL editor, supports writing, executing, and debugging SQL statements, facilitating querying, debugging, and validation; Automatic SQL formatting and syntax tips with highlighting enhance development efficiency.<br><br>* SQL Diagnosis: By analyzing the SQL execution status and Query mode, potential performance issues are identified, and optimization suggestions are provided to improve the overall efficiency of the SQL. |* [Working with databases, tables and views](https://docs.byteplus.com/docs/bytehouse/docs-databases-tables-and-views)<br><br>* [SQL Worksheet](https://docs.byteplus.com/docs/bytehouse/docs-query-editor-and-worksheet) |
|**Resource Management** |* Virtual Warehouse Group management is responsible for the creation, unsubscribe, launch, cancel, and expansion of computing resources, ensuring the safe and stable operation of SQL queries and data entry actions. Supports on\-demand launch and Suspend of VW, a feature that helps users save costs when computing is not needed. Virtual Warehouses (VW) allocate dedicated computing resources for different tenants or workloads, achieving computational resource isolation to prevent interference and ensure stability and performance for each business.<br><br>* Dedicated Server management is responsible for creating, unsubscribing, and expanding servers, ensuring that users can build private servers to handle peak traffic demands in scenarios with high concurrency.<br><br>* Local cache management is responsible for adding local caches to computation groups (Virtual Warehouse), ensuring the performance of query analysis for hotspot business data. |* [Virtual Warehouse](https://docs.byteplus.com/en/docs/bytehouse/docs-virtual-warehouses_1)<br><br>* [Private server](https://docs.byteplus.com/docs/bytehouse/private-server)<br><br>* [Use virtual warehouse local disk](https://docs.byteplus.com/docs/bytehouse/intelligent-cache) |
|**Monitoring Alarms** |* System Monitoring: Controls and monitors the status of various components, including CPU, memory, storage, and Token usage, ensuring the system operates under normal conditions. It also monitors the execution time, QPS, and other metrics of various queries for performance optimization and troubleshooting.<br><br>* Custom Alarms: Users can add alarms for key metrics that automatically trigger alerts when the metrics exceed set thresholds. |[Monitoring and alarm](https://docs.byteplus.com/docs/bytehouse/monitoring-and-alarm) |
|**Data Import** |ByteHouse Cloud Data Warehouse offers various built\-in data import capabilities, supporting quick and convenient data load from different sources into the data warehouse, facilitating users to easily experience the core functionalities of ByteHouse.<br><br><br>* Batch Import: Supports local files, TOS/S3 data files in common formats including CSV, JSON, Parquet. Users upload files via command\-line or Web console and load them into target tables.<br><br>* Real\-time Import: Real\-time data import is enabled through the Kafka engine, suitable for scenarios requiring high real\-time performance, such as real\-time business data collection and log data import. |[Data import](https://docs.byteplus.com/en/docs/bytehouse/docs-data-import-e8caa19b) |
|**Connections & Network** |* ByteHouse Cloud Data Warehouse provides a variety of developer tools to ensure a smooth integration experience. Users can access and manage ByteHouse services using the ByteHouse Console, ByteHouse CLI, and SDKs in various programming languages.<br><br>* Supports environment\-level VPC/EIP configuration, allowing each tenant to bind independent domain names to resources in different environments, enhancing security and network isolation capabilities. |[Network settings](https://docs.byteplus.com/docs/bytehouse/network-settings) |
|**Backup and Restore** |* Total Backup: ByteHouse Cloud Data Warehousing supports full backups and restoration through a continuous data snapshot mechanism, automatically recording all data changes in storage, allowing the recovery of an entire database or specific tables at any point in time.<br><br>* Time Travel: Through the "Time Travel" feature, users can access and restore data from any point within a specified time window (up to 90 days), supporting quick recovery of entire tables or databases from data corruption or mishandling. （2025.H1） |None |
|**Ecosystem Integration** |* SQL Ecosystem: Compatible with MySQL syntax, ClickHouse syntax, ANSI SQL syntax; facilitates seamless migration of ClickHouse and MySQL core OLAP databases to ByteHouse without the need for application layer modifications.<br><br>* BI Ecosystem: Supports QuickBI, FineBI, Tableau, ABI, PowerBI, Metabase, SugarBI, and other BI tool ecosystems. IDE Ecosystem: Supports DBeaver, DataGrip, Navicat, SQL Workbench, and other database management tool ecosystems.<br><br>* Data Development & Scheduling Ecosystem: Supports Dataleap, DBT, Airflow, DophinScheduler, AirByte, and other tool ecosystems. |* [SQL Compatibility](https://docs.byteplus.com/en/docs/bytehouse/sql-compatibility)<br><br>* [Ecosystem Tools](https://docs.byteplus.com/en/docs/bytehouse/docs-ecosystem) |
|**Security & Audit** |* Access Control: Manages using username/password, supports access keys (AK/SK); combined with IAM policies, supports RBAC (Role\-Based Access Control) model to manage your data & resources.<br><br>* Data Encryption: End\-to\-end encryption, supports TLS during transmission.<br><br>* Audit Log: Fully supports auditing user activities (log in, sign out), SQL operations (query, write), permission changes (database, table, resources), and virtual warehouse operations (create, use), ensuring full traceability of all user actions. |[Audit Log](https://docs.byteplus.com/en/docs/bytehouse/audit-log) |


<span id="7ead2bb5"></span>
## Service access layer


|Component |Component Introduction |
|---|---|
|**Service Component (Server)**  |The Service Component (Server) is the core execution unit of ByteHouse Cloud Data Warehouse, responsible for receiving user query requests, performing SQL analysis and optimization, and distributing query tasks to execution nodes.<br><br><br>* SQL Analysis and Execution: Receives SQL query requests, completes syntax and semantic analysis, and generates execution plans.<br><br>* Query Scheduling: By combining the query optimizer and execution engine, the optimal execution path is determined to achieve efficient querying. |
|**TSO（Time Stamp Oracle）**  |TSO is a distributed timestamp allocator used in transaction management to ensure global order and consistency of distributed transactions.<br><br><br>* Global Transaction Management: Provides unique Timestamp for multi\-node distributed transactions, helping to implement MVCC (Multi\-Version Concurrency Control).<br><br>* Transaction Isolation: Ensures consistency and isolation levels between read and write operations, especially during data write and concurrent queries, ensuring data accuracy. |
|**Daemon Manager** |Daemon Manager is a component that manages backend processes, responsible for managing and monitoring background tasks in the system, including maintenance, cleanup, and state monitoring.<br><br><br>* Task Scheduling: Responsible for scheduling system backend tasks, such as data organization, backup, and index rebuilding.<br><br>* System Health Monitoring: Monitors the running status of various services in the system, providing alerts and automatic recovery mechanisms. |
|**Resource Manager** |Resource Manager manages and allocates computational and storage resources in the system to ensure efficient operation in a multi\-tenant environment.<br><br><br>* Resource Scheduling: Dynamically manages computational resources (such as CPU, memory) and storage resources, and flexibly allocates them according to workload demands.<br><br>* Multi\-Tenant Support: Provides multi\-tenant isolation to ensure that different users or workloads do not affect each other, optimizing the overall performance of the system. |
|**Metadata Management** |Metadata services store and manage metadata such as table structure, partition information, and data location, supporting efficient execution and optimization of queries.<br><br><br>* Metadata Management: Includes storing and maintaining information about databases, tables, columns, indexes, and partitions.<br><br>* Metadata Cache: Provides efficient metadata caching services to speed up query execution. |


<span id="73ec0d20"></span>
## Compute layer


|Component |Component Introduction |Related Documents |
|---|---|---|
|**Virtual Warehouse (VW)**  |Virtual Warehouse is a logical abstraction of computing resources, providing isolated resources for executing SQL queries and write operations. Virtual Warehouses do not interfere with each other, suitable for multi\-tenant and multi\-business workload scenarios.<br><br><br>* Compute isolation: Provides independent computing resources for different users or workloads to avoid resource contention. |[Virtual warehouse](https://docs.byteplus.com/en/docs/bytehouse/docs-virtual-warehouses_1) |
|**Virtual Warehouse Local Disk** |In ByteHouse's data analysis scenarios, the query engine needs to scan data files on CFS or object storage. The more data files actually read, the greater the I/O overhead; repeated access to the same data will also result in redundant I/O overhead. Data Cache caches the remote storage data to compute nodes, avoiding the overhead of repeated remote data retrieval and enhancing the performance of hot data query analysis.<br><br>Current Data Cache is considered local disk 1.0, mainly Local Cache; ByteHouse will release local disk 2.0 in the first half of 2025, which is built for enhanced querying and concurrency as a distributed cache. |[Use virtual warehouse local disk](https://docs.byteplus.com/docs/bytehouse/intelligent-cache) |


<span id="d54ed61a"></span>
## Storage layer

The Storage Layer (Cloud Storage) in ByteHouse's disaggregated storage and compute architecture is responsible for data persistence, typically based on object storage technology. Supports seamless integration with cloud service providers such as AWS S3 and Alibaba Cloud OSS for object storage, achieving high scalability.


* Data persistence: Persistently stores data blocks in cloud object storage, ensuring high reliability and durability of data.

* Data sharding and compression: Data is stored in a columnar format and is sharded and compressed to reduce storage costs and enhance reading efficiency.


<span id="8f365acc"></span>
## Data lake

ByteHouse Cloud Data Warehouse has built all\-in\-one lake\-warehouse capabilities as the computing engine to directly analyze data from the data lake. Users can directly query data stored on data lakes like Apache Hive, Apache Iceberg, Apache Hudi, Apache Paimon through ByteHouse's External Catalog, without the need for data migration.

ByteHouse’s all\-in\-one lake\-warehouse supports storage systems including CFS/HDFS, S3, OSS, TOS, and file formats including Parquet, ORC, CSV.

In the data lake analysis scenario, ByteHouse Cloud Data Warehouse is responsible for data computation and analysis, while the data lake primarily handles data storage. ByteHouse Cloud Data Warehouse, as the computing engine for the data lake, can fully utilize the vectorized engine and query optimizer to enhance the analytical performance of the data lake.
