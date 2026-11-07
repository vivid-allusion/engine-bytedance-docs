---
title: "Best practice: ByteHouse column defaults"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/best-practice-bytehouse-column-defaults"
---

ByteHouse supports defining a default value for a column without inserting and importing data. The column can be automatically populated with data according to rules.

<span id="c4622485"></span>
# Application scenario

<span id="4ecac6b8"></span>
## Sharding export

Use ByteHouse as a data source and use DataSail to export the data in ByteHouse to other platforms. DataSail supports selecting a sharding key (must be numeric) to divide the data into several parts, and then read the data concurrently to speed up the export speed.

When there is no suitable field in the table as the sharding key, you can define a column to be populated with the default value, the content of the filling is modulo HASH or random value, and then use the virtual column as the sharding key to achieve concurrent export.

<span id="20f0acf4"></span>
# Use example

We use rand () [Random Function](https://docs.byteplus.com/docs/bytehouse/random-function) as an example, as the default value of a column in the data table, its function isReturns a random number of type UInt32.

<span id="e4c0bb66"></span>
## Modulo random numbers according to requirements

Suppose we want to limit the range of random numbers based on the size of the user table, we can define a default column, generate random values by default, and then hash modulo, the size of modulo depends on the size of the requirement.

```SQL
`ext_key` Int32 DEFAULT cityHash64(rand()) % 1000000 
```


Suppose there is a database named testDB, we can create a distribution table based on the following two table building statements.

```SQL
CREATE TABLE testDB.test_default_local on CLUSTER <cluster_name>
( 
    `id` Int32,
    `ext_key` Int32 DEFAULT cityHash64(rand()) % 1000000
)
ENGINE = MergeTree
ORDER BY id;

CREATE TABLE testDB.test_default  on CLUSTER <cluster_name> as testDB.test_default_local
ENGINE = Distributed(<cluster_name>, testDB, test_default_local, cityHash64(id))
```


When inserting data, it is not necessary to DEFAULT columnext_keyAssignment.

```SQL
insert into testDB.test_default_local (id) select number from numbers(1000000); 
```


Grouped by 100,000 steps, we can find that the results are basically evenly distributed.

```SQL
SELECT
    floor(ext_key / 100000) AS g,
    count()
FROM testDB.test_default_local 
GROUP BY g
ORDER BY g ASC

Query id: da191201-deb5-41f3-9c13-bce8b1c56382

┌─g─┬─count()─┐
│ 0 │  100559 │
│ 1 │  100117 │
│ 2 │   99703 │
│ 3 │  100213 │
│ 4 │   99702 │
│ 5 │   99890 │
│ 6 │  100042 │
│ 7 │  100041 │
│ 8 │  100278 │
│ 9 │   99455 │
└───┴─────────┘
```


<span id="57bac45d"></span>
## No modulo method

We can also set any value when creating the table, and after inserting the data as usual, we can also refer to the following example to query the distribution of the data.

```SQL
CREATE TABLE testDB.test_default_no_mod_local on CLUSTER <cluster_name>
( 
    `id` Int32,
    `ext_key` Int32 DEFAULT cityHash64(rand()) 
)
ENGINE = MergeTree
ORDER BY id;

CREATE TABLE testDB.test_default_no_mod  on CLUSTER <cluster_name> as testDB.test_default_no_mod_local
ENGINE = Distributed(<cluster_name>, testDB, test_default_no_mod_local, cityHash64(id))
```


```SQL
insert into testDB.test_default_no_mod_local (id) select number from numbers(1000000); 
```


```SQL
SELECT
    floor((ext_key % 1000000) / 100000) AS g,
    count()
FROM testDB.test_default_no_mod_local
GROUP BY g
ORDER BY g ASC

Query id: 3af9e3d3-96ab-4c03-831b-4d6d26917790

┌─g─┬─count()─┐
│ 0 │  100095 │
│ 1 │  100151 │
│ 2 │  100148 │
│ 3 │   99666 │
│ 4 │  100389 │
│ 5 │  100494 │
│ 6 │   99858 │
│ 7 │   99568 │
│ 8 │   99435 │
│ 9 │  100196 │
└───┴─────────┘

SELECT count()
FROM testDB.test_default_no_mod_local
WHERE ((ext_key % 1000000) >= 100000) AND ((ext_key % 1000000) <= 200000)

Query id: b135e252-9669-4a64-8cfe-5594fe79cedb

┌─count()─┐
│  100151 │
└─────────┘
```
