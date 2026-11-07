---
title: "Practical implementation of large-scale vector retrieval with the Milvus for VectorDB Python client and DiskANN"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Milvus_for_VectorDB_Python_client_and_DiskANN_practice"
---

With the rapid development of applications such as generative AI, recommendation systems, and semantic search, vector data volume continues to grow. Traditional retrieval methods based on keywords or structured indexes struggle to meet the similarity search needs of high\-dimensional vector data. Milvus for VectorDB, as a high\-performance vector database, provides storage and approximate nearest neighbor (ANN) search capabilities for massive vector data. DiskANN uses a disk\-based index structure to significantly reduce memory consumption while maintaining high query efficiency, enabling vector retrieval on billion\-scale data.

This article introduces how to build a large\-scale vector retrieval system by combining Milvus for VectorDB Python client with DiskANN indexes.

<span id="mqg9zH4G"></span>
## Prerequisites


* A Milvus for VectorDB instance has been created; obtain the instance’s private network address and enable public resolution for the private network address. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance) and [View instance information](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_instance_information).

* PyMilvus SDK has been installed or upgraded. The current Milvus for VectorDB instance is based on kernel version 2.5. It is recommended to use SDK version 2.5 as well to ensure compatibility. The command example is as follows.

   ```Bash
   # Install a specified version of the PyMilvus SDK, e.g., 2.5.18
   pip install pymilvus==2.5.18
   
   # Upgrade the PyMilvus SDK to the latest version
   pip install --upgrade pymilvus
   
   # Verify the installation was successful
   python -m pip list | grep pymilvus
   ```
   

* The Python\-based client has been initialized. The example code is as follows.

   ```Python
   from pymilvus import MilvusClient, DataType
   
   #1. Access the client using the admin user.
   client = MilvusClient(
       uri="http://xxxxxx.milvus.ivolces.com:19530", Obtain the instance's private network address.
       token="admin:<password>",  <password> is the password for the admin user.
   )
   
   2. Access the client with a non-admin user.
   client = MilvusClient(
       uri="http://xxxxxx.milvus.ivolces.com:19530", Obtain the instance's private network address.
       token="<user>:<password>",  Username and password.
   )
   ```
   


<span id="kQ12qDs8"></span>
## Database management

The common code for database management is as follows.

```Python
# Create a database
client.create_database(
    db_name="my_database_2"
)

# query database
databases = client.list_databases()

# delete database
client.drop_database(
    db_name="my_database_2"
)
```


For more database properties, see [Manage database properties](https://milvus.io/docs/zh/manage_databases.md#Manage-database-properties).

<span id="qY3I8Rdf"></span>
## Collection management

The common code for collection management is as follows.

```Python
# create schema
schema = MilvusClient.create_schema(
    auto_id=False,
    enable_dynamic_field=True,
)

# add fields
schema.add_field(field_name="id", datatype=DataType.INT64, is_primary=True)
schema.add_field(field_name="vector", datatype=DataType.FLOAT_VECTOR, dim=5)
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The schema includes a primary key and at least one vector field. For supported schema types, see <a href="https://milvus.io/docs/zh/schema.md">Schema explanation</a>.</div>


If you need to perform an Upsert operation, the primary key must be set to `auto_id=False` If `auto_id=True` is set, the Upsert function cannot be used

It is recommended to create indexes when creating a collection The vector field must define an index; indexes are also strongly recommended for scalar fields frequently used for filtering The example code is as follows

```Python
index_params = client.prepare_index_params()

index_params.add_index(
    field_name="id",
    index_type="AUTOINDEX"
)

index_params.add_index(
    field_name="vector", 
    index_type="AUTOINDEX",
    metric_type="COSINE"
)
```


Create a collection using Schema, then use `list_collections` to get and view the current collection list

```Python
# create collection
client.create_collection(
    collection_name="customized_setup_1",
    schema=schema,
    index_params=index_params
)

# view loading status
res = client.get_load_state(
    collection_name="customized_setup_1"
)

# view collection list
collections = client.list_collections()

View collection details
res = client.describe_collection(
    collection_name="customized_setup_1"
)

Delete a collection
client.drop_collection(
    collection_name="customized_setup_1"
)
```


<span id="BxPUZxcH"></span>
## Entity management

Entities are similar to a row in a relational database or a document in Elasticsearch Common code for entity management is shown below

```Python
# insert
data = [
    {"id": 0, "vector": [0.3580376395471989, -0.6023495712049978, 0.18414012509913835, -0.26286205330961354, 0.9029438446296592], "color": "pink_8682"},
    {"id": 1, "vector": [0.19886812562848388, 0.06023560599112088, 0.6976963061752597, 0.2614474506242501, 0.838729485096104], "color": "red_7025"}]

res = client.insert(
    collection_name="customized_setup_1",
    data=data
)

# update
data=[
    {"id": 0, "vector": [-0.619954382375778, 0.4479436794798608, -0.17493894838751745, -0.4248030059917294, -0.8648452746018911], "color": "black_9898"},
    {"id": 1, "vector": [0.4762662251462588, -0.6942502138717026, -0.4490002642657902, -0.628696575798281, 0.9660395877041965], "color": "red_7319"}]
    
res = client.upsert(
    collection_name='customized_setup_1',
    data=data
)

# delete
res = client.delete(
    collection_name="customized_setup_1",
    ids=[0,1]
)
```


<span id="9bakoek1"></span>
## Index management

When defining a Collection, you can specify indexes to create for faster search performance, and each vector field must have an index configured. The commonly used code for index management is as follows.

```Python
index_params = client.prepare_index_params()

# add index
index_params.add_index(
    field_name="id",
    index_type="AUTOINDEX"
)

index_params.add_index(
    field_name="vector",
    index_type="AUTOINDEX",
    metric_type="COSINE"
)

client.create_collection(
    collection_name="test_entities",
    schema=schema,
    index_params=index_params # Index parameters
)
```


Different field types support different index types. Vector fields can use AUTOINDEX or other index types. For details on index types, see [Index explanation](https://milvus.io/docs/zh/index-explained.md).

<span id="wMXsnXGR"></span>
## Search management

If the Collection was previously released, it needs to be loaded before searching. For details, see [Load and release](https://milvus.io/docs/zh/load-and-release.md). The loading code is shown below.

```Bash
client.load_collection(collection_name="your_collection_name")
```


The code to check loading status is shown below.

&nbsp;

```Bash
res = client.get_load_state(collection_name="your_collection_name")
print(res)
# print out：{"state": "<LoadState: Loaded>"}
```


Confirm the Collection has loaded successfully before performing search operations. The code is as follows. The example search code is as follows.

```Bash
# Single vector search
query_vector = [0.3580376395471989, -0.6023495712049978, 0.18414012509913835, -0.26286205330961354, 0.9029438446296592]
res = client.search(
    collection_name="customized_setup_1",
    anns_field="vector",
    data=[query_vector],
    limit=3,
    search_params={"metric_type": "IP"}
)

# Batch vector search
query_vectors = [
    [0.041732933, 0.013779674, -0.027564144, -0.013061441, 0.009748648],
    [0.0039737443, 0.003020432, -0.0006188639, 0.03913546, -0.00089768134]
]

res = client.search(
    collection_name="customized_setup_1",
    data=query_vectors,
    limit=3,
)
```


<span id="1vCFr3uf"></span>
## DiskANN index management

The example code to create a DiskANN index is as follows.

```SQL
index_params = {
    "index_type": "DISKANN",
    "metric_type": "L2",
    "params": {
        "search_list_size": 128,
        "max_degree": 64,
    }
}

collection.create_index(
    field_name="vector",
    index_params=index_params
)
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Modifying parameters such as <code>pq_code_budget_gb_ratio</code> and <code>search_cache_budget_gb_ratio</code> is not recommended; default values are well optimized for most workloads. Parameters <code>search_list_size</code> and <code>max_degree</code> usually have a positive correlation with recall rate but a negative impact on QPS performance, so adjust them carefully based on actual performance requirements.</div>


<span id="olujPXnu"></span>
## Build parameters (RaBitQ and PQ)


|**Parameter** |**Type** |**Default value** |**Value range** |**Description** |
|---|---|---|---|---|
|store_strategy |String |MEMORY |* DISK<br><br>* MEMORY |Specify DiskANN’s storage strategy.<br><br><br>* MEMORY: build the index entirely in memory (best performance).<br><br>* DISK: build the index on disk, suitable for large\-scale data or memory\-limited environments. |
|quant_type |String |RABITQ |* RABITQ<br><br>* PQ |Defines the quantization method used for index construction.<br><br><br>* RABITQ: use RaBitQ quantization.<br><br>* PQ: use Product Quantization. This parameter is ignored when `legacy=true`. |
|distance_strategy |String |QUANT THEN MORE BITS |* FULL, SINGLE QUANT<br><br>* QUANT THEN FULL<br><br>* QUANT THEN MORE BITS |Specify the distance calculation strategy for search.<br><br><br>* FULL means full\-precision search.<br><br>* SINGLE QUANT: pure quantized search.<br><br>* QUANT THEN FULL: quantized search followed by full\-precision reranking.<br><br>* QUANT THEN MORE BITS: 1\-bit RaBitQ search followed by 4\-bit RaBitQ reranking. When `quant_type=PQ`, it automatically falls back to **SINGLE QUANT**. |
|num_threads |Int |2 |[2, int_max] |Number of threads used during index building. Increasing this value improves build throughput but must match the machine's CPU resources. |
|legacy |String |"false" |* false<br><br>* true |Enable legacy DiskANN implementation.<br><br><br>* false: use the new DiskANN engine (recommend).<br><br>* true: use the legacy implementation from the open\-source version of Milvus. |
|max_degree |Int |48 |[1, 2048] |The maximum number of neighbors allowed for each node in the graph. The larger the value, the higher the graph quality, but the construction time and memory consumption will also increase. |
|build_dram_budget_gb |Int |0 |[0, int_max] |Total DRAM budget available for index building. `0` means automatic. The build process automatically switches to subgraph building mode when memory is insufficient. |
|search_cache_budget_gb_ratio |Float |0.1 |[0.0, 0.3) |The cache size ratio relative to the original data set size. Increasing this value improves search performance but increases memory usage. |
|rabitq_centers |Int |64 |[1, int_max] |Number of cluster centers used by RaBitQ. Modification is generally not recommended unless there is a clear need. |
|pq_code_budget_gb_ratio |Float |0.125 |(0.0, 0.25] |Disk budget ratio for storing PQ codes: PQ code size = original vector size × `pq_code_budget_gb_ratio`. It is recommended to keep the default value. |
|search_list_size |Int |128 |[1, int_max] |The candidate node pool size during graph traversal is an important parameter for balancing recall rate and performance. Construction phase: the larger the value, the higher the graph quality; search phase: the larger the value, the higher the recall rate but the lower the QPS. |
|beam_width_ratio |Int |4 |[1, max(128 / CPU_count, 16)] |The ratio between the maximum number of I/O requests allowed per search iteration and the number of CPUs. The larger the value, the higher the concurrency, but it may increase I/O pressure. |
