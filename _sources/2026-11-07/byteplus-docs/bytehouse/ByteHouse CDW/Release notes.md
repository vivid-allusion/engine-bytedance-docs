---
title: "Release notes"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/Release-Notes"
---

This article introduces the latest developments in ByteHouse Cloud Data Warehouse related features. The new features will be released in various regions one after another. Welcome to experience them. Some new features may require whitelist access or be in a limited release phase. We recommend reviewing the user documentation for relevant features to understand access requirements before trying new features. If you need whitelisting assistance or encounter issues during use, please submit a support ticket or contact the ByteHouse team.

<span id="9ea6765e"></span>
# 2025

<span id="f896ae34"></span>
## December 2025 \- V2.21.0


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Object table |Adds support for object tables. ByteHouse Cloud Data Warehouse establishes a connection to BytePlus Object Storage (TOS) through object tables, mapping unstructured data in object storage (such as text, images, and more) into internal ByteHouse tables. This is suitable for multimodal data management scenarios, such as managing unstructured data like images and text in AI applications. |[Object table](https://docs.byteplus.com/docs/bytehouse/object-table) |Dec 2025 |
|Visual retrieval of image/text vectors |Adds support for visual retrieval of image/text vectors. ByteHouse Cloud Data Warehouse supports visual retrieval of image/text vectors, enabling multimodal vector retrieval for text, images, and mixed image\-text data. It supports creation, management, and retrieval testing of retrieval objects, making it suitable for scenarios in finance compliance, e\-commerce recommendation, intelligent driving, gaming, and many other fields that require efficient retrieval of unstructured data. This significantly improves retrieval efficiency and adapts to complex business requirements. |[Visual image-text vector search](https://docs.byteplus.com/docs/bytehouse/visual-image-text-vector-search) |Dec 2025 |
|Backup and restore |Adds support for incremental data restore, enabling precise restore to any specified point in time. You can flexibly choose between full restore and full plus incremental restore strategies, ensuring data integrity and security while greatly reducing restore time and improving data restore efficiency. |[Backup and restore](https://docs.byteplus.com/docs/bytehouse/full-backup-restore) |Dec 2025 |
|Asynchronous materialized view |Adds support for configuring security optimization parameters for asynchronous materialized views to help improve query performance. Contact the ByteHouse team before use to enable the corresponding parameters as needed. |[Visual management of asynchronous materialized views](https://docs.byteplus.com/docs/bytehouse/visually-manage-asynchronous-materialized-view) |Dec 2025 |
|Statistics |New statistics toggle feature. After enabling, the optimizer's CBO optimization capability can be activated to further optimize query efficiency and write performance, but this will also occupy part of the resources of the default write virtual warehouse. |[Set statistics feature](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters#d659ba84) |Dec 2025 |
|Network information |The network information module in this version has optimized the following feature points:<br><br><br>* Private network: Support viewing private network IP through private network details. In general, it is recommended to use the private network domain name as a priority.<br><br>* IP allowlist: Optimized the display effect of the IP allowlist page. |[Network settings](https://docs.byteplus.com/docs/bytehouse/network-settings) |Dec 2025 |


<span id="b3560e87"></span>
## October 2025 \- V2.20.0


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Intelligent assistant |Adds support for generating SQL from natural language. ByteHouse intelligent assistant generates SQL statements from your natural language input and supports features such as generating example queries, SQL query optimization, and more\*.\* |[Intelligent assistant](https://docs.byteplus.com/docs/bytehouse/intelligent-assistant) |Oct 2025 |
|External catalogs |* Adds support for Iceberg and Paimon external catalogs, and metadata storage types now support Hive, LAS, Hadoop, and Filesystem, resulting in a wider range of supported types.<br><br>* Supports visual display of databases, tables, and table preview information in a catalog; supports adding and deleting a catalog; supports viewing database and table information in a catalog; and supports configuring catalog resource and data privileges. |[Manage external catalog](https://docs.byteplus.com/docs/bytehouse/manage-external-catalog) |Oct 2025 |
|Preload |* Adds support for visual preloading management: In addition to automatic cache cleanup based on the current preloading management policy, manual cleanup of table or partition cache is now supported, making operations more flexible.<br><br>* Adds support for real\-time preloading of materialized views. The system will automatically obtain the latest data written to materialized views and load it into the cache. |[Preload](https://docs.byteplus.com/docs/bytehouse/docs-query-acceleration-preload) |Oct 2025 |
|Distributed cache |Adds support for distributed cache. Distributed cache is the cache sharing solution provided by ByteHouse Cloud Data Warehouse. Based on distributed cache technology and deployed across computing nodes, it enables globally shared cache resources, effectively improving data query performance and meeting your requirements for high\-performance queries and stability. |[Distributed cache](https://docs.byteplus.com/docs/bytehouse/distributed-cache) |Oct 2025 |
|Virtual warehouse local disk |The intelligent cache name has been changed to local disk to make it easier to understand. |[Use virtual warehouse local disk](https://docs.byteplus.com/docs/bytehouse/intelligent-cache) |Oct 2025 |
|Project/tag\-based cost allocation |Adds support for binding projects or tags to virtual warehouses, private servers, and storage resources. After configuration, you can use the Cost Analysis feature in the BytePlus Cost Center to view cost details by project or tag, enabling precise management of cloud resource costs. |[Manage cost allocation](https://docs.byteplus.com/docs/bytehouse/manage-cost-allocation) |Oct 2025 |
|SQL worksheet |SQL worksheets support selecting a database. Before executing a query, you can first select the target database. For subsequent queries, simply use the table name in the SQL statement; there is no need to specify the database name. |[SQL Worksheet](https://docs.byteplus.com/docs/bytehouse/docs-query-editor-and-worksheet) |Oct 2025 |
|Task center |Optimized the function buttons of the task center and the display of task details:<br><br><br>* An immediate execution button has been added to the task list, allowing tasks to be executed directly from the task list page, making operation more convenient.<br><br>* The task details page supports displaying the query ID and more detailed error information to facilitate troubleshooting. |[Cron task](https://docs.byteplus.com/docs/bytehouse/docs-cron-task) |Oct 2025 |
|Data privileges |Adds support for managing data privileges, including global, UDF, and external catalog privileges, making privilege management more flexible. |[Data privilege management](https://docs.byteplus.com/docs/bytehouse/docs-permission) |Oct 2025 |
|Hive metastore cache |Adds support for Hive metastore cache. ByteHouse has developed a Hive metastore cache feature that stores metadata information in server memory. This reduces the overhead of accessing the Hive Metastore and significantly improves query performance when the same tables or partitions are frequently accessed in business scenarios. |[Hive metastore cache](https://docs.byteplus.com/docs/bytehouse/hive-metastore-cache) |Oct 2025 |
|View SQL Security |Adds support for view SQL Security starting from version 2.3, the ByteHouse Cloud Data Warehouse engine introduces the SQL Security feature for views, adding DEFINER and INVOKER security contexts to control the execution behavior of views. This feature is suitable for scenarios where restricted data access permissions need to be provided to different users. |[Create view (CREATE VIEW)](https://docs.byteplus.com/docs/bytehouse/create-statement#dd83b29d) |Oct 2025 |


<span id="2329befd"></span>
## September 2025 \- V2.19.0


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|SQL Param group |Adds support for SQL params. An SQL parameter group refers to a set of parameters provided when running SQL statements in the ByteHouse console. You can select the required SQL parameter group when executing queries in the SQL worksheet, and the SQL parameter group will take effect in the session running in the ByteHouse console. |[SQL Worksheet](https://docs.byteplus.com/docs/bytehouse/docs-query-editor-and-worksheet) |Sep 2025 |
|IAM subuser \- default virtual warehouse setting |Adds support for administrators to set a default virtual warehouse for IAM users, and optimize compute resource allocation efficiency. |[Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management) |Sep 2025 |
|Cache loading |* Adds support for single preloading tasks. It supports preloading data for a specified date in a single operation. After the data is loaded, the least recently used (LRU) eviction strategy will be applied to clear the data.<br><br>* Optimized the display of periodic cache tasks, now supporting cache loading status display at the partition level. It also supports retrying preloading tasks for either the entire table or individual partitions, and displays information such as task duration, success status, success percentage, and failure reasons. |[Preload](https://docs.byteplus.com/docs/bytehouse/docs-query-acceleration-preload) |Sep 2025 |
|SQL worksheet |The SQL worksheet has been optimized. The optimization points are as follows:<br><br><br>* Adds query results processing<br><br>   * Supports sorting and filtering of results, making it easy to quickly locate key data.<br><br>   * You can remove query results as needed to reduce page cache load. Removed query results are not deleted and can be viewed in the audit log under SQL history.<br><br>* Adds support for real\-time display of run duration in queries, providing an intuitive understanding of execution efficiency.<br><br>* Adds tenant\-level dialect settings, which can record the last selected dialect, eliminating the need for repeated selection.<br><br>* User experience optimizations:<br><br>   * Small screens now support dragging the scrollbar.<br><br>   * When you create a new worksheet, the system will check for duplicate names.<br><br>   * Opening or switching worksheets requires only a single click, making actions more convenient. |[SQL Worksheet](https://docs.byteplus.com/docs/bytehouse/docs-query-editor-and-worksheet) |Sep 2025 |
|SQL audit |* Optimized the SQL audit information display, supporting one\-click switching between two search modes: "by Query ID" and "by SQL Statement", which improves retrieval efficiency.<br><br>* Supports searching for running queries. You can search by query ID, SQL statement, or virtual warehouse. |[Query history](https://docs.byteplus.com/docs/bytehouse/sql-audit) |Sep 2025 |
|Resource privileges \- global audit log |Adds support for the global audit log resource privilege, allowing administrators to grant this privilege to sub\-users. Once a sub\-user obtains this privilege, the sub\-user can view global audit logs. |[Resource privilege management](https://docs.byteplus.com/docs/bytehouse/resource-privilege-management)<br><br>[Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)<br><br>[Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)<br><br>[Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration) |Sep 2025 |


<span id="c9964ced"></span>
## July 2025 \- V2.17.0


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|[Beta] Intelligent assistant |Adds support for intelligent assistant. ByteHouse intelligent assistant provides intelligent Q&A and AI log retrieval functions, helping you use ByteHouse. The intelligent assistant also supports linking your created knowledge bases for more accurate answers and problem identification.<br><br><br>* Intelligent Q&A: Intelligent assistant can quickly resolve issues you encounter using ByteHouse.<br><br>* AI log retrieval and analysis: Intelligent assistant supports log insights, summarizes key log points, analyzes potential problems, and provides optimization suggestions. The intelligent assistant also converts your natural language commands into SQL statements and searches the corresponding logs.<br><br>* Link your knowledge base: Intelligent assistant supports linking your created knowledge bases, combining your business and industry knowledge for more precise answers to usage questions and abnormal event analysis, improving problem resolution efficiency. |[Intelligent assistant](https://docs.byteplus.com/docs/bytehouse/intelligent-assistant) |July 2025 |
|[Beta] Knowledge base |Adds support for the knowledge base. ByteHouse supports uploading your own knowledge base, offering a complete process for knowledge creation, management, and intelligent application. It ensures data security through fine\-grained permission management and suits scenarios such as enterprise business knowledge management and intelligent Q&A support. |[Knowledge base](https://docs.byteplus.com/docs/bytehouse/knowledge-base) |July 2025 |
|[Beta] Virtual warehouse \- Load elasticity |Adds support for virtual warehouse load elasticity. Load elasticity is the auto\-scaling feature of the virtual warehouse that dynamically allocates elastic resources and adjusts specifications automatically based on preset policies to adapt to workload fluctuations. You can set the load elasticity policy for the virtual warehouse as needed. The system automatically scales according to the set thresholds. |[Create⧸Edit virtual warehouse](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse) |July 2025 |
|Virtual warehouse \- database level write virtual warehouse |Adds support for configuring dedicated write virtual warehouses for databases. After setting a database\-level write virtual warehouse for a database, writing data to that database will use the specified virtual warehouse by default. |[Create⧸Edit virtual warehouse](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse) |July 2025 |
|Virtual warehouse \- Custom parameters |Adds support for custom SQL parameters to further improve SQL execution efficiency and better adapt to your business scenarios for optimized data processing. |[Manage parameters](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters) |July 2025 |
|Query history |Query history adds support for CPU total duration and maximum memory usage.<br><br><br>* CPU total duration: The total CPU time of all segments in the virtual warehouse. Since the segments run in parallel, this value may exceed the query duration.<br><br>* Max memory usage (segment): The maximum memory usage of all segments executed by this virtual warehouse. |[Query history](https://docs.byteplus.com/docs/bytehouse/sql-audit) |July 2025 |
|Data encryption |Adds support for transparent data encryption, allowing encryption of entire tables or specific columns. This enhances core data security and meets your regulatory and compliance requirements. |[Data encryption](https://docs.byteplus.com/docs/bytehouse/data-encryption) |July 2025 |


<span id="7d6aa311"></span>
## June 2025 \- V2.16.0


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|External Catalog |ByteHouse supports visual display and management of external catalogs, including adding/deleting catalogs, viewing databases and table information within catalogs, and configuring catalog resources and data permissions. |[Manage external catalog](https://docs.byteplus.com/docs/bytehouse/manage-external-catalog) |June 2025 |
|IP Whitelist Management |Adds support for IP whitelist management. It allows defining accessible IP ranges for granular access control. |[Network settings](https://docs.byteplus.com/docs/bytehouse/network-settings) |June 2025 |
|Diagnostics \- Intelligent Patrol |Adds support for intelligent patrol. Intelligent patrol is a preventive maintenance measure for checking system status and proactively identifying potential issues. It generates reports by inspection items, enabling users to detect and resolve issues early, reducing system failures and downtime while improving stability and reliability. |[Intelligent patrol](https://docs.byteplus.com/docs/bytehouse/cdw-intelligent-patrol) |June 2025 |
|Log Retrieval Analysis |Adds support for log exploration and analysis with full\-text visual search capabilities. This feature resembles Kibana's Discover functionality, providing visual analysis of log data. ByteHouse also integrates an AI\-powered search assistant that automatically generates SQL queries and offers log insights, allowing you to perform log analysis and obtain optimization suggestions through natural language input. |[Log retrieval analysis](https://docs.byteplus.com/docs/bytehouse/log-retrieval-analysis) |June 2025 |
|Vector Search |ByteHouse Vector Search supports storage and efficient similarity retrieval of vector features from unstructured data (text, images, videos, etc.). This feature is applicable to scenarios like image\-to\-image search, video retrieval, text search, and integration with large models for intelligent applications. ByteHouse currently supports vector search using HNSW or Faiss index via SQL commands or Python API. |[Enable vector search](https://docs.byteplus.com/docs/bytehouse/vector-retrieval)<br><br>[Perform vector search using SQL](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-SQL)<br><br>[Perform vector search using Python API](https://docs.byteplus.com/docs/bytehouse/perform-vector-search-using-python-api) |June 2025 |
|Intelligent Caching |Supports caching historical/real\-time data and loading table\-level/partition\-level data into the cache. |[Use virtual warehouse local disk](https://docs.byteplus.com/docs/bytehouse/intelligent-cache) |June 2025 |
|[Beta] Binlog |Supports real\-time Binlog data subscriptions to enable event\-driven real\-time data warehouses. Deeply integrated with Flink, ByteHouse supports Flink consumption for incremental data production/materialized views, synchronizing real\-time data warehouse changes to external systems. |None |June 2025 |
|[Alpha] Row Storage & Row\-level Indexes |Supports hybrid row/column storage to address I/O bottlenecks in point query scenarios. When row storage is enabled during table creation, point queries require only one I/O per row, achieving order\-of\-magnitude performance improvements in wide\-table scenarios.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The row\-storage table and row\-level index functions are Alpha features and can be used for PoC. If you need to use the row\-store table function, please submit a work order or contact the ByteHouse team to obtain whitelist permission.</div><br> |None |June 2025 |
|[Beta] Dynamic Partitioned Tables |Adds support for creating dynamic partitioned tables and dynamic scaling of bucket tables. It allows defining bucket keys via expressions and using `SETTINGS` parameters to create dynamic partitioned tables. It also supports dynamically adjusting the total bucket count for bucket tables (including unique\-key tables) to optimize load balancing and query parallelism when data growth or query loads require scaling. |[Create dynamic partitioned tables](https://docs.byteplus.com/docs/bytehouse/create-statement#b9a1a39f)<br><br>[Bucket table dynamic expansion](https://docs.byteplus.com/docs/bytehouse/bucket-table-dynamic-expansion) |June 2025 |
|Funnel Analysis Functions |ByteHouse now supports dedicated funnel analysis functions optimized for user behavior analysis. Funnel analysis function helps observe user funnel aggregation per time unit (day) within a selected time range to analyze conversion paths efficiently. |[Funnel analysis functions](https://docs.byteplus.com/docs/bytehouse/cdw-funnel-analysis-functions) |June 2025 |
|[Beta] Python UDF |Adds support for Python User\-Defined Functions (UDFs), allowing data processing with Python. It supports `CREATE`, `DROP`, `SHOW`, `SHOW CREATE`, and `SELECT` operations. |[User-defined Functions (UDF)](https://docs.byteplus.com/docs/bytehouse/docs-user-defined-functions-udf) |June 2025 |
|Hive External Tables |Updates for Hive external tables:<br><br><br>* Adds BSP mode support.<br><br>* Materialized views now support Hive external tables.<br><br>* Metadata fetching supports cached retrieval.<br><br>* Supports CSV/Text format.<br><br>* Performance optimization for `INSERT-SELECT` operations on Hive external tables. |[Hive external table](https://docs.byteplus.com/docs/bytehouse/hive-external-table) |June 2025 |
|Monitoring & Alerts |Adds monitoring/alerting for caches and dedicated servers, optimized virtual warehouse monitoring, and enhanced comprehensive data resource monitoring to improve operational stability. |None |June 2025 |
|Flink CDC Connector |Supports multi\-sink partial column updates. |None |June 2025 |


<span id="9f70d3fe"></span>
## April 2025 \- V2.15.0


|**Feature Name** |**Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Manage Virtual Warehouse Parameters |Creating virtual warehouses supports selecting virtual warehouse types, including OLAP and ELT types. Editing virtual warehouses supports managing parameters, such as changing list permissions, switching virtual warehouses, and editing parameters. The description of the new virtual warehouse type is as follows:<br><br><br>* OLAP: Suitable for high\-concurrency and low\-latency OLAP queries, supports complex SQL queries and interactive analysis.<br><br>* ELT: Suitable for long\-running batch processing, applied to batch data import, cleaning, and large\-scale offline computation scenarios. |[Create⧸Edit virtual warehouse](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse)<br><br>[Manage parameters](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters) |Apr 2025 |
|Create Table |Creating tables supports configuring partition keys using expressions, offering more partition selections; the table editing interface is optimized, requiring attention only to editable table properties. |[Working with databases, tables and views](https://docs.byteplus.com/docs/bytehouse/docs-databases-tables-and-views) |April 2025 |
|Private Server |Exclusive Server binding writing virtual warehouse process optimization. When ByteHouse is first activated, the exclusive Server is also activated synchronously, with the default writing virtual warehouse being the virtual warehouse created at the time of activation. If multiple virtual warehouses are activated simultaneously, the system will use the first created virtual warehouse as the default write virtual warehouse. |[Private server](https://docs.byteplus.com/docs/bytehouse/private-server) |April 2025 |
|Database Account |ByteHouse separates IAM account and database account, supports independent creation of database accounts, grants resource permissions and data permissions to the account, and supports access to ByteHouse database through CLI, BI tools, ELT tools, IDE tools, API, and other methods. |[Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account) |April 2025 |
|Diagnostic Analysis |Adds support for partition health monitoring and diagnostics to help you visually monitor partition statuses, provide partition diagnostic information, and assist in optimizing partition tables. |[Partition health diagnosis](https://docs.byteplus.com/docs/bytehouse/partition-health-diagnosis) |April 2025 |
|Sync Materialized Views |Support the management of sync materialized views in a visual manner; you can create sync materialized views through the ByteHouse console page. |[Visual management of synchronous materialized views](https://docs.byteplus.com/docs/bytehouse/visually-manage-synchronous-materialized-view) |April 2025 |
|Async Materialized Views |Support the management of async materialized views in a visual manner; you can create async materialized views through the ByteHouse console page. |[Visual management of asynchronous materialized views](https://docs.byteplus.com/docs/bytehouse/visually-manage-asynchronous-materialized-view) |April 2025 |
|Manage Environment |Support adding an environment display name to better distinguish the purposes of different environments. It also supports modifying the environment display name after creation. |[Manage environment](https://docs.byteplus.com/docs/bytehouse/manage-environment) |April 2025 |


<span id="1ba5252f"></span>
## March 2025 \- V2.13.0, V2.14.0


|**Feature name** |**Description** |**Related Documents** |**Release date** |
|---|---|---|---|
|Dedicated Server |Add functionality to bind the dedicated server to a write virtual warehouse when purchasing. This further secures resources. |[Private server](https://docs.byteplus.com/docs/bytehouse/private-server) |Mar 2025 |
|Cache loading |Add support for creating cache loading tasks via a GUI. You can create tasks to cycle load existing data and to load the latest real\-time data. |[Preload](https://docs.byteplus.com/docs/bytehouse/docs-query-acceleration-preload) |Mar 2025 |
|Virtual warehouse |When purchasing virtual warehouses, add the capability to customize specifications. You can flexibly choose to buy N (11 or more) XL\-sized virtual warehouses to enhance configuration flexibility. |None |Mar 2025 |
|Audit Log |Add support for user activity related audit logs. You can view detailed user behavior log data through user activity audit logs. The operations you can view include: **Backup & Restore**, **Environment**, **Network**, **Dedicated Server**, **User & Roles**. You can view the details of the add, delete, and modify logs for the corresponding operational objects. |[User activities](https://docs.byteplus.com/docs/bytehouse/User_activities) |Mar 2025 |
||Enhanced SQL audit capabilities. You can turn on the detailed log toggle, which will generate a query_log table in the system to record detailed SQL operation logs. |[Query history](https://docs.byteplus.com/docs/bytehouse/sql-audit) |Mar 2025 |
|Permission Management |Enhanced ByteHouse’s permission management capabilities, adding support for USE and ALL in the permissions scope for the virtual warehouse.<br><br><br>* USE: Allows querying using the virtual warehouse and restoring the group when "Auto Restore" is activated.<br><br>* All: Grant all permissions to the virtual warehouse. |[Resource privilege management](https://docs.byteplus.com/docs/bytehouse/resource-privilege-management)<br><br>[Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration)<br><br>[Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management) |March 2025 |


<span id="262e41ff"></span>
# 2024

<span id="3e2b5b6f"></span>
## December 2024 \- V2.12.0


|**Feature name** |**Feature description** |**Related Documents** |**Release date** |
|---|---|---|---|
|Environment management |Add support for multi\-environment management capabilities. Starting from version 2.12, support users to set up multiple environments according to their needs, where computing, storage, databases, network, audits, and permissions are completely isolated in different environments. This can meet user requirements for multiple instances, access to multiple VPCs, and others. |[Manage environment](https://docs.byteplus.com/docs/bytehouse/manage-environment) |December 2024 |
|External table |Enhanced external appearance capabilities:<br><br><br>* External table read: Added support for Hive, Hudi, Paimon, and Iceberg types for external table reading capabilities.<br><br>* External table write: Added support for writing to Hive external tables.<br><br>* Through the optimization of external table metadata and data caching functions, the performance of external table queries has been improved. |[External table](https://docs.byteplus.com/en/docs/bytehouse/external-table) |December 2024 |
|Backup and Restore |Added support for data backup functions, which can resolve issues of data restoration after accidental deletions or modifications, as well as disaster recovery capabilities in extreme situations. |[Full backup restore](https://docs.byteplus.com/docs/bytehouse/full-backup-restore) |December 2024 |
|Materialized Views |Supports asynchronous multi\-table materialized views and unique table materialized views. |[SQL management of asynchronous materialized view by SQL](https://docs.byteplus.com/docs/bytehouse/Asynchronous_Materialized_View) |December 2024 |
|Syntax Compatibility |Adds self\-increasing column feature. |None |December 2024 |


<span id="f2981bd3"></span>
## November 2024 \- V2.10.0


|**Feature name** |**Function description** |**Related Documents** |**Release date** |
|---|---|---|---|
|Add Intelligent Caching Feature |The intelligent caching feature can cache cold data from object storage, increase the probability of hot reads, and significantly boost query efficiency for high\-performance, high\-QPS scenarios. |[Use virtual warehouse local disk](https://docs.byteplus.com/docs/bytehouse/intelligent-cache) |2024\-11\-20 |
|Add Johor node |ByteHouse CDW has added a Johor node, following the nodes in North China 2 (Beijing), East China 2 (Shanghai), and South China 1 (Guangzhou). |*  |2024\-12\-06 |
|Purchase Exclusive Server |For business scenarios with high concurrency and high QPS, users can purchase dedicated Server resources. |[Specifications and pricing](https://docs.byteplus.com/docs/bytehouse/specifications-and-pricing) |2024\-12\-13 |


<span id="d256084b"></span>
## September 2024 \- V2.9.0


|**Feature Name** |**Feature Description** |**Related Documents** |**Release Date** |
|---|---|---|---|
|Interface Optimization |Optimized experience for visualized library table management (materialized views, external tables, library tables). |*  |2024\-09\-30 |
|Audit Log |The console has added the Audit Log module, which can audit and manage SQL, virtual warehouses, and permissions. |[Audit Log](https://docs.byteplus.com/en/docs/bytehouse/audit-log) |2024\-09\-30 |


&nbsp;

<span id="f0813f80"></span>
## August 2024 \- v2.7.0


|**Function name** |**Function description** |**Related Documentation** |**Release time** |
|---|---|---|---|
|Enhanced ELT ability |ELT enhances failure retry capability, observability logging, and operation and maintenance monitoring assurance capabilities. |[ELT Support](https://docs.byteplus.com/docs/bytehouse/docs-elt-support) |2024\-08\-15 |
|Support for full\-text search advanced features |Full\-text search (or text\-only search) provides the ability to identify natural language documents that satisfy a query.<br><br>The most common type of search is to find all documents that contain a given query term. Full\-text indexing allows documents to be preprocessed and indexed for quick search later. |[Full-text search](https://docs.byteplus.com/docs/bytehouse/full_text_search) |2024\-08\-15 |
|Asynchronous materialized views |ByteHouse has added an asynchronous materialized view function, which can better support scenarios associated with multiple tables and reduce the impact on data import.<br><br>The main uses of asynchronous views include complex query acceleration and data processing. | |2024\-08\-15 |
|Ecosystem support |Enhanced support for popular BIs (Jasper Studio, Grafana, etc.) and IDEs (DataGrip, DBeaver, Navicat). |[Ecosystem](https://docs.byteplus.com/en/docs/bytehouse/docs-ecosystem) |2024\-08\-15 |


<span id="7da7ee96"></span>
## June 2024 \- v2.4.0


|**Function name** |**Function description** |**Related Documentation** |**Release time** |
|---|---|---|---|
|Support billing mode switching |Support, annual subscription, and pay\-as\-you\-go modes switch to each other to provide users with a more flexible payment model. |[Virtual warehouse specification change](https://docs.byteplus.com/docs/bytehouse/virtual-warehouse-specification-change) |2024\-06\-10 |
|Enhanced rights management capabilities |* Support user\-level rights management, allowing users to directly grant permissions (resource permissions, data permissions) or roles.<br><br>* Support, resource rights management, granting resource permissions to users or roles<br><br>* Support, data rights management, granting data rights to users or roles |[Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management) |2024\-06\-10 |
|Enhanced monitoring alarm function |Support, task center, storage, connectivity, module visual monitoring and custom alarms |None |2024\-06\-10 |
|Data import support validation |Support, data validation in general mode, expert mode |None |2024\-06\-10 |


<span id="78762b2c"></span>
## April 2024 \- v2.3.0


|**Function name** |**Function description** |**Related Documentation** |**Release time** |
|---|---|---|---|
|ELT Function Enhancement |ELT capability supports BSP, query queue, failure retry; |[ELT Support](https://docs.byteplus.com/docs/bytehouse/docs-elt-support) |2024\-04\-10 |
|Optimization, billing model |The tenant\-level billing mode sinks to the computing group level, and the billing mode is no longer distinguished at the tenant level; |[Create⧸Edit virtual warehouse](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse) |2024\-04\-10 |
|Support full text search capability (beta) |Full\-text search provides the ability to identify natural language documents that satisfy a query. We added the ability to index text inverted to support faster ways of text retrieval and filtering. |[Full-text search](https://docs.byteplus.com/docs/bytehouse/full_text_search) |2024\-04\-10 |
|MySQL compatibility enhancements |MySQL compatibility is over 80%. |[MySQL-compatible syntax](https://docs.byteplus.com/en/docs/bytehouse/docs-mysql-compatibility_1) |2024\-04\-10 |


<span id="00c98f68"></span>
## March 2024 \- v2.2.0


|**Function name** |**Function description** |**Release time** |
|---|---|---|
|Added tenant management module |* Support tenant\-level basic resource management, and support users to unsubscribe from storage.<br><br>* Support users to bind VPC/EIP to build tenant\-level private network and public network domain name, and provide tenant\-level connection URL;<br><br>* Support tenant default parameter configuration; |2024\-03\-07 |
|Custom monitoring alarm function |* Reoptimized CDW monitoring dashboard for cloud monitoring to support custom alarms (virtual warehouses, certificates & keys).<br><br>* AWS metrics pushed to CloudWatch, support custom alerts;<br><br><br> |2024\-03\-07 |
|Query history optimization |Support slow query, error query, QueryID directional query to solve the performance problem of mass query; |2024\-03\-07 |


<span id="d8000860"></span>
## January 2024 \- v2.1.0


|**Function name** |**Function description** |**Release time** |
|---|---|---|
|User experience optimization |* Optimize the experience of using the task center:<br><br>   * Virtual warehouse (VM) allows users to set scaling time and auto\-scaling time;<br><br>   * Support setting the task run time zone.<br><br>* Visual table building supports copying complex SQL into SQL worksheets for execution.<br><br>* SQL worksheet experience:<br><br>   * Supports cursor selection of full SQL (including subqueries) execution.<br><br><br> |2024\-01\-31 |
|Payment method optimization adjustment |* The prepaid model supports purchase, renewal, unsubscribe, volume expansion and contraction calculation groups.<br><br>* The storage type is adjusted to post\-paid, billed monthly based on usage. |2024\-01\-31 |


<span id="2dadeb06"></span>
# 2023

<span id="521c7b5f"></span>
## December 2023 \- v2.0.4


|**Function name** |**Function description** |**Release time** |
|---|---|---|
|Function Enhancement Optimization |* ELT Enhancement: Support BSP scheduling mode, which can run large queries and ELT tasks more stably; Dafu optimizes the performance of Join /agg spill.<br><br>* VW Enhancement: Support for Backup Virtual Warehouse, which improves the availability of single VW services.<br><br>* Execution plan: supports Explain\-Simple SQL, does not print node information. |2023\-12 |
|Performance and Diagnostic Optimization |* Cold read performance improvement: The introduction of ReadBuffer's Preload and other optimizations has improved S3 read performance by 134% and HDFS by 27%.<br><br>* Observability: Introduces the ability to trace problems across the entire link.<br><br>* SQL diagnostics: Support SQL Profiler to quickly diagnose and analyze SQL problems. |2023\-12 |


<span id="ab14d9ab"></span>
## October 2023 \- v2.0.0


|**Function name** |**Function description** |**Release time** |
|---|---|---|
|Ecological compatibility improvement |* ClickHouse compatibility<br><br>   * Function: Consistent with ClickHouse 21.8 function<br><br>   * New data types: Time/Bool/Date32/Uint256/Decimal256<br><br>   * New table engine: CnchCollapsingMergeTree, CnchReplacingMergeTree, CnchSummingMergeTree, CnchGraphiteMergeTree, CnchVersionedCollapsingMergeTree<br><br>* MySQL Compatibility: ByteHouse is compatible with MySQL syntax. Users who are already familiar with MySQL can use ByteHouse more easily, thus enabling a faster transition to efficient use of ByteHouse.<br><br>   * MySQL dialect (DML)<br><br>   * MySQL Functions<br><br>   * MySQL protocol<br><br>* Connectors: Start supporting Power BI/Sugar BI/Quick BI/DolphinScheduler |2023\-10 |
|New features |* ELT Support Phase 1: ByteHouse has gradually introduced support for Extract\-Load\-Transform (ELT). This allows users to avoid maintaining multiple heterogeneous data systems.<br><br>* Timed tasks: ByteHouse users can use timed tasks to set up schedules to expand and contract the size of the virtual warehouse (VW) to match query traffic/workload, allowing users to save costs.<br><br>* Preload: Load data remotely into the local disk cache to speed up upcoming queries. Once the preload is complete, the query will read data from local disk instead of remote storage. |2023\-10 |


&nbsp;
