---
title: "Load and release a collection"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Load_and_release_a_collection"
---

In Milvus for VectorDB, loading and releasing a collection are key operations for managing system memory resources. You can load the collection's vector data and indices from disk into memory, enabling high\-performance vector queries and hybrid searches. Conversely, the release operation removes this data from memory to reclaim resources and improve overall system efficiency. By properly loading and releasing collections, you can achieve an optimal balance between query performance and resource usage. This topic describes how to load and release a collection.

<span id="WGDSYk8z"></span>
## Prerequisites


* Created a Milvus for VectorDB instance and completed authorization. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance) and [Authorize to use an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Authorize_to_use_an_instance).

* Collection has been created. For specific steps, refer to [Create collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection).

* When loading a collection, the collection must be in the **Not loaded** status. When releasing a collection, the collection must be in the **Loaded** status. A collection is loaded by default after creation.


<span id="j8rl4ZV0"></span>
## Precautions

Only Dedicated instances and Serverless instances support loading and releasing collections.

<span id="bee35m0y"></span>
## Load collection


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, select the **Dedicated** or **Serverless** tab, choose the Completed authorized Instance, then click **View**.

5. On the **Collections** page, expand the database containing the target Collection, then click  **...**  on the right of the target Collection. **Load**.

6. In the **Load collection** dialog, configure the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Whether to enable memory replica |Whether to keep a complete data replica of the Collection in memory. Enabling this improves query performance but uses more memory resources. |
   |Replicas |Enter the number of Collection replicas. |
   


<span id="gHH5aoW2"></span>
## Release a collection


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, select the **Dedicated** or **Serverless** tab, choose the Completed authorized Instance, then click **View**.

5. On the **Collections** page, expand the database containing the target Collection, then click  **... \> Release** on the right of the target Collection.

6. In the **Release collection** dialog, click **OK.**
