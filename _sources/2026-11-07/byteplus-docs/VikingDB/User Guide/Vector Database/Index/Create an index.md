---
title: "Create an index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Create_an_index"
---

<span id="creating-an-index"></span>
# Creating an index

To accelerate vector similarity search, you can create an index that groups and sorts raw data in your vector database. This guide provides step\-by\-step instructions on how to create an index and details the various configuration parameters, such as index algorithms and distance metrics, to help you optimize search performance and accuracy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">A maximum of 200 indexes can be added under an account, and a maximum of 100 indexes can be added for a collection.</div>



<span id="8ee35684"></span>
# Procedure

You can use either of the following ways to enter the index creation page.

Method 1: Click **Indexes** in the left navigation pane. On the page that appears, click **Create Index** in the upper\-left corner.

Method 2: Click **Collection** in the left navigation pane. On the page that appears, click **Create Index** in the Action column of an existing collection. If you use this method to create an index, the specific collection cannot be modified.

Set related parameters on the index creation page, as described in the following table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4681ce8d75a2414ea7daef1fe59bf1bc~tplv-goo7wpa0wc-image.image) </span>


|**Section** |**Parameter** |**Description** |
|---|---|---|
|Basic information |Name |The name of the index. **This parameter is required**.<br><br><br>* The name can contain letters, digits, and underscores (_). It must start with a letter.<br><br>* The name must be 1 to 128 characters in length.<br><br>* The name must be unique. |
||||
||||
||||
||Description |The description of the index. The description can be up to 500 characters in length. **This parameter is optional**. |
|Index settings |Collection |* If you use method 1 to enter the index creation page, you can select a collection for which you want to create an index from the drop\-down list. **This parameter is required**.<br><br>* If you use method 2 to enter the index creation page, you do not need to select a collection again and the collection name is displayed by default. |
||||
||CPU quota |The quota of CPU cores consumed by the index. The value is a positive integer. One CPU core is approximately equal to 100 queries per second (QPS). If the consumed CPU cores exceed the quota, the index will be throttled. **This parameter is required**. |
||Index sharding |The index sharding mode. Valid values:<br><br><br>* Customized sharding: In this mode, the maximum number of shards is 256, and the default value is 1. Estimated number of shards = Estimated data volume/30 million.<br><br>* Automatic sharding: Automatic sharding is triggered when the number of data records in a single shard exceeds the upper limit (30 million) or the memory of a single shard exceeds 50 GB. The number of data records is obtained in real time. |
||||
||||
||Index algorithm |The index algorithm. Valid values are HNSW (default), HNSW\-Hybrid, FLAT, and IVF. This parameter is required.<br><br><br>* HNSW: Hierarchical Navigable Small World (HNSW) is a graph\-based algorithm that performs approximate nearest neighbor (ANN) searches in high\-dimensional spaces. The algorithm constructs a multi\-layered network to reduce the number of nodes to be accessed, improving the ANN search efficiency. This index type applies to large\-size collections that require high search performance.<br><br>* HNSW\-Hybrid: The hybrid HNSW algorithm supports both dense and sparse vector indexes. It automatically integrates the similarity scores of the two vector types based on their weights. This index type applies to large\-size collections that require high hybrid retrieval performance.<br><br><br>The collection indexed by HNSW\-Hybrid must contain sparse_vector type data. Specifically, it must contain a sparse_vector type field or bind a pipeline that can generate sparse_vector type vectors.<br><br><br>* FLAT: Flat indexes leverage brute\-force search to traverse all vectors in the vector database and calculate the distance between each vector in the database and the target vector. Search by flat index is slow, but provides a 100% recall. Therefore, this index type applies to small\-size collections that require high search precision.<br><br>* IVF: Inverted indexes store vectors under each cluster centroid. When you perform a vector search, vectors under the nearest centroids are searched, shortening search time while lowering precision. This index type applies to mid\-size collections that emphasize search efficiency over precision. |
||||
||||
||||
||||
||||
||||
||Distance |The type of distance between vectors. Valid values are IP (default), L2, and COSINE. This parameter is required.<br><br><br>* IP: The inner product of two vectors, which is obtained by multiplying the corresponding components of the vectors. A larger value indicates a higher similarity.<br><br>* L2: The Euclidean distance between two vectors. A smaller value indicates a higher similarity.<br><br>* Cosine: The cosine of the angle between two high\-dimensional vectors. A smaller cosine value indicates a larger angle between the vectors, which means a lower similarity.<br><br><br>When you set distance to Cosine, vectors are normalized by default.<br><br>If you set index type to IVF, the distance can be set to IP or Cosine.<br><br>The selected distance type must be consistent with the metric used for embedding model training. |
||||
||||
||||
||||
||||
||||
||Quantization |The quantization method. Quantization is a technique that reduces the storage size of vector indexes through compression, which can reduce the complexity and costs of calculating the similarity between high\-dimensional and large\-scale vectors. Valid values are Int8 (default), Float, Fix16, and PQ. This parameter is required.<br><br><br>* Int8: Four\-byte floating data is compressed into one\-byte data to reduce storage costs and computing latency. As a result, the precision is slightly lowered. For example, the cosine distance may be greater than 1. This slight decrease in retrieval precision is traded for higher retrieval performance and lower resource costs.<br><br>* Float: No quantization is performed to retain full data precision.<br><br>* Fix16: Four\-byte floating data is compressed into two\-byte data to reduce storage costs and computing latency. As a result, the precision is slightly lowered. This slight decrease in retrieval precision is traded for higher retrieval performance and lower resource costs.<br><br>* PQ: Converts high\-dimensional vectors into low\-dimensional codebook vectors to reduce memory utilization and improve retrieval efficiency.<br><br><br>For Int8, applicable index algorithms are HNSW and FLAT and applicable distance types are IP and Cosine.<br><br>For Float, applicable index algorithms are HNSW, FLAT, and DiskANN and applicable distance types are IP, L2, and Cosine.<br><br>For Fix16, applicable index algorithms are HNSW and FLAT and applicable distance types are IP, L2, and Cosine.<br><br>For PQ, applicable index algorithms are DiskANN and IVF and applicable distance types are IP, L2, and Cosine. |
||||
||||
||||
||||
||||
||||
||||
||||
||Subindex partitioning field |The field for partitioning the index. You can divide a collection into multiple partitions by a specific scalar field and construct these partitions as subindexes. This way, hybrid retrieval can be performed within subindexes to reduce filtering frequency and improve retrieval performance. **This parameter is optional**.<br><br><br>* This parameter specifies the name of a field, while the **Subindex** parameter on the **Retrieval test** tab indicates the value of the field.<br><br>* Select a field name from the drop\-down list. Supported field types are int64, list, and string.<br><br>* It is recommended that you divide a collection into no more than 1000 partitions.<br><br>* Too many subindexes may cause the index to be unavailable or not updated.<br><br>* Regardless of the data volume of a subindex, at least 100,000 bytes are occupied. Too many subindexes will occupy excessive memory, increasing storage costs.<br><br>* If you do not set **partition_by**, the default value of **partition** is default.<br><br>* Use this parameter when you want to divide a collection into multiple partitions and search for data within a certain partition or subindex. For example, you can divide a collection into subindexes by country ID and then search for data by a specific subindex without needing to set filters. This way, search performance can be improved. |
||||
||||
||||
||||
||||
||||
||||
||Filter field |The scalar field for filtering. You can select the scalar fields to be returned from the drop\-down list, which are used for index creation and occupy certain memory space. **This parameter is optional**.<br><br><br>* Filter fields cannot include primary key ID or vector type.<br><br>* The field used for subindex partitioning cannot also be selected as a filter field.<br><br>* All scalar fields are returned when this parameter is not set. |
||||
||||
||||



3. Click **Submit** in the lower\-right corner after you complete parameter configuration. The index list page is displayed once the index is created.

4. You can perform a retrieval test on the created index only when its status is Ready.
