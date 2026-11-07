---
title: "Console release notes"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/release-notes"
---

<span id="512e1d51"></span>
# Year 2025

<span id="3f38d6bb"></span>
## V 25.8 \- Release Date: October 2025


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Intelligent inspection |* Add cluster inspection items such as the number of slow queries in the cluster, the number of tables with the maximum primary\-secondary sync latency, and the number of delayed files associated with distributed tables. This provides more comprehensive cluster inspection support.<br><br>* Expand the sections on the impact of abnormalities and handling suggestions in inspection reports. In addition, add a new document containing high\-risk handling recommendations for inspection items to provide you with more specific inspection recommendations. |[Intelligent patrol](https://docs.byteplus.com/docs/bytehouse/intelligent-patrol)<br><br>[Suggestions for high-risk intelligent patrol results](https://docs.byteplus.com/docs/bytehouse/suggestions-for-intelligent-patrol) |Oct 2025 |
|Metadata diagnosis |Adds support for metadata diagnostics. Metadata diagnosis is used to detect the consistency of table metadata in the current cluster, and the diagnosis results are updated weekly. You can resolve issues by following the solutions for metadata problems provided by ByteHouse to improve the availability and stability of the cluster. This feature is applicable to scenarios such as troubleshooting table unavailability, repairing metadata exceptions, regularly checking the health of instances, and more. |[Metadata diagnosis](https://docs.byteplus.com/docs/bytehouse/metadata-diagnosis) |Oct 2025 |
|Advanced diagnosis |Add support for advanced diagnosis.<br><br><br>* Advanced Diagnosis is used to collect relevant metadata of tables in a cluster, including creation date, storage volume, and more information, so that the business can perform fine\-grained governance of tables.<br><br>* ByteHouse Enterprise also provides a table index diagnosis feature. By diagnosing the metadata of the table's indexes across different dimensions, such as storage mode and index settings, this feature helps you achieve more efficient table governance to improve instance stability and query performance. This feature is applicable to daily table governance, query performance optimization, resource management and control, and many other scenarios. |[Advanced diagnosis](https://docs.byteplus.com/docs/bytehouse/advanced-diagnosis) |Oct 2025 |
|Resource management |Adds support for resource management, allowing administrators to grant specified resource usage permissions to roles or users and refine permission management. |[Resource management](https://docs.byteplus.com/docs/bytehouse/resource-management) |Oct 2025 |
|Dictionary authorization |Adds support for dictionary resource authorization management, allowing administrators to grant sub\-users permissions for dictionary CREATE, DROP, SHOW, dictGet functions, and many other operations. Once the relevant permissions are obtained, sub\-users can use dictionary resources. |[Access control model](https://docs.byteplus.com/docs/bytehouse/privilege-model)<br><br>[Role management](https://docs.byteplus.com/docs/bytehouse/role-management)<br><br>[IAM sub-user management](https://docs.byteplus.com/docs/bytehouse/sub-user-management)<br><br>[Database user management](https://docs.byteplus.com/docs/bytehouse/database-user-management) |Oct 2025 |


<span id="9e994d8b"></span>
## V 25.7 \- Release Date: September 2025


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Access control |Adds support for the TRUNCATE, MYSQL, CREATE TEMPORARY TABLE, ALTER DELETE, and ALTER UPDATE privileges when assigning privileges for users or roles. |[Description of grantable database and table privileges](https://docs.byteplus.com/docs/bytehouse/privilege-model#e75a2c67) |Sep 2025 |
|Data export |When exporting data, the export file name is now optional. Users can either specify a custom export file name or leave the export file name unspecified.<br><br>Not specifying a file name is suitable when exporting large files. During export, the system will split the source file into several smaller files, and the exported files will use system\-generated default names. |[Export data](https://docs.byteplus.com/docs/bytehouse/export-data-ce) |Sep 2025 |


<span id="73801674"></span>
## V 25.6 \- Release Date: August 2025


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Diagnostic\-Query insight |Adds support for Query insight. This feature, based on slow query logs and system table data in ByteHouse Enterprise, provides detailed execution information for the current query, including a query overview, execution plan visualization, resource consumption, data tables, error information, and more, helping you quickly locate and identify abnormal query issues. This function is applicable to troubleshooting slow queries, analyzing resource bottlenecks, optimizing SQL performance, and other scenarios. |[Query insight](https://docs.byteplus.com/docs/bytehouse/query-insight) |Aug 2025 |
|Diagnostic\-SQL diagnostic |Adds support for SQL diagnostic. This feature collects slow query logs. It provides multidimensional analyses of performance metrics, trends, and details to help you gain insights into the performance of clusters and instances, accurately identify inefficient queries, and achieve targeted SQL optimization. |[SQL diagnosis](https://docs.byteplus.com/docs/bytehouse/sql-diagnostic) |Aug 2025 |
|User profile management |Optimized user profile privilege management. Privileges can now be granted directly on the user parameter interface, simplifying the management of parameter access rights across different users. |[Modify configuration parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters) |Aug 2025 |
|Edit a table |Adds support for modifying column data types. |[Edit table](https://docs.byteplus.com/docs/bytehouse/edit-table) |Aug 2025 |
|Sub\-user management |Adds support for incremental synchronization of IAM sub\-users. This feature supports manually synchronizing sub\-users created on BytePlus to ByteHouse. |[IAM sub-user management](https://docs.byteplus.com/docs/bytehouse/sub-user-management) |Aug 2025 |
|Database user management |Adds support for **database users**. ByteHouse Enterprise separates IAM sub\-users from database users, supports the independent creation of database users, and grants data privileges to these users. You can use a database user account to access the ByteHouse database via API, CLI, connection drivers, BI tools, IDE tools, and other methods. |[Database user management](https://docs.byteplus.com/docs/bytehouse/database-user-management) |Aug 2025 |


<span id="514dade9"></span>
## V 25.5 \- Release Date: June 2025


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Data export |ByteHouse supports creating data export tasks to export data to BytePlus Object Storage (Torch Object Storage, TOS) either once or regularly, facilitating your data analysis. |[Export data](https://docs.byteplus.com/docs/bytehouse/export-data-ce) |June 2025 |
|Sub\-user management |Adds “ByteHouseCEReadOnlyAccess” policy: No roles/permissions; users can log in to the control panel and view all clusters, but cannot access any data within clusters without additional data authorization. |[IAM sub-user management](https://docs.byteplus.com/docs/bytehouse/sub-user-management) |June 2025 |


<span id="57430d64"></span>
## V 25.4 \- Release Date: May 2025


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Whitelist management |ByteHouse Enterprise Edition supports setting up whitelists for clusters to manage cluster access permissions and to realize fine\-grained access control. |[Whitelist management](https://docs.byteplus.com/docs/bytehouse/whitelist-management) |May 2025 |


<span id="4327a976"></span>
## V 25.3 \- Release Date: May 2025


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Role Management |Refine role permission management, split the functions of role management and authorization management, support granting table and database permissions to roles, and support granting and revoking role permissions for users, further enhancing the user experience of role management functions. |[Role management](https://docs.byteplus.com/docs/bytehouse/role-management) |May 2025 |
|Diagnostic \- Table Statistics |Add support for table statistics. ByteHouse supports collecting statistics from tables within the cluster, helping you view and analyze table information within the cluster. You can take optimization measures based on this information to enhance the cluster performance. |[Table statistics](https://docs.byteplus.com/docs/bytehouse/table-statistics) |May 2025 |
|Diagnostic \- Intelligent patrol |Add support for intelligent patrol. Intelligent patrol is used to check the system and cluster status to detect potential issues in a timely manner. You can create periodic patrol tasks or manually trigger tasks. The intelligent patrol will output reports according to patrol items, helping you detect and solve problems in advance, reduce system failures and downtime, and ensure system stability and reliability. |[Intelligent patrol](https://docs.byteplus.com/docs/bytehouse/intelligent-patrol) |May 2025 |


<span id="ccd07b3f"></span>
## V 25.1 \- Release Date: Mar 2025


|**Feature name** |**Description** |**Related Documents** |**Release date** |
|---|---|---|---|
|Cluster reconfiguration \- Horizontal scaling |Optimization of horizontal scaling capabilities, decoupling the strong synchronous relationship between horizontal scaling and table redistribution, and supporting manual configuration of redistribution strategies on the horizontal scaling page, with table\-level redistribution supporting manual redistribution as needed based on capacity and time. |[Reconfigure a cluster](https://docs.byteplus.com/docs/bytehouse/reconfigure-a-cluster)<br><br>[Data redistribution](https://docs.byteplus.com/docs/bytehouse/data-redistribution) |March 2025 |
|Resource group |When creating a resource group, it now supports graphical configuration of usage limits for the group, with options for soft and hard limits.<br><br><br>* Hard limit: Limits the number of CPU cores that can be used by the current resource group.<br><br>* Soft limit: Limits the current resource's maximum total CPU usage by percent. |[Create new resource group](https://docs.byteplus.com/docs/bytehouse/create-resource-group) |March 2025 |
|Data Management \- Create New Tables |Graphically creating tables now supports configuring jump number indexes. |[Create a new database/table](https://docs.byteplus.com/docs/bytehouse/create-a-new-database-table) |March 2025 |
|Data Management \- Table Retrieval |Optimize the data management page on the console to enhance table retrieval capabilities, conducting searches by accurate match. |Not involved |March 2025 |
|Permission Management |Add support for interface\-based configuration of row permissions, allowing flexible configuration and authorization of cluster row permission strategies via the console. |[Row privilege](https://docs.byteplus.com/docs/bytehouse/row-privilege) |March 2025 |


<span id="7300749a"></span>
# Year 2024

<span id="64b77804"></span>
## V 24.11 \- Release Date: Nov 2024


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Cold Storage Bandwidth Package |ByteHouse offers a service to adjust additional bandwidth where you can expand your throughput based on business needs, allowing for the purchase of up to 650 MB/s of extra bandwidth. |[Add extra bandwidth](https://docs.byteplus.com/docs/bytehouse/add-extra-bandwidth) |2024\-11\-30 |


<span id="c5b7a446"></span>
## V 24.9 \- Release Date: Oct 2024


|**Feature Name** |**Function Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|General Table Creation Mode |ByteHouse Enterprise starts supporting "General Table Creation Mode" which allows for the creation of one table to complete the construction of historical distributed tables and a local table. |[Table creation mode](https://docs.byteplus.com/docs/bytehouse/table-creation-mode) |2024\-11\-05 |
|DDL Template |Supports DDL template function, quickly insert commonly used create and modify SQL. |[Create a new database/table: Based on the DDL template](https://docs.byteplus.com/docs/bytehouse/create-a-database-table-based-on-ddl-template) |2024\-10\-15 |
|Paimon External Table Support |Supports reading Paimon external tables [Beta]. |[Paimon external table](https://docs.byteplus.com/docs/bytehouse/ce-paimon-external-table) |2024\-10\-15 |


<span id="5eadd52a"></span>
## V 24.8 \- Release Date: Augt 2024


* Starting from Augt 2024, ByteHouse Enterprise Edition version number has been changed to V24.8 and will be updated on this version number thereafter.



|**Feature name** |**description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Preprocessing Template |The purpose of a Prepared Statement is to efficiently execute the same (or similar) SQL statements repeatedly, avoiding repeated parsing and plan construction. |[Preprocessing query PREPARED STATEMENT](https://docs.byteplus.com/docs/bytehouse/preprocessing-query-prepared-statement) |2024\-08\-31 |


<span id="7f13ac11"></span>
## V 2.11.0 \- Release Date: Jul 2024


|**Feature Name** |**Feature Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Add Southeast Asian Node Support |ByteHouse Enterprise Edition has added a new node in Southeast Asia (Johor), which is the third node following North China 2 (Beijing) and East China 2 (Shanghai). |Not involved |2024\-07\-31 |
|GIS Spatiotemporal Analysis |Supports scenario\-based analysis for digital twins, geofences, store location selection, and advertising. |[Feature introduction](https://docs.byteplus.com/docs/bytehouse/gis-introduction) |2024\-07\-31 |
|Vector Search |Supports application scenarios such as recommendation systems, picture and video retrieval, search engines, and large model knowledge bases. |[Enable vector search](https://docs.byteplus.com/docs/bytehouse/start-vector-search-service) |2024\-07\-31 |
|Full Text Search [Beta] |Supports keyword search in text data for scenarios like log analysis. |[Use full-text search](https://docs.byteplus.com/docs/bytehouse/full-text-search) |2024\-07\-31 |


<span id="7e14cb79"></span>
## V 2.10.0 \- Release Date: Apr 2024

Performance


* Support new node specifications: 16 cores 128GB, 32 cores 256GB, 64 cores 512GB

* Visualization table creation feature optimization, supporting the import of table structure through JSON, Language Schema and others;


Engine


* Concurrency performance improvement, supporting topN optimization, Prepared Statement, unique_index and other high\-concurrency features;


DataRanger's Technical Support


* Support one\-click configuration for recommended alerts.


<span id="58b5d16f"></span>
## V 2.9.1 \- Release date: 2024\-Mar

Performance


* Add configuration template: wide table query template, complex query template, high concurrency template and others, activate high\-performance queries with one\-click.


User Experience


* Supports selecting a timezone, synchronizing BytePlus strategies, and other experience enhancements when creating.


<span id="0465f906"></span>
## V 2.9.0 \- Release date: Jan 2024

DataRanger's Technical Support


* Query Diagnosis: Supports query diagnosis function, one\-click diagnosis of slow query execution plans, query configurations, and load during execution.


Engine


* SQL Syntax: Basically compatible with ClickHouse SQL syntax 23.3.

* Data Type: Supports native ClickHouse types including JSON, Int128, Date64, GIS related data types (Point).

* Secondary Indexes: Supports HNSW indexes (for vector queries) and R\-Tree (for geographical retrieval).


<span id="26c5cc24"></span>
# Year 2023

<span id="815fe416"></span>
## Version 2.8.2 \- Release Date: Oct 2023

Security Management


* Permission granularity: Added control for accessing the management interface.

* Encryption: Supports SSL transport encryption and database transparent encryption.


DataRanger's Technical Support


* Scale\-Out: Support for replication increment.

* Modify configuration: Supports high concurrency mode and large query mode in two configuration templates.

* Resource Group Management: Supports limiting user's CPU and memory usage through resource groups.


Engine


* HaUniqueMergeTree fully supports Alter syntax.


<span id="df706902"></span>
## V 2.2~2.7


|**Version number** |**Release date** |**Feature description** |
|---|---|---|
|2.7.2 |2023/9 |Supports selecting 3\-5 replicas when creating |
|2.7.1 |2023/8 |Compatible with MySQL clients and common functions |
|2.7.0 |2023/7 |Officially supports horizontal scaling features |
|||Supports activating cold storage based on object storage to save user costs (Beta) |
|||Supports visual modification of user configurations |
|2.6.0 |2023/6 |Supports visual modification of system configuration |
|2.4.2 |2023/5 |The on\-prem version supports complete monitoring and alert functions (Email alerts, Lark alerts). |
|2.4.1 |2023/4 |Supports cluster health status (Beta) |
|||Supports horizontal scaling (Beta) |
|||The query gateway supports TCP protocol |
|||Cluster server list, supports search for CPU/memory/storage metrics of the current server |
|2.4.0 |2023/3 |Supports creating scheduled tasks for SQL/import |
|||Supports initiating long SQL asynchronously in the control plane |
|||Supports importing from ClickHouse/Hive data sources to ByteHouse (Beta) |
|2.3.0 |2023/2 |Supports table\-level backup and restoration |
|||Supports the Hive external table engine |
|||Cluster mode that supports the MaterializeMySQL library engine (Distributed_mode) |
|2.2.0 |2023/1 |Supports the management of maintenance tasks, capable of managing database creation, table creation, and user changes. |
|||Supports vertical scaling |


<span id="c0f4fb98"></span>
# Year 2022

<span id="fefabfbb"></span>
## Version 2.1 \- Release date: 2022\-11\-1

Change Log:


1. Supports single\-copy mode;

2. Supports cloud monitoring;

3. Supports viewing server states in the cluster;

4. Adds a new object storage import method.


<span id="ac5ec872"></span>
## Version 2.0 \- Release date: 2022\-10\-10

Change Log:


1. Enterprise Edition first activated on BytePlus.

2. Supports self\-service cluster application and monthly payments.
