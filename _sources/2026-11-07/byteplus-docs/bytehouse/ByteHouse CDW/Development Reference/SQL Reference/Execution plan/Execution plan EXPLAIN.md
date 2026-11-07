---
title: "Execution plan EXPLAIN"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/execute-plan-explain"
---

ByteHouse supports generating the corresponding execution plan for SQL statements through the EXPLAIN statement, helping you understand how ByteHouse executes queries and enabling you to optimize SQL statements in a targeted manner. This tutorial uses SQL from TPCH\-Q1 as an example to demonstrate how to use different types of EXPLAIN statements.

<span id="7a202dcb"></span>
# Feature overview

In ByteHouse, the Query Optimizer achieves end\-to\-end query optimization through rule\-based optimization (RBO), cost\-based optimization (CBO), native distributed plan coordination, and advanced capabilities (dynamic filter pushdown/materialized view rewriting). After enabling the optimizer, running the `EXPLAIN` statement will generate the corresponding execution plan for the SQL statement, display detailed information about the execution plan, and produce a more efficient execution plan. This helps developers quickly identify SQL performance bottlenecks and optimize index design, expression complexity, or distributed execution strategies in a targeted manner, ensuring results are returned quickly with minimal resource consumption.

ByteHouse currently supports the following types of EXPLAIN statements:


|Type |Definition |
|---|---|
|EXPLAIN |Used to display the logical execution plan. |
|[EXPLAIN DISTRIBUTED](https://docs.byteplus.com/docs/bytehouse/execution-plan-explain#d39ad8de) |Used to display the distributed execution plan. |
|[EXPLAIN ANALYZE](https://docs.byteplus.com/docs/bytehouse/execute-plan-explain#26f7b9d6) |Used to display the execution plan with runtime information, which can be further divided into the following types:<br><br><br>* EXPLAIN ANALYZE<br><br>* [EXPLAIN ANALYZE DISTRIBUTED](https://docs.byteplus.com/docs/bytehouse/execute-plan-explain#4c754cec): Used to display the distributed execution plan with runtime information. |
|[EXPLAIN AST](https://docs.byteplus.com/docs/bytehouse/execute-plan-explain#357ea37a) |Dumps the abstract syntax tree (AST) of the query; supports all types of queries, not only `SELECT` **.**  |
|[EXPLAIN SYNTAX](https://docs.byteplus.com/docs/bytehouse/execute-plan-explain#3eca852f) |Returns the query after syntax optimization. |
|[EXPLAIN METADATA](https://docs.byteplus.com/docs/bytehouse/execution-plan-explain#64871731) |This statement is used to display information parsed during the SQL Analyzer phase, including database name, table name, column name, function name, settings, and more. |


<span id="025c4059"></span>
# Syntax

```SQL
EXPLAIN [DISTRIBUTED | ANALYZE | AST | SYNTAX | METADATA ] [setting = value, ...]
    [
      SELECT ... |
      tableFunction(...) [COLUMNS (...)] [ORDER BY ...] [PARTITION BY ...] [PRIMARY KEY] [SAMPLE BY ...] [TTL ...]
    ]
    [FORMAT ...]
```


<span id="54359fe9"></span>
## Parameter description


|Parameter |Required |Description |
|---|---|---|
|DISTRIBUTED |ANALYZE |AST |
|setting = value |No |Set custom query execution parameters.<br><br>For example, you can use json to set whether to print the plan in JSON format; setting it to 1 prints the plan in JSON format, while setting it to 0 does not. This parameter has the same effect as setting FORMAT. Example: `json = 1`. |
|SELECT |Select either SELECT or tableFunction(...) |Select either SELECT or tableFunction(...). Set the SELECT query statement to be analyzed. |
|tableFunction(...) |Select either tableFunction(...) or SELECT. |Select either tableFunction(...) or SELECT. Set the table function to be analyzed. |
|COLUMNS (...) |No |Define the column names and types that the table function should return. |
|ORDER BY |No |Define the sorting key for the table function. |
|PARTITION BY |No |Define the data partitioning rule for the table function. |
|PRIMARY KEY |No |Set the index primary key for the table function. |
|SAMPLE BY |No |Declare the sampling expression for the table function. |
|TTL |No |Configure the data expiration policy for the table function. |
|FORMAT |No |Define the output format for the results. |


<span id="8a4ce28e"></span>
## Example

```SQL
EXPLAIN json=0
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


**Output result**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/722b9c6c41204ab9bea1b3c084efbc3d~tplv-goo7wpa0wc-image.image) </span>

<span id="e1eb560b"></span>
# EXPLAIN type

<span id="d7ad0d3f"></span>
### EXPLAIN DISTRIBUTED

This statement is used to display the distributed execution plan.

<span id="faeebe84"></span>
#### Syntax

```SQL
EXPLAIN DISTRIBUTED <SQL>;
```


<span id="e71029a5"></span>
#### Example

```SQL
EXPLAIN DISTRIBUTED
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC 
```


**Output result**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e20ab138b1be48cf9f53e14d2fffc48d~tplv-goo7wpa0wc-image.image) </span>

<span id="26f7b9d6"></span>
### EXPLAIN ANALYZE

EXPLAIN ANALYZE is used to display the execution plan with runtime information, and also supports displaying the distributed execution plan with runtime information through EXPLAIN ANALYZE DISTRIBUTED.

The general setting parameters supported by this type of statement are as follows:


|Parameter |Required |Description |
|---|---|---|
|json |No |Set whether to print the plan in JSON format. The default value is 0, which means the plan is not output in JSON format; setting it to 1 prints the plan in JSON format. Example: `json = 1` |
|stats |No |Set whether to output the number of rows and cost in the statistics information. The default value is 1, which means output is enabled; setting it to 0 disables output. Example: `stats = 1`. |
|profile |No |Set whether to output execution profiles. The default value is 1, which means output is enabled; setting it to 0 means output is disabled. Example: `profile = 1`. |
|verbose |No |Set whether to output detailed content of the logical plan node. The default value is 1, which means output is enabled; setting it to 0 means output is disabled. Example: `verbose = 1`. |
|indexes |No |Set whether to print index usage. Setting it to 1 means printing is enabled; setting it to 0 means printing is disabled. Example: `indexes = 1`. |
|segment_id |No |Set the segment id. When printing a distributed plan, you can specify to print the content of a specific segment. |
|segment_profile |No |Set whether to print the segment time when printing a distributed plan. Setting it to 1 means printing is enabled; setting it to 0 means printing is disabled. Example: `segment_profile = 1`. |


<span id="cc01671a"></span>
#### EXPLAIN ANALYZE

This statement is used to display the execution plan with runtime information. For detailed field descriptions, please refer to [Explain analyze field description](https://docs.byteplus.com/docs/bytehouse/explain-analyze-field-description).

<span id="7562a10d"></span>
##### Syntax

```SQL
EXPLAIN ANALYZE <SQL>;
```


<span id="d626b61e"></span>
##### Parameter description

In addition to general parameters, EXPLAIN ANALYZE also supports the following setting parameters:


* processor_profile_events: Specifies whether to output ProfileEvents metrics for each PlanNode during execution of the execution plan. When set to 1, the system outputs the relevant content and aggregates by node; when set to 0, it does not output. Example: `processor_profile_events = 1`.


<span id="fe4abb84"></span>
##### Example

```SQL
EXPLAIN ANALYZE
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


**Output result**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3f2669fc5c14ebbb3a45ceb6d421391~tplv-goo7wpa0wc-image.image) </span>

<span id="4c754cec"></span>
#### EXPLAIN ANALYZE DISTRIBUTED

This statement is used to display the distributed execution plan with runtime information. For detailed field descriptions, please refer to [Explain analyze field description](https://docs.byteplus.com/docs/bytehouse/explain-analyze-field-description).

<span id="4cc2b961"></span>
##### Syntax

```SQL
EXPLAIN ANALYZE DISTRIBUTED <SQL>;
```


<span id="1030e5ff"></span>
##### Parameter description

In addition to general parameters, EXPLAIN ANALYZE DISTRIBUTED also supports the following setting parameters:


* processor_profile_events: Specifies whether to output ProfileEvents metrics for each PlanNode during execution of the execution plan. When set to 1, the system will output relevant content and aggregate it by node; when set to 0, no output will be generated. Example: `processor_profile_events = 1`.

* profile_events_list: Used to output ProfileEvents during distributed plan execution; aggregation is enabled by default. To display ProfileEvents for each node separately, set aggregate_profiles=0. Example: `profile_events_list='QueryAnalyzerTime'`. If there are multiple parameter values, separate them with commas (,).

* aggregate_profiles: Setting `aggregate_profiles = 1` prints the aggregated profile for each worker; setting `aggregate_profiles = 0` causes the system to print profiles for each worker separately.


<span id="15cdf772"></span>
##### Example

```SQL
EXPLAIN ANALYZE DISTRIBUTED
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


**Output result**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67b252cbf2fb4822b2ce991da518bcb0~tplv-goo7wpa0wc-image.image) </span>

<span id="357ea37a"></span>
### EXPLAIN AST

Dumps the abstract syntax tree (AST) of the query. Supports all types of queries, not limited to `SELECT` **.** 

<span id="f0b0ca7b"></span>
#### Syntax

```SQL
EXPLAIN AST <SQL>;
```


<span id="d2d609c1"></span>
#### **Example**

```SQL
EXPLAIN AST
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


**Output result**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f203052f9c234cf4a56ec645d709f34e~tplv-goo7wpa0wc-image.image) </span>

<span id="3eca852f"></span>
### EXPLAIN SYNTAX

Returns the query after syntax optimization.

<span id="4d2d7cf8"></span>
#### Syntax

```SQL
EXPLAIN SYNTAX <SQL>;
```


<span id="7b302c35"></span>
#### **Example**

```SQL
EXPLAIN SYNTAX
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


**Output result**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/232120795c79468f83fd69932c2610a2~tplv-goo7wpa0wc-image.image) </span>

<span id="befb5a30"></span>
### EXPLAIN METADATA

This statement is used to display information parsed during the SQL Analyzer phase, including database name, table name, column name, function name, settings, and more.

<span id="e18e29cc"></span>
#### Usage restrictions


* Only available in the form `EXPLAIN METADATA <SQL>`;

* Applies only to SELECT and INSERT SELECT queries.


<span id="d17e3045"></span>
#### Syntax

```SQL
EXPLAIN METADATA <SQL>;
```


<span id="05feb64c"></span>
#### Parameter description

EXPLAIN METADATA supports the following setting parameters:


* format_json: Setting `format_json = 1` means the output content is in JSON format.

* lineage: Specifies whether to output SQL lineage information; set to 1 to display, set to 0 to hide. Example: `lineage = 1`.


<span id="5ca07398"></span>
#### Example 1

```SQL
explain metadata select t1.a, t2.b from metadata t1 join metadata2 t2 on t1.a=t2.a settings enable_optimizer=1;
```


**Output result**


|tables |databases |column_lists |userd_function_names |settings |insert_info |
|---|---|---|---|---|---|
|["metadata","metadata2"] |["2100xxxxxx.test","2100xxxxxx.test"] |[["a"],["a","b"]] |["equals"] | |[] |


The field descriptions are as follows:


* tables: Tables involved in the query, array type.

* databases: The databases corresponding to the tables in the tables field, array(String) type.

* column_lists: Columns used from the tables in the current query, array(array(String)) type.

* used_function_names: Function names used in the query, array(String) type.

* settings: Names of settings effective in the query, map(string, string) type.

* insert_info: Database name, table name, and column name for insert, array(array(String)) type.


<span id="2f09d653"></span>
#### Example 2

```SQL
EXPLAIN METADATA format_json = 1, lineage = 1
WITH t3 AS
    (
        SELECT
            count() AS a,
            sum(b) AS b
        FROM cache2
        GROUP BY c
    )
SELECT
    a,
    b
FROM
(
    (
        SELECT
            t3.b AS a,
            t2.b AS b
        FROM cache AS t2
        INNER JOIN t3 ON t2.a = t3.a
    )
    UNION ALL
    (
        SELECT 
            *
        FROM t3
    )
) AS t1
WHERE t1.a = 1
SETTINGS enable_optimizer = 1
FORMAT TabSeparatedRaw
```


**Output result**

```SQL
{
 "UsedTablesInfo" : [
  {
   "Database" : "test",
   "Table" : "cache",
   "Columns" : [
    "a",
    "b"
   ]
  },
  {
   "Database" : "test",
   "Table" : "cache2",
   "Columns" : [
    "b",
    "c"
   ]
  }
 ],
 "UsedFunctions" : [
  "count",
  "equals",
  "sum"
 ],
 "UsedSettings" : {
  "enable_optimizer" : "1"
 },
 "InsertInfo" : {
 },
 "FunctionsInfo" : [

 ],
 "LineageInfo" : {
  "TableSources" : [
   {
    "Database" : "test",
    "Table" : "cache2",
    "Columns" : [
     {
      "Id" : 3,
      "Name" : "b"
     },
     {
      "Id" : 2,
      "Name" : "c"
     }
    ]
   },
   {
    "Database" : "test",
    "Table" : "cache",
    "Columns" : [
     {
      "Id" : 1,
      "Name" : "a"
     },
     {
      "Id" : 0,
      "Name" : "b"
     }
    ]
   }
  ],
  "ExpressionSources" : [
   {
    "Sources" : [
     {
      "Database" : "test",
      "Table" : "cache2"
     }
    ],
    "Expression" : [
     {
      "Id" : 4,
      "Name" : "expr#count()"
     }
    ]
   }
  ],
  "OutputLineageInfo" : [
   {
    "Name" : "b",
    "SourceIds" : [
     3,
     0
    ]
   },
   {
    "Name" : "a",
    "SourceIds" : [
     4,
     3
    ]
   }
  ],
  "InsertLinageInfo" : {
  }
 }
}
```


The field descriptions are as follows:


* TableSources: Original column information for all tables in the query; each column corresponds to an ID.

* ExpressionSources: Information about expressions, constants, and aggregate functions in the query that cannot be mapped to original column information; each expression also corresponds to an ID. The Sources field contains the table information involved in generating the expression.

* OutputLineageInfo: All output field names of the query and the corresponding IDs of original columns or expressions; Name is the output field name, SourceIds are the IDs of the corresponding columns or expressions.

* InsertLinageInfo: The mapping between the tables and columns inserted in the insert select statement and the corresponding output field names in the select clause. InsertColumnName is the column name in the insert statement, and InputName is the corresponding output field name in OutputLineageInfo.
