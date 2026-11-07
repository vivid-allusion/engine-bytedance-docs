---
title: "Enable vector search"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/start-vector-search-service"
---

ByteHouse vector retrieval supports storing and efficiently searching vector features of unstructured data such as text, images, and videos. It applies to scenarios like image\-to\-image search, image\-to\-video search, text retrieval, and text\-to\-image search, and can integrate with large models to build intelligent applications. This article explains how to activate the vector retrieval feature and configure related parameters.

<span id="adf85a1e"></span>
# Notes

The vector retrieval service cannot be disabled once activated. Please proceed with caution.

<span id="75a36e4e"></span>
# Enable vector retrieval feature

<span id="dc5cf1bb"></span>
## Enable during cluster creation

You can enable vector retrieval while creating a cluster. You can activate the **vector retrieval** feature in the advanced features module. For detailed pricing information, see the pricing description.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a5f0407cd704dafbf1d66916e4ef5df~tplv-goo7wpa0wc-image.image) </span>

<span id="9501d45a"></span>
## Enable independently in the console


1. On ByteHouse Console, go to **Cluster management \> Cluster list** page, click **Advanced Features**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/730f2e6517d04d91a708aa5357c05dce~tplv-goo7wpa0wc-image.image) </span>

2. Select the applicable cluster and activate the vector search feature.

3. Click **Submit**. The system will automatically activate the vector search feature.


<span id="2b64c4d9"></span>
# Configure vector search parameters

For better vector search performance, it is recommended to configure relevant user parameters and cluster parameters according to [Modify configuration parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters). Meanwhile, ByteHouse also provides [Best practice for vector search](https://docs.byteplus.com/docs/bytehouse/best-practice-for-vector-search) which you can configure as needed.

The supported total parameters are as follows:


|Param |Description |Configuration method |Default |Suggestions |
|---|---|---|---|---|
|`enable_new_ann` |Whether to use the new ANN execution path. |Set in users.xml. |0 |Set to 1 to enable the new ANN path. |
|`hnsw_ef_s` |Search parameter used during HNSW index\-based search; higher values increase accuracy. |Set in users.xml. |10 |For recall scenarios above 90, typically set it to 128 or higher. |
|`nprobe` |Search parameter for Faiss IVF indexes (IVF_FLAT, IVF_PQ, IVF_PQ_FS) indicating the number of clusters used in the search. In theory, a larger nprobe increases accuracy and latency. |Set in users.xml. |0 (default 0 means not set, the default parameter used in index is 1) |For recall above 90, consider setting it more than 1/4 of nlist. |
|`k_factor_rf` |Search parameter for Faiss index with refine (IVF_PQ_FS index). The larger k_factor_rf, the more results are used for sorting, increasing accuracy and latency. |Set in users.xml. |0 (same as above) |For index with refine, if recall is low, try increasing k_factor_rf. Start with 100 and fine\-tune as needed. |
|`vector_index_build_threads` |Number of build threads per part. |Set in users.xml. |8 |Control build threads for a single part; reduce if concurrent import or merge concurrency is high. |
|`enable_global_vector_index_preload` |Whether to load the index directly into cache after server startup or part creation. |Set in users.xml. |0 |Write acceleration. The vector index of the written part goes directly into cache, eliminating index loading time. |
|`log_processors_profiles` |Inactivate processor configuration file logs to reduce log writing overhead and improve query performance. |Set in users.xml. |0 (Inactivate) |It is suggested to set it as 0. |
|`compile_expressions` |Disable expression compilation optimization to avoid lengthy compilation time in complex vector calculations. |Set in users.xml. |0 (Inactivate) |It is suggested to set it as 0. |
|`compile_sort_description` |Disable sorting description compilation optimization to improve vector sorting performance. |Set in users.xml. |0 (inactivate) |It is suggested to set it as 0. |
|`vector_index_cache_size` |Memory cache size available to vector index. Evicted using LRU strategy. |Set in config.xml. |max_server_memory_usage \* 0.5 |Reserve part of the cache for index building. Considering possible background merge or mutation tasks, it is suggested to reserve no more than half of the max memory for the index cache. If merge concurrency is high, consider further reducing the index cache size. |
|`enable_use_local_lock` |Activate the local lock mechanism to reduce write conflicts and improve vector data write performance in high concurrency scenarios. |Set in config.xml. |0 (Inactivate) |Setting it to 1 (Activate) is recommended. |
|`disk_unique_key_index_meta_cache_size` |Cache size for unique key index metadata, optimizing key\-value retrieval performance. |Set in config.xml. |None |2GB or more is recommended. |
|`disk_unique_key_index_data_cache_size` |The cache size for unique key index data, improving data read speed. |Set in config.xml. |None |5GB or more is recommended. |
|`additional_services` |Enable additional services dynamically without restarting the service. |Set in config.xml. |0 (Inactivate) |You can enable it as needed. |


<span id="050c92dd"></span>
# Next steps: Use vector search

ByteHouse supports vector search through SQL and Python APIs. You can refer to the following document for operation.


* [Use vector search with SQL](https://docs.byteplus.com/docs/bytehouse/use-vector-search)

* [Use vector search with Python API](https://docs.byteplus.com/docs/bytehouse/python-api)
