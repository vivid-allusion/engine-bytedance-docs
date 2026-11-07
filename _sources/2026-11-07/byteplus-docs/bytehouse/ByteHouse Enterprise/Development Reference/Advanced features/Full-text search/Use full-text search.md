---
title: "Use full-text search"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/full-text-search"
---

Full\-text search (or text search) is used to identify natural language documents that meet query conditions. The most common use is to find all documents containing specified query terms. By preprocessing documents through building full\-text indexes, efficient subsequent searches can be achieved. ByteHouse Enterprise Edition enhances the text inverted index capability to support faster text retrieval and filtering and allows full\-text search using SQL syntax. This article introduces how to create full\-text indexes and perform queries using SQL commands.

<span id="b397509d"></span>
# Prerequisites

Before using the inverted index, ensure that the selected cluster has enabled the advanced full\-text search feature. To enable it, refer to [Enable full-text search](https://docs.byteplus.com/docs/bytehouse/enable-full-text-search-ce).

<span id="b808a7b4"></span>
# Feature overview

Inverted indexes can build inverted indexes for String, Array(String), and String type in JSON, providing fast text search and filtering methods. Support for nullable type inverted indexes will be available later. Stay tuned.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94f42b3b6ff74c3fa49f05c889019b9b~tplv-goo7wpa0wc-image.image) </span>

<span id="74cb2e4e"></span>
# Index definition

Inverted indexes are managed using the [ClickHouse secondary index API](https://clickhouse.com/docs/en/sql-reference/statements/alter/skipping-index). Common secondary index commands also apply to inverted indexes, such as ADD INDEX / DROP INDEX / MATERIALIZE INDEX / CLEAR INDEX. For operation details, refer to [Common ALTER INDEX commands for modifying indexes](https://docs.byteplus.com/docs/bytehouse/full-text-search#ecf64ec2). The following shows the basic syntax for creating an inverted index.


* Define the index when creating a table.

   ```SQL
   CREATE TABLE test_inverted_with_token
   (
       `key` UInt64,
       `doc` String,
       INDEX doc_idx doc TYPE inverted('standard', '{"version":"v3"}') GRANULARITY 1
   )
   ENGINE = MergeTree()
   ORDER BY key;
   ```
   

* For existing tables, use ALTER ADD INDEX to add an index.

   ```SQL
   ALTER TABLE test_inverted_with_token ADD INDEX doc_idx doc TYPE inverted('standard', '{"version":"v3"}') GRANULARITY 1;
   ```
   

* Build indexes for existing data.

   ```SQL
   ALTER TABLE test_inverted_with_token MATERIALIZE INDEX doc_idx;
   ```
   


Common settings parameters are explained below:


* `GRANULARITY`: Under normal circumstances, the GRANULARITY in the inverted index can be set to 1, which is more universal. You can also adjust it to 8192 or a larger value.

* Adding the settings parameter `filter_with_inverted_index_segment = 1` during queries enables a more efficient filtering method.


<span id="f780d6a3"></span>
# SQL reference

<span id="ecf64ec2"></span>
## ALTER INDEX commands

The inverted index is managed using secondary index APIs; common secondary index commands also apply to inverted indexes.

<span id="67b6d107"></span>
### ADD INDEX

Add an index without building it for existing data.

```SQL
ALTER TABLE test_inverted_with_token ON CLUSTER {cluster} ADD INDEX doc_idx doc TYPE inverted('standard', '{"version":"v3"}') GRANULARITY 1;
```


To build indexes for existing data, run the following command:

```SQL
ALTER TABLE test_inverted_with_token MATERIALIZE INDEX doc_idx;
```


<span id="719ab8ae"></span>
### DROP INDEX

Delete the index and clear index files.

```SQL
ALTER TABLE test_inverted_with_token ON CLUSTER {cluster} DROP INDEX doc_idx;
```


<span id="f5a38fba"></span>
### MATERIALIZE INDEX

Build index for existing data.

```SQL
ALTER TABLE test_inverted_with_token ON CLUSTER {cluster} MATERIALIZE INDEX doc_idx;
```


<span id="1493e95c"></span>
### CLEAR INDEX

Clear existing data index files but keep the index.

```SQL
ALTER TABLE test_inverted_with_token ON CLUSTER {cluster} CLEAR INDEX doc_idx;
```


<span id="25739f6b"></span>
## Switch inverted index version

ByteHouse inverted index supports three versions. You can use the corresponding version by specifying the `"version"` parameter. Differences among versions are explained as follows:


|Version |Function description |
|---|---|
|Version 3 |Supports token search, fuzzy matching, and high cardinality point queries.<br><br>Based on Version 1, ByteHouse optimized the dictionary to avoid the technical bottleneck in Version 1 that required fully loading the dictionary into memory for queries, reducing IO and memory resource consumption. |
|Version 2 |Supports text similarity search, BM25 algorithm, combined with vectors for hybrid retrieval.<br><br>On top of Version 1’s inverted list of row information, ByteHouse added inverted lists with frequency and position information to calculate text similarity. |
|Version 1 |Inherited from ClickHouse community version. V3 is recommended. |


<span id="afe70925"></span>
#### Use Version 3

```SQL
INDEX doc_idx doc TYPE inverted('standard', '{"version":"v3"}') GRANULARITY 1
```


<span id="d2c3c252"></span>
#### Use Version 2

```SQL
INDEX doc_idx doc TYPE inverted('standard', '{"version":"v2"}') GRANULARITY 1
```


<span id="476801ff"></span>
#### Use Version 1

```SQL
INDEX doc_idx doc TYPE inverted('standard', '{"version":"v1"}') GRANULARITY 1
```


<span id="f32a07e3"></span>
## Build inverted index for Array/JSON/MAP column text content

ByteHouse supports specifying Array/JSON/MAP sub\-columns through the `sub_column_filters.value` configuration and building inverted indexes for them.

<span id="60d50109"></span>
#### Array column

```SQL
CREATE TABLE test_inverted_with_arry_str
(
    `id` UInt64,
    `doc` Array(String),
    INDEX doc_idx doc TYPE inverted('token', '{"sub_column_filters": {"doc": ["*"]}}') GRANULARITY 1
)
ENGINE = MergeTree()
ORDER BY id
```


<span id="d19b1a3d"></span>
#### JSON column


* Build an inverted index for the specified JSON subcolumn text content.

   ```SQL
   CREATE TABLE index_partial_subcols
   (
       `key` Int,
       `value` JSON,
       INDEX val_ivt value TYPE inverted('token', '{"sub_column_filters": {"value": ["k0", "k1"]}}') GRANULARITY 1
   )
   ENGINE = MergeTree
   ORDER BY key
   ```
   

* Build an inverted index for the entire JSON subcolumn text content.

   ```SQL
   CREATE TABLE index_partial_subcols
   (
       `key` Int,
       `value` JSON,
       INDEX val_ivt value TYPE inverted('token', '{"sub_column_filters": {"value": ["*"]}}') GRANULARITY 1
   )
   ENGINE = MergeTree
   ORDER BY key
   ```
   


<span id="8f556a23"></span>
#### MAP(String,String) column

```SQL
CREATE TABLE map_test.test_map
(
    `id` UInt32,
    `m` Map(String, String) KV,
    -- Build inverted index for specified key1, key2
    INDEX m_inv m TYPE inverted('token', '{"version":"v3", "sub_column_filters": { "m" : ["key1","key2"] } }') GRNULARITY 1
)
ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 8192
```


<span id="a1b0050d"></span>
## Tokenization algorithm

Different tokenization algorithms have varying filtering efficiency under specific query conditions, which also affects recall rate. Rule\-based tokenization algorithms (standard/token/ngram/char_sep) significantly outperform semantic\-based algorithms (ICU tokenization) in write speed in most cases. In general, rule\-based tokenization algorithms are recommended for keyword search and fuzzy matching scenarios, while semantic tokenization algorithms should be used as needed for similarity search scenarios.


|Tokenization algorithm |Algorithm type |Selection recommendation |
|---|---|---|
|standard segmentation |Rule\-based segmentation |Segmentation based on non\-alphabetic characters in ASCII codes. For UTF8 encoded words, the standard analyzer splits words separately.<br><br>For mixed Chinese\-English text, English is segmented by words, and Chinese by characters. This segmenter is recommended for most search scenarios (behaves like Elasticsearch's default segmenter). |
|token segmentation |Rule\-based segmentation |Segmentation based on spaces and punctuation. This method mainly suits languages like English that use spaces to separate words, and also applies to string id fields without punctuation or spaces. |
|ngram segmentation |Rule\-based tokenization |Split text continuously by the specified length (n). This method is especially suitable for languages without spaces (such as Chinese) or texts containing long compound words. It is commonly used to support fuzzy match queries, such as searching long Chinese texts without separators. |
|Custom delimiter | |Custom delimiter currently only supports specifying ASCII symbols. After specifying the custom delimiter, the system splits text by all characters defined in separators. |
|ICU tokenization |Semantic tokenization |ICU tokenization ([International Components for Unicode](https://icu.unicode.org/)) is a general semantic tokenizer that supports multi\-language semantic tokenization without requiring dictionary configuration, covering mainstream internationalization (i18n) languages. However, this segmentation is less efficient than rule\-based segmentation and is recommended only for similarity search scenarios. |


<span id="5ec9985a"></span>
#### Standard tokenization

```SQL
INDEX doc_idx doc TYPE inverted('standard', '{"version":"v3"}') GRANULARITY 1
```


<span id="9b0aae09"></span>
#### Token segmentation

```SQL
INDEX doc_idx doc TYPE inverted('token', '{"version":"v3"}') GRANULARITY 1
```


<span id="16301478"></span>
#### ngram segmentation

`"ngrams": 3` splits the text into triplets.

```SQL
INDEX doc_idx doc TYPE inverted('ngram','{"version":"v3", "ngrams": 3 }') GRANULARITY 1
```


<span id="5495b1d9"></span>
#### Custom delimiter

In the example below, the system splits using `,` and `;`.

```SQL
INDEX doc_idx doc TYPE inverted('char_sep','{"version":"v3","seperators": ",;"}') GRANULARITY 1
```


<span id="0c934daf"></span>
#### ICU segmentation

Specify the text language using `language`. In the example, "language": "zh" indicates Chinese.

```SQL
inverted('icu', '{"version": "v2", "language":"zh"}')
```


<span id="b36cfd48"></span>
## Common query functions

<span id="4ecb4adf"></span>
### String type


|Function name |Description |
|---|---|
|`hasTokens({column_name},'{value}')` |If an inverted index exists, the system fully segments the query terms according to the tokenizer and performs index filtering. After index filtering, the system reads the actual data and passes it to the upper\-level function for precise character matching filtering. Filtering efficiency usually outperforms `like '%xxx%'` fuzzy matching. Equivalent to Elasticseatch match_phrase semantics at the index level. |
|`{colum_name} = '{value}'` |Check if the field value equals the specified value. |
|`{colum_name} != '{value}'` |Check if the field value does not equal the specified value. |
|`{colum_name} like '{value}'` |Check if the field value matches the specified pattern. |
|`{colum_name} notlike '{value}'` |Check if the field value does not match the specified pattern. |
|`hasToken({column_name},'{value}')` |Check if the field value contains the specified token. |
|`startsWith({column_name},'{value}')` |Check if the field value starts with the specified prefix. |
|`endsWith({column_name},'{value}')` |Check if the field value ends with the specified suffix. |
|`multiSearchAny(column_name, [value1, ..., valueN])` |Perform multiple searches on any field value using the specified search terms. |
|`{column_name} notIn [value1, ..., valueN]` |Check if the field value is not in the specified list of values. |
|`{column_name} In [value1, ..., valueN]` |Check if the field value is in the specified value list. |
|`hasTokenBySeperator(column_name, value_literal, seperator)` |Check whether the `column_name` contains a specific value `value_literal` after being split by `seperator`. |


<span id="4e8828ca"></span>
### Array(String) type


|Function name |Function description |
|---|---|
|`has({column_name}, '{value}')` |Determine whether an element is in the given array or set. |
|`hasAny({column_name}, [value1, ..., valueN])` |Determine whether at least one element in the given array or set meets the specified condition. |
|`arraySetCheck({column_name}, [value1, ..., valueN])` |Check whether an array or set meets the specified condition. |


<span id="38be7d71"></span>
### Similarity search

The following example uses version 2 index based on the BM25 algorithm to recall text content similar to the search text through the textSearch function.

```SQL
select * from table where textSearch(doc, 'text for sim') order by _text_search_score desc limit n;
```


<span id="ff3088e7"></span>
# Related SETTINGS parameters

<span id="cb834042"></span>
## Query related


|Parameters |Description |Default value |
|---|---|---|
|enable_inverted_index |Enable inverted index. |1 |
|filter_with_inverted_index_segment |Quickly filter Marks using index segment granularity. |0 |
|filtered_ratio_to_use_skip_read |Set the filter ratio to enable line filtering: 0 means off, 1 means always on. |0 |
|skip_inverted_index_term_size |If the tokenizer splits a term larger than this value, index filtering will not be applied to the term. |512 |


<span id="ceb17e3c"></span>
## Table creation related


|Parameter |Description |Default value |
|---|---|---|
|max_digestion_size_per_segment |When building an index, a specified amount of text is processed to form one index block.<br><br>When there is sufficient memory, it is recommended to increase max_digestion_size_per_segment as much as possible. Data compression and query efficiency are optimal when only one segment exists within a part. |256 \* 1024 \* 1024 （256MB） |


<span id="3fad14f3"></span>
## Service configuration related


|Parameter |Description |Default value |
|---|---|---|
|ginindex_store_cache_size |Maximum cache size for the inverted index LRU Cache. |One\-eighth of the total available memory on the current node |
|ginindex_store_cache_sst_block_cache_size |Maximum cache size of the inverted index dictionary LRU cache. |Total available memory of the current node 1/16 |


<span id="902f8b13"></span>
# Common system table queries

<span id="da448b79"></span>
## Inverted index disk usage query

```SQL
SELECT
    name,
    formatReadableSize(sum(file_size)) as index_size
FROM system.checksums
WHERE (database = '{database}') AND (table = '{table}') AND active AND (file_name LIKE '%{index_name}%')
GROUP BY name
```


Output:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/403b6c2233304091bd85c6f4ea4facc1~tplv-goo7wpa0wc-image.image) </span>

<span id="03e0f44e"></span>
## Inverted index memory (LRU replacement policy) usage query

```SQL
SELECT
    *,
    formatReadableSize(value)
FROM system.asynchronous_metrics
WHERE (metric LIKE '%Cache%') AND (metric LIKE '%Unified%')
ORDER BY metric ASC
```


Output:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a74abcc063604e28be3614666a4edaba~tplv-goo7wpa0wc-image.image) </span>


* UnifiedGINCacheBytes: inverted index cache usage; the maximum cache usage is configurable via the `ginindex_store_cache_size` parameter.

* UnifiedSSTCacheBytes: dictionary cache usage; this parameter applies only to version 3. The maximum dictionary cache usage is configurable via the `ginindex_store_cache_sst_block_cache_size` parameter.
