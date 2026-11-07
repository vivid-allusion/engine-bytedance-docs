---
title: "Skipping index"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/skipping-index"
---

ByteHouse Enterprise provides a secondary index—the skipping index—which supports asynchronous addition after table creation. This feature addresses the limitation that sort indexes can only be set during table creation, making index adjustments more flexible and helping you accelerate queries more conveniently. This article introduces the basic concepts and usage of skipping indexes.

<span id="d8846b9d"></span>
# Applicable scenarios

The ByteHouse MergeTree family table engine supports configuring sort indexes during table creation. When query conditions include sort index fields, the system can pre\-filter data to reduce IO consumption and thereby accelerate queries. However, sort indexes have limitations: they can only be set during table creation and cannot be adjusted afterward, resulting in insufficient flexibility. To address this, ByteHouse provides the skipping index as a type of secondary index, which supports asynchronous addition after table creation. Its principle is similar to that of sort indexes, as it also builds a sparse index on fields to enable partial data pruning during queries. Although the query acceleration effect of skipping indexes is not as strong as that of sort indexes, their flexible adjustment capability allows them to play a broad role in practical scenarios.

<span id="ee38c828"></span>
# Index types

The commonly used skipping index types are described as follows:


|Index type |Description |
|---|---|
|`minmax` |Lightweight index, no need to set additional parameters. `minmax` is used to store the minimum and maximum values of the index expression in each data block. If the expression is a tuple, the values of each element in the tuple are stored separately. This type is suitable for columns that are loosely sorted by value. The minmax index usually has the lowest application cost in query processing, but it is only applicable to scalar or tuple expressions and does not support expressions that return arrays or maps. |
|`set` |Lightweight index. It is used to store all values in a data block. `set` index supports setting a single parameter, which is the maximum size of the value set in each data block. When this parameter is set to 0, an unlimited number of discrete values can be stored. If the number of values in a data block exceeds this maximum capacity, the index will be empty.<br><br>The `set` index is suitable for columns with low cardinality within each data granule but high overall cardinality. Its indexing cost, query performance, and effectiveness depend on the cardinality within the data block. If each data block contains a large number of unique values, the cost of evaluating query conditions for large index sets will increase significantly, or the index will be empty due to the number of values exceeding the maximum capacity. In this case, the set index will not be effective. |
|`Bloom Filter` |A Bloom filter is a data structure that enables efficient set membership testing with a slight allowance for false positives. Since Bloom filters can process test scenarios with a large number of discrete values more efficiently, they are suitable for condition expressions that need to match many test values, and they support application to arrays. Skipping indexes based on Bloom filters include the following three types: |
||`bloom_filter`: Supports setting the allowed "false positive rate", with a value range of 0 to 1. If not specified, the default value is 0.025. This parameter is optional. |
||`tokenbf_v1`: Only applicable to String and FixedString data types. This index splits the input expression into a sequence of tokens according to non\-alphanumeric characters. For example, the column value "This is a candidate for a 'full text' search" will be split into `This` `is` `a` `candidate` `for` `full` `text` `search`. `tokenbf_v1` is suitable for LIKE, EQUALS, IN, hasToken(), and similar search scenarios. It can be used to search for words and other values in longer strings, and supports setting three parameters:<br><br><br>* **Filter size**: Measured in bytes. The larger the filter, the lower the false positive rate, but the storage cost increases accordingly.<br><br>* **Number of hash functions**: The more hash functions, the lower the false positive rate.<br><br>* **Seed value for Bloom filter hash functions**. |
||`ngrambf_v1`: Splits the string into ngrams of fixed length. For example, when the ngram length is set to 4, the string "A short string with an ngram size of 4" will be indexed as: 'A sh', ' sho', 'shor', 'hort', 'ort ', 'rt s', 't st', ' str', 'stri', 'trin', 'ring'. This index is also suitable for text search scenarios, especially for languages without word intervals, such as Chinese. This index supports setting four parameters:<br><br><br>* **ngram length**;<br><br>* **Filter size**: Measured in bytes. The larger the filter, the lower the false positive rate, but the storage cost increases accordingly.<br><br>* **Number of hash functions**: The more hash functions, the lower the false positive rate.<br><br>* **Seed value for Bloom filter hash functions**. |


Apart from the dedicated parameters mentioned for each of the above skipping index types, all skipping indexes support configuring the GRANULARITY (index granularity) parameter. It is generally recommended to set GRANULARITY to 1 to achieve a higher data filtering rate; if GRANULARITY is set to a larger value, although it can reduce the storage usage of the index, the corresponding data filtering effect may be weakened. The currently supported configuration range for this parameter is 1 to 10.

<span id="588b08d2"></span>
# Caution


1. Using skipping indexes requires an understanding of data distribution and is more suitable for high\-cardinality column scenarios, as well as for equality queries or small\-range queries; it is not suitable for low\-cardinality column scenarios or for scenarios where query conditions will hit a large range of data.

2. The recommended priority order for skipping index types corresponding to different data type fields is as follows:

   * For numerical value type fields, `minmax` index or `bloom_filter` index is usually preferred;

   * For String type fields, `bloom_filter` index can be uniformly selected. It is recommended to configure the false positive rate to 0.1, that is, `bloom_filter(0.1)`, which is convenient and efficient to use;

   * If you want to use an index in LIKE query scenarios and the LIKE substring logic is not complex, it is recommended to select the `ngrambf_v1` index. The recommended parameter configuration is: `ngrambf_v1(2/3, 4096/8192, x, 0)`.


<span id="8b132449"></span>
# Usage

<span id="3bb35eaa"></span>
## Add index (ADD INDEX)

```SQL
-- Add minmax type index
ALTER TABLE skiptest on cluster {cluster_name} 
    ADD INDEX
    index_name column_name TYPE minmax GRANULARITY 1;
   
-- Add tokenbf_v1 type index
ALTER TABLE skiptest on cluster {cluster_name} 
    ADD INDEX
    index_name column_name TYPE tokenbf_v1(4096, 3, 0) GRANULARITY 1;
    
-- Add ngrambf_v1 type index
ALTER TABLE skiptest on cluster {cluster_name} 
    ADD INDEX
    index_name column_name TYPE ngrambf_v1(3, 4096, 3, 0) GRANULARITY 1;
    
-- Add set type index
ALTER TABLE skiptest on cluster {cluster_name} 
    ADD INDEX
    index_name column_name TYPE set(0) GRANULARITY 1;
    
-- Add bloom_filter type index
ALTER TABLE skiptest on cluster {cluster_name} 
    ADD INDEX
    index_name column_name TYPE bloom_filter(0.1) GRANULARITY 1;
    
```


<span id="7bd45d9e"></span>
## Delete index (DROP INDEX)

```SQL
ALTER TABLE skiptest on cluster {cluster_name} 
    DROP INDEX index_name 
```


<span id="12268a75"></span>
## Add index when creating a table

```SQL
-- Add to table structure:
INDEX index_name column_name TYPE bloom_filter(0.1) GRANULARITY 1;
 
-- For example:
CREATE TABLE default.test_skip_index
(
    `id` UInt16,
    `name` String,
    INDEX name_idx name TYPE bloom_filter(0.1) GRANULARITY 1
)
ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 8192;
```


<span id="f1bf0273"></span>
## Add index for historical data

```SQL
ALTER TABLE  skipindex on cluster {cluster_name} MATERIALIZE INDEX index_name;
```
