---
title: "Modify collection configuration"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Modify_collection_configuration"
---

After creating a collection, you can modify its configuration based on your business requirements. This topic describes how to modify the configuration.

<span id="Blx9Irt1"></span>
## Prerequisites


* Created a Milvus for VectorDB instance and completed authorization. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance) and [Authorize to use an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Authorize_to_use_an_instance).

* A collection is created. For information about how to create a collection, see [Create a collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_database).


<span id="p4SssXrO"></span>
## Precautions

External collections do not support configuration modifications.

<span id="YgggmTVZ"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, choose the **Dedicated**, **Serverless**, or **On\-Demand** tab, select the authorized instance, then click **view**.

5. On the **Collections** page, click the target database, select the target collection, click the **Property** tab, and then click **Modify configuration**.

6. Set the running values of the following parameters based on your business requirements, then click **Submit**.

   
   |Parameter |Description |Value range |
   |---|---|---|
   |collection.autocompaction.enabled |Automatic compression switch configuration at the Collection level allows independent control of enabling or disabling the automatic compression function for a single Collection. |* true<br><br>* false |
   |collection.bulkLoadRate.max.mb |Controls the maximum bulk load data rate at the Collection level, measured in MB/s. Prevents a single Collection's bulk load operations from consuming excessive system resources. |0~2147483647 |
   |collection.bulkLoadRate.min.mb |Provides a minimum batch loading data rate guarantee at the collection level. Unit: MB/s. This parameter is used to ensure that a specific collection receives a minimum batch loading bandwidth. |0~2147483647 |
   |collection.deleteRate.max.mb |Controls the maximum data deletion rate at the Collection level, measured in MB/s. Prevents a single collection's delete actions from consuming excessive system resources |0~2147483647 |
   |collection.deleteRate.min.mb |Provide a minimum data deletion rate guarantee at the Collection level, measured in MB/s. Ensure that a specific Collection receives a minimum guaranteed deletion bandwidth. |0~2147483647 |
   |collection.diskProtection.diskQuota.mb |Controls the disk usage quota at the collection level. Unit: MB. This parameter is used to prevent a collection from occupying too much disk space. |0~2147483647 |
   |collection.insertRate.max.mb |Control the maximum insertion data rate at the Collection level, measured in MB/s. Used to prevent a single Collection's insertion operations from consuming excessive system resources. |0~2147483647 |
   |collection.insertRate.min.mb |Provides minimum insertion data rate guarantee at the collection level. Unit: MB/s. This parameter is used to ensure that a specific collection receives a minimum insertion bandwidth. |0~2147483647 |
   |collection.queryRate.max.qps |Controls the maximum query data rate at the Collection level, measured in QPS (Queries Per Second). Prevents a single Collection's query operations from consuming excessive system resources. |0~2147483647 |
   |collection.queryRate.min.qps |Provide a minimum query data rate guarantee at the Collection level, measured in QPS. Ensure that a specific Collection receives a minimum guaranteed query bandwidth. |0~2147483647 |
   |collection.replica.number |Specifies the number of replicas of the collection on query nodes. The default value is **1**, which means a single replica.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter only applies to Dedicated capacity instances.</div><br> |1~2147483647 |
   |collection.resource_groups |Specifies the list of resource groups a collection can use to control resource allocation and isolation for the collection's query nodes Presented as a comma\-separated list |\- |
   |collection.searchRate.max.vps |Control the maximum vector search rate at the Collection level, measured in VPS (Vectors Per Second). Used to prevent a single Collection's search operations from consuming excessive system resources. |0~2147483647 |
   |collection.searchRate.min.vps |Provide a minimum guaranteed vector search rate at the Collection level, measured in QPS (Queries Per Second). Ensure that a specific Collection receives a minimum guaranteed query bandwidth. |0~2147483647 |
   |collection.ttl.seconds |TTL (Time to Live) configuration property at the Collection level, used to set the expiration time for data in the Collection. Expired data will no longer be queried or searched and will be cleaned up by the garbage collection mechanism. If not configured in the Collection properties, the `common.entityExpiration` configuration applies. |\-1~2147483647 |
   |collection.upsertRate.max.mb |Controls the maximum update data rate at the collection level. Unit: MB/s. This parameter is used to prevent update operations of a single collection from consuming excessive system resources.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter applies only to version 2.5 instances.</div><br> |0~2147483647 |
   |collection.upsertRate.min.mb |Provide a minimum update data rate guarantee at the Collection level, measured in MB/s. Ensure that a specific Collection receives a minimum guaranteed update bandwidth.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter applies only to version 2.5 instances.</div><br> |0~2147483647 |
   |lazyload.enabled |Enables or disables delayed data loading.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter applies only to Dedicated edition instances.</div><br> |* true<br><br>* false |
   |mmap.enabled |Enables Mmap, which allows direct memory access to large files on disk, enabling Milvus to store indexes and data in both memory and disk.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter only applies to Dedicated capacity instances.</div><br> |* true<br><br>* false |
   |partition.diskProtection.diskQuota.mb |Controls the disk usage quota at the Partition level, measured in MB. Prevents a single Partition from occupying excessive disk space. |0~2147483647 |
   |partitionkey.isolation |Enable partition key isolation. When partition key isolation is enabled, Milvus groups entities by partition key values and creates separate indexes for each group. When receiving a search request, the system locates the corresponding index based on the partition key value specified in the filter criteria, limiting the search scope to the entities within that index. This avoids scanning unrelated entities and significantly improves search performance. |* true<br><br>* false |
