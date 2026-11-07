---
title: "Insert statement (INSERT)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/insert-statement"
---

Add data to the table.

<span id="b1912949"></span>
### INSERT INTO

You can use the basic INSERT INTO statement to write data.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When using a unique key table to insert, the default is to implement "upsert" semantics, which retains the latest value of each unique key.</div>


**Syntax**


* General syntax


```SQL
INSERT INTO [TABLE] [tableIdentifier] [columnsClause] VALUES
```



* Set the data writing format


Data can be delivered in formats supported by ByteHouse for INSERT.

```SQL
INSERT INTO [TABLE] [tableIdentifier] [columnsClause] FORMAT format_name
```


**Example**


* Example 1: General write


```SQL
--step1: create a tableCREATE TABLE 
example_table
(
    a Int8,
    b String,
    c Date
)
ENGINE = CnchMergeTree
ORDER BY (a)
--step2: insert 2 rows into the table
INSERT INTO example_table VALUES (1, 'a', '2021-07-27'), (2, 'b', '2021-07-27')
```



* Example 2: Set data write Format


```SQL
-- step 1: create a table
CREATE TABLE `example_table`
(
    `a` Int8,
    `b` String,
    `c` Date
)
ENGINE = `CnchMergeTree`
ORDER BY (`a`) 

-- step 2: insert 2 rows in value format into the table
INSERT INTO example_table FORMAT VALUES (1, 'a', '2021-07-27'), (2, 'b', '2021-07-27');
```


<span id="91f48eea"></span>
### INSERT SELECT

Insert the results of the SELECT query. Columns are mapped according to their positions in the SELECT clause. However, their names in the SELECT expression and INSERT table may differ. Type conversion will be performed if necessary.

**Syntax**

```SQL
INSERT INTO [TABLE] [tableIdentifier] [columnsClause] [selectUnionStmt]
```


**Example**

```SQL
INSERT INTO example_table SELECT * FROM example_table
```


<span id="0be4f666"></span>
### INSERT INFILE

Insert data from a file into a table. Limited to gateway\-client

Supported file formats:


* .csv

* .json

* .avro

* .parquet


**Syntax**

```SQL
INSERT INTO [TABLE] [tableIdentifier] [columnsClause] [FORMAT format_name] INFILE filepath
```


**Example**

```SQL
INSERT INTO my_table FORMAT csvwithnames INFILE '/Users/my_name/Downloads/ETH-USD.csv'
```


<span id="ebdc7748"></span>
### INSERT OVERWRITE

The function of this statement is to overwrite a table or specific partitions of a table.


* Overwriting is an atomic operation.

* During partition replacement, data not matching the specified partition is automatically filtered.


**Syntax**

```SQL
INSERT OVERWRITE TABLE table_name
[ PARTITION (p1, ... | *) ]
[ (COLUMN [, ...]) ]
{ VALUES ([, ...] ), ([, ...]) | QUERY }
```


**Param**


* table_name: The target table name to overwrite.

* PARTITION: The partition to overwrite.

   * Can be a partition id or a partition tuple.

   * It can be one or more, separated by commas

   * The outermost layer needs to use parentheses

   * If the partition field is omitted, it results in a full table rewrite

* COLUMN: The columns that need to be written to the target table

   * It can be one or more, separated by commas

   * The outermost layer needs to use parentheses

* VALUES: List of values that need to be written

* QUERY: The query that needs to be written


**Example**

Partition rewrite for a single partition key

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (1) SELECT * FROM test.insert_overwrite_s WHERE d = 1;
```


Partition rewrite with single partition key VALUES

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (2) VALUES (2,6), (3,3);
```


Multiple partition rewrite with single partition key

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (1,2) SELECT * FROM test.insert_overwrite_s;
```


Multiple partition rewrite with multiple partition keys

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (('1',1), ('2',2)) SELECT * FROM test.insert_overwrite_s;
```


Import rewrite with specified columns for multiple partition keys

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (('1',1)) (s,d,n) SELECT s,d,n FROM test.insert_overwrite_s;
```


Partition rewrite using Partition ID

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (ID '2f4b47c7cb10a88d637501e1a15cbb47') SELECT * FROM test.insert_overwrite_s;
```


Multiple partition rewrite using Partition ID

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (ID '2f4b47c7cb10a88d637501e1a15cbb47', ID 'fe7805ebd452ed4c738bdbbab09c6617') SELECT * FROM test.insert_overwrite_s;
```


Entire table rewrite

```SQL
INSERT OVERWRITE test.insert_overwrite_t SELECT * FROM test.insert_overwrite_s;
```


<span id="16a2fc23"></span>
### INSERT THROW

Unique key table supports insert throw semantics, checks if the unique key already exists, and returns an error if it does.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only the unique key table supports the use of "INSERT THROW."</div>


```SQL
-- example table
CREATE TABLE mysql_test(
    `a` Int32,
    `b` Nullable(Int32)
)
ENGINE = CnchMergeTree
ORDER BY a
UNIQUE KEY a

:) insert into mysql_test values (1, 1);
:) select * from mysql_test;
┌─a─┬─b─┐
│ 1 │ 1 │
└───┴───┘

:) insert into mysql_test FORMAT Values SETTINGS dedup_key_mode='throw' (1,1);

DB::Exception: Found duplication when insert with setting dedup_key_mode=DedupKeyMode::THROW
```


<span id="2c3c55f2"></span>
### INSERT IGNORE

The unique key table supports the "insert ignore" semantics. If the unique key already exists, the new data being written is ignored.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only the unique key table supports the use of "INSERT IGNORE."</div>


```SQL
-- example table
CREATE TABLE mysql_test(
    `a` Int32,
    `b` Nullable(Int32)
)
ENGINE = CnchMergeTree
ORDER BY a
UNIQUE KEY a

:) insert into mysql_test values (1, 1);
:) select * from mysql_test;
┌─a─┬─b─┐
│ 1 │ 1 │
└───┴───┘

:) insert ignore into mysql_test values (1,2);
:) select * from mysql_test;
┌─a─┬─b─┐
│ 1 │ 1 │
└───┴───┘
1 rows in set.
```
