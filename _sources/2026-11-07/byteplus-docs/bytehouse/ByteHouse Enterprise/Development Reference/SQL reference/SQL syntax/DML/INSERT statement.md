---
title: "INSERT statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-insert-statement"
---

Add data to the table.

<span id="b1912949"></span>
# Insert value

Data can be inserted using a basic query style.

<span id="cc32ebc2"></span>
## **Syntax**

```SQL
INSERT INTO [TABLE] [tableIdentifier] [columnsClause] VALUES
```


<span id="00c173da"></span>
## **Example**

```SQL
--step 1: Create a table
CREATE TABLE 
example_table
(
    a Int8,
    b String,
    c Date
)
ENGINE = MergeTree
ORDER BY (a)
--step 2: Insert 2 rows of data into the table
INSERT INTO example_table VALUES (1, 'a', '2021-07-27'), (2, 'b', '2021-07-27')
```


<span id="0bbf7717"></span>
# Insert format

Data can be passed to INSERT in formats supported by ByteHouse.

<span id="884c7ef2"></span>
## **Syntax**

```SQL
INSERT INTO [TABLE] [tableIdentifier] [columnsClause] FORMAT format_name
```


<span id="0c62bde3"></span>
## **Example**

```SQL
-- step 1: Create a table
CREATE TABLE `example_table`
(
    `a` Int8,
    `b` String,
    `c` Date
)
ENGINE = `MergeTree`
ORDER BY (`a`) 

-- step 2: Insert 2 rows of data in value format into the table
INSERT INTO example_table FORMAT VALUES (1, 'a', '2021-07-27'), (2, 'b', '2021-07-27');
```


<span id="91f48eea"></span>
# INSERT SELECT

Insert the results of the SELECT search. Columns are mapped accoding to their location in the SELECT subclause. However, their names in the SELECT expression and the INSERT table could be different. Type conversion is performed if necessary.

<span id="323230aa"></span>
## **Syntax**

```SQL
INSERT INTO [TABLE] [tableIdentifier] [columnsClause] [selectUnionStmt]
```


<span id="6915aa36"></span>
## **Example**

```SQL
INSERT INTO example_table SELECT * FROM example_table
```


<span id="0be4f666"></span>
# INSERT INFILE

Insert data from a file into a table. Limited to gateway\-client.

Supported file formats:


* .csv

* .json

* .avro

* .parquet


<span id="c972214a"></span>
## **Syntax**

```SQL
INSERT INTO [TABLE] [tableIdentifier] [columnsClause] [FORMAT format_name] INFILE filepath
```


<span id="18d319a1"></span>
## **Example**

```SQL
INSERT INTO my_table FORMAT csvwithnames INFILE '/Users/my_name/Downloads/ETH-USD.csv'
```


<span id="ebdc7748"></span>
# INSERT OVERWRITE

The function of this statement is to overwrite a table or some


* Overwriting is an atomic operation

* Partition substitution will automatically filter out data that does not conform to the specified partition


<span id="6be2101a"></span>
## **Syntax**

```SQL
INSERT OVERWRITE TABLE table_name
[ PARTITION (p1, ... | *) ]
[ (COLUMN [, ...]) ]
{ VALUES ([, ...] ), ([, ...]) | QUERY }
```


**Parameter**


* table_name: The target table name to be rewritten

* PARTITION: The partition to be rewritten

   * Can be a partition id or a partition tuple

   * Can be one or more, separated by commas

   * Parentheses are required around the outermost level

   * If the partition field is not specified, it defaults to rewriting the entire table

* COLUMN: The column to be written to the target table

   * Can be one or multiple, separated by commas

   * The outermost layer needs to use parentheses

* VALUES: The list of values to be written

* QUERY: The query to be written


<span id="7823acb1"></span>
## **Example**

Single partition key partition rewrite

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (1) SELECT * FROM test.insert_overwrite_s WHERE d = 1;
```


Single partition key partition VALUES rewrite

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (2) VALUES (2,6), (3,3);
```


Single partition key multi\-partition rewrite

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (1,2) SELECT * FROM test.insert_overwrite_s;
```


Multi\-partition key multi\-partition rewrite

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (('1',1), ('2',2)) SELECT * FROM test.insert_overwrite_s;
```


Multi\-partition key specified column import rewrite

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (('1',1)) (s,d,n) SELECT s,d,n FROM test.insert_overwrite_s;
```


Use Partition ID for partition rewriting

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (ID '2f4b47c7cb10a88d637501e1a15cbb47') SELECT * FROM test.insert_overwrite_s;
```


Use Partition ID for multi\-partition rewriting

```SQL
INSERT OVERWRITE test.insert_overwrite_t PARTITION (ID '2f4b47c7cb10a88d637501e1a15cbb47', ID 'fe7805ebd452ed4c738bdbbab09c6617') SELECT * FROM test.insert_overwrite_s;
```


Complete table rewriting

```SQL
INSERT OVERWRITE test.insert_overwrite_t SELECT * FROM test.insert_overwrite_s;
```
