---
title: "Data skipping index"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-data-skipping-index"
---

When attempting to process large amounts of data, query performance may deteriorate as a full scan of each column value may be necessary to apply conditions in the WHERE clause.

To address this issue, ByteHouse supports data skipping indexes, enabling users to skip major data blocks that are confirmed to have no matching values.

<span id="7a4d3415"></span>
## Create Data Skipping Index

Users can only apply data skipping indexes to the CnchMergeTree table family. These indexes involve four main parameters:


1. **Index Name:**  Serves as an identifier for creating the index file. It is a necessary parameter for operations such as deleting or materializing the index.

2. **Index Expression:**  The index expression is a formula used to calculate and determine the range of values stored in the index. It may include a combination of columns, basic operators, and a specified subset of functions designated by the index type.

3. **Type:**  The type of index defines the computations that can be skipped while reading and evaluating each index block.

4. **Granularity:**  Each index block is composed of a defined number of granules, determined by the granularity parameter. For example, if the primary table index has a granularity of 8192 rows, and the index granularity is set to 4, each index "block" will contain 32,768 rows (8192 rows x 4 granularity).


<span id="2257f31d"></span>
### Data Skipping Index syntax example

```SQL
/*
Index Name: key_i_idx
Index expression: key_i
Type: minmax
Granularity: 1
*/
INDEX key_i_idx key_i TYPE minmax GRANULARITY 1, 
```


<span id="320483b9"></span>
### Supported data types

<span id="18a98ce4"></span>
#### Minmax

This efficient indexing method can operate without any specific parameters. It retains the minimum and maximum values of the index expression for each block. For tuple expressions, it individually preserves the ends of each element within the tuple. It is most effective for columns that tend to loosely sort values. This type of index is usually the most cost\-effective during query execution among various index types. However, it should be noted that this index is only suitable for scalar or tuple expressions and cannot be used with expressions that generate arrays or map data types.

<span id="baa2dc3b"></span>
#### Set

This lightweight index type allows the use of a single parameter, max_size, which sets the value collection for each block. When set to 0, it accommodates an unlimited number of different values in the block content. The set contains all the values in the block, or if the number of values exceeds max_size, it is empty. Although it has a high overall cardinality, this index type is particularly effective for columns in each granule group where values are clustered together.

The cost, performance, and effectiveness of the index depend on the cardinality within these blocks. If each block has a large number of unique values, the cost of evaluating query conditions against large index sets becomes very high. Alternatively, if the set is empty because it exceeds the specified max_size, the index will not be applied.

<span id="b0d1fb3f"></span>
#### Bloom filter types

Bloom filters are a compact data structure designed to determine whether collection members are valid, with a very small possibility of false positives. In the use of hop\-count indexing, this is not a major issue, as it only leads to reading some extra, unnecessary blocks. However, it is noteworthy that potential false positives mean that the index expression should be true. Otherwise, valid data may inadvertently be skipped. It is important to design index expressions to minimize the risk of false positives and ensure the accurate skipping of irrelevant blocks.

Bloom filters are very effective for efficiently testing a large number of discrete values and are suitable for scenarios that generate numerous conditional expressions. Specifically, Bloom filter indexes can be applied to arrays, with each value in the array being tested. This adjustment allows for the effective judgment of member validity in arrays or mappings, thereby enhancing the indexing capabilities of such data structures.


* Specialized `tokenbf_v1` indexes are custom\-designed for enhanced Bloom filter functionality and require the adjustment of three related parameters:

   * **Filter Size (in bytes)** : This parameter controls the size of the Bloom Filter in bytes. A larger filter can reduce the likelihood of false positives, at the expense of increased storage space.

   * **Number of Hash Functions**: The number of hash functions applied to the Bloom Filter. Using more hash functions helps reduce false positives.

   * **Hash Function Seed**: The seed used to generate the hash functions of the Bloom Filter.

   * This index is only applicable to String, FixedString types of data. The input expression is split into sequences of characters separated by non\-alphanumeric characters. For example, column value `This is a candidate for a "full text" search` will be split into `This is a candidate for full text search`.

   * This index is used for searching words and other values in long strings with LIKE, EQUALS, in, hasToken(), and similar functions. For example, one potential use is to search for a small number of class names or line numbers in unstructured application log lines.

* More professional **ngrambf_v1**. The functionality of this index is the same as tokenbf_v1. Before setting up the Bloom filter, an additional parameter is needed: the size of the ngram to be indexed. An ngram is any string of length n; for instance, if n is 4, `A short string` would be split into `A sh`, `shor`, `hort`, `ort s`, `or st`, `r str`, `stri`, `trin`, `ring`. This index is also very useful for text searches, especially for languages without word breaks, such as Chinese.

* You can choose to use the **`false_positive`** parameter to specify the probability of receiving a false positive response from this filter, with values ranging from 0 to 1. The default is 0.025. Supported data types include: Int\*, UInt\*, Float\*, Enum, Date, DateTime, String, FixedString, Array, LowCardinality, Nullable, UUID.


Syntax: `bloom_filter([false_positive])`

<span id="c5a695fe"></span>
## Usage example

<span id="d3e882b8"></span>
### Load dataset into ByteHouse

```SQL
DROP DATABASE IF EXISTS test_si;
CREATE DATABASE test_si;

--create table to load numbers_source.csv dataset
CREATE TABLE test_si.numbers
(
    `number` UInt64
)
ENGINE = CnchMergeTree
ORDER BY number;
```


Download the file below and load the dataset into the test_si.numbers table using the data loading function.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1b356e261e543d4be9bac5ce3e8b8b9~tplv-goo7wpa0wc-image.image" name="numbers_source.csv">numbers_source.csv</Attachment>


&nbsp;

<span id="9eeeca3f"></span>
### Create a table without indexes

```SQL
USE test_si;

--Table creation
CREATE TABLE test_skipindex
(
    `id` UInt64,
    `key_i` UInt64,
    `p_date` Date
)
ENGINE = CnchMergeTree
PARTITION BY p_date
ORDER BY id;

--Insert test dataset into table 
INSERT INTO test_skipindex SELECT
    number,
    number,
    today()
FROM test_si.numbers
LIMIT 10000000;

--Check to see if data has been added successfully
SELECT sum(id) FROM test_skipindex WHERE key_i = 1;
```


If we run the command below,

```SQL
--Simple query to select all rows from the table test_skipindex where the key_i column has values of 200 or 700
select * from `test_skipindex` where key_i in (200, 700);
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6791eebb032d456faea4c003eadbfe9b~tplv-goo7wpa0wc-image.image) </span>

As a result, without any indexes, 1 million rows of data were processed.

<span id="d9ca14ab"></span>
### Add indexes

<span id="16448301"></span>
#### **Add indexes to the new table**

```SQL
DROP TABLE if EXISTS test_si.test_skipindex;
USE test_si;

--Table creation
CREATE TABLE test_skipindex
(
    `id` UInt64,
    `key_i` UInt64,
    `p_date` Date,

--Add index during creation of table
    INDEX key_i_idx key_i TYPE minmax GRANULARITY 1
)
ENGINE = CnchMergeTree
PARTITION BY p_date
ORDER BY id
--If we do not set the index_granularity, default would be 8192
SETTINGS index_granularity = 8192;

--Insert test dataset into table 
INSERT INTO test_skipindex SELECT
    number,
    number,
    today()
FROM test_si.numbers
LIMIT 1000000;

--Check to see if data has been added successfully
SELECT sum(id) FROM test_skipindex WHERE key_i = 1;
```


Run the same command as above,

```SQL
--Simple query to select all rows from the table test_skipindex where the key_i column has values of 200 or 700
select * from `test_skipindex` where key_i in (200, 700); 
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e47593ef2fb4ba395f3bd14802aac4f~tplv-goo7wpa0wc-image.image) </span>

As a result, using the index, only 8192 rows of data were processed, and the execution speed was faster.

<span id="5fa0345d"></span>
#### Add subsequent data indexes to the existing table

```SQL
DROP TABLE if EXISTS test_si.test_skipindex;
USE test_si;
--Table creation
CREATE TABLE test_skipindex
(
    `id` UInt64,
    `key_i` UInt64,
    `p_date` Date
)
ENGINE = CnchMergeTree
PARTITION BY p_date
ORDER BY id;

--Insert test dataset into table 
INSERT INTO test_skipindex SELECT
    number,
    number,
    today()
FROM test_si.numbers
LIMIT 1000000;

--Add index after creation of table
ALTER TABLE test_si.test_skipindex ADD index key_i_idx key_i TYPE minmax GRANULARITY 1;

--Check to see if data has been added successfully
SELECT sum(id) FROM test_skipindex WHERE key_i = 1;
```


If we run the same command, our result will be processing 1 million lines.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/163b5f5d978f4386a91baf24fa71a5d5~tplv-goo7wpa0wc-image.image) </span>

This is because the data added before the index creation is considered Historical data, and for Historical data, we must carry out the Add to Step to build the index.

<span id="c9c42302"></span>
#### Add indexes for historical data

To build an index for Historical data, you need to use `MATERIALIZE INDEX` in your command. If you use the `ALTER TABLE...ADD` command without executing `MATERIALIZE INDEX`, indexes will only be generated for the newly written data.

```SQL
--Run this additional code block
ALTER TABLE test_si.test_skipindex MATERIALIZE INDEX key_i_idx;
```


Query results indicate that the index addition for Historical data was successful. Only processes 8192 lines, and the speed is faster.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b277416c90e4f1fa728d40cf639cde7~tplv-goo7wpa0wc-image.image) </span>

<span id="3a03d50f"></span>
#### Add indexes for historical data partition

`MATERIALIZE INDEX` by default generates indexes for all Historical data. If you want to add a specific Partition to Historical data, we must use `IN PARTITION` with `MATERIALIZE INDEX`. This means that only the specified partitions will generate indexes.

```SQL
DROP TABLE if EXISTS test_si.test_skipindex;
USE test_si; 
--Table creation
CREATE TABLE test_skipindex
(
    `id` UInt64,
    `key_i` UInt64,
    `p_date` Date
)
ENGINE = CnchMergeTree
PARTITION BY p_date
ORDER BY id;

--Insert test dataset into table 
INSERT INTO test_skipindex SELECT
    number,
    number,
    today()
FROM test_si.numbers
LIMIT 1000000;

--Insert test dataset into table 
INSERT INTO test_skipindex SELECT
    number,
    number,
    today()-1
FROM test_si.numbers
LIMIT 1000000;

ALTER TABLE test_si.test_skipindex ADD index key_i_idx key_i TYPE minmax GRANULARITY 1;
```


```SQL
--Assuming the date of the day before today is 20230927, index is generated only for the 20230927 date partition 
ALTER TABLE test_si.test_skipindex MATERIALIZE INDEX key_i_idx IN PARTITION '20230927';

--Check to see if data has been added successfully
SELECT sum(id) FROM test_skipindex WHERE key_i = 1 AND p_date = today()-1;

--Check to see if data has been added successfully
SELECT sum(id) FROM test_skipindex WHERE key_i = 1 AND p_date = today();
```


If we run the simple query shown below, we can see that Historical data in the partition 20230927 [today() \- 1] has generated an index.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d18338b02fa446d2aa4913c4936851de~tplv-goo7wpa0wc-image.image) </span>

For Historical data without a specified partition, indexes are not generated.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d05d04095f6b4fbe90f4f324fd3e5866~tplv-goo7wpa0wc-image.image) </span>

<span id="91eb61a2"></span>
### Delete the index

```SQL
ALTER TABLE test_si.test_skipindex DROP INDEX key_i_idx;

SHOW CREATE TABLE test_skipindex;

SELECT sum(id) FROM test_skipindex WHERE key_i = 1;
```


<span id="16d4899e"></span>
## Usage recommendation

Generally, when the data volume is small, the cost of creating indexes is not high. However, if we aim to index all historical data and the data volume is extremely large, directly using `MATERIAL INDEX` to add indexes to all historical data might put a significant load on the cluster. In this scenario, it is recommended to create indexes by partition.
