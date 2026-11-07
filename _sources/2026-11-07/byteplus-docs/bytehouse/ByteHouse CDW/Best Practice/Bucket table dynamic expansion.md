---
title: "Bucket table dynamic expansion"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bucket-table-dynamic-expansion"
---

ByteHouse added support project for dynamic expansion of bucket tables, allowing dynamic adjustment of the total number of buckets in bucketed tables, including unique key tables.

<span id="025f4863"></span>
# Caution

This feature is currently undergoing a gradual rollout (gray release). If you encounter any issues during use, please submit a support ticket or contact the ByteHouse team.

<span id="6dda7b87"></span>
# Function overview

Dynamic expansion of bucket tables means you can adjust the number or distribution of buckets according to changes in the data volume or load in the data table. When data continuously grows or query load increases in bucket tables, the original number of buckets may not efficiently handle the data, affecting query performance. The dynamic expansion feature of bucket tables addresses this by adjusting the number or distribution of buckets to optimize load balancing and lift query parallelism.

ByteHouse's dynamic expansion of bucket tables is implemented via settings parameters. Currently, ByteHouse supports the following settings parameters. This article explains how to use these settings parameters with specific scenarios.


|Settings Parameters |Description |
|---|---|
|enable_recluster_multiple_parts |Table settings. After this parameter is enabled, it can reduce the number of output parts post\-bucketing, enhancing query performance. The default value is 0 (disable), and it can be set to 1 (enable). |
|enable_scale_bucket_optimization |Table settings. After this parameter is enabled, it supports using a new bucket key expression for select queries. This feature also applies to scenarios where the total number of buckets in different parts varies due to adjustments in the number of buckets. If not enabled, the old bucket keys will still be used during the query, prohibiting the use of the new bucket key expressions. The default value is 0 (disable), which can be set to 1 (enable). |
|force_modify_unique_table_cluster_by |Query settings. It is used to modify the `cluster by` statements in tables with unique keys. The default value is 0 (disable), which can be set to 1 (enable). |
|enable_legacy_cluster_by |Query settings. When enabled, it supports modifying bucket definitions using the new bucket key expressions (`CLUSTER BY expression`) and old bucket key syntax (`CLUSTER BY <column_name>`). The default value is 1 (Activate). Setting this value to 0 (Terminated) will only support creating bucket tables and modifying bucket quantity with the new bucket key expressions. |


<span id="8a260117"></span>
# Scene 1: Convert a non\-bucketed table to a bucketed table

<span id="f6fce81a"></span>
## Steps


1. Use the `ALTER TABLE` command to add a bucketing expression.

   ```SQL
   ALTER TABLE t MODIFY CLUSTER BY EXPRESSION cityHash64V2(x + y) INTO 4 BUCKETS SETTINGS enable_legacy_cluster_by=1 [, force_modify_unique_table_cluster_by=1]
   
   ALTER TABLE t MODIFY SETTINGS enable_recluster_multiple_parts=1
   ```
   

   Parameter description as follows:

   
   |Param |Required |Description |
   |---|---|---|
   |`ALTER TABLE t` |Yes |Specifies the table name to be adjusted. |
   |`MODIFY CLUSTER BY EXPRESSION cityHash64V2(x + y)` |Yes |Uses an expression to define a bucketing key. To achieve better performance, it is recommended to use `cityHash64V2` to wrap the expression. Of which x, y are column names, x + y represents column name concatenation. |
   |`INTO 4 BUCKETS` |Yes |Define the number of buckets. |
   |`SETTINGS` |Yes |Configuration parameters. Use settings parameters to perform operations related to dynamic expansion of bucketed tables. |
   

2. Execute any of the following commands as needed to perform the rebucketing operation, applying the new bucketing key to existing data. The rebucketing task will run asynchronously.

   * Specify a particular partition

      Replace the "2025\-04\-14" in the command with the actual partition key you set.

      ```SQL
      ALTER TABLE t RECLUSTER PARTITION '2025-04-14'  
      ```
      

   * Specify all partitions

      ```SQL
      ALTER TABLE t RECLUSTER PARTITION WHERE 1=1  
      ```
      

   * Specify the partition that meets the conditions

      ```SQL
      ALTER TABLE t RECLUSTER PARTITION WHERE ...  
      ```
      

   You can check the task status with the following command.

   ```SQL
   SELECT * FROM system.mutations WHERE database='...' and table = '...'
   ```
   

3. Change the table settings, so subsequent select queries will support the use of the new bucket key expression.

   ```SQL
   ALTER TABLE t MODIFY SETTINGS enable_scale_bucket_optimization=1
   ```
   


<span id="5a2551a8"></span>
# Scenario 2: Expand existing number of buckets

<span id="a8d5c232"></span>
## Precautions

After expanding the bucketing, the existing data in the table will not move or be rebucketed, but this will not affect normal usage. If you want to further optimize the existing data, you can continue to execute the command from Step 2 to rebucket the existing data.

<span id="3b0ea370"></span>
## Steps


1. Modify the number of buckets. The new number of buckets must be a multiple of the previous number set.

   For instance, assume the initial bucket count was 4; executing this command will store new data into 8 buckets.

   ```SQL
   ALTER TABLE t MODIFY SETTING enable_recluster_multiple_parts=1, enable_scale_bucket_optimization=1 -- This command only needs to be executed once per table
   ALTER TABLE t MODIFY BUCKET NUMBER 8
   ```
   

2. (Optional) Perform the following command as needed to rerun the bucketing process and apply the new bucketing definition to the existing data. Rebucketing tasks will run asynchronously.

   * Specify a partition

      Replace the "2025\-04\-14" with the actual partition key you set.

      ```SQL
      ALTER TABLE t RECLUSTER PARTITION '2025-04-14'  
      ```
      

   * Specify all partitions

      ```SQL
      ALTER TABLE t RECLUSTER PARTITION WHERE 1=1  
      ```
      

   * Specify the partitions that meet the condition

      ```SQL
      ALTER TABLE t RECLUSTER PARTITION WHERE ...  
      ```
      

   You can check the task status with the following command.

   ```SQL
   SELECT * FROM system.mutations WHERE database='...' and table = '...'
   ```
   


<span id="b94d3e61"></span>
# Scenes 3: Modify the bucketing key.

<span id="8ffe04aa"></span>
## Caution

After modifying the bucketing key, the bucketing keys used by the stock data and newly inserted data in the table differ, causing the engine to be unable to use the new bucketing key expression to perform optimized query operations, thus, it is not advised to change the bucketing key. But if your business scenario necessitates changing the bucketing key, it is suggested that you follow step 2 after making the change to trigger re\-bucketing of stock data.

<span id="ce28d9f9"></span>
## Steps


1. Modify the bucketing key.

   ```SQL
   ALTER TABLE t MODIFY CLUSTER BY EXPRESSION cityHash64V2(x - y) INTO 4 BUCKETS settings enable_legacy_cluster_by=1 [, force_modify_unique_table_cluster_by=1]
   ```
   

2. Execute any of the following commands as needed to re\-bucket, applying the new bucket keys to existing data. The re\-bucketing task will run asynchronously.

   * Specify a partition

      Change the date "2025\-04\-14" in the command to the actual partition key that you have set.

      ```SQL
      ALTER TABLE t RECLUSTER PARTITION '2025-04-14'  
      ```
      

   * Specify all partitions

      ```SQL
      ALTER TABLE t RECLUSTER PARTITION WHERE 1=1  
      ```
      

   * Specify only the partitions that meet theconditions

      ```SQL
      ALTER TABLE t RECLUSTER PARTITION WHERE ...  
      ```
      

   You can check the task status by the following command to confirm if the re\-bucketing task has been completed.

   ```SQL
   SELECT * FROM system.mutations WHERE database='...' and table = '...'
   ```
   


<span id="255eaa4e"></span>
# FAQ

<span id="3a49e388"></span>
## How should memory usage or sudden OOM issues be handled after performing re\-bucketing actions?

Reduce the number of `max_addition_mutation_task_num` in the table.

<span id="4e88b9ce"></span>
## How to handle a core dump caused by rebucketing operations?

Set `max_addition_mutation_task_num=0` in the table definition.

<span id="59c89da6"></span>
# Related Documents


* For how to create a bucket table, please refer to [Create dynamic partitioned tables](https://docs.byteplus.com/docs/bytehouse/create-statement#b9a1a39f).

* If you want to use bucket to realize deduplication optimization for a unique key table, please refer to [Bucket deduplication optimizations](https://docs.byteplus.com/docs/bytehouse/bytehouse-best-practice-for-unique-key-tables#a8c5dffd).
