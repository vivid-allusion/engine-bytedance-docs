---
title: "Spatial analysis management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Spatial_analysis_management"
---

Database Workshop DBW provides spatial analysis capabilities. This feature allows you to view the space usage of your Document Database for MongoDB instance, historical space usage trends, analysis task records, and collection\-level space details, helping you identify space hotspots and assist with scaling, cleanup, and capacity planning.

<span id="FYeLuezy"></span>
## Prerequisites


* An instance and account for Document Database for MongoDB have been created, and the instance status is running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) and [Creating an account](https://docs.byteplus.com/en/docs/mongodb/create-account).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For details, see [Enable security control for Document Database for MongoDB instances](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control) and [Apply for Operation and maintenance permissions for Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket__).


<span id="Dc8Fhkfa"></span>
## Precautions


* While using the spatial analysis feature, do not modify the instance configuration, as this may prevent you from viewing the instance's spatial analysis information normally.

* Space analysis supports up to 10,000 collections, and a single database view displays up to 2,000 collections.

* In sharded instances, if the same collection is distributed across multiple shards, statistics are calculated per shard.

* The feature to predict the remaining available days of the current MongoDB database space is not yet available. Evaluate based on the current space overview and trend information.

* History retention duration, filterable time range, and failure retry rules for space analysis tasks.


<span id="FgFmC7G3"></span>
## Applicable scenarios


* Capacity planning and scaling decisions: Helps determine if the instance is about to run out of disk resources.

* Cluster health and balance check: In replica set or sharded cluster architectures, confirm that data synchronization and load are balanced across nodes.

* Anomalous growth investigation and auditing: Trace the cause when disk space grows unexpectedly.

* Granular storage governance: Conduct in\-depth analysis for specific businesses to identify large tables, redundant indexes, or fragmentation.


<span id="7CyO2pcv"></span>
## Advantages


* Multidimensional visual panoramic display: Overcomes the fragmentation limitations of traditional command\-line space viewing.

* Flexible task\-based analysis mechanism: Supports on\-demand triggering, balancing real\-time performance and system efficiency.

* Precise object\-level positioning: Extends from viewing instances to viewing collections and databases.

* Intuitive replica set status monitoring: Quickly verifies data consistency of replica sets.


<span id="deVqsSLg"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **Space usage**. On the Space usage tab, switch to the target instance.

   1. In the drop\-down list in the upper\-right corner of the page, select the target database type, which is **Document Database for MongoDB**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **Space usage ** tab, you can view the following information:

   
   <Tabs>
   <Tab zoneid="bsMMF4RqD6" title="View spatial profile">
   <TabTitle>View spatial profile</TabTitle>
   
   In the **Spatial profile** area, you can view the total usage and total quota of the current instance, helping you quickly assess the overall capacity.
   
   
   </Tab>
   <Tab zoneid="CjTDYqk6Nl" title="View capacity information">
   <TabTitle>View capacity information</TabTitle>
   
   In the capacity section, you can view the space usage of each node in a replica set or sharding cluster. By comparing the **Space usage** and **Space utilization** of each node, you can determine whether data distribution is even. If a node's utilization is significantly higher than others, you may need to check the shard key strategy or synchronization status.
   
   
   </Tab>
   <Tab zoneid="PS14fZuvFX" title="Create space analysis">
   <TabTitle>Create space analysis</TabTitle>
   
   1. On the **Space analysis** tab, in the **Space Analysis** section, click **Analyze Now**.
   
   2. In the **Create space usage task** dialog box, select the **Analysis scope** as needed:
   
      * Analyze all database collections: Select **All database collections**, click **OK**.
   
      * Analyze specified library: Select **Specified database collections**, select the target databases and collections as needed, and then click **OK**.
   
   
   You can select multiple databases for analysis at the same time. However, if you select multiple databases, filtering by collection is not supported, and all collections in those databases will be analyzed.
   
   
   </Tab>
   <Tab zoneid="VF8QwHllfT" title="View space analysis results">
   <TabTitle>View space analysis results</TabTitle>
   
   You can filter analysis tasks by generation time. By default, tasks from the last 1 day are displayed, and you can view historical records for up to the last 30 days.
   
   
   * View task list: Displays an overview of all analysis tasks, including task type, target object, creation time, completion time, state, and error message.
   
   * View task details: In the task list, click **View details** in the **Actions** column of the target task to go to the space analysis page. On this page, you can view the **Space overview**, **Capacity information (by node)** , and **Collection space** information of the specified space.
   
      The **Collection space** section provides a detailed analysis of the space usage of all collections across the entire database instance or within a specified database. This section helps you quickly identify large collections, collections with severe fragmentation, or potential optimization targets, enabling you to perform storage optimization, performance tuning, and resource planning. To ensure performance, the system imposes limits on the analysis scope:
   
      * Instance\-level analysis limit: Up to 10,000 collections can be analyzed per database instance.
   
      * Collection\-level analysis limit: Up to 2,000 collections can be displayed per database view.
   
      * In sharded instances, if the same collection is distributed across multiple shards, statistics are calculated per shard.
   
         In the left panel of the collection space section, click a database name to switch and view detailed collection space information for that database. You can also filter databases by entering the database name in the search box. The specific details displayed include:
   
         * **Collection space**: The total actual disk space occupied by this collection after compression. Collection space = Index space + Data space.
   
         * **Collection space proportion**: The proportion of this collection's space in the instance's used space.
   
         * **Index space**: The space occupied by all indexes of this collection.
   
         * **Data space**: The size of the logical data after compression.
   
         If the index space is significantly larger than the data space, there may be redundant indexes or an unreasonable index design.
   
         * **Reclaimable space**: Space that can be reused. When this value is large, it is recommended to perform a compact operation to release disk space.
   
         * **Expansion rate**: The ratio of logical size to disk space usage, reflecting the efficiency of data storage. A high expansion rate usually indicates a large amount of fragmentation or wasted space reserved due to frequent document updates.
   
         * **Fragmentation ratio**: The ratio of reclaimable space to data space, directly reflecting the degree of data file fragmentation. A high fragmentation ratio can severely impact data read performance.
   
         * **Average length**: The average number of bytes per document. It helps determine whether the document size meets expectations. An abnormal average length may indicate changes in the data structure.
   
   
   </Tab>
   </Tabs>
