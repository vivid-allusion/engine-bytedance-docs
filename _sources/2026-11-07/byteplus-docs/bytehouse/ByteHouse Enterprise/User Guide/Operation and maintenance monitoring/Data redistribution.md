---
title: "Data redistribution"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/data-redistribution"
---

Data Redistribution (Resharding) refers to splitting each table of the MergeTree family according to the sharding key to each shard, making the data on each node of the cluster more balanced and providing more balanced performance for queries.

<span id="c382e7c4"></span>
# Background information

The schematic of data redistribution is as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f579f35dc76436c849c434633afaa59~tplv-goo7wpa0wc-image.image) </span>

<span id="d9c177dd"></span>
## Applicable scenarios


* Scenarios where horizontal expansion has just been carried out but data has not been redistributed, or some partitions of the table have not been redistributed;

* Scenarios where data is uneven due to direct inserts into the local table or upstream partition quantity not configured according to best practices when importing using Kafka (not applicable to cases where the incorrect setting of the Sharding Key causes data imbalance);


<span id="aa53d484"></span>
## Non\-applicable scenarios


* Incomplete tables scenario: If users do not create tables according to best practices (e.g., some tables only exist on some nodes), these data will not be redistributed.

* Special Data Types: Tables containing Bitmap64 type cannot be redistributed.

* Special Table Engines: MySQL, S3 and other external table engines, View, Merge, Join and other no\-data storage table engines do not support redistribution.

* Materialized Table Engines: MaterializedView, MaterializeMySQL do not currently support data redistribution, but you can resync data by rebuilding the database/table after expansion.


<span id="318062b9"></span>
# Cautions


* Each old node needs to reserve storage capacity equal to the largest table's capacity. For example, if the total size of the table is 100GB and there are currently 10 nodes, and if reducing to 5 nodes, then more than 100GB/5 = 20GB of storage needs to be reserved at each old node.

* During data redistribution, each table will sequentially enter a read\-only state, and meanwhile, the cluster's computational and IO load will be higher. The read performance is estimated to decrease and be unstable.

* When there is existing data in the HaUniqueMergeTree table, in order to ensure the consistency of deduplication, the topology of the table before and after expansion will not change. That is, if 2 shards are used before expansion, 2 shards will still be used after expansion. However, in order to make the most of the cluster resources, it is strongly recommended that you promptly redistribute the HaUniqueMergeTree table with existing data after the expansion is completed. After redistribution, the topology of the table will be consistent with the cluster topology.

* Special case: The HaUniqueMergeTree table engine can only deduplicate within a single shard. Thus, if using Kafka for import, the mapping relationship between Kafka Partition \-\> ByteHouse Shard needs to remain unchanged. For example:

   * After expansion: unique_key = 1 \-\> original Kafka partition 1 \-\> original ByteHouse shard 1

   * After expansion: unique_key = 1 \-\> ByteHouse shard 3, then you need to adjust unique_key = 1 \-\> new Partition, to ensure stable writing into ByteHouse shard 3.

   * If you have any related questions, please submit a ticket.


<span id="5e5d09ab"></span>
# Steps

You can refer to the following steps to complete the redistribution operation, which requires cluster administrator or system administrator permission during the operation.


1. After logging in and entering the ByteHouse CE Console, click **Manage clusters** at the top, in the **Actions** column of the cluster list, click **Show more** \> **Redistribute**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8dbe50874c94f9bb21caba12d1bd636~tplv-goo7wpa0wc-image.image) </span>

2. Select the tables to redistribute in the popup sidebar.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/559415622dea4f78abc5994629055d3a~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration Description |
   |---|---|
   |Select Redistribution Method |Currently supported redistribution methods include: complete redistribution, minimum redistribution, and customized redistribution.<br><br><br>* All Redistribution: Redistributes all partitions of the table, improving the read performance of existing data, but an excessive amount of data can cause the table to be unwritable for an extended period.<br><br>* Minimum Redistribution: Only redistributes the active partitions of the HaUniqueMergeTree table (partitions with data written within 72 hours), significantly shortening the time the table is unwritable.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If after performing minimal redistribution, there are still data writes to partitions outside those with data written within 72 hours, data deduplication can't occur. It is advisable to redistribute potential data\-writing history partitions sooner.   </div><br>   <br><br>* Custom Redistribution: Customizes the redistribution of tables and specific partitions as needed, suitable for scenarios requiring flexible configuration.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you customize the distribution for a unique table, it is advisable to select active partitions for redistribution first, otherwise it may cause the logic for de\-duplicating new data entries to fail.   </div><br>    |
   |Select Redistribution Scope |You can choose to redistribute all tables or manually select some tables to redistribute.<br><br><br>* Different redistribution methods support different selectable redistribution scopes:<br><br>   * **All Redistribution**: By default, it selects all tables for redistribution, but also supports manually switching to the **Part of Tables** tab to choose some tables for redistribution.<br><br>   * **Min Redistribution**: Only supports redistributing active partitions of all HaUniqueMergeTree tables.<br><br>   * **Custom Redistribution**:<br><br>      * By default, it selects all tables for redistribution, with settings to choose the **redistribution scope** of tables (all tables, active partitions, specified partitions, time limit), and support for batch settings of partitions.<br><br>      * It also supports manually switching to the **Part of Tables** tab to select some tables for redistribution and setting the **redistribution scope** for selected tables (all tables, active partitions, specified partitions, time limit), with partitions supporting batch settings.<br><br>* If after selecting the scope of tables for redistribution, the page reminds you that there are tables which do not support the redistribution action, you can click **View Details** to see the list of tables that do not support redistribution and the reasons. You can refer to these reasons to repair the tables, and after fixing, redistribute them again. |
   

3. Start redistribution.

   * The system will split the data to all nodes based on the Sharding_key; each table will enter read\-only mode meanwhile the cluster's compute and IO load will be higher, the estimated read performance will decrease and become unstable.

   * Once the HaUnique table is redistributed, the topology will automatically join the expansion nodes, and new data written will be distributed according to the new topology.


<span id="bb863173"></span>
# Subsequent steps


1. You can view the currently submitted redistribution tasks and check the redistribution status on the Task center \> **Maintenance center** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abb4b02c903a43ada6436f16102960b9~tplv-goo7wpa0wc-image.image) </span>

2. For tasks that fail to redistribute, you can click on **redistribution details** to view the tables and reasons for the failure on the redistribution details page that appears. Make modifications according to the interface prompts and then resubmit the redistribution task.
