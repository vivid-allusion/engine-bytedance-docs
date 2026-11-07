---
title: "GROUPING function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/grouping-function-cdw"
---

This tutorial introduces the usage of the `GROUPING` function and the `GROUPING SETS` modifier, and explains the core differences and applicable scenarios between the `GROUPING SETS` and `CUBE` modifiers and the basic `GROUP BY` clause.

<span id="e25e1e44"></span>
### GROUPING

`ROLLUP` and `CUBE` are modifiers for [GROUP BY](https://docs.byteplus.com/en/docs/bytehouse/select-statement#group-by-clause), both used to calculate data subtotals:


* `ROLLUP` accepts an ordered list of columns (such as `(day, month, year)`) and calculates subtotals at each level of aggregation in sequence, finally returning the grand total;

* `CUBE` calculates subtotals across all possible combinations of the specified columns.


The `GROUPING` function is used to distinguish between two types of rows in the results returned by `ROLLUP` or `CUBE`: one type is higher\-level aggregate rows (superaggregate, that is, subtotal rows), and the other type is the regular grouped rows that the GROUP BY clause itself would return when `ROLLUP`/`CUBE` modifiers are not used.

The GROUPING function accepts multiple columns as parameters and returns a bitmask value. The meaning of the return value is as follows:


* `1`: Indicates that the row is a subtotal row returned by `GROUP BY` with the `ROLLUP` or `CUBE` modifier;

* `0`: Indicates that the row is not a subtotal row returned by `GROUP BY` with the `ROLLUP` or `CUBE` modifier (that is, a regular grouped row).


<span id="74271f23"></span>
### GROUPING SETS

By default, the `CUBE` modifier calculates subtotals for all possible combinations of the columns provided; whereas `GROUPING SETS` allows you to directly specify the exact column combinations to be calculated, offering greater flexibility. Typical application scenarios for the `ROLLUP`, `CUBE`, and `GROUPING SETS` modifiers include hierarchical data analysis.

The examples in this tutorial are based on a data table that records the Linux distributions and their corresponding version information installed in two data centers. Analyzing the data by distribution, version, and data center location provides valuable insights for business analysis.

<span id="d235d9b3"></span>
#### Sample data

This tutorial will use the following data table as an example. The sample commands are as follows:

Create table:

```SQL
CREATE DATABASE bh_demo;

CREATE TABLE bh_demo.servers (
    datacenter VARCHAR(255),
    distro VARCHAR(255) NOT NULL,
    version VARCHAR(50) NOT NULL,
    quantity INT
)
ENGINE = CnchMergeTree()  
ORDER BY (datacenter, distro, version);
```


Insert data:

```SQL
INSERT INTO bh_demo.servers(datacenter, distro, version, quantity)
VALUES ('Schenectady', 'Arch','2022.08.05',50),
       ('Westport', 'Arch','2022.08.05',40),
       ('Schenectady','Arch','2021.09.01',30),
       ('Westport', 'Arch','2021.09.01',20),
       ('Schenectady','Arch','2020.05.01',10),
       ('Westport', 'Arch','2020.05.01',5),
       ('Schenectady','RHEL','9',60),
       ('Westport','RHEL','9',70),
       ('Westport','RHEL','7',80),
       ('Schenectady','RHEL','7',80)
```


Query data:

```SQL
SELECT 
    *
FROM
    bh_demo.servers;
```


Query results:

```SQL
┌─datacenter──┬─distro─┬─version────┬─quantity─┐
│ Schenectady │ Arch   │ 2020.05.01 │       10 │
│ Schenectady │ Arch   │ 2021.09.01 │       30 │
│ Schenectady │ Arch   │ 2022.08.05 │       50 │
│ Schenectady │ RHEL   │ 7          │       80 │
│ Schenectady │ RHEL   │ 9          │       60 │
│ Westport    │ Arch   │ 2020.05.01 │        5 │
│ Westport    │ Arch   │ 2021.09.01 │       20 │
│ Westport    │ Arch   │ 2022.08.05 │       40 │
│ Westport    │ RHEL   │ 7          │       80 │
│ Westport    │ RHEL   │ 9          │       70 │
└─────────────┴────────┴────────────┴──────────┘

10 rows in set. Elapsed: 0.359 sec.
```


<span id="14e81833"></span>
#### Simple query

The following queries use the basic `GROUP BY` clause to count the number of servers by different dimensions, clarifying the distribution of quantities under each dimension:


* Statistics by "data center + distribution" combined dimension

   Count the total number of servers for each Linux distribution (distro) in each data center.

   Execute query:

   ```SQL
   SELECT
       datacenter,
       distro, 
       SUM (quantity) qty
   FROM
       bh_demo.servers
   GROUP BY
       datacenter,
       distro; 
   ```
   

   Query results:

   ```SQL
   ┌─datacenter──┬─distro─┬─qty─┐
   │ Schenectady │ RHEL   │ 140 │
   │ Westport    │ Arch   │  65 │
   │ Schenectady │ Arch   │  90 │
   │ Westport    │ RHEL   │ 150 │
   └─────────────┴────────┴─────┘
   
   4 rows in set. Elapsed: 0.060 sec.
   ```
   

* Statistics by the "data center" dimension

   Count the total number of servers for each datacenter (regardless of distribution).

   Execute query:

   ```SQL
   SELECT
       datacenter, 
       SUM (quantity) qty
   FROM
       bh_demo.servers
   GROUP BY
       datacenter; 
   ```
   

   Query result:

   ```SQL
   ┌─datacenter──┬─qty─┐
   │ Westport    │ 215 │
   │ Schenectady │ 230 │
   └─────────────┴─────┘
   
   2 rows in set. Elapsed: 0.051 sec. 
   ```
   

* Statistics by the "distribution" dimension

   Count the total number of servers for each Linux distribution (regardless of datacenter).

   Execute query:

   ```SQL
   SELECT
       distro, 
       SUM (quantity) qty
   FROM
       bh_demo.servers
   GROUP BY
       distro; 
   ```
   

   Query result:

   ```SQL
   
   ┌─distro─┬─qty─┐
   │ Arch   │ 155 │
   │ RHEL   │ 290 │
   └────────┴─────┘
   
   2 rows in set. Elapsed: 0.037 sec. 
   ```
   

* Aggregate statistics (no grouping dimension)

   Count the total number of all servers (regardless of datacenter and distribution).

   Execute query:

   ```SQL
   SELECT
       SUM(quantity) qty
   FROM
       bh_demo.servers; 
   ```
   

   Query result:

   ```SQL
   ┌─qty─┐
   │ 445 │
   └─────┘
   
   1 row in set. Elapsed: 0.030 sec. 
   ```
   


<span id="170056b6"></span>
#### Comparing GROUP BY and GROUPING SETS Queries

The following examples compare two approaches to implementing multi\-dimensional aggregate statistics:


* The former uses basic `GROUP BY` combined with `UNION ALL` to concatenate subqueries.

* The latter uses a single statement with `GROUPING SETS`.


The core purpose of the following examples is to obtain, in a single query, the server count statistics for the four dimensions: "datacenter + distribution", "datacenter", "distribution", and "overall".


* Query using `GROUP BY`

   Execute query:

   ```SQL
   SELECT
       datacenter,
       distro, 
       SUM (quantity) qty
   FROM
       bh_demo.servers
   GROUP BY
       datacenter,
       distro
   UNION ALL
   SELECT
       datacenter, 
       null,
       SUM (quantity) qty
   FROM
       bh_demo.servers
   GROUP BY
       datacenter
   UNION ALL
   SELECT
       null,
       distro, 
       SUM (quantity) qty
   FROM
       bh_demo.servers
   GROUP BY
       distro
   UNION ALL
   SELECT
       null,
       null,
       SUM(quantity) qty
   FROM
       bh_demo.servers;
   ```
   

   Query result:

   ```SQL
   ┌─datacenter─┬─distro─┬─qty─┐
   │ ᴺᵁᴸᴸ       │ ᴺᵁᴸᴸ   │ 445 │
   └────────────┴────────┴─────┘
   ┌─datacenter──┬─distro─┬─qty─┐
   │ Westport    │ ᴺᵁᴸᴸ   │ 215 │
   │ Schenectady │ ᴺᵁᴸᴸ   │ 230 │
   └─────────────┴────────┴─────┘
   ┌─datacenter──┬─distro─┬─qty─┐
   │ Schenectady │ RHEL   │ 140 │
   │ Westport    │ Arch   │  65 │
   │ Schenectady │ Arch   │  90 │
   │ Westport    │ RHEL   │ 150 │
   └─────────────┴────────┴─────┘
   ┌─datacenter─┬─distro─┬─qty─┐
   │ ᴺᵁᴸᴸ       │ Arch   │ 155 │
   │ ᴺᵁᴸᴸ       │ RHEL   │ 290 │
   └────────────┴────────┴─────┘
   
   9 rows in set. Elapsed: 0.066 sec. 
   ```
   

* Query using `GROUPING SETS`

   Execute query:

   ```SQL
   SELECT
       datacenter,
       distro, 
       SUM (quantity) qty
   FROM
       bh_demo.servers
   GROUP BY
       GROUPING SETS(
           (datacenter,distro),
           (datacenter),
           (distro),
           ()
       );
   ```
   

   Query result:

   ```SQL
   ┌─datacenter──┬─distro─┬─qty─┐
   │ Schenectady │ RHEL   │ 140 │
   │ Westport    │ Arch   │  65 │
   │ Schenectady │ Arch   │  90 │
   │ Westport    │ RHEL   │ 150 │
   └─────────────┴────────┴─────┘
   ┌─datacenter──┬─distro─┬─qty─┐
   │ Westport    │        │ 215 │
   │ Schenectady │        │ 230 │
   └─────────────┴────────┴─────┘
   ┌─datacenter─┬─distro─┬─qty─┐
   │            │        │ 445 │
   └────────────┴────────┴─────┘
   ┌─datacenter─┬─distro─┬─qty─┐
   │            │ Arch   │ 155 │
   │            │ RHEL   │ 290 │
   └────────────┴────────┴─────┘
   
   9 rows in set. Elapsed: 0.040 sec.
   ```
   


<span id="01092d56"></span>
#### Comparing CUBE and GROUPING SETS Queries

`CUBE` generates **all possible combinations of dimensions** for the specified columns (including invalid or meaningless combinations). For example, in the following `CUBE` query, the `CUBE(datacenter, distro, version)` modifier generates combinations of columns that may not meet actual analysis requirements. Comparing versions across different distributions (Arch and RHEL) is not meaningful, as their release cycles and version naming conventions differ, so a direct comparison is not meaningful.

In contrast, `GROUPING SETS` supports **customizing the combinations of dimensions to be counted, ensuring only valid ones are included**, which better fits business needs. For example, in the following example, `GROUPING SETS` allows you to group `version` within `distro`, ensuring that version comparisons are always based on the same distribution dimension, which makes the analysis more logical.


* Query using CUBE

   Execute query:

   ```SQL
   SELECT
      datacenter,
      distro,
      version,
      SUM(quantity)
   FROM
      bh_demo.servers
   GROUP BY
      CUBE(datacenter,distro,version)
   ORDER BY
      datacenter,
      distro; 
   ```
   

   Query result:

   ```SQL
   ┌─datacenter──┬─distro─┬─version────┬─sum(quantity)─┐
   │             │        │ 7          │           160 │
   │             │        │ 2020.05.01 │            15 │
   │             │        │ 2021.09.01 │            50 │
   │             │        │ 2022.08.05 │            90 │
   │             │        │ 9          │           130 │
   │             │        │            │           445 │
   │             │ Arch   │ 2021.09.01 │            50 │
   │             │ Arch   │ 2022.08.05 │            90 │
   │             │ Arch   │ 2020.05.01 │            15 │
   │             │ Arch   │            │           155 │
   │             │ RHEL   │ 9          │           130 │
   │             │ RHEL   │ 7          │           160 │
   │             │ RHEL   │            │           290 │
   │ Schenectady │        │ 9          │            60 │
   │ Schenectady │        │ 2021.09.01 │            30 │
   │ Schenectady │        │ 7          │            80 │
   │ Schenectady │        │ 2022.08.05 │            50 │
   │ Schenectady │        │ 2020.05.01 │            10 │
   │ Schenectady │        │            │           230 │
   │ Schenectady │ Arch   │ 2022.08.05 │            50 │
   │ Schenectady │ Arch   │ 2021.09.01 │            30 │
   │ Schenectady │ Arch   │ 2020.05.01 │            10 │
   │ Schenectady │ Arch   │            │            90 │
   │ Schenectady │ RHEL   │ 7          │            80 │
   │ Schenectady │ RHEL   │ 9          │            60 │
   │ Schenectady │ RHEL   │            │           140 │
   │ Westport    │        │ 9          │            70 │
   │ Westport    │        │ 2020.05.01 │             5 │
   │ Westport    │        │ 2022.08.05 │            40 │
   │ Westport    │        │ 7          │            80 │
   │ Westport    │        │ 2021.09.01 │            20 │
   │ Westport    │        │            │           215 │
   │ Westport    │ Arch   │ 2020.05.01 │             5 │
   │ Westport    │ Arch   │ 2021.09.01 │            20 │
   │ Westport    │ Arch   │ 2022.08.05 │            40 │
   │ Westport    │ Arch   │            │            65 │
   │ Westport    │ RHEL   │ 9          │            70 │
   │ Westport    │ RHEL   │ 7          │            80 │
   │ Westport    │ RHEL   │            │           150 │
   └─────────────┴────────┴────────────┴───────────────┘
   
   39 rows in set. Elapsed: 0.051 sec. 
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the version is not associated with the distribution as a dimension, that is, as in the example above where <code>version</code> (distribution version) is considered independently, then this grouping logic lacks practical analytical significance. If the analysis concerns the kernel version, this grouping logic is more reasonable, because the kernel version is universally applicable across distributions and can be associated with any distribution.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In this scenario, choosing <code>GROUPING SETS</code> for grouped queries (as shown in the next example) better aligns with actual analytical requirements.   </div>
   

* Query using GROUPING SETS

   Execute query:

   ```SQL
   SELECT
       datacenter,
       distro,
       version,
       SUM(quantity)
   FROM bh_demo.servers
   GROUP BY
       GROUPING SETS (
           (datacenter, distro, version),
           (datacenter, distro));
   ```
   

   Query result:

   ```SQL
   ┌─datacenter──┬─distro─┬─version────┬─sum(quantity)─┐
   │ Westport    │ RHEL   │ 9          │            70 │
   │ Schenectady │ Arch   │ 2022.08.05 │            50 │
   │ Schenectady │ Arch   │ 2021.09.01 │            30 │
   │ Schenectady │ RHEL   │ 7          │            80 │
   │ Westport    │ Arch   │ 2020.05.01 │             5 │
   │ Westport    │ RHEL   │ 7          │            80 │
   │ Westport    │ Arch   │ 2021.09.01 │            20 │
   │ Westport    │ Arch   │ 2022.08.05 │            40 │
   │ Schenectady │ RHEL   │ 9          │            60 │
   │ Schenectady │ Arch   │ 2020.05.01 │            10 │
   └─────────────┴────────┴────────────┴───────────────┘
   ┌─datacenter──┬─distro─┬─version─┬─sum(quantity)─┐
   │ Schenectady │ RHEL   │         │           140 │
   │ Westport    │ Arch   │         │            65 │
   │ Schenectady │ Arch   │         │            90 │
   │ Westport    │ RHEL   │         │           150 │
   └─────────────┴────────┴─────────┴───────────────┘
   
   14 rows in set. Elapsed: 0.041 sec. 
   ```
