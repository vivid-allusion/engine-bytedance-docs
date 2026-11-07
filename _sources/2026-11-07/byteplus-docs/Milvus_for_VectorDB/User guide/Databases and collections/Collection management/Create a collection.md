---
title: "Create a collection"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection"
---

This topic describes how to create a collection in the database using the collection management feature of Milvus for VectorDB.

## Prerequisites

* Created a Milvus for VectorDB instance and completed authorization. For specific steps, refer to [Create Instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance) and [Authorize instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Authorize_to_use_an_instance).

* Database created. For specific steps, refer to [Create a database](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_database).

## Procedure

**Serverless instances**

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, select the **Dedicated** or **Serverless** tab, choose an authorized instance, then click **View**.

5. On the **Collections** page, click  **+** , then select **Create collection**

6. On the **Create collection** page, configure the following parameters, then click **Submit**

   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Database name |Select the database where the collection will be created from the dropdown list.<br><br>> **tip**<br><br><br>> For Serverless instances, the database name is fixed as the system default database and cannot be changed.<br> |
   |Collection Name |Enter the name of the collection. Naming rules are as follows:<br><br><br>* Cannot start with a number or underscore (_).<br><br>* The length must be between 1 and 64 characters.<br><br>* Can only contain letters, digits, and underscores (_). |
   |Remarks (optional) |Enter remarks for the collection. Supports up to 255 characters. |
   |**Schema** ||
   |Fields |Configure fields in the schema, which by default includes a primary key and one vector field. You can also click **Add field** to add vector or scalar fields. For details, see [Field description](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection#q9lVIZFL). |
   |Dynamic field |When turned on, all fields and their values not defined in the schema will be stored as key\-value pairs in the dynamic field. |
   |**Advanced configurations** ||
   |Function |Set the Function at the field level to enable full text search, create sparse vector indexes, and improve text search performance. Both VarChar and SparseFloatVector field types are required for configuration. You can click **Add Function configuration** to add multiple configurations. Configuration includes the following fields:<br><br><br>* Enter a field: select VarChar as the field type from the dropdown list.<br><br>   > **tip**<br>   <br><br>   > VarChar type requires a tokenizer to be enabled and cannot be empty.<br>   <br><br>* Function type: select Function type from the dropdown list.<br><br>* Output fields: select SparseFloatVector as the field type from the dropdown list. |
   |Partition Key |Select whether to set the scalar field as the Partition Key, which improves query performance in large\-scale multi\-tenant scenarios. Partition Key must be Int64 or VarChar type and cannot be empty. |
   |Partition Num |Set the number of partitions. Milvus for VectorDB will create the specified number of partitions within this collection. After receiving the inserted data, Milvus for VectorDB calculates a hash value using the partition key of the data, then performs a modulo operation based on the hash value and the collection’s `partitions_num` property to determine the target partition ID, finally storing the data in the target partition.<br><br>> **tip**<br><br><br>> This parameter is visible only when **Partition Key** is enabled.<br> |
   |Shard Num |Set the number of shards. The recommended number of shards depends on the expected write volume and concurrency level. A general reference standard is 1 shard per 100 million expected rows of data. Increasing the number of shards may improve data ingestion speed but will also increase resource consumption. |
   |Consistency configuration |Configure consistency options:<br><br><br>* Strong: read operations always return the latest data, ensuring all replicas synchronize immediately after writing; highest consistency but lower performance. Guarantees absolutely up\-to\-date data but may reduce performance. Suitable for scenarios requiring precise data like financial transactions and banking systems.<br><br>* Session: the same client always reads its latest write during the session, ensuring consistency; different sessions may read old data. Suitable for single\-user operations, such as personal account management and web applications.<br><br>* Bounded: allows short data delays but guarantees eventual synchronization. Suitable for low\-latency scenarios that allow brief data inconsistencies. Examples include social media feeds, leaderboards, and recommendation systems.<br><br>* Eventually: allows reading old data but eventually achieves consistency. Suitable for data synchronization in non\-critical systems like logging and caching. |
   |TTL |Automatically expire and delete data from the collection in Milvus for VectorDB after a specified time. |

**Dedicated or On-Demand instance**

Supports the following two types of collections:

* Managed Collection: data storage managed by the platform. Supported by Dedicated edition and On\-Demand edition instances.

* External Collection: uses external data storage. Supported by Dedicated 3.0 edition instances and On\-Demand edition instances.

   > **tip**

   > Milvus 3.0 version instances currently require whitelist access. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000255) for approval.</a\>

### Create Managed Collection

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, select the **Dedicated** or **On\-Demand** tab, choose an authorized instance, then click **view**.

5. On the **Collections** page, click  **+** , then select **Create collection**

6. On the **Create collection** page, configure the following parameters, then click **Submit**

   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Database name |Select the database where the collection will be created from the dropdown list.<br><br>> **tip**<br><br><br>> For On\-Demand edition instances, the database name is fixed as the system default database and cannot be changed.<br> |
   |Collection Name |Enter the name of the collection. Naming rules are as follows:<br><br><br>* Cannot start with a number or underscore (_).<br><br>* The length must be between 1 and 64 characters.<br><br>* Can only contain letters, digits, and underscores (_). |
   |Remarks (optional) |Enter remarks for the collection. Supports up to 255 characters. |
   |**Schema** ||
   |Fields |Configure fields in the schema, which by default includes a primary key and one vector field. You can also click **Add field** to add vector or scalar fields. For details, see [Field description](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection#q9lVIZFL). |
   |Dynamic field |When turned on, all fields and their values not defined in the schema will be stored as key\-value pairs in the dynamic field. |
   |**Advanced configurations** ||
   |Function |Set the Function at the field level to enable full text search, create sparse vector indexes, and improve text search performance. Both VarChar and SparseFloatVector field types are required for configuration.<br><br><br>* Enter a field: select VarChar field type.<br><br>   > **tip**<br>   <br><br>   > VarChar type requires a tokenizer to be enabled and cannot be empty.<br>   <br><br>* Function type: select Function type from the dropdown list.<br><br>* Output fields<br><br>   * When the **Function type** is set to **BM25**, select **SpareFloatVector**.<br><br>   * When the **Function type** is set to **TextEmbedding**, select the added embedding model, then choose fields that are not SpareFloatVector.<br><br>      > **tip**<br>      <br><br>      * > Before setting the **Function type** to **TextEmbedding**, configure embedding for the instance; otherwise, the system will report an error. For detailed steps, see [Configure Embedding](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/configure-embedding).<br>      <br><br>      * > Refer to [Embedding model management](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/embedding-model-management) for operations on adding Embedding models.<br>      <br><br>   * When the **Function type** is set to **MinHash**, select **Binary Vector**.<br><br><br>You can click **Add function configuration** to add multiple configurations. |
   |Partition Key |Select whether to set the scalar field as the Partition Key, which improves query performance in large\-scale multi\-tenant scenarios. Partition Key must be Int64 or VarChar type and cannot be empty. |
   |Partition Num |Set the number of partitions. Milvus for VectorDB will create the specified number of partitions within this collection. After receiving the inserted data, Milvus for VectorDB calculates a hash value using the partition key of the data, then performs a modulo operation based on the hash value and the collection’s `partitions_num` property to determine the target partition ID, finally storing the data in the target partition.<br><br>> **tip**<br><br><br>> This parameter is visible only when **Partition Key** is enabled.<br> |
   |Shard Num |Set the number of shards. The recommended number of shards depends on the expected write volume and concurrency level. A general reference standard is 1 shard per 100 million expected rows of data. Increasing the number of shards may improve data ingestion speed but will also increase resource consumption. |
   |Consistency configuration |Configure consistency options:<br><br><br>* Strong: read operations always return the latest data, ensuring all replicas synchronize immediately after writing; highest consistency but lower performance. Guarantees absolutely up\-to\-date data but may reduce performance. Suitable for scenarios requiring precise data like financial transactions and banking systems.<br><br>* Session: the same client always reads its latest write during the session, ensuring consistency; different sessions may read old data. Suitable for single\-user operations, such as personal account management and web applications.<br><br>* Bounded: allows short data delays but guarantees eventual synchronization. Suitable for low\-latency scenarios that allow brief data inconsistencies. Examples include social media feeds, leaderboards, and recommendation systems.<br><br>* Eventually: allows reading old data but eventually achieves consistency. Suitable for data synchronization in non\-critical systems like logging and caching. |
   |Time zone configuration |Define the time zone for all **Timestamptz** fields in this collection.<br><br>> **tip**<br><br><br>> This parameter is supported only in version 2.6 instances and later.<br> |
   |TTL |Automatically expire and delete data from the collection in Milvus for VectorDB after a specified time. |
   |Allow Auto ID insert |When enabled, users can provide primary key values during Insert, Upsert, and Bulk Insert even if the collection uses Auto ID as the primary key.<br><br>> **tip**<br><br><br>> This parameter is supported only in version 2.6 instances and later.<br> |

### Create External Collection

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, select the **On\-Demand edition** tab, choose the authorized instance, then click **view**.

5. On the **Collections** page, click  **+** , then select **External Collection**.

6. On the **Create External Collection** page, configure the following parameters, then click **submit**.

   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Database name |Select the database where the collection will be created from the dropdown list.<br><br>> **tip**<br><br><br>> For On\-Demand edition instances, the database name is fixed as the system default database and cannot be changed.<br> |
   |Collection Name |Enter the name of the collection. Naming rules are as follows:<br><br><br>* Cannot start with a number or underscore (_).<br><br>* The length must be between 1 and 64 characters.<br><br>* Can only contain letters, digits, and underscores (_). |
   |Remarks (optional) |Enter remarks for the collection. Supports up to 255 characters. |
   |**External information source** ||
   |External integration |Select the integration created in the Integration center from the dropdown list. For details, see [Create integration](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_integration). |
   |Path prefix |Select the directory where the external data files are stored from the dropdown list. |
   |Format |Select the storage format of external data files from the dropdown list. Currently supported: **Parquet**. |
   |refresh immediately after creation (optional) |Set whether to automatically refresh the external information source after the collection is created. |
   |**Schema** ||
   |Fields |Configure fields in the Schema, which by default displays one scalar field `id` (non\-primary key) and one vector field. You can also click **Add field** to add vector or scalar fields. For details, see [Field description](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection#q9lVIZFL).<br><br>> **warning**<br><br><br>> Fill in the vector dimension according to the actual dimension of the external field. If inconsistent, it will cause subsequent query failure.<br> |
   |Dynamic field |When turned on, all fields and their values not defined in the schema will be stored as key\-value pairs in the dynamic field. |
   |**Advanced configurations** ||
   |Consistency configuration |Configure consistency options:<br><br><br>* Strong: read operations always return the latest data, ensuring all replicas synchronize immediately after writing; highest consistency but lower performance. Guarantees absolutely up\-to\-date data but may reduce performance. Suitable for scenarios requiring precise data like financial transactions and banking systems.<br><br>* Session: the same client always reads its latest write during the session, ensuring consistency; different sessions may read old data. Suitable for single\-user operations, such as personal account management and web applications.<br><br>* Bounded: allows short data delays but guarantees eventual synchronization. Suitable for low\-latency scenarios that allow brief data inconsistencies. Examples include social media feeds, leaderboards, and recommendation systems.<br><br>* Eventually: allows reading old data but eventually achieves consistency. Suitable for data synchronization in non\-critical systems like logging and caching. |
   |Time zone configuration |Define the time zone for all **TIMESTAMPTZ** fields in this collection.<br><br>> **tip**<br><br><br>> This parameter is only supported in version 2.6 instances.<br> |

## Field description

The following table summarizes the field details supported in the Collection Schema of Milvus for VectorDB.

|Field name |Field type |Field configuration |Index type |Actions |
|---|---|---|---|---|
|Primary key: enter the primary key field. You can check **Auto ID** to assign the primary key automatically. |Select primary key field type:<br><br><br>* Int64<br><br>* VarChar |When the **Field type** is set to **VarChar**, specify the field's maximum length. |\- |Click the gear icon to add a field description.<br><br>The primary key cannot be deleted. |
|Vector: enter the vector name. |Select vector field type:<br><br><br>* FloatVector<br><br>* BinaryVector<br><br>* Float16Vector<br><br>* BFloat16Vector<br><br>* SparseFloatVector<br><br>* Int8Vector (supported only by version 2.6 instances) |Set vector dimension and select metric type:<br><br><br>* L2<br><br>* IP<br><br>* COSINE |Click  **+**  to add an index type:<br><br><br>* AUTOINDEX<br><br>* FLAT<br><br>* IVF_FLAT<br><br>* IVF_SQ8<br><br>* IVF_PQ<br><br>* HNSW<br><br>* HNSW_SQ<br><br>* HNSW_PQ<br><br>* HNSW_PRQ<br><br>* SCANN<br><br>* DISKANN_RABITQ (supported only by capacity instances)<br><br>* DISKANN_PQ (supported only by capacity instances)<br><br>* DISKANN (supported only by capacity instances)<br><br>* GPU_CAGRA (supported only by GPU and hybrid instances)<br><br>* GPU_IVF_FLAT (supported only by GPU instances)<br><br>* GPU_IVF_PQ (supported only by GPU instances)<br><br>* GPU_BRUTE_FORCE (supported only by GPU instances)<br><br>* GPU_IVF_PQ (supported only by GPU instances) |You can click the gear icon to add field descriptions.<br><br>Default vector fields cannot be deleted. |
|Scalar: enter the scalar name. |Select vector field type:<br><br><br>* VarChar<br><br>* Int8<br><br>* Int16<br><br>* Int32<br><br>* Int64<br><br>* Float<br><br>* Double<br><br>* Bool<br><br>* JSON<br><br>* Timestampz (supported only in version 2.6 instances and later)<br><br>* Array |* When the **Field type** is set to **VarChar**, specify the field's maximum length.<br><br>* When the **Field type** is set to **Array**, specify the field's maximum capacity. |Click  **+**  to add an index type:<br><br><br>* AUTOINDEX<br><br>* TRIE<br><br>* BITMAP<br><br>* INVERTED |You can click the gear icon to set whether it can be null, set the default value, and add field description.<br><br>You can click the delete icon to delete the scalar field. |
