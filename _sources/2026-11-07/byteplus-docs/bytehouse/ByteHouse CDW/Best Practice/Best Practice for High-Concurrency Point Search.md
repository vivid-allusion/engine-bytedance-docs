---
title: "Best Practice for High-Concurrency Point Search"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/best-practice-for-high-concurrency-point-search"
---

ByteHouse CDW supports efficient analysis of PB\-scale massive data. This article introduces best practices for improving query efficiency and cost\-effectiveness in high\-concurrency point search scenarios.

<span id="0d3af8ea"></span>
# Resource recommendation

<span id="27985501"></span>
## Purchase a private server

The Server component of ByteHouse CDW handles SQL parsing, optimization, and query scheduling. In high\-concurrency scenarios with QPS \> 1000, public servers can easily become a performance bottleneck. Therefore, when you need ByteHouse CDW to support high\-concurrency point search operations, we recommend you purchase a dedicated Server for optimal performance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7299668ff44444f0a111b4fc12aea959~tplv-goo7wpa0wc-image.image) </span>

Private Server is ByteHouse CDW's **private computing resource** solution, which provides users with independent computing nodes (Server) to achieve resource isolation, performance guarantee, and higher flexibility. For more details, refer to [Private server](https://docs.byteplus.com/docs/bytehouse/private-server).

After successfully purchasing a dedicated Server, subsequent queries will automatically use the dedicated Server to ensure the computational resources of the queries.

<span id="35f11185"></span>
## Isolation & specifications recommendation for virtual warehouse

If you have not purchased a dedicated Server and are using a public compute group, and you have multiple query scenarios like point search, OLAP, ELT at the same time, to avoid the point search operations being affected by other scenarios, we recommend you purchase an independent compute group for the point search operations. Start with XL (32 cores, 128GB, 2 nodes), and later upgrades or downgrades can be made on demand.

After purchasing a dedicated compute group, you can specify the compute group to be used in Query SQL through the SET parameter, thereby ensuring resource isolation for the compute group. Examples are as follows:


* You can place this at the end of SQL: `select ...` `settings virtual_warehouse='xxx'`

* You can set this at session level: `set virtual_warehouse='xxx'`


<span id="03ff7649"></span>
# Table Settings DDL Suggestion

In high\-concurrency point search scenarios, it is advised to set appropriate sort keys/bucket keys/indexes for the table while creating.

Take the following point search SQL as an example: id is the unique key of the table, and date is the partition field.

```SQL
SELECT * FROM t WHERE id = ? and date = ? and ...;
```


Recommended DDL for table creation is:

```SQL
CREATE TABLE t
(
  id Int64,
  date Date,
  ....，
  INDEX idx_id id TYPE bloom_filter GRANULARITY 1
)
ENGINE = CnchMergeTree
PARTITION BY date
UNIQUE KEY id
ORDER BY id
[CLUSTER BY EXPRESSION cityHash64(id) INTO <N> BUCKETS] -- Consider adding it when the number of rows in the table or a single partition exceeds 1 million.
SETTINGS index_granularity = 1024;
```


Modeling description


|Important Settings |Examples |Description |
|---|---|---|
|Table Parameters (Settings) |`index_granularity = 1024` |ByteHouse enhances the storage and memory usage efficiency for large datasets by defining the smallest unit of an index not as a row, but as index_granularity rows (referred to as **granule**). This technology is called **sparse indexing**.<br><br>The default size of index_granularity is 8129, that is, every 8192 rows form a granule. In point query scenes, the search usually hits only one row of data. At this time, reducing the index_granularity parameter can decrease the read amplification effect during the reading process. However, the smaller the index_granularity, the higher the storage occupation and computational cost of the index will be.<br><br>After flight evaluations, 1024 is the recommended value for point query scenes. |
|Sort key (ORDER BY) |`ORDER BY id` |In the example SQL, the filter condition of the unique key column id has the best filtering effect. Using the id column as the first field of the sort key allows the query to fully utilize the Primary Index to filter out granules that cannot hit the predicate in advance. |
|Skip Index |`INDEX idx_id id TYPE bloom_filter GRANULARITY 1` |Since the primary index is a sparse index, even if a data file does not contain the specified ID, it usually requires reading at least one granule.<br><br>To reduce false positive rates, a skip index of the type bloom filter can be created for the ID column, which creates a bloom filter for each granule. This way, when a data file does not contain the specified ID, there is a very high likelihood of skipping the file's reading. |
|Bucketing (CLUSTER BY) |`CLUSTER BY id INTOBUCKETS` |Bucketing allows rows with the same bucketing key value to be allocated to the same data file. For queries that precisely filter based on the bucketing key, bucket pruning technology can be used during the query planning phase to exclude data files and computing nodes that cannot hit the predicates, significantly enhancing concurrency performance.<br><br>In this example, the point\-lookup SQL initially required all nodes of the computing group to participate in the calculation, but after adding ID column bucketing and utilizing bucket pruning technology, only one node needs to participate in the calculation. It can significantly enhance the point\-lookup QPS.<br><br>The number of bucketsis generally a multiple of the number of compute group nodes, it is recommended to use `#nodes x 1` or `#nodes x 2`. |


<span id="a1743f33"></span>
# DQL query suggestions


* For point lookup SQL suggestions, specify **enable_point_lookup_profile = 1** parameter to achieve optimal performance.

   ```SQL
   SELECT * FROM t WHERE id = 10000 SETTINGS enable_point_lookup_profile = 1;
   ```
   

* For the Flink lookup scene, improving the overall QPS can be achieved by increasing the query concurrency through asynchronous lookup.
