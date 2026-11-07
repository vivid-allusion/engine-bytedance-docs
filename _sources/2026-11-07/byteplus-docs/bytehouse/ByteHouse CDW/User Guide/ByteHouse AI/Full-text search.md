---
title: "Full-text search "
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/full_text_search"
---

Full\-text search (or text\-only search) provides the ability to identify natural language documents that satisfy a query. The most common type of search is to find all documents that contain a given query term. Full\-text indexing allows documents to be preprocessed and indexed for quick search later. We support a faster way of text retrieval and filtering by adding the ability to index text inverted.

ByteHouse Cloud Data Warehouse Edition supports full\-text search through SQL syntax. This article will introduce how to create a full\-text index and query.

<span id="5047a574"></span>
## Indexing method

At present, full\-text search supports two text segmentation indexing methods:


* Language Token segmentation: Token segmentation with **space** and **Punctuation** For word segmentation, it is usually suitable for languages such as English that have obvious space\-punctuated word segmentation.

* Ngram participle: Ngram participle encounters **specified character** to split the text (e.g., whitespace, punctuation), and then returns the [N-grams](https://en.wikipedia.org/wiki/N-gram) of each word with the specified length. This is typically used for queries in languages that do not use spaces or have longer compound words


<span id="e28f51f7"></span>
## Syntax

<span id="3413a85f"></span>
### Basic syntax

The basic syntax for creating a full\-text search is as follows. Depending on the indexing method, we need to set different values for inverted ().

```SQL
-- Create an index when creating a table.
CREATE TABLE table_with_ivt_idx
(
    key UInt64,  
    str String,
    INDEX inv_idx(str) TYPE inverted() GRANULARITY 1
)
ENGINE = CnchMergeTree
ORDER BY key;

-- Add an index after creating a table.
ALTER TABLE  {table_name} ADD INDEX {index_name} {column_to_index} TYPE {index_type_and_arguments} GRANULARITY {index_granularity};

-- Materialize the added indexes.
ALTER TABLE {table_name}  MATERIALIZE INDEX {index_name};

-- Delete an index from the table definition and remove all the data of the index.
ALTER TABLE  {table_name} DROP INDEX {index_name};

-- Keep the index in the table definition but delete all the data of the index.
ALTER TABLE  {table_name} CLEAR INDEX {index_name};
```


<span id="535deee8"></span>
### Token participle

set`inverted(0)`or`inverted()`When the word segmentation is set to "tokens", which splits the string along spaces and punctuation.

```SQL
CREATE TABLE test_inverted_with_token
(
    key UInt64,
    doc String,-- low(doc) only converts English letters to lowercase before performing text processing
    INDEX doc_idx lower(doc) TYPE inverted GRANULARITY 1 -- By default, Token is used for word segmentation when no special specification is made
)
ENGINE = CnchMergeTree()
ORDER BY key;
```


<span id="4ead7c54"></span>
### Ngram participle

Set to`inverted(N)` When, that is, using the N\-gram particifier, the range is [2,8].

```SQL
CREATE TABLE test_inverted_with_ngram
(
    key UInt64,
    doc String,-- low(doc) only converts English letters to lowercase and then performs text processing
    INDEX doc_idx lower(doc) TYPE inverted(4) GRANULARITY 1-- Specify the number 4 means using 4-gram for text word segmentation)
)
ENGINE = CnchMergeTree()
ORDER BY key;
```


<span id="b70f012c"></span>
## Use example

The database contains the data of a Chinese work, and the table is built and imported for testing by ngram.

```SQL
-- Original table
CREATE TABLE test_gin.ch_docs
(
    row UInt64,    
    doc String
)
ENGINE = CnchMergeTree
ORDER BY row;

insert into test_gin.ch_docs format CSVWithNames infile '/home/user/sample.csv';

-- 2-gram word segmentation table
CREATE TABLE test_gin.ch_docs_ngram
(
    row UInt64,
    doc String,
    INDEX inv_idx doc TYPE inverted(2) GRANULARITY 1
)
ENGINE = CnchMergeTree
ORDER BY row;

insert into test_gin.ch_docs_ngram format CSVWithNames infile '/home/user/sample.csv';
```


The query statement is as follows:

```SQL
select count() from test_gin.ch_docs where doc like '%datawarehouse%'; 
select count() from test_gin.ch_docs_ngram where doc like '%datawarehouse%'; 

select count() from test_gin.ch_docs where doc like '%cloudcomputing%'; 
select count() from test_gin.ch_docs_ngram where doc like '%cloudcomputing%';
```


<span id="774d771a"></span>
## Query function

<span id="83ced9d5"></span>
### String type


|Function name |Description |
|---|---|
|`equals` |Checks whether the field value is equal to the specified value. |
|`notEquals` |Checks whether the field value is not equal to the specified value. |
|`like` |Checks whether the field value matches the specified pattern. |
|`notLike` |Checks if the field value does not match the specified pattern. |
|`hasToken` |Checks whether the field value contains the specified token. |
|`startsWith` |Checks whether a field value starts with the specified prefix. |
|`endsWith` |Checks whether a field value ends with the specified suffix. |
|`multiSearchany` |Performs a multi\-search on any value of a field using the specified search term. |
|`notIn` |Checks if the field value is not in the specified value list. |
|`in` |Checks whether the field value is in the specified value list. |


<span id="e2deb784"></span>
### Array String type


|Function name |Function description |
|---|---|
|`has` |Determine whether an element is in a given array or set. |
|`hasAny` |Determines whether at least one element in a given array or set satisfies the specified condition. |
|`arraySetCheck` |Checks whether an array or collection meets the specified conditions. |
